# MOSS Unsafe Numeric Uint Fix Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Prevent MOSS Core from silently converting unsafe JavaScript numeric uint inputs into a different bigint while preserving exact decimal-string input.

**Architecture:** Keep the fix inside the existing `uint` semantic type. Validate numeric inputs with `Number.isInteger` and `Number.isSafeInteger` before `BigInt` conversion; strings continue through the existing arbitrary-precision path. Prove the behavior at the semantic decoding boundary with a focused regression test and ship it as a patch changeset.

**Tech Stack:** TypeScript 5.9, Vitest 3, pnpm 11, Changesets, Git/GitHub CLI.

---

## File Structure

- Modify `packages/core/src/semantics.ts`: reject unsafe numeric uint values before conversion.
- Modify `packages/core/test/core-unit.test.ts`: add boundary and regression coverage for `uint` decoding.
- Create `.changeset/safe-uint-inputs.md`: declare the `@themoss/core` patch release and user-visible safety fix.

No other MOSS source, documentation, example, lockfile, or protocol package belongs in this PR.

### Task 1: Create an isolated branch from the official upstream

**Files:** None.

- [ ] **Step 1: Verify repository identity and current state**

Run from the existing MOSS clone:

```bash
pwd
git rev-parse --show-toplevel
git remote -v
git status --short --branch --untracked-files=all
gh repo view NeoWeb3Nova/moss --json nameWithOwner,parent,url
gh pr view 31 --repo nishuzumi/moss --json state,isDraft,headRefName,baseRefName,updatedAt,url
```

Expected:

- The repository is the MOSS submodule clone.
- `origin` is `NeoWeb3Nova/moss`.
- The worktree is clean.
- PR #31 remains visible; its state is recorded before implementation.

- [ ] **Step 2: Configure and verify the official upstream**

```bash
if git remote get-url upstream >/dev/null 2>&1; then
  git remote set-url upstream https://github.com/nishuzumi/moss.git
else
  git remote add upstream https://github.com/nishuzumi/moss.git
fi
git fetch upstream main
git remote -v
git rev-parse upstream/main
gh api repos/nishuzumi/moss/commits/main --jq .sha
```

Expected: `git rev-parse upstream/main` equals the official GitHub `main` SHA.

- [ ] **Step 3: Create an isolated worktree and feature branch**

Use `superpowers:using-git-worktrees` before running this step. Create the worktree outside the internship parent repository so it does not alter the registered submodule pointer:

```bash
git worktree add /home/neo/workspace/worktrees/moss-unsafe-uint \
  -b fix/unsafe-numeric-uint upstream/main
```

Then verify inside the new worktree:

```bash
pwd
git rev-parse --show-toplevel
git branch --show-current
git status --short --branch --untracked-files=all
git log -1 --oneline
```

Expected:

- Top level: `/home/neo/workspace/worktrees/moss-unsafe-uint`.
- Branch: `fix/unsafe-numeric-uint`.
- Clean status based on the current official `main`.

### Task 2: Add the failing uint precision regression test

**Files:**
- Modify: `packages/core/test/core-unit.test.ts:1-74`
- Test: `packages/core/test/core-unit.test.ts`

- [ ] **Step 1: Import the `uint` semantic type**

Change the semantic import to include `uint`:

```ts
import {
  address,
  decodeParams,
  nativeAmount,
  slippageBps,
  token,
  tokenAmount,
  uint,
} from "../src/semantics.js";
```

- [ ] **Step 2: Add the regression test inside `describe("semantic types", ...)`**

Add this test after the address test:

```ts
it("rejects unsafe numeric uints and preserves exact decimal strings", async () => {
  const maxSafe = Number.MAX_SAFE_INTEGER;
  expect((await decodeParams({ id: uint }, { id: maxSafe }, ctx)).id).toBe(BigInt(maxSafe));

  await expect(
    decodeParams({ id: uint }, { id: maxSafe + 1 }, ctx),
  ).rejects.toThrow(/unsafe integer.*decimal string/i);

  expect(
    (await decodeParams({ id: uint }, { id: "9007199254740992" }, ctx)).id,
  ).toBe(9_007_199_254_740_992n);
});
```

- [ ] **Step 3: Run the focused test and verify the regression is red**

```bash
pnpm --filter @themoss/core exec vitest run test/core-unit.test.ts \
  -t "rejects unsafe numeric uints"
```

Expected: FAIL because the current implementation resolves `maxSafe + 1` instead of rejecting it.

Do not change the expected assertion to match the current unsafe behavior.

### Task 3: Implement the minimal safe-number guard

**Files:**
- Modify: `packages/core/src/semantics.ts:82-98`
- Test: `packages/core/test/core-unit.test.ts`

- [ ] **Step 1: Split numeric validation from string parsing**

Replace the current `uint.decode` body with:

```ts
decode(value) {
  if (typeof value !== "string" && typeof value !== "number") {
    throw new Error(`expected an integer, got ${typeof value}`);
  }
  if (typeof value === "number") {
    if (!Number.isInteger(value)) {
      throw new Error(`expected an integer, got "${value}"`);
    }
    if (!Number.isSafeInteger(value)) {
      throw new Error("unsafe integer number; pass large integers as a decimal string");
    }
  }
  let n: bigint;
  try {
    n = BigInt(value);
  } catch {
    throw new Error(`expected an integer, got "${value}"`);
  }
  if (n < 0n) throw new Error("must be non-negative");
  return n;
},
```

This keeps safe numeric inputs backward-compatible and leaves arbitrary-precision strings exact.

- [ ] **Step 2: Run the focused test and verify it is green**

```bash
pnpm --filter @themoss/core exec vitest run test/core-unit.test.ts \
  -t "rejects unsafe numeric uints"
```

Expected: PASS.

- [ ] **Step 3: Run all Core tests**

```bash
pnpm --filter @themoss/core test
```

Expected: all `@themoss/core` tests pass.

### Task 4: Add package release metadata

**Files:**
- Create: `.changeset/safe-uint-inputs.md`

- [ ] **Step 1: Create the patch changeset**

Write exactly:

```markdown
---
"@themoss/core": patch
---

Reject unsafe JavaScript number inputs for uint parameters before precision can be lost. Pass large uint values as decimal strings for exact decoding.
```

- [ ] **Step 2: Verify the changeset status**

```bash
pnpm changeset status
```

Expected: `@themoss/core` is listed for a patch release and no unrelated package is included.

### Task 5: Run repository verification

**Files:** None unless a check exposes a defect in the three owned files.

- [ ] **Step 1: Run formatting and lint checks**

```bash
pnpm lint
```

Expected: exit code 0. If formatting fails only in the owned files, run:

```bash
pnpm exec biome check --write packages/core/src/semantics.ts packages/core/test/core-unit.test.ts
```

Then rerun `pnpm lint`.

- [ ] **Step 2: Build before typechecking**

```bash
pnpm -r build
pnpm -r typecheck
```

Expected: both commands exit 0. Build must precede typecheck because cross-package types resolve from `dist`.

- [ ] **Step 3: Run the complete offline suite**

```bash
MOSS_SKIP_E2E=1 pnpm -r test
```

Expected: all offline tests pass.

- [ ] **Step 4: Run the live suite when the Monad RPC is reachable**

```bash
NODE_USE_ENV_PROXY=1 pnpm -r test
```

Expected: all tests, including Monad mainnet e2e, pass. If infrastructure prevents the live suite, retain the exact failure output and do not report it as a product failure or a passing check.

- [ ] **Step 5: Inspect the exact diff**

```bash
git diff --check
git status --short --untracked-files=all
git diff -- packages/core/src/semantics.ts packages/core/test/core-unit.test.ts .changeset/safe-uint-inputs.md
```

Expected owned path set:

```text
.changeset/safe-uint-inputs.md
packages/core/src/semantics.ts
packages/core/test/core-unit.test.ts
```

No lockfile or unrelated generated file should be included.

### Task 6: Commit the focused fix

**Files:**
- `.changeset/safe-uint-inputs.md`
- `packages/core/src/semantics.ts`
- `packages/core/test/core-unit.test.ts`

- [ ] **Step 1: Reverify identity immediately before staging**

```bash
pwd
git remote -v
git status --short --branch --untracked-files=all
git diff --cached --name-status
git diff --name-status
```

Expected: the worktree is the isolated MOSS worktree and no unrelated staged files exist.

- [ ] **Step 2: Stage only the owned files**

```bash
git add -- \
  .changeset/safe-uint-inputs.md \
  packages/core/src/semantics.ts \
  packages/core/test/core-unit.test.ts

git diff --cached --name-only
git diff --cached --check
```

Expected: exactly the three owned paths.

- [ ] **Step 3: Commit**

```bash
git commit -m "fix(core): reject unsafe numeric uint inputs"
```

Expected: one focused commit with the exact conventional title selected for the PR.

### Task 7: Review, push, and open the Pull Request

**Files:** None.

- [ ] **Step 1: Review the commit against official main**

Use `superpowers:requesting-code-review` and fix Critical or Important findings before pushing. Then run:

```bash
git diff --stat upstream/main...HEAD
git diff --check upstream/main...HEAD
git log --oneline upstream/main..HEAD
git status --short --branch --untracked-files=all
```

Expected: one commit, three changed files, clean worktree.

- [ ] **Step 2: Push the feature branch to the user Fork**

```bash
git push --set-upstream origin fix/unsafe-numeric-uint
```

Expected: the remote branch exists at `NeoWeb3Nova/moss`.

- [ ] **Step 3: Create the upstream PR**

Use the file-writing tool to create `/tmp/moss-unsafe-uint-pr.md` with this exact content:

```markdown
## Motivation

JavaScript numbers above `Number.MAX_SAFE_INTEGER` are rounded before `BigInt` conversion. The `uint` semantic type currently accepts those values, which can silently build calldata for a different integer, including a different ERC-721 token ID.

## What changed

- reject non-integer and unsafe numeric uint inputs before `BigInt` conversion
- preserve safe numeric inputs
- preserve arbitrary-precision decimal-string inputs
- add a patch changeset and regression coverage

## Evidence

- focused regression test demonstrates unsafe numbers are rejected
- `pnpm lint`
- `pnpm -r build`
- `pnpm -r typecheck`
- `MOSS_SKIP_E2E=1 pnpm -r test`

## Scope

This PR intentionally does not change the general floating-point policy for token amounts or include unrelated framework work.
```

Then run:

```bash
PR_URL=$(gh pr create \
  --repo nishuzumi/moss \
  --base main \
  --head NeoWeb3Nova:fix/unsafe-numeric-uint \
  --title "fix(core): reject unsafe numeric uint inputs" \
  --body-file /tmp/moss-unsafe-uint-pr.md)
printf '%s\n' "$PR_URL"
```

Expected: a PR URL under `https://github.com/nishuzumi/moss/pull/`.

- [ ] **Step 4: Verify CI**

```bash
gh pr checks "$PR_URL" --watch
```

Expected: all required checks pass. If any check fails, obtain the failed run ID with `gh run list --repo nishuzumi/moss --branch fix/unsafe-numeric-uint --limit 5`, assign it to `RUN_ID`, then run `gh run view "$RUN_ID" --repo nishuzumi/moss --log-failed`; fix only the root cause, rerun local checks, commit, and push.

### Task 8: Record challenge proof in the internship parent repository

**Files:** Determine the existing Week 2 Tech challenge log/submission file before editing; do not create a duplicate if one already exists.

- [ ] **Step 1: Search the parent repository for the challenge record**

From `/home/neo/workspace/projects/Web3SummerInternshipProgram-MonadBuilderCamp`:

```bash
git status --short --branch --untracked-files=all
```

Use the file search tool for `Pull Request`, `Moss`, and `Week 2` under `tasks/`, `daily/`, and `submissions/`.

Expected: identify the canonical existing record or the correct Week 2 Tech destination.

- [ ] **Step 2: Record verifiable evidence**

Include:

- PR title and URL;
- GitHub profile: `https://github.com/NeoWeb3Nova`;
- branch and commit SHA;
- local verification results;
- GitHub Actions status;
- Review or Merge URL when available.

Do not claim Review or Merge before it occurs.

- [ ] **Step 3: Commit only the challenge proof files**

Reverify the parent repository identity and dirty worktree, stage explicit paths only, run `git diff --cached --check`, commit, and report the exact files. Preserve all unrelated Week 2 article and image changes.
