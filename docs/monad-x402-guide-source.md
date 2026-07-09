> ## Documentation Index
>
> Fetch the complete documentation index at: </llms.txt>
>
> Use this file to discover all available pages before exploring further.

[Monad Documentation home page![light logo](https://mintcdn.com/monadfoundation-40611fb6/gCj3ii1FXtCtIson/static/logo/full-mark-light.png?fit=max&auto=format&n=gCj3ii1FXtCtIson&q=85&s=2a722496725c21beb43e852aed0b0395)![dark logo](https://mintcdn.com/monadfoundation-40611fb6/gCj3ii1FXtCtIson/static/logo/full-mark-dark.png?fit=max&auto=format&n=gCj3ii1FXtCtIson&q=85&s=4616a760e77429106496e25ad2118d82)](/)

[Documentation](/)[Learn](/monad-arch)[Node Operations](/node-ops)

[Guides](/guides/index)

[More guides](/guides/scaffold-eth)

# How to set up an x402-enabled endpoint with Monad support

This guide shows how to set up payable endpoints using x402 payments and Monad’s facilitator. It works on Monad testnet/mainnet.

## [​](#what-is-x402) What is x402?

x402 is the HTTP 402 “Payment Required” status code reborn as a minimal protocol for internet‑native micropayments. Instead of subscriptions or paywalls that require accounts, x402 lets any HTTP endpoint become instantly payable:

1. Client requests a resource
2. Server responds 402 with a small JSON payment requirement
3. Client signs a payment authorization and resends the request
4. Server verifies and serves the content

### [​](#beyond-legacy-limitations) Beyond legacy limitations

x402 is designed for a modern internet economy, solving key limitations of legacy systems:

* **Reduce fees and friction:** Direct onchain payments without intermediaries, high fees, or manual setup.
* **Micropayments & usage-based billing:** Charge per call or feature with simple, programmable pay-as-you-go flows.
* **Machine-to-machine transactions:** Let AI agents pay and access services autonomously with no keys or human input needed.

## [​](#why-x402-on-monad) Why x402 on Monad?

Monad is a fully EVM‑compatible Layer 1 with:

* 10,000 TPS
* ~0.4s block times
* Single‑slot finality
* Parallel execution
* Extremely low fees

These properties make Monad an ideal environment for **true micropayments and agent-to-agent commerce**. Payments **settle instantly at low cost and avoid mempool congestion**, perfect when many AI agents pay per API call.

### [​](#core-flow-direct-payment) Core Flow (Direct Payment)

### [​](#facilitator-flow-recommended-for-production) Facilitator Flow (Recommended for Production)

A facilitator service is optional but recommended in production. Facilitators can batch transactions, cover gas, handle refunds, and simplify client logic.

## [​](#building-an-x402-based-app-using-monad-x402-facilitator) Building an x402-based app using Monad x402 facilitator

### [​](#prerequisites) Prerequisites

* Node.js 18+
* An EVM wallet
* Access to Monad testnet funds (USDC test tokens below)

Monad Facilitator only supports x402 version 2 and above.Migration guide that explains the differences: <https://docs.x402.org/guides/migration-v1-to-v2>

How to get USDC tokens on Monad testnet

You can get USDC tokens for Monad testnet using Circle’s faucet:

1. Visit <https://faucet.circle.com>
2. Select **USDC** as the token
3. Select **Monad Testnet** from the Network dropdown
4. Enter your wallet address
5. Click **Send 1 USDC**

**Limit:** One request per (stablecoin, testnet) pair every 2 hoursYou’ll also need testnet MON tokens for gas fees. Get them from the [Monad faucet](https://faucet.monad.xyz).

### [​](#step-1-initialize-a-next-js-app) Step 1: Initialize a Next.js App

Create a new Next.js project:

```
npx create-next-app@latest my-x402-app npx create-next-app@latest my-x402-app
```

When prompted, select the following options:

* ✅ TypeScript
* ✅ ESLint
* ✅ Tailwind CSS
* ✅ `src/` directory
* ✅ App Router
* ✅ Customize default import alias: `@/*` (default)

Navigate to your project:

```
cd my-x402-app cd my-x402-app
```

Install the x402 packages:

Use `@x402/evm >= 2.2.0` for the exact scheme. If you are using the upto scheme, use `@x402/evm 2.12.0` — see [Supported payment schemes](#supported-payment-schemes) for details.

```
npm install @x402/core @x402/evm @x402/fetch @x402/next npm  install @x402/core @x402/evm @x402/fetch @x402/next
```

Create a `.env.local` file for your environment variables:

```
touch .env.local touch .env.local
```

### [​](#step-2-create-a-payto-address) Step 2: Create a `payTo` address

A `payTo` address is used to receive payments and interact with the blockchain from your backend. Copy the wallet address and add it to your `.env.local` file as `PAY_TO_ADDRESS`

```
PAY_TO_ADDRESS=0xYourWalletPAY_TO_ADDRESS=0xYourWallet 
```

### [​](#step-3-create-a-server-side-payable-endpoint) Step 3: Create a server side payable endpoint

src/app/api/premium/route.ts

```
import { NextResponse } from "next/server"; import { NextResponse } from "next/server";import { withX402, type RouteConfig } from "@x402/next"; import { withX402, type  RouteConfig } from "@x402/next";import { x402ResourceServer, HTTPFacilitatorClient } from "@x402/core/server"; import { x402ResourceServer, HTTPFacilitatorClient } from "@x402/core/server";import { ExactEvmScheme } from "@x402/evm/exact/server"; import { ExactEvmScheme } from "@x402/evm/exact/server";import type { Network } from "@x402/core/types"; import  type { Network } from "@x402/core/types"; // Monad Testnet configuration// Monad Testnet configurationconst MONAD_NETWORK: Network = "eip155:10143"; const  MONAD_NETWORK:  Network = "eip155:10143";const MONAD_USDC_TESTNET = "0x534b2f3A21130d7a60830c2Df862319e593943A3"; const  MONAD_USDC_TESTNET =  "0x534b2f3A21130d7a60830c2Df862319e593943A3"; // Monad Facilitator URL// Monad Facilitator URLconst FACILITATOR_URL = "https://x402-facilitator.molandak.org"; const  FACILITATOR_URL = "https://x402-facilitator.molandak.org"; if (!process.env.PAY_TO_ADDRESS) {if (! process. env. PAY_TO_ADDRESS) { throw new Error("PAY_TO_ADDRESS environment variable is required");  throw  new  Error("PAY_TO_ADDRESS environment variable is required");}}const PAY_TO = process.env.PAY_TO_ADDRESS; const  PAY_TO =  process. env. PAY_TO_ADDRESS; // Create facilitator client for Monad// Create facilitator client for Monadconst facilitatorClient = new HTTPFacilitatorClient({ url: FACILITATOR_URL }); const  facilitatorClient =  new  HTTPFacilitatorClient({ url:  FACILITATOR_URL }); // Create and configure x402 resource server// Create and configure x402 resource serverconst server = new x402ResourceServer(facilitatorClient); const  server =  new  x402ResourceServer(facilitatorClient); // Create Exact EVM Scheme with custom money parser for Monad USDC// Create Exact EVM Scheme with custom money parser for Monad USDCconst monadScheme = new ExactEvmScheme(); const  monadScheme =  new  ExactEvmScheme();monadScheme.registerMoneyParser(async (amount: number, network: string) => {monadScheme. registerMoneyParser(async (amount:  number, network:  string) => { if (network === MONAD_NETWORK) { if (network ===  MONAD_NETWORK) { // Convert decimal amount to USDC smallest units (6 decimals). // Convert decimal amount to USDC smallest units (6 decimals). // `Math.floor(amount * 1_000_000)` is safe up to ~9 billion USDC // `Math.floor(amount * 1_000_000)` is safe up to ~9 billion USDC // (~9 quadrillion atomic units) — bounded by JS Number's 2^53 precision. // (~9 quadrillion atomic units) — bounded by JS Number's 2^53 precision. // For tokens with 18 decimals or very large balances, use `BigInt` to avoid // For tokens with 18 decimals or very large balances, use `BigInt` to avoid // precision loss, e.g.: // precision loss, e.g.: // BigInt(Math.round(amount * 1e6)).toString() // USDC, 6 decimals // BigInt(Math.round(amount * 1e6)).toString() // USDC, 6 decimals // (BigInt(Math.round(amount * 1e9)) * 1_000_000_000n).toString() // 18d, ≤9 fractional digits // (BigInt(Math.round(amount * 1e9)) * 1_000_000_000n).toString() // 18d, ≤9 fractional digits const tokenAmount = Math.floor(amount * 1_000_000).toString();  const  tokenAmount =  Math. floor(amount *  1_000_000). toString(); return { return { amount: tokenAmount, amount:  tokenAmount, asset: MONAD_USDC_TESTNET, // Raw address for EIP-712 verifyingContract asset:  MONAD_USDC_TESTNET, // Raw address for EIP-712 verifyingContract extra: { extra: { name: "USDC", name:  "USDC", version: "2", version:  "2", }, }, }; }; } } return null; // Use default parser for other networks  return  null; // Use default parser for other networks});}); // Register Monad network with custom scheme// Register Monad network with custom schemeserver.register(MONAD_NETWORK, monadScheme); server. register(MONAD_NETWORK, monadScheme); // Route configuration// Route configurationconst routeConfig: RouteConfig = {const  routeConfig:  RouteConfig = { accepts: { accepts: { scheme: "exact", scheme:  "exact", network: MONAD_NETWORK, network:  MONAD_NETWORK, payTo: PAY_TO, payTo:  PAY_TO, price: "$0.001", price: "$0.001", }, }, resource: "http://localhost:3000/api/premium", // Use relative path to avoid host mismatch resource: "http://localhost:3000/api/premium", // Use relative path to avoid host mismatch};}; // Handler that returns full article content// Handler that returns full article contentasync function handler(request: NextRequest) {async  function  handler(request:  NextRequest) { return NextResponse.json({ return  NextResponse. json({ content: "Return premium content", content:  "Return premium content", unlockedAt: new Date().toISOString(), unlockedAt:  new  Date(). toISOString(), }); });}} // Export GET method wrapped with x402 payment protection// Export GET method wrapped with x402 payment protectionexport const GET = withX402(handler, routeConfig, server); export  const  GET =  withX402(handler, routeConfig, server);
```

### [​](#step-4-client-side-setup-consuming-paid-endpoint) Step 4: Client-side setup (consuming paid endpoint)

Below is an example of consuming the paid endpoint using a Next.js app, however the endpoint can be consumed via an agent script as well.

src/app/page.tsx

```
"use client"; "use client"; import { useState, useCallback, useEffect } from "react"; import { useState, useCallback, useEffect } from  "react";import { useAccount, useWalletClient } from "wagmi"; import { useAccount, useWalletClient } from  "wagmi";import { wrapFetchWithPayment } from "@x402/fetch"; import { wrapFetchWithPayment } from "@x402/fetch";import { ExactEvmScheme } from "@x402/evm"; import { ExactEvmScheme } from "@x402/evm";import { x402Client } from "@x402/core/client"; import { x402Client } from "@x402/core/client"; // x402 configuration// x402 configurationconst x402Config = {const  x402Config = { chainId: "eip155:10143" as const, chainId: "eip155:10143"  as  const, usdcAddress: "0x534b2f3A21130d7a60830c2Df862319e593943A3", // MONAD USDC TESTNET usdcAddress:  "0x534b2f3A21130d7a60830c2Df862319e593943A3", // MONAD USDC TESTNET facilitator: "https://x402-facilitator.molandak.org", // MONAD FACILITATOR URL facilitator: "https://x402-facilitator.molandak.org", // MONAD FACILITATOR URL price: "0.001", // USDC price: "0.001", // USDC};}; export default function Home() {export  default  function  Home() { const { isConnected, address } = useAccount();  const { isConnected, address } =  useAccount(); const { data: walletClient } = useWalletClient();  const { data: walletClient } =  useWalletClient(); const [message, setMessage] = useState("Pay $0.001 USDC to unlock premium content");  const [message, setMessage] =  useState("Pay $0.001 USDC to unlock premium content"); const [status, setStatus] = useState<"idle" | "loading" | "success" | "error">("idle");  const [status, setStatus] =  useState< "idle"  |  "loading"  |  "success"  |  "error">("idle");  // This function allows signing a message, and pay USDC gaslessly.  // This function allows signing a message, and pay USDC gaslessly.  const handleUnlock = useCallback(async () => { const  handleUnlock =  useCallback(async () => { if (!walletClient || !address) { if (! walletClient  || ! address) { setError("Please connect your wallet first");  setError("Please connect your wallet first"); return;  return; } }  setIsLoading(true);  setIsLoading(true); setError(null);  setError(null);  try { try { // Create EVM signer compatible with x402 ClientEvmSigner interface // Create EVM signer compatible with x402 ClientEvmSigner interface const evmSigner = { const  evmSigner = { address: address as `0x${string}`, address:  address  as  `0x${string} `, signTypedData: async (message: { signTypedData:  async (message: { domain: Record<string, unknown>;  domain:  Record< string, unknown>; types: Record<string, unknown>;  types:  Record< string, unknown>; primaryType: string;  primaryType:  string; message: Record<string, unknown>;  message:  Record< string, unknown>; }) => { }) => { return walletClient.signTypedData({ return  walletClient. signTypedData({ domain: message.domain as Parameters<typeof walletClient.signTypedData>[0]["domain"], domain:  message. domain  as  Parameters< typeof  walletClient. signTypedData>[0]["domain"], types: message.types as Parameters<typeof walletClient.signTypedData>[0]["types"], types:  message. types  as  Parameters< typeof  walletClient. signTypedData>[0]["types"], primaryType: message.primaryType, primaryType:  message. primaryType, message: message.message, message:  message. message, }); }); }, }, }; };  // Create the Exact EVM scheme for signing // Create the Exact EVM scheme for signing const exactScheme = new ExactEvmScheme(evmSigner);  const  exactScheme =  new  ExactEvmScheme(evmSigner);  // Create x402 client and register the scheme // Create x402 client and register the scheme const client = new x402Client()  const  client =  new  x402Client() .register(x402Config.chainId, exactScheme); . register(x402Config. chainId, exactScheme);  console.log("x402 client configured for network:", x402Config.chainId);  console. log("x402 client configured for network:", x402Config. chainId);  // Wrap fetch with x402 payment capability // Wrap fetch with x402 payment capability const paymentFetch = wrapFetchWithPayment(fetch, client);  const  paymentFetch =  wrapFetchWithPayment(fetch, client);  console.log("Making payment request to /api/article...");  console. log("Making payment request to /api/article...");  // Make request to protected endpoint // Make request to protected endpoint const response = await paymentFetch("/api/premium", { const  response =  await  paymentFetch("/api/premium", { method: "GET", method:  "GET", headers: { headers: { "Content-Type": "application/json", "Content-Type": "application/json", }, }, }); });  if (!response.ok) { if (! response. ok) { // Try to parse x402 payment-required header for detailed error // Try to parse x402 payment-required header for detailed error const paymentHeader = response.headers.get("payment-required");  const  paymentHeader =  response. headers. get("payment-required");  if (paymentHeader && response.status === 402) { if (paymentHeader  &&  response. status ===  402) { try { try { const paymentData = JSON.parse(atob(paymentHeader));  const  paymentData =  JSON. parse(atob(paymentHeader)); console.error("Payment error details:", paymentData);  console. error("Payment error details:", paymentData);  // Extract user-friendly error message // Extract user-friendly error message if (paymentData.error?.includes("insufficient_funds")) { if (paymentData. error?. includes("insufficient_funds")) { throw new Error("INSUFFICIENT_FUNDS");  throw  new  Error("INSUFFICIENT_FUNDS"); } } if (paymentData.error?.includes("unexpected_error")) { if (paymentData. error?. includes("unexpected_error")) { throw new Error("UNEXPECTED_ERROR");  throw  new  Error("UNEXPECTED_ERROR"); } } if (paymentData.error) { if (paymentData. error) { throw new Error(paymentData.error);  throw  new  Error(paymentData. error); } } } catch (e) { } catch (e) { if (e instanceof Error && e.message === "INSUFFICIENT_FUNDS") { if (e  instanceof  Error  &&  e. message ===  "INSUFFICIENT_FUNDS") { throw e;  throw  e; } } // Failed to parse header, continue to generic error // Failed to parse header, continue to generic error } } } }  const errorText = await response.text().catch(() => "");  const  errorText =  await  response. text(). catch(() =>  ""); let errorData: Record<string, unknown> = {};  let  errorData:  Record< string, unknown> = {}; try { try { errorData = JSON.parse(errorText);  errorData =  JSON. parse(errorText); } catch { } catch { // Not JSON // Not JSON } } throw new Error( throw  new  Error( errorData.error as string ||  errorData. error  as  string  || errorData.details as string ||  errorData. details  as  string  || `Request failed: ${response.status}` `Request failed: ${response. status} ` ); ); } }  const data = await response.json();  const  data =  await  response. json();  // Cache the unlocked content in LocalStorage // Cache the unlocked content in LocalStorage localStorage.setItem( localStorage. setItem( "premimum_content_unlocked",  "premimum_content_unlocked", JSON.stringify({ JSON. stringify({ content: data.content, content:  data. content, timestamp: Date.now(), timestamp:  Date. now(), }) }) ); ); } catch (err) { } catch (err) { console.error("Unlock error:", err);  console. error("Unlock error:", err); const message = err instanceof Error ? err.message : "Failed to unlock article";  const  message =  err  instanceof  Error  ?  err. message :  "Failed to unlock article";  // Map technical errors to user-friendly messages // Map technical errors to user-friendly messages if ( if ( message.includes("User rejected") ||  message. includes("User rejected") || message.includes("User denied") ||  message. includes("User denied") || message.includes("user rejected")  message. includes("user rejected") ) { ) { setError("CANCELLED");  setError("CANCELLED"); } else if (message === "INSUFFICIENT_FUNDS" || message.includes("insufficient_funds")) { } else  if (message ===  "INSUFFICIENT_FUNDS"  ||  message. includes("insufficient_funds")) { setError("INSUFFICIENT_FUNDS");  setError("INSUFFICIENT_FUNDS"); } else if (message === "UNEXPECTED_ERROR" || message.includes("unexpected_error")) { } else  if (message ===  "UNEXPECTED_ERROR"  ||  message. includes("unexpected_error")) { setError("UNEXPECTED_ERROR");  setError("UNEXPECTED_ERROR"); } else { } else { setError(message);  setError(message); } } } finally { } finally { setIsLoading(false);  setIsLoading(false); } } }, [walletClient, address]); }, [walletClient, address]);  return ( return ( <main className="min-h-screen bg-zinc-950 flex items-center justify-center p-6"> < main  className ="min-h-screen bg-zinc-950 flex items-center justify-center p-6"> <div className="max-w-md w-full space-y-6"> < div  className ="max-w-md w-full space-y-6"> <div className="text-center space-y-2"> < div  className ="text-center space-y-2"> <h1 className="text-2xl font-bold text-white">x402 on Monadh1>  <p className="text-zinc-400 text-sm">  Micropayments via Thirdweb facilitator.{" "}  <a href="https://docs.monad.xyz/guides/x402-guide" className="text-violet-400 hover:underline">  Docs  a>  p>  div>   <button  onClick={handleUnlock}  disabled={status === "loading"}  className="w-full py-3 px-4 bg-violet-600 hover:bg-violet-500 disabled:bg-violet-800 disabled:cursor-wait text-white font-medium rounded-lg transition-colors"  >  {status === "loading" ? "Processing..." : "Pay & Unlock Content"}  button>   <div className={`p-4 rounded-lg text-sm ${  status === "error" ? "bg-red-950 text-red-300" :  status === "success" ? "bg-green-950 text-green-300" :  "bg-zinc-900 text-zinc-300"  }`}>  {message}  div>  div>  main>  ); }  < h1  className ="text-2xl font-bold text-white"> x402 on Monadh1> h1> <p className="text-zinc-400 text-sm"> < p  className ="text-zinc-400 text-sm"> Micropayments via Thirdweb facilitator.{" "} Micropayments via Thirdweb facilitator.{" "} <a href="https://docs.monad.xyz/guides/x402-guide" className="text-violet-400 hover:underline"> < a  href ="https://docs.monad.xyz/guides/x402-guide"  className ="text-violet-400 hover:underline">  Docs  Docs a>  p>  div>   <button  onClick={handleUnlock}  disabled={status === "loading"}  className="w-full py-3 px-4 bg-violet-600 hover:bg-violet-500 disabled:bg-violet-800 disabled:cursor-wait text-white font-medium rounded-lg transition-colors"  >  {status === "loading" ? "Processing..." : "Pay & Unlock Content"}  button>   <div className={`p-4 rounded-lg text-sm ${  status === "error" ? "bg-red-950 text-red-300" :  status === "success" ? "bg-green-950 text-green-300" :  "bg-zinc-900 text-zinc-300"  }`}>  {message}  div>  div>  main>  ); }  a> a> p>  div>   <button  onClick={handleUnlock}  disabled={status === "loading"}  className="w-full py-3 px-4 bg-violet-600 hover:bg-violet-500 disabled:bg-violet-800 disabled:cursor-wait text-white font-medium rounded-lg transition-colors"  >  {status === "loading" ? "Processing..." : "Pay & Unlock Content"}  button>   <div className={`p-4 rounded-lg text-sm ${  status === "error" ? "bg-red-950 text-red-300" :  status === "success" ? "bg-green-950 text-green-300" :  "bg-zinc-900 text-zinc-300"  }`}>  {message}  div>  div>  main>  ); }  p> p> div>   <button  onClick={handleUnlock}  disabled={status === "loading"}  className="w-full py-3 px-4 bg-violet-600 hover:bg-violet-500 disabled:bg-violet-800 disabled:cursor-wait text-white font-medium rounded-lg transition-colors"  >  {status === "loading" ? "Processing..." : "Pay & Unlock Content"}  button>   <div className={`p-4 rounded-lg text-sm ${  status === "error" ? "bg-red-950 text-red-300" :  status === "success" ? "bg-green-950 text-green-300" :  "bg-zinc-900 text-zinc-300"  }`}>  {message}  div>  div>  main>  ); }  div> div>  <button < button onClick={handleUnlock}  onClick ={handleUnlock} disabled={status === "loading"}  disabled ={status ===  "loading"} className="w-full py-3 px-4 bg-violet-600 hover:bg-violet-500 disabled:bg-violet-800 disabled:cursor-wait text-white font-medium rounded-lg transition-colors"  className ="w-full py-3 px-4 bg-violet-600 hover:bg-violet-500 disabled:bg-violet-800 disabled:cursor-wait text-white font-medium rounded-lg transition-colors" > > {status === "loading" ? "Processing..." : "Pay & Unlock Content"} {status ===  "loading"  ? "Processing..." :  "Pay & Unlock Content"} button>   <div className={`p-4 rounded-lg text-sm ${  status === "error" ? "bg-red-950 text-red-300" :  status === "success" ? "bg-green-950 text-green-300" :  "bg-zinc-900 text-zinc-300"  }`}>  {message}  div>  div>  main>  ); }  button> button>  <div className={`p-4 rounded-lg text-sm ${ < div  className ={`p-4 rounded-lg text-sm ${ status === "error" ? "bg-red-950 text-red-300" :  status ===  "error"  ? "bg-red-950 text-red-300" : status === "success" ? "bg-green-950 text-green-300" :  status ===  "success"  ? "bg-green-950 text-green-300" : "bg-zinc-900 text-zinc-300" "bg-zinc-900 text-zinc-300" }`}> } `}> {message} {message} div>  div>  main>  ); }  div> div> div>  main>  ); }  div> div> main>  ); }  main> main> ); );}}
```

## [​](#running-your-x402-app) Running Your x402 App

Now you’re ready to test your x402 payment flow:

1. Start your development server:

   ```
   npm run dev npm  run  dev
   ```
2. Open <http://localhost:3000> in your browser
3. Click “Pay & Unlock Content”
4. Connect your wallet
5. Approve the USDC payment
6. See the content unlock instantly!

## [​](#facilitator-api) Facilitator API

For developers who are interested in using the barebones Facilitator API, here are the supported endpoints with examples. Facilitator URL: `https://x402-facilitator.molandak.org` Network support: Mainnet and Testnet.

### [​](#supported-payment-schemes) Supported payment schemes

The Monad facilitator advertises two x402 v2 schemes via `GET /supported`:

| Scheme ID | When to use | Mechanism |
| --- | --- | --- |
| `v2-eip155-exact` | Fixed-price payments (default for USDC) | EIP-3009 `transferWithAuthorization` direct on the token, or Permit2-proxy fallback for non-EIP-3009 tokens |
| `v2-eip155-upto` | Variable-amount / metered payments (LLM tokens, bandwidth, compute) | Permit2-only — client signs a maximum, facilitator settles for actual usage ≤ max. Supports $0 settlement (no on-chain tx) |

For USDC on Monad, **exact** is the recommended scheme per the x402 specification. **Upto** requires the canonical `x402UptoPermit2Proxy` at `0x4020A4f3b7b90ccA423B9fabCc0CE57C6C240002` (see [Canonical Contracts](/developer-essentials/network-information#canonical-contracts)) and an `extra.facilitatorAddress` advertised by the facilitator that the client must bind into the Permit2 witness.

**Use `@x402/evm 2.12.0` for the upto scheme.** Versions 2.9.0–2.11.0 include the upto module but reference a proxy address that is not deployed on Monad (`0x402039b3d6E6BEC5A02c2C9fd937ac17A6940002`). Payments will fail at settlement with no clear error. The correct address (`0x4020A4f3b7b90ccA423B9fabCc0CE57C6C240002`) was first included in 2.12.0.If you upgrade to a newer version in future, confirm it references the same proxy address before deploying to production.

### [​](#possible-http-status-codes) Possible HTTP status codes

In addition to the standard `200` / `4xx` / `5xx` codes, the facilitator may return:

* **`412 PRECONDITION_FAILED`** — Returned when a Permit2 payment cannot proceed because the user’s Permit2 allowance for the proxy contract is insufficient (`PERMIT2_ALLOWANCE_REQUIRED`). The client must approve the proxy via Permit2 and retry. Distinct from `400` (malformed body) and `402` (the resource server’s payment-required response).

### [​](#get-/supported) GET `/supported`

Returns supported networks, schemes, and signer addresses.

```
const FACILITATOR_URL = "https://x402-facilitator.molandak.org"; const  FACILITATOR_URL = "https://x402-facilitator.molandak.org"; async function testSupported(): Promise<void> {async  function  testSupported():  Promise< void> { console.log("\n--- GET /supported ---");  console. log(" \n --- GET /supported ---");  const response = await fetch(`${FACILITATOR_URL}/supported`);  const  response =  await  fetch(`${FACILITATOR_URL}/supported`); if (!response.ok) throw new Error(`Failed: ${response.status}`);  if (! response. ok) throw  new  Error(`Failed: ${response. status} `);  const data = await response.json();  const  data =  await  response. json(); console.log(JSON.stringify(data, null, 2));  console. log(JSON. stringify(data, null, 2)); return data;  return  data;}}
```

### [​](#post-/verify) POST `/verify`

Verify a payment signature.

```
interface NetworkConfig {interface  NetworkConfig { chainId: Network;  chainId:  Network; name: string;  name:  string; rpcUrl: string;  rpcUrl:  string; explorerUrl: string;  explorerUrl:  string; usdcAddress: `0x${string}`;  usdcAddress:  `0x${string} `; usdcDecimals: number;  usdcDecimals:  number; chainIdNumber: number;  chainIdNumber:  number;}} /**/** * This function manually constructs and signs the EIP-712 typed data that * This function manually constructs and signs the EIP-712 typed data that * the x402 client library handles automatically. * the x402 client library handles automatically. */ */async function testVerify(async  function  testVerify( account: ReturnType<typeof privateKeyToAccount>,  account:  ReturnType< typeof  privateKeyToAccount>, networkConfig: NetworkConfig  networkConfig:  NetworkConfig): Promise<{ isValid: boolean; payload: any }> {):  Promise<{ isValid:  boolean; payload:  any }> { console.log("\n--- POST /verify ---");  console. log(" \n --- POST /verify ---"); const now = Math.floor(Date.now() / 1000);  const  now =  Math. floor(Date. now() /  1000); const nonce = keccak256(toHex(Math.random().toString()));  const  nonce =  keccak256(toHex(Math. random(). toString())); const ACCOUNT_ADDRESS = "0x0000000000000000000000000000000000000000";  const  ACCOUNT_ADDRESS =  "0x0000000000000000000000000000000000000000";  // TransferWithAuthorization parameters (ERC-3009) // TransferWithAuthorization parameters (ERC-3009) const authorization = { const  authorization = { from: ACCOUNT_ADDRESS, // Account that is paying from:  ACCOUNT_ADDRESS, // Account that is paying to: PAY_TO_ADDRESS, // Receiver address to:  PAY_TO_ADDRESS, // Receiver address value: "1000", // 0.001 USDC (6 decimals) value:  "1000", // 0.001 USDC (6 decimals) validAfter: (now - 60).toString(), // Start validity 60s in the past to handle clock skew validAfter: (now -  60). toString(), // Start validity 60s in the past to handle clock skew validBefore: (now + 900).toString(), // 15 minutes validBefore: (now +  900). toString(), // 15 minutes nonce,  nonce, }; };  // EIP-712 domain - must match USDC contract's DOMAIN_SEPARATOR // EIP-712 domain - must match USDC contract's DOMAIN_SEPARATOR const domain = { const  domain = { name: "USDC", // Monad USDC uses "USDC" (not "USD Coin") name:  "USDC", // Monad USDC uses "USDC" (not "USD Coin") version: "2", version:  "2", chainId: BigInt(networkConfig.chainIdNumber), chainId:  BigInt(networkConfig. chainIdNumber), verifyingContract: networkConfig.usdcAddress, verifyingContract:  networkConfig. usdcAddress, }; };  // EIP-712 type definition for TransferWithAuthorization // EIP-712 type definition for TransferWithAuthorization const types = { const  types = { TransferWithAuthorization: [ TransferWithAuthorization: [ { name: "from", type: "address" }, { name:  "from", type:  "address" }, { name: "to", type: "address" }, { name:  "to", type:  "address" }, { name: "value", type: "uint256" }, { name:  "value", type:  "uint256" }, { name: "validAfter", type: "uint256" }, { name:  "validAfter", type:  "uint256" }, { name: "validBefore", type: "uint256" }, { name:  "validBefore", type:  "uint256" }, { name: "nonce", type: "bytes32" }, { name:  "nonce", type:  "bytes32" }, ], ], }; };  const message = { const  message = { from: authorization.from, from:  authorization. from, to: authorization.to, to:  authorization. to, value: BigInt(authorization.value), value:  BigInt(authorization. value), validAfter: BigInt(authorization.validAfter), validAfter:  BigInt(authorization. validAfter), validBefore: BigInt(authorization.validBefore), validBefore:  BigInt(authorization. validBefore), nonce: authorization.nonce as `0x${string}`, nonce:  authorization. nonce  as  `0x${string} `, }; };  const signature = await account.signTypedData({ const  signature =  await  account. signTypedData({ domain,  domain, types,  types, primaryType: "TransferWithAuthorization", primaryType:  "TransferWithAuthorization", message,  message, }); });  const requestBody = { const  requestBody = { x402Version: 2, x402Version:  2, payload: { payload: { authorization,  authorization, signature,  signature, }, }, // `resource` (and its `url` / `description` / `mimeType` fields) is OPTIONAL // `resource` (and its `url` / `description` / `mimeType` fields) is OPTIONAL // in x402 v2; the facilitator only requires `payload` + `accepted`. Include it // in x402 v2; the facilitator only requires `payload` + `accepted`. Include it // when the resource server wants its identity recorded alongside the settlement. // when the resource server wants its identity recorded alongside the settlement. resource: { resource: { url: "http://test/resource", url: "http://test/resource", description: "Test resource", description:  "Test resource", mimeType: "application/json", mimeType: "application/json", }, }, accepted: { accepted: { scheme: "exact", scheme:  "exact", network: networkConfig.chainId, network:  networkConfig. chainId, amount: authorization.value, amount:  authorization. value, asset: networkConfig.usdcAddress, asset:  networkConfig. usdcAddress, payTo: authorization.to, payTo:  authorization. to, maxTimeoutSeconds: 300, maxTimeoutSeconds:  300, extra: { extra: { name: "USDC", name:  "USDC", version: "2", version:  "2", }, }, }, }, }; };  const response = await fetch(`${FACILITATOR_URL}/verify`, { const  response =  await  fetch(`${FACILITATOR_URL}/verify`, { method: "POST", method:  "POST", headers: { "Content-Type": "application/json" }, headers: { "Content-Type": "application/json" }, body: JSON.stringify(requestBody), body:  JSON. stringify(requestBody), }); });  const data = await response.json();  const  data =  await  response. json(); console.log(JSON.stringify(data, null, 2));  console. log(JSON. stringify(data, null, 2));  return { isValid: data.isValid, payload: requestBody };  return { isValid:  data. isValid, payload:  requestBody };}}
```

### [​](#post-/settle) POST `/settle`

Execute the payment on-chain. Facilitator pays gas.

```
interface NetworkConfig {interface  NetworkConfig { chainId: Network;  chainId:  Network; name: string;  name:  string; rpcUrl: string;  rpcUrl:  string; explorerUrl: string;  explorerUrl:  string; usdcAddress: `0x${string}`;  usdcAddress:  `0x${string} `; usdcDecimals: number;  usdcDecimals:  number; chainIdNumber: number;  chainIdNumber:  number;}} /** POST /settle - Execute the payment on-chain. Facilitator pays gas. *//** POST /settle - Execute the payment on-chain. Facilitator pays gas. */async function testSettle(async  function  testSettle( payload: any,  payload:  any, networkConfig: NetworkConfig  networkConfig:  NetworkConfig): Promise<void> {):  Promise< void> { console.log("\n--- POST /settle ---");  console. log(" \n --- POST /settle ---");  const response = await fetch(`${FACILITATOR_URL}/settle`, { const  response =  await  fetch(`${FACILITATOR_URL}/settle`, { method: "POST", method:  "POST", headers: { "Content-Type": "application/json" }, headers: { "Content-Type": "application/json" }, body: JSON.stringify(payload), body:  JSON. stringify(payload), }); });  const data = await response.json();  const  data =  await  response. json(); console.log(JSON.stringify(data, null, 2));  console. log(JSON. stringify(data, null, 2));  if (data.success && data.transaction) { if (data. success  &&  data. transaction) { // Transaction success // Transaction success } else if (data.errorReason) { } else  if (data. errorReason) { console.log(`Failed: ${data.errorReason}`);  console. log(`Failed: ${data. errorReason} `); } }}}
```

## [​](#what’s-next) What’s Next?

You’ve successfully built an x402 payment-enabled app on Monad! Here are some ideas to extend your implementation:

* **Add more payable endpoints** - Create different pricing tiers for various content or API calls
* **Build AI agent integrations** - Enable autonomous agents to pay for and access your APIs

## [​](#resources) Resources

* [x402 Protocol Specification](https://www.x402.org/)
* [Monad Developer Discord](https://discord.gg/monaddev)
* [Migration Guide: V1 to V2](https://docs.x402.org/guides/migration-v1-to-v2)

## [​](#need-help) Need Help?

If you run into issues or have questions, join the [Monad Developer Discord](https://discord.gg/monaddev) Happy building!

[How to build an MCP server that can interact with Monad Testnet](/guides/monad-mcp)[How to register and build with ERC-8004 (Trustless Agents) on Monad](/guides/erc-8004)

Responses are generated using AI and may contain mistakes.