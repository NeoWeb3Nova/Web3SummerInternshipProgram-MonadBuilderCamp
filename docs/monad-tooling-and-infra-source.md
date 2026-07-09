# Agentic Payments
Source: https://docs.monad.xyz/tooling-and-infra/agentic-payments



<Note>
  See also the [x402 guide](/guides/x402) for a step-by-step tutorial on building x402-enabled endpoints.
</Note>

## Overview

Agentic payments enable autonomous, machine-to-machine transactions over HTTP. Rather than requiring accounts, subscriptions, or API keys, any HTTP endpoint can become instantly payable using onchain payment authorization.

Monad's high throughput, sub-second finality, and low fees make it an ideal settlement layer for micropayments and agent-to-agent commerce.

## Provider summary

<div>
  <table>
    <thead>
      <tr>
        <th>Service</th>
        <th>Protocol</th>
        <th>Supported (Mainnet)</th>
        <th>Docs</th>
        <th>Notes</th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td>Monad x402 Facilitator</td>
        <td>[x402](https://www.x402.org/)</td>
        <td>✅</td>
        <td>[Guide](/guides/x402)</td>
        <td>URL: <CopyToClipboard>`https://x402-facilitator.molandak.org`</CopyToClipboard></td>
      </tr>

      <tr>
        <td>MPP SDK</td>
        <td>[MPP](https://mpp.dev/)</td>
        <td>✅</td>
        <td>[Reference](/reference/mpp/overview)</td>
        <td>NPM: [`@monad-crypto/mpp`](https://www.npmjs.com/package/@monad-crypto/mpp)</td>
      </tr>
    </tbody>
  </table>
</div>

## Provider details

### Monad x402 Facilitator

The Monad x402 Facilitator is a hosted service that simplifies [x402](https://www.x402.org/) payment flows on Monad. x402 brings the HTTP 402 "Payment Required" status code to life as a minimal protocol for internet-native micropayments.

**How it works:**

1. A client requests a resource from a server.
2. The server responds with HTTP 402 and a JSON payment requirement.
3. The client signs a payment authorization (no onchain transaction needed from the client).
4. The server verifies the signature and serves the content.
5. The facilitator settles the payment onchain, covering gas fees.

**Facilitator URL:** <CopyToClipboard>`https://x402-facilitator.molandak.org`</CopyToClipboard>

**Key features:**

* Supports Monad mainnet and testnet
* Handles payment verification and onchain settlement
* Covers gas fees on behalf of clients
* Enables usage-based billing and per-call micropayments
* Works with USDC on Monad

**Facilitator API endpoints:**

* `GET /supported` — Returns supported networks, schemes, and signer addresses
* `POST /verify` — Verifies a payment signature before serving content
* `POST /settle` — Executes the payment onchain after content is served

To get started building x402-enabled endpoints on Monad, see the [x402 guide](/guides/x402).

Learn more at [x402.org](https://www.x402.org/).

### MPP SDK

The MPP SDK ([`@monad-crypto/mpp`](https://www.npmjs.com/package/@monad-crypto/mpp)) is a TypeScript/JavaScript library for integrating [Machine Payments Protocol](https://mpp.dev/) into your applications on Monad. It provides utilities for constructing and managing payment transactions programmatically.

* **NPM package:** [`@monad-crypto/mpp`](https://www.npmjs.com/package/@monad-crypto/mpp)
* **Reference docs:** [`@monad-crypto/mpp` Reference](/reference/mpp/overview)


# Analytics
Source: https://docs.monad.xyz/tooling-and-infra/analytics



## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Service</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Description</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Blockaid](https://www.blockaid.io//)</td>
            <td>✅</td>

            <td />

            <td>Real-time detection platform for on-chain monitoring and fraud prevention</td>
          </tr>

          <tr>
            <td>[Birdeye](https://birdeye.so)</td>
            <td>✅</td>
            <td>[Docs](https://docs.birdeye.so/)</td>
            <td>Birdeye platform provides comprehensive multi-market data for cryptocurrency tokens, pulling information from both decentralized exchanges (DEX) and centralized exchanges (CEX). </td>
          </tr>

          <tr>
            <td>[Bubblemaps](https://bubblemaps.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.bubblemaps.io/)</td>
            <td>Visual analytics platform to investigate wallets, trace funds, and map token activity in real time</td>
          </tr>

          <tr>
            <td>[CoinGecko](https://www.coingecko.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.coingecko.com/)</td>
            <td>Comprehensive crypto price & market data provider with on-chain DEX data, token discovery, and trading analytics</td>
          </tr>

          <tr>
            <td>[Collab.Land](https://collab.land)</td>
            <td>✅</td>
            <td>[Docs](https://docs.collab.land/)</td>
            <td>Community management tool that supports a wide range of projects, including DAOs, NFT communities, brands, and creators of all sizes</td>
          </tr>

          <tr>
            <td>[DeBank](https://debank.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.cloud.debank.com/)</td>
            <td>DeFi portfolio tracker and analytics platform</td>
          </tr>

          <tr>
            <td>[DeFiLlama](https://defillama.com/)</td>
            <td>✅</td>
            <td>[Docs](https://defillama.com/docs/api)</td>
            <td>Open-source DeFi TVL and analytics platform aggregating data from thousands of protocols across multiple chains. See [How to list a DeFi project](https://docs.llama.fi/list-your-project/submit-a-project)</td>
          </tr>

          <tr>
            <td>[Dune](https://www.dune.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.dune.com/home)</td>
            <td>Datasets and dashboards about on-chain activity</td>
          </tr>

          <tr>
            <td>[Flipside](https://www.flipsidecrypto.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.flipsidecrypto.xyz/)</td>
            <td>AI-powered analytics for on-chain activity</td>
          </tr>

          <tr>
            <td>[InsightX](https://app.insightx.network)</td>
            <td>✅</td>
            <td>[Docs](https://docs.insightx.network/docs)</td>
            <td>Web3 transparency and security platform combining smart contract scanning with real-time holder maps for on-chain trading</td>
          </tr>

          <tr>
            <td>[Matrica](https://matrica.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.matrica.io/)</td>
            <td>Cross-chain Web3 social platform and community management solution.</td>
          </tr>

          <tr>
            <td>[Nansen](https://www.nansen.ai/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.nansen.ai/)</td>
            <td>Blockchain analytics platform providing wallet profiling, smart money tracking, and on-chain insights</td>
          </tr>

          <tr>
            <td>[Phalcon Explorer by Blocksec](https://blocksec.com/explorer)</td>
            <td>✅</td>
            <td>[Docs](https://docs.blocksec.com/phalcon/phalcon)</td>
            <td>Explorer for understanding transaction details with fund flow, balance changes, invocation flow, gas usage, and more</td>
          </tr>

          <tr>
            <td>[Philidor](https://philidor.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.philidor.io/docs)</td>
            <td>Independent DeFi risk ratings and monitoring, scoring on-chain assets, vaults, and protocols across asset, platform, and governance dimensions</td>
          </tr>

          <tr>
            <td>[Tenderly](https://tenderly.co/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.tenderly.co/)</td>
            <td>Comprehensive toolkit including virtual testnets, explorer, debugger, transaction simulator, and monitoring</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Service</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Description</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Dune](https://www.alchemy.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.dune.com/home)</td>
            <td>Datasets and dashboards about on-chain activity</td>
          </tr>

          <tr>
            <td>[Flipside](https://www.flipsidecrypto.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.flipsidecrypto.xyz/)</td>
            <td>AI-powered analytics for on-chain activity</td>
          </tr>

          <tr>
            <td>[Phalcon](https://blocksec.com/explorer)</td>
            <td>✅</td>
            <td>[Docs](https://docs.blocksec.com/phalcon/phalcon)</td>
            <td>Explorer for understanding transaction details with fund flow, balance changes, invocation flow, gas usage, and more</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Birdeye

[Birdeye](https://birdeye.so/) platform provides comprehensive multi-market data for cryptocurrency tokens, pulling information from both decentralized exchanges (DEX) and centralized exchanges (CEX). This allows users to monitor and analyze token performance across different exchange types in real-time, providing a holistic view of the market landscape.

To learn more about the platform, check out the [documentation](https://docs.birdeye.so/).

### Blockaid

[Blockaid](https://blockaid.io) is the real-time detection platform purpose-built for web3 builders
and operators to measure performance, mitigate risk, and prevent theft.

### Bubblemaps

[Bubblemaps](https://bubblemaps.io) is a visual analytics platform to investigate wallets,
trace funds, and map token activity in real time across all chains.

To get started, check out the [docs](https://docs.bubblemaps.io/) or launch the
[app](https://v2.bubblemaps.io/).

### CoinGecko

[CoinGecko API](https://www.coingecko.com/en/api) is one of the most comprehensive and reliable crypto price & market data providers, serving on-chain DEX data across 250+ blockchain networks. CoinGecko provides real-time token prices, market statistics, trading data, OHLCV charts, and token discovery tools including trending pools, new pools, and advanced filtering capabilities.

To get started, visit the [documentation](https://docs.coingecko.com/) for full details, or [sign up](https://www.coingecko.com/en/api/pricing) for a free API key.

### Collab.Land

[Collab.Land](https://docs.collab.land/) is a community management tool that supports a wide range of projects, including DAOs, NFT communities, brands, and creators of all sizes. Our mission is to provide tools that encourage pro-social activity within communities, particularly those that use tokens as a means of membership verification.

To learn more about Collab.Land, check out the [documentation](https://docs.collab.land/).

### DeBank

[DeBank](https://debank.com/) is a DeFi portfolio tracker and analytics platform that helps users manage their crypto assets across multiple chains. It provides comprehensive portfolio tracking, transaction history, and protocol analytics.

To get started, check out the [DeBank documentation](https://docs.cloud.debank.com/)

### DeFiLlama

[DeFiLlama](https://defillama.com/) is the largest open-source Total Value Locked (TVL) and DeFi analytics platform. It aggregates data from thousands of DeFi protocols across multiple chains, providing comprehensive insights into protocol TVL, token prices, yields, and DeFi trends. DeFiLlama offers both a user-friendly dashboard and a robust API for developers.

To get started, visit the [DeFiLlama platform](https://defillama.com/) or check out the [API documentation](https://defillama.com/docs/api).

### Dune

Dune is a blockchain analytics platform that empowers users to query, visualize, and share on-chain data across dozens of blockchains. It uses SQL as its primary query language, enabling analysts, developers, and researchers to build custom dashboards and explore everything from DeFi protocols to NFT markets. With a large library of community-created dashboards and visualizations, Dune fosters collaboration and open access to blockchain intelligence, while also offering premium features such as faster queries and private dashboards for professional teams.

To get started, check out the [Dune documentation](https://docs.dune.com/home)

### Flipside

[Flipside](https://flipsidecrypto.xyz/home/) generates the most reliable and comprehensive blockchain data. All for free.

To get started, check out the [Flipside documentation](https://docs.flipsidecrypto.xyz/).

### InsightX

[InsightX](https://app.insightx.network) delivers actionable transparency and security insights across multiple chains, enabling traders to rapidly assess the risk and potential of on-chain assets in real time.

To get started, check out the [docs](https://docs.insightx.network/docs) or launch the [app](https://app.insightx.network).

### Matrica

[Matrica](https://matrica.io/) is a popular cross-chain web3 social platform and community management solution. It provides essential infrastructure for digital identity and community engagement, primarily focusing on Non-Fungible Tokens (NFTs).

To get started, check out the [documentation](https://docs.matrica.io/)

### Nansen

[Nansen](https://www.nansen.ai/) is a blockchain analytics platform that combines on-chain data with millions of wallet labels to provide actionable insights. It offers features like smart money tracking, wallet profiling, token analytics, and real-time alerts to help users discover opportunities and understand blockchain activity.

To get started, visit the [Nansen platform](https://www.nansen.ai/) or check out the [Nansen documentation](https://docs.nansen.ai/).

### Phalcon

Blocksec [Phalcon Explorer](https://blocksec.com/explorer) is a powerful transaction explorer designed for the DeFi community. It provides comprehensive data on invocation flow, source code, balance changes, transaction fund flows, gas profiler, and state changes. It also supports transaction debugging and transaction simulation. This tool aims to help developers, security researchers, and traders intuitively understand transactions.

To get started, check out the [explorer](https://blocksec.com/explorer) or the [Phalcon documentation](https://docs.blocksec.com/phalcon/explorer).

### Philidor

[Philidor](https://philidor.io/) is an independent DeFi risk infrastructure platform that scores and monitors on-chain assets, vaults, and protocols using open, independent risk models. It produces deterministic composite risk scores across three vectors — asset, platform, and governance — delivered through dashboards and public APIs for allocators, protocol teams, and agents.

To get started, check out the [documentation](https://docs.philidor.io/docs).

### Tenderly

[Tenderly](https://tenderly.co) is a comprehensive toolkit for smart contract developers. The
platform offers features like real-time transaction monitoring, advanced debugging with detailed
stack traces, gas profiling, smart contract verification, and simulation environments that allow
developers to fork mainnets and test contract interactions without deploying to live networks.

To get started, check out the [explorer](https://dashboard.tenderly.co/explorer) or the
[documentation](https://docs.tenderly.co).


# Block Explorers
Source: https://docs.monad.xyz/tooling-and-infra/block-explorers



## Block Explorer Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Block explorer</th>
            <th>Powered by</th>
            <th>Status</th>
            <th>URL</th>
            <th>Verifier Type & URL</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>**MonadVision**</td>
            <td>BlockVision</td>
            <td>✅</td>

            <td>
              <CopyToClipboard>[https://monadvision.com/](https://monadvision.com/)</CopyToClipboard>
            </td>

            <td>
              Sourcify: <CopyToClipboard>`https://sourcify-api-monad.blockvision.org`</CopyToClipboard>
            </td>
          </tr>

          <tr>
            <td>**Monadscan**</td>
            <td>Etherscan</td>
            <td>✅</td>

            <td>
              <CopyToClipboard>[https://monadscan.com/](https://monadscan.com/)</CopyToClipboard>
            </td>

            <td>
              Etherscan: <CopyToClipboard>`https://api.monadscan.com/api`</CopyToClipboard>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Block explorer</th>
            <th>Powered by</th>
            <th>Status</th>
            <th>URL</th>
            <th>Verifier Type & URL</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>**MonadVision**</td>
            <td>BlockVision</td>
            <td>✅</td>

            <td>
              <CopyToClipboard>[https://testnet.monadvision.com/](https://testnet.monadvision.com/)</CopyToClipboard>
            </td>

            <td>
              Sourcify: <CopyToClipboard>`https://sourcify-api-monad.blockvision.org`</CopyToClipboard>
            </td>
          </tr>

          <tr>
            <td>**Monadscan**</td>
            <td>Etherscan</td>
            <td>✅</td>

            <td>
              <CopyToClipboard>[https://testnet.monadscan.com/](https://testnet.monadscan.com/)</CopyToClipboard>
            </td>

            <td>
              Etherscan: <CopyToClipboard>`https://api-testnet.monadscan.com/api`</CopyToClipboard>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## UserOp Explorers

<div>
  <table>
    <thead>
      <tr>
        <th>UserOp Explorer</th>
        <th>Status</th>
        <th>URL</th>
        <th>Notes</th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td>JiffyScan</td>
        <td>✅</td>

        <td>
          <CopyToClipboard>[https://jiffyscan.xyz/?network=monad](https://jiffyscan.xyz/?network=monad)</CopyToClipboard>
        </td>

        <td>UserOp explorer for EIP-4337</td>
      </tr>
    </tbody>
  </table>
</div>

## Detailed Transaction Explorers

<div>
  <table>
    <thead>
      <tr>
        <th>Transaction Explorer</th>
        <th>Status</th>
        <th>URL</th>
        <th>Notes</th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td>Tenderly Explorer</td>
        <td>✅</td>

        <td>
          <CopyToClipboard>[https://dashboard.tenderly.co/explorer](https://dashboard.tenderly.co/explorer)</CopyToClipboard>
        </td>

        <td>Detailed transaction analyzer featuring call stack, balance changes, gas usage, and more</td>
      </tr>

      <tr>
        <td>Blocksec Phalcon Explorer</td>
        <td>✅</td>

        <td>
          <CopyToClipboard>[https://blocksec.com/explorer](https://blocksec.com/explorer)</CopyToClipboard>
        </td>

        <td>Detailed transaction analyzer featuring call stack, balance changes, fund flows, and more</td>
      </tr>
    </tbody>
  </table>
</div>

## Provider Details

### BlockVision

[MonadVision](https://monadvision.com) is built by [BlockVision](https://blockvision.org/), a
leading provider of next-gen data infrastructure and enterprise solutions for the blockchain.
BlockVision is supports the EVM and Sui and specializes in explorer service, RPC nodes, indexing
APIs and validator service.

To get started, visit the [documentation](https://docs.blockvision.org/reference/monad-indexing-api).

### Monadscan

[Monadscan](https://monadscan.com) is built by [Etherscan](https://etherscan.io/) to deliver trusted
and high-performance access to on-chain data. Leveraging Etherscan's industry-leading expertise,
MonadScan provides robust explorer tools, developer-friendly APIs, and reliable infrastructure
tailored for the Monad ecosystem.

To get started, visit the [documentation](https://docs.monadscan.com/).


# Cross-Chain
Source: https://docs.monad.xyz/tooling-and-infra/cross-chain



## Definitions

At a high level, bridges offer the following features:

<div>
  <table>
    <thead>
      <tr>
        <th>Feature</th>
        <th>Description</th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td>**Arbitrary Messaging Bridge (AMB)**</td>
        <td>Allows arbitrary messages to be securely relayed from a smart contract on chain 1 to a smart contract on chain 2.<br /><br />
        AMB provides guarantees that messages delivered to chain 2 represent events finalized on chain 1.</td>
      </tr>

      <tr>
        <td>**Token Bridge**</td>
        <td>Allows user to lock native tokens or ERC20 tokens on chain 1 and mint claim tokens on chain 2.<br /><br />
        Bridge maintains the invariant that, for each token minted on chain 2, there exists a corresponding token locked on chain 1.</td>
      </tr>

      <tr>
        <td>**Intents Bridge / Liquidity Layer**</td>
        <td>Allows user to turn in tokens on one chain and quickly redeem tokens on another chain,
        typically relying on drawing on a pool of assets maintained on each side. Provides
        greater immediacy relative to waiting for full finality of an AMB.</td>
      </tr>

      <tr>
        <td>**Bridge Aggregator**</td>
        <td>Aggregates multiple liquidity layers or token bridges, potentially integrating
        swapping as well so that users may receive a different token than the one they input.</td>
      </tr>

      <tr>
        <td>**Chain Abstraction**</td>
        <td>Enables a user experience exempt from the manual processes required to interact with multiple chains.</td>
      </tr>
    </tbody>
  </table>
</div>

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Bridge Type</th>
            <th>Contract Addresses</th>
            <th>Explorer</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Across](https://app.across.to/bridge-and-swap)</td>
            <td>✅</td>
            <td>[Docs](https://docs.across.to/)</td>
            <td>Intents Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/across.jsonc)</td>

            <td />
          </tr>

          <tr>
            <td>[Axelar](https://www.axelar.network/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.axelar.dev/)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/axelar.jsonc)</td>
            <td>[Axelarscan](https://axelarscan.io/)</td>
          </tr>

          <tr>
            <td>[Bungee](https://www.bungee.exchange/?fromChainId=1\&fromTokenAddress=0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee\&toChainId=143\&toTokenAddress=0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee)</td>
            <td>✅</td>
            <td>[Docs](https://docs.bungee.exchange/)</td>
            <td>Bridge Aggregator</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/bungee.jsonc)</td>

            <td />
          </tr>

          <tr>
            <td>[ChangeHero](https://changehero.io/)</td>
            <td>✅</td>
            <td>[Docs](https://api-docs.changehero.io/)</td>
            <td>Bridge Aggregator</td>

            <td />

            <td />
          </tr>

          <tr>
            <td>[Chainlink CCIP](https://chain.link/cross-chain)</td>
            <td>✅</td>
            <td>[Docs](https://docs.chain.link/ccip)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/chainlink.jsonc)</td>
            <td>[CCIP Explorer](https://ccip.chain.link/)</td>
          </tr>

          <tr>
            <td>[Circle CCTP](https://www.circle.com/cross-chain-transfer-protocol)</td>
            <td>✅</td>
            <td>[Docs](https://developers.circle.com/cctp)</td>
            <td>Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/circle_cctp.jsonc)</td>

            <td />
          </tr>

          <tr>
            <td>[deBridge](https://app.debridge.com/?inputChain=1\&outputChain=143)</td>
            <td>✅</td>
            <td>[Docs](https://docs.debridge.com/)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/debridge.jsonc)</td>
            <td>[deExplorer](https://app.debridge.finance/orders)</td>
          </tr>

          <tr>
            <td>[Flashnet](https://flashnet.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.flashnet.xyz/products/orchestration/overview)</td>
            <td>Liquidity Layer</td>

            <td />

            <td />
          </tr>

          <tr>
            <td>[Garden](https://garden.finance/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.garden.finance/)</td>
            <td>Token Bridge for BTC</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/garden.jsonc)</td>

            <td />
          </tr>

          <tr>
            <td>[Gas.zip](https://www.gas.zip)</td>
            <td>✅</td>
            <td>[Docs](https://dev.gas.zip)</td>
            <td>Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/gas_zip.jsonc)</td>
            <td>[Explorer](https://www.gas.zip/scan)</td>
          </tr>

          <tr>
            <td>[Houdini](https://houdiniswap.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.houdiniswap.com/overview/getting-started/what-is-houdini)</td>
            <td>Bridge Aggregator</td>

            <td />

            <td />
          </tr>

          <tr>
            <td>[Hyperlane](https://nexus.hyperlane.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.hyperlane.xyz)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/hyperlane_nexus.jsonc)</td>
            <td>[Hyperlane Explorer](https://explorer.hyperlane.xyz)</td>
          </tr>

          <tr>
            <td>[Jumper](https://jumper.exchange)</td>
            <td>✅</td>

            <td />

            <td>Bridge aggregator</td>

            <td />

            <td />
          </tr>

          <tr>
            <td>[LayerZero](https://layerzero.network/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.layerzero.network)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/layerzero.jsonc)</td>
            <td>[LayerZeroScan](https://testnet.layerzeroscan.com/)</td>
          </tr>

          <tr>
            <td>[Li.fi](https://li.fi/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.li.fi/)</td>
            <td>Bridge aggregator SDK</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/li_fi.jsonc)</td>
            <td>[Li.Fi Scan](https://scan.li.fi/)</td>
          </tr>

          <tr>
            <td>[Mayan](https://swap.mayan.finance/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.mayan.finance/)</td>
            <td>Bridge Aggregator</td>

            <td />

            <td>[Mayan Explorer](https://explorer.mayan.finance/)</td>
          </tr>

          <tr>
            <td>[Particle Network](https://particle.network/)</td>
            <td>✅</td>
            <td>[Docs](https://developers.particle.network/intro/introduction)</td>
            <td>Chain Abstraction</td>

            <td />

            <td>Explorer: `https://universalx.app/activity/details?id=${transactionId}`<br />
            (Replace `transactionId`)</td>
          </tr>

          <tr>
            <td>[Polymer](https://polymerlabs.org/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.polymerlabs.org/docs/build/start/)</td>
            <td>AMB</td>

            <td />

            <td>[PolyScan](https://dashboard.polymerlabs.org/)</td>
          </tr>

          <tr>
            <td>[Relay](https://relay.link/bridge)</td>
            <td>✅</td>
            <td>[Docs](https://docs.relay.link)</td>
            <td>Liquidity Layer</td>

            <td />

            <td>[Transactions](https://relay.link/transactions)</td>
          </tr>

          <tr>
            <td>[SimpleSwap](https://simpleswap.io/)</td>
            <td>✅</td>
            <td>[Docs](https://api.simpleswap.io/docs/getting-started/)</td>
            <td>Bridge Aggregator</td>

            <td />

            <td />
          </tr>

          <tr>
            <td>[Socket](https://www.socket.tech/)</td>
            <td>✅</td>
            <td>[Docs](https://www.socket.tech/)</td>
            <td>AMB</td>

            <td />

            <td>[Socketscan](https://www.socketscan.io/)</td>
          </tr>

          <tr>
            <td>[Squid](https://www.squidrouter.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.squidrouter.com)</td>
            <td>Liquidity Layer</td>

            <td />

            <td>[Explorer (Axelarscan)](https://axelarscan.io)</td>
          </tr>

          <tr>
            <td>[Stargate](https://stargate.finance/?srcChain=ethereum\&srcToken=0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48\&dstChain=monad\&dstToken=0x754704Bc059F8C67012fEd69BC8A327a5aafb603)</td>
            <td>✅</td>
            <td>[Docs](https://docs.stargate.finance/)</td>
            <td>Liquidity Layer</td>

            <td />

            <td />
          </tr>

          <tr>
            <td>[Trails](https://trails.build/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.trails.build/)</td>
            <td>Intents Bridge / Liquidity Layer</td>

            <td />

            <td />
          </tr>

          <tr>
            <td>[Trustware](https://trustware.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.trustware.io/)</td>
            <td>Chain Abstraction</td>

            <td />

            <td />
          </tr>

          <tr>
            <td>[Wormhole](https://wormhole.com/) / [Portal](https://portalbridge.com/)</td>
            <td>✅</td>
            <td>[Docs](https://wormhole.com/docs)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/wormhole_portal.jsonc)</td>
            <td>[WormholeScan](https://wormholescan.io/#/?network=Testnet)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Bridge Type</th>
            <th>Contract Addresses</th>
            <th>Explorer</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>Axelar</td>
            <td>✅</td>
            <td>[Docs](https://docs.axelar.dev/)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/testnet/axelar.jsonc)</td>
            <td>[Axelarscan](https://axelarscan.io/)</td>
          </tr>

          <tr>
            <td>Chainlink CCIP</td>
            <td>✅</td>
            <td>[Docs](https://docs.chain.link/ccip)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/testnet/chainlink_ccip.jsonc)</td>
            <td>[CCIP Explorer](https://ccip.chain.link/)</td>
          </tr>

          <tr>
            <td>[Garden](https://testnet.garden.finance)</td>
            <td>✅</td>
            <td>[Docs](https://docs.garden.finance/)</td>
            <td>Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/testnet/garden.jsonc)</td>

            <td />
          </tr>

          <tr>
            <td>LayerZero</td>
            <td>✅</td>
            <td>[Docs](https://docs.layerzero.network)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/testnet/layerzero.jsonc)</td>
            <td>[LayerZeroScan](https://testnet.layerzeroscan.com/)</td>
          </tr>

          <tr>
            <td>Polymer</td>
            <td>✅</td>
            <td>[Docs](https://docs.polymerlabs.org/docs/build/start)</td>
            <td>AMB</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/testnet/polymer.jsonc)</td>
            <td>[PolyScan](https://dashboard.sepolia.polymer.zone/)</td>
          </tr>

          <tr>
            <td>Wormhole</td>
            <td>✅</td>
            <td>[Docs](https://wormhole.com/docs)</td>
            <td>AMB; Token Bridge</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/testnet/wormhole_portal.jsonc)</td>
            <td>[WormholeScan](https://wormholescan.io/#/?network=Testnet)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Axelar

[Axelar](https://www.axelar.network/) is an interchain platform that connects blockchains to enable universal web3 transactions. By integrating with Axelar, applications built on Monad can now easily send messages and assets between the 49+ blockchains connected via Axelar.

To learn more about Axelar visit our [docs](https://docs.axelar.dev/) and [GitHub](https://github.com/axelarnetwork/axelar-examples).

To view current transactions and live stats about the Axelar network, please visit the [Axelarscan block explorer](https://axelarscan.io/).

### Bungee Exchange

[Bungee](https://www.bungee.exchange/) provides seamless swaps between any blockchain. With over
\$24B in volume and trusted by major wallets and dApps, Bungee makes moving assets between networks
efficient, secure, and accessible to everyone, powered by the SOCKET.

To learn more, check out the [docs](https://docs.bungee.exchange/).

### ChangeHero

[ChangeHero](https://changehero.io/) is a cross-chain swap platform enabling frictionless asset exchanges across a wide range of networks. Leveraging aggregated liquidity and optimized routing logic, it delivers fast settlement and consistent pricing for any supported pair. Its clean integration pathways and dependable execution make ChangeHero a straightforward tool for powering multi-chain swaps within decentralized applications.

To learn more, check out the [docs](https://api-docs.changehero.io/).

### Chainlink CCIP

[Chainlink](https://chain.link/) Cross-Chain Interoperability Protocol (CCIP) is the standard for cross-chain interoperability. CCIP enables developers to build secure cross-chain apps that can transfer tokens, send messages, and initiate actions across blockchains.

Through the [Cross-Chain Token (CCT)](https://blog.chain.link/ccip-v-1-5-upgrade/) standard, CCIP enables token developers to integrate new and existing tokens with CCIP in a self-serve manner in minutes, without requiring vendor lock-in, hard-coded functions, or external dependencies that may limit future optionality. CCTs support self-serve deployments, full control and ownership for developers, zero-slippage transfers, and enhanced programmability via configurable rate limits and reliability features such as Smart Execution. CCIP is powered by Chainlink decentralized oracle networks (DONs)—a proven standard with a track record of securing tens of billions of dollars and enabling over \$19 trillion in onchain transaction value.

Key CCIP developer tools:

* [CCIP official documentation](https://docs.chain.link/ccip): start integrating CCIP into your cross-chain application.
* [CCIP Token Manager](https://tokenmanager.chain.link/): an intuitive front-end web interface for the deployment of new and management of existing CCTs by their developers, including no-code guided deployments and configuration tools.
* [CCIP SDK](https://docs.chain.link/ccip/ccip-javascript-sdk): a software development kit that streamlines the process of integrating CCIP, allowing developers to use JavaScript to create a token transfer frontend dApp.

Contract Addresses:

* Router (testnet): [`0x5f16e51e3Dcb255480F090157DD01bA962a53E54`](https://testnet.monadvision.com/address/0x5f16e51e3Dcb255480F090157DD01bA962a53E54)
* Router (mainnet): `0x33566fE5976AAa420F3d5C64996641Fc3858CaDB`

### Circle CCTP

[Cross-Chain Transfer Protocol (CCTP)](https://www.circle.com/cross-chain-transfer-protocol) by Circle is a permissionless onchain utility that facilitates USDC transfers securely between supported blockchains via native burning and minting.

Circle created CCTP to improve capital efficiency and minimize trust assumptions when using USDC across blockchains.

CCTP enables developers to build multichain applications that allow users to perform 1:1 transfers of USDC securely across blockchains.

To get started, visit the [Circle CCTP documentation](https://developers.circle.com/cctp)

### deBridge

Build once, interoperate everywhere. deBridge enables secure, fast, and capital-efficient
connectivity across 20+ chains, so you can swap and transfer assets natively, trigger Cross-Chain
logic in seconds, all with chain abstraction and one unified protocol.

To get started, visit the deBridge [documentation](https://docs.debridge.com/) or check out the
[app](https://app.debridge.finance/).

### Flashnet

[Flashnet](https://flashnet.xyz/) builds Bitcoin exchange infrastructure. Its Orchestra API enables cross-chain swaps between stablecoins and native BTC with sub-10 second settlement and ultra-low-fees. Orchestra handles all routing, execution, and settlement, allowing applications on Monad to offer the best native Bitcoin swaps through a single integration.

To get started, visit the [documentation](https://docs.flashnet.xyz/products/orchestration/overview).

### Garden

[Garden](https://garden.finance/) is transforming Bitcoin interoperability with its next-gen bridge. It is built by the renBTC team using an intents based architecture with trustless settlement, enabling cross-chain Bitcoin swaps in as little as 30 seconds with zero custody risk.

In its first year, Garden processed over \$1 billion in volume—proving the market's demand for seamless, cost-effective Bitcoin bridging solutions.

Now, Garden is unlocking a new era of interoperability—supporting non-likewise assets, external liquidity, and a wallet-friendly API—to onboard the next wave of partners and users.

To get started, visit the [documentation](https://docs.garden.finance/).

### Gas.zip

[Gas.zip](https://www.gas.zip/) is a token bridge that enables seamless cross-chain asset transfers.

Contract Address:

* Deployment: `0x9E22ebeC84c7e4C4bD6D4aE7FF6f4D436D6D8390`

### Houdini

[Houdini](https://houdiniswap.com/) is a non-custodial, privacy-focused cross-chain swap aggregator that routes transactions through a combination of decentralized exchanges, centralized exchange liquidity, and cross-chain solvers. It supports swaps across 100+ chains, including Monad, without requiring users to bridge manually, connect a wallet, or complete KYC.

Houdini offers three swap modes: Private Swap (breaks the on-chain link between sender and receiver via compliant privacy routing), No Wallet Connect Swap (execute a swap with only a receiving address), and Onchain DEX Swap (cross-chain swaps via leading DEXs). It includes MEV protection, slippage control, gasless options, and AML/OFAC screening.

To get started, visit the [Houdini documentation](https://docs.houdiniswap.com/overview/getting-started/what-is-houdini) or explore the [developer hub](https://docs.houdiniswap.com/developer-hub/overview/what-you-can-build) for API integration.

### Hyperlane

[Hyperlane](https://hyperlane.xyz/) is a permissionless interoperability protocol for cross-chain communication. It enables message passing and asset transfers across different chains without relying on centralized intermediaries or requiring any permissions.

To get started, visit the [Hyperlane documentation](https://docs.hyperlane.xyz/).

#### Hyperlane Explorer

To view status of your cross chain transactions, please visit the [Hyperlane Explorer](https://explorer.hyperlane.xyz/).

### LayerZero

[LayerZero](https://layerzero.network/) is an omnichain interoperability protocol that enables cross-chain messaging. Applications built on Monad can use the LayerZero protocol to connect to 35+ supported blockchains seamlessly.

To get started with integrating LayerZero, visit the LayerZero [documentation](https://docs.layerzero.network/v1/developers/evm/evm-guides/send-messages) and provided examples on [GitHub](https://github.com/LayerZero-Labs/endpoint-v1-solidity-examples).

### Li.fi

[LI.FI](https://li.fi/) delivers a seamless solution for multi-chain payments and swaps through a single unified API and SDK. By combining access to all liquidity sources—including DEX aggregators, bridges, and solvers—it ensures comprehensive coverage across ecosystems. Its smart routing technology identifies the cheapest and fastest path for any payment or trade, optimizing efficiency and cost.

Additionally, LI.FI offers a plug-and-play [widget](https://docs.li.fi/widget/overview) that enables instant, user-friendly payment flows, making integration simple for developers and intuitive for end users.

To get started, visit [Li.fi documentation](https://docs.li.fi/)

### Particle Network

Particle Network enables chain abstraction through its [Universal Accounts](https://developers.particle.network/universal-accounts/cha/overview) (UA) infrastructure. A UA provides each user with a single account and a combined balance across [multiple chains](https://developers.particle.network/universal-accounts/cha/chains) (EVM and non-EVM).

This allows users to interact with a dApp on Monad even if their assets are held on another network—without manual bridging or chain-switching.

Universal Accounts support:

* Cross-chain deposits and swaps without manual bridging  
* Unified balance aggregation across chains  
* Gas abstraction, allowing transaction fees to be paid in any [supported token](https://developers.particle.network/universal-accounts/cha/chains#primary-assets)

### Mayan

[Mayan](https://mayan.finance/) is a cross-chain swap protocol that enables fast and efficient token transfers across multiple blockchains.

Mayan provides seamless token bridging with optimized routing to ensure the best execution for cross-chain transfers.

To get started, visit the [Mayan documentation](https://docs.mayan.finance/) or explore transactions on the [Mayan Explorer](https://explorer.mayan.finance/).

### Polymer

[Polymer](https://www.polymerlabs.org/) is an interoperability protocol tailor made for multi-rollup applications. It places control in the hands of the builder, by combining cross-chain merkle proofs and a simple API to allow application builders to flexibly adopt Polymer's infrastructure for their own needs. Prove any action. Cross-chain.

To get started visit the [Polymer documentation](https://docs.polymerlabs.org/docs/build/start).

### Relay

[Relay](https://relay.link/bridge) is the fastest and cheapest way to bridge and transact across chains, offering a multichain payments network that makes swapping and transacting across hundreds of blockchains delightfully simple. Since its launch in 2024, Relay has served over 5 million users, processed 50 million transactions, and facilitated more than \$5 billion in volume across 85+ networks.

At its core, Relay combines two powerful components: instant, low-cost cross-chain intents powered by the Relay Protocol, and comprehensive DEX meta-aggregation spanning 85 chains (including Monad), ensuring users always get the best execution.

To get started, visit the [Relay documentation](https://docs.relay.link/what-is-relay)

### SimpleSwap

[SimpleSwap](https://simpleswap.io/) is a privacy-focused, self-custody crypto exchange aggregator with 3000+ currencies and cross-chain support across 130+ blockchains. It offers competitive rates and timing, significantly simplifying buying and exchanging crypto with sign-up-free solutions.

To learn more, check out the [docs](https://api.simpleswap.io/docs/getting-started/).

### Socket

[SOCKET Protocol](https://socket.tech) is the first chain-abstraction protocol, empowering
developers to build applications that seamlessly leverage multiple blockchains. It enables the
creation of chain-abstracted apps that interact across chains as if operating on a single one.

To get started, visit the SOCKET [documentation](https://docs.socket.tech/).

### Squid

[Squid](https://www.squidrouter.com/) creates unlimited access for anything in crypto. Squid can be used to seamlessly swap tokens from 100+ chains across including Monad.

Squid’s API, SDK, and Widgets offer ease of integration for projects building on any chain to enable cross-chain functionality in just 1 click.

### Stargate

[Stargate Finance](https://stargate.finance) is a cross-chain bridge protocol that enables users
to transfer native assets between different blockchains with instant guaranteed finality using
unified liquidity pools.

To get started, visit the Stargate [documentation](https://docs.stargate.finance/).

### Trails

[Trails](https://trails.build/) is the universal intents SDK for 1-click crypto transactions. Trails lets users transact with any wallet, any token, across any chain by orchestrating swaps, bridges, and payments behind the scenes. Developers can integrate pay, swap, fund, and checkout flows through a single SDK with cross-chain execution, gasless transactions, and the ability to pay gas with any token including USDC.

To get started, visit the [documentation](https://docs.trails.build/).

### Trustware

[Trustware](https://trustware.io/) is a chain abstraction platform that acts as a Universal Deposit Layer, letting apps accept any asset on any chain and settle to any destination. It handles routing, swaps, and settlement under the hood, so users on Monad can deposit from another chain or token without manual bridging or chain-switching. Trustware can be integrated via a drop-in React widget, a hosted wallet bridge, or a headless REST API for backend control.

To get started, visit the [documentation](https://docs.trustware.io/).

### Wormhole

[Wormhole](https://wormhole.com/) is a cross-chain interoperability protocol that provides secure communication between blockchains. Monad uses two Wormhole products: **Messaging** and **NTT (Native Token Transfers)**.

By integrating Wormhole, a Monad application can access users and liquidity on > 30 chains and > 7 different platforms.

#### Wormhole Messaging

Wormhole Messaging is a generic messaging protocol that enables secure cross-chain communication and arbitrary data transfer between blockchains.

To get started with Wormhole Messaging:

* [Quickstart Guide](https://wormhole.com/docs/products/messaging/get-started/)
* [GitHub Examples](https://github.com/wormhole-foundation/demo-wormhole-messaging)

#### Wormhole NTT (Native Token Transfers)

Wormhole NTT (Native Token Transfer) framework enables seamless cross-chain token movement without wrapping or liquidity pools, allowing projects to maintain token ownership and customize their cross-chain token deployment.

To get started with Wormhole NTT:

* [Quickstart Guide](https://wormhole.com/docs/products/token-transfers/native-token-transfers/get-started/)
* [GitHub Examples](https://github.com/wormhole-foundation/demo-ntt-connect)

For end-users looking to bridge assets, you can use [Wormhole Portal Bridge](https://portalbridge.com).

For more information on integrating Wormhole, visit their [documentation](https://wormhole.com/docs/).

Contract Addresses for Monad Testnet:

* Core: [`0xBB73cB66C26740F31d1FabDC6b7A46a038A300dd`](https://testnet.monadvision.com/address/0xBB73cB66C26740F31d1FabDC6b7A46a038A300dd)
* Relayer: [`0x362fca37E45fe1096b42021b543f462D49a5C8df`](https://testnet.monadvision.com/address/0x362fca37E45fe1096b42021b543f462D49a5C8df)


# Custody
Source: https://docs.monad.xyz/tooling-and-infra/custody



<Note>
  See also [Institutional Wallets](/tooling-and-infra/wallets/institutional-wallets).
</Note>

## Provider Summary

The Monad blockchain and MON token are supported by a number of leading custody providers.

<div>
  <table>
    <thead>
      <tr>
        <th>Service</th>
        <th>Supported (Mainnet)</th>
        <th>Docs</th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td>[Anchorage Digital](https://www.anchorage.com/)</td>
        <td>✅</td>

        <td />
      </tr>

      <tr>
        <td>[BitGo](https://www.bitgo.com/)</td>
        <td>✅</td>
        <td>[Docs](https://developers.bitgo.com/)</td>
      </tr>

      <tr>
        <td>[Coinbase Custody](https://www.coinbase.com/custody)</td>
        <td>✅</td>
        <td>[Docs](https://docs.cdp.coinbase.com/prime/introduction/welcome)</td>
      </tr>

      <tr>
        <td>[Fireblocks](https://www.fireblocks.com/)</td>
        <td>✅</td>
        <td>[Docs](https://developers.fireblocks.com/)</td>
      </tr>

      <tr>
        <td>[HexTrust](https://www.hextrust.com/)</td>
        <td>✅</td>

        <td />
      </tr>
    </tbody>
  </table>
</div>

## Provider Details

### Anchorage Digital

As the trusted custodian for leading institutions, Anchorage Digital offers a solution built to
deliver the highest standards of security, mitigating the risk of human error and attack vectors
while offering participation in digital assets through regulated entities.

Clients can access Anchorage Digital's custody services through Anchorage Digital Bank, the only
federally chartered crypto bank in the U.S. and an unequivocal qualified custodian, or Anchorage
Digital Singapore, a licensed Major Payment Institution by the Monetary Authority of Singapore (MAS).

Learn more at [anchorage.com](https://www.anchorage.com/).

### BitGo

BitGo is the digital asset infrastructure company, delivering custody, wallets, staking, trading,
financing, and settlement services from regulated cold storage. Since its founding in 2013, BitGo
has been focused on accelerating the transition of the financial system to a digital asset economy.
With a global presence and multiple regulated entities, BitGo serves thousands of institutions,
including many of the industry's top brands, exchanges, platforms, and millions of investors.

For more information, visit [bitgo.com](https://www.bitgo.com/).

### Coinbase Custody

Coinbase Custody provides a secure, institutional-grade cold storage solution for digital assets,
enabling institutions to safely store and manage crypto assets with advanced security measures and
operational controls.

Learn more at [coinbase.com/custody](https://www.coinbase.com/custody).

### Fireblocks

Fireblocks is the world's most trusted digital asset infrastructure company, empowering
organizations of all sizes to build, manage and grow their business on the blockchain.
Secure and manage your digital assets with cutting-edge security technology, execute day-to-day
treasury operations with automated workflows and connect seamlessly to exchanges, on/off-ramps,
and DeFi protocols to access liquidity and earn yield.

Learn more at [fireblocks.com](https://www.fireblocks.com/).

### HexTrust

Hex Trust is a licensed and regulated financial institution for digital assets, providing
institutional-grade Markets, Custody, and Staking solutions. Trusted by builders, investors, and
service providers, Hex Trust integrates directly with protocols and platforms to deliver secure,
compliant, and scalable digital asset infrastructure.

Learn more at [hextrust.com](https://www.hextrust.com/).


# Tooling and Infrastructure
Source: https://docs.monad.xyz/tooling-and-infra/index



The most popular Ethereum tools and infrastructure providers support Monad. The enclosing pages survey each category of tools and attempt a feature comparison.

See also the [`protocols`](https://github.com/monad-crypto/protocols) repo for a listing of contract addresses for each protocol.

<CardGroup>
  <Card title="Analytics" href="/tooling-and-infra/analytics">
    Tools for understanding app activity on Monad
  </Card>

  <Card title="Block Explorers" href="/tooling-and-infra/block-explorers">
    View accounts and transactions; read and write contracts
  </Card>

  <Card title="Cross-Chain" href="/tooling-and-infra/cross-chain">
    Bridges and protocols for cross-chain communication
  </Card>

  <Card title="Custody" href="/tooling-and-infra/custody">
    Institutional-grade custody solutions for secure asset management
  </Card>

  <Card title="Indexers" href="/tooling-and-infra/indexers">
    Common transformations for blockchain data + custom calculators
  </Card>

  <Card title="Onramps" href="/tooling-and-infra/onramps">
    Ways to convert between fiat and crypto
  </Card>

  <Card title="Oracles" href="/tooling-and-infra/oracles">
    Data feeds bringing off-chain information on-chain
  </Card>

  <Card title="Payment Orchestrators" href="/tooling-and-infra/payment-orchestrators">
    Unified APIs that route stablecoin and fiat flows across providers and chains
  </Card>

  <Card title="RPC Providers" href="/tooling-and-infra/rpc-providers">
    Endpoints for interacting with Monad
  </Card>

  <Card title="Toolkits" href="/tooling-and-infra/toolkits">
    Development frameworks and tools for building on Monad
  </Card>

  <Card title="Wallets" href="/tooling-and-infra/wallets">
    Tools for storing private keys, signing transactions, and managing assets
  </Card>

  <Card title="Wallet Infrastructure" href="/tooling-and-infra/wallet-infra">
    Embedded wallets and smart accounts
  </Card>
</CardGroup>


# Common Data
Source: https://docs.monad.xyz/tooling-and-infra/indexers/common-data



## Features

In order to improve developer understanding of feature coverage, we have collected the most common features offered by providers:

| Feature         | Sub-Feature | Description                                                                                                                    |
| --------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Chain data**  |             | Raw data (blocks, transactions, logs, traces) in SQL-like format. Transactions and logs may optionally be decoded based on ABI |
| **Balances**    | Native      | Native token holdings of an address, real-time or snapshot. May include price annotations                                      |
|                 | ERC20       | ERC20 holdings of an address, real-time or snapshot. May include price annotations                                             |
|                 | NFT         | NFT (ERC721 or ERC1155) holdings of an address, real-time or snapshot                                                          |
| **Transfers**   | Native      | Native token transfers involving a particular address. May include price annotations                                           |
|                 | ERC20       | ERC20 transfers involving a particular address. May include price annotations                                                  |
|                 | NFT         | NFT transfers involving a particular address                                                                                   |
| **DEX trades**  |             | Normalized trade data across major DEXes                                                                                       |
| **Market data** |             | Market data for ERC20s                                                                                                         |

Balances are nontrivial because each ERC20 and NFT collection stores its balances in contract storage. Transfers are nontrivial because they frequently occur as subroutines. Annotating with prices and normalizing across DEXes add additional convenience.

## Access models

* **APl**: Data lives on provider's servers; make queries via API
* **Stream**: Data is replicated to your environment

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Supported services</th>
            <th>Access model</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Allium](https://www.allium.so/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.allium.so/)</td>
            <td>**Chain data** (blocks, transactions, logs, traces, contracts) (via [Explorer](https://docs.allium.so/app/overview) (historical) and [Datastreams](https://docs.allium.so/realtime/kafka-blockchains-70+) (realtime) products)<br />
            **Transfers** (native, ERC20, and NFTs) (via [Developer](https://docs.allium.so/data-products-real-time/allium-developer/wallet-apis/activities) (realtime) product)</td>
            <td>API, except streaming for Datastreams product</td>
          </tr>

          <tr>
            <td>[Birdeye Data Services](https://bds.birdeye.so/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.birdeye.so/)</td>
            <td>[**DEX trades**](https://docs.birdeye.so/reference/get-defi-price)<br />
            [**Market data**](https://docs.birdeye.so/reference/get-defi-v3-token-market-data) for tokens<br />
            [**Token metadata**](https://docs.birdeye.so/reference/get-defi-tokenlist) and analytics</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Codex](https://www.codex.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.codex.io/)</td>
            <td>Token- and trading-centric data:<br />
            [Token](https://docs.codex.io/recipes/discover-tokens) charts, metadata, prices, events, and detailed stats<br />
            NFT metadata, events, and detailed stats</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Dune Sim](https://sim.dune.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sim.dune.com/)</td>
            <td>**Chain data:** Transactions, logs (raw or decoded)<br />
            **Balances:** Native, ERC20</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[GoldRush](https://goldrush.dev/) (by Covalent)</td>
            <td>✅</td>
            <td>[Docs](https://goldrush.dev/docs/overview)</td>
            <td>**Chain data:** Blocks, enriched transactions and logs (raw and decoded)<br />
            **Balances:** native, ERC20, NFTs & Portfolio<br />
            **Transactions:** Full historical with decoded transfer events</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Goldsky](https://goldsky.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.goldsky.com/)</td>
            <td>**Chain data:** blocks, enriched transactions, logs, and traces via [Mirror](https://docs.goldsky.com/mirror/introduction). [Fast scan](https://docs.goldsky.com/mirror/sources/direct-indexing#backfill-vs-fast-scan) is supported</td>
            <td>API; Streaming</td>
          </tr>

          <tr>
            <td>[Mobula](https://mobula.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.mobula.io/introduction)</td>
            <td>**Chain data**<br />
            **Balances:** [native, ERC20](https://docs.mobula.io/rest-api-reference/endpoint/wallet-portfolio) and [NFT](https://docs.mobula.io/rest-api-reference/endpoint/wallet-nfts)<br />
            **Transfers:** [native, ERC20](https://docs.mobula.io/rest-api-reference/endpoint/wallet-transactions) and NFT<br />
            [**DEX trades**](https://docs.mobula.io/rest-api-reference/endpoint/market-trades-pair)<br />
            [**Market data**](https://docs.mobula.io/rest-api-reference/endpoint/market-data) for ERC20s</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Moralis](https://moralis.com)</td>
            <td>✅</td>
            <td>[Docs](https://docs.moralis.com)</td>
            <td>**Chain Data:** [blocks](https://docs.moralis.com/web3-data-api/evm/reference/blockchain-api#get-blocks), [transactions](https://docs.moralis.com/web3-data-api/evm/reference/blockchain-api#get-transactions), [logs](https://docs.moralis.com/rpc-nodes/reference/eth_getLogs)<br />
            **Balances:** [native, ERC20,](https://docs.moralis.com/web3-data-api/evm/reference/wallet-api/get-wallet-token-balances-price?address=0xcB1C1FdE09f811B294172696404e88E658659905\&chain=eth\&token_addresses=\[]\&limit=50) [NFTs](https://docs.moralis.com/web3-data-api/evm/reference/wallet-api#get-wallet-nft-balances) (with metadata, logos, spam / low-liquidity filtering)<br />
            [**Token Prices**](https://docs.moralis.com/web3-data-api/evm/reference/price-api#get-token-prices): USD valuation included<br />
            **Transfers:** [native, ERC20](https://docs.moralis.com/web3-data-api/evm/reference/wallet-api/get-transactions-by-wallet?address=0x1f9090aaE28b8a3dCeaDf281B0F12828e676c326\&chain=eth\&limit=50\&order=DESC), and [NFTs](https://docs.moralis.com/web3-data-api/evm/reference/wallet-api/get-wallet-nft-transfers?address=0xcB1C1FdE09f811B294172696404e88E658659905\&chain=eth\&contract_addresses=\[]\&format=decimal\&limit=25\&order=DESC) (decoded events), [wallet history](https://docs.moralis.com/web3-data-api/evm/reference/wallet-api/get-wallet-history?address=0xcB1C1FdE09f811B294172696404e88E658659905\&chain=eth\&order=DESC\&limit=25) (categorized transfers + approvals)<br />
            [**Streams**](https://docs.moralis.com/streams-api/evm): real-time address/contract monitoring via webhooks<br />
            [**Datashare**](https://moralis.com/datashare/): Export massive crypto datasets<br />
            [**RPC Nodes**](https://docs.moralis.com/rpc-nodes): Raw blockchain data access</td>
            <td>APIs, Streaming (webhooks)</td>
          </tr>

          <tr>
            <td>[Quicknode](https://www.quicknode.com/)</td>
            <td>✅</td>
            <td>[Docs](https://www.quicknode.com/docs/streams/getting-started)</td>
            <td>[**Streams**](https://www.quicknode.com/streams), [**Webhooks**](https://www.quicknode.com/webhooks)</td>
            <td>Streams, Webhooks</td>
          </tr>

          <tr>
            <td>[Rarible](https://rarible.org/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.rarible.org/)</td>
            <td>[**NFT data**](https://docs.rarible.org/reference): metadata; holdings by address (current and historic); trade data; spam scoring</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Sequence](https://sequence.xyz/)</td>
            <td>❓</td>
            <td>[Docs](https://docs.sequence.xyz/solutions/indexer/overview)</td>
            <td>**Balances**: native, ERC20, and NFT<br />
            **Transfers**: native, ERC20, and NFTs<br />
            **Other:** Transaction history; webhooks</td>
            <td>API; Streaming (webhooks)</td>
          </tr>

          <tr>
            <td>[SQD](https://sqd.ai/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sqd.ai/)</td>
            <td>**Chain data:** blocks, transactions, logs, traces, state diffs (via [Portal](https://docs.sqd.dev/en/portal/evm/overview) and [Subsquid SDK](https://github.com/subsquid/squid-sdk))<br />
            **Other:** [MCP server](https://docs.sqd.dev/en/ai/mcp-server) for AI agent integration</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[SonarX](https://sonarx.com)</td>
            <td>✅</td>

            <td />

            <td>**Chain data:** blocks, transactions, logs, traces<br />
            **Transfers:** tokens, NFTs, internal transfers, net internal transfers (with/without pricing)<br />
            **Balances:** PIT and current balances<br />
            **DEX trades** and balances<br />
            **Other:** Approvals and failed transactions</td>
            <td>Cloud Platforms Data Shares (Snowflake, BigQuery, Azure, Databricks); Streaming (Kafka); File delivery (CSV, Parquet, Iceberg); API</td>
          </tr>

          <tr>
            <td>[thirdweb](https://thirdweb.com/)</td>
            <td>✅</td>
            <td>[Docs](https://insight-api.thirdweb.com/guide/getting-started)</td>
            <td>**Chain data:** [blocks](https://insight-api.thirdweb.com/reference#tag/blocks), [transactions](https://insight-api.thirdweb.com/guide/blueprints#transactions-blueprint), [logs](https://insight-api.thirdweb.com/guide/blueprints#events-blueprint), [contracts](https://insight-api.thirdweb.com/reference#tag/contracts)<br />
            [**Balances**](https://insight-api.thirdweb.com/guide/blueprints#tokens-blueprint): native, ERC20, NFTs<br />
            **Other:** [NFTs](https://insight-api.thirdweb.com/reference#tag/nfts)</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Unmarshal](https://unmarshal.io/)</td>
            <td>❓</td>
            <td>[Docs](https://docs.unmarshal.io)</td>
            <td>[**Balances**](https://docs.unmarshal.io/reference/fungibleerc20tokenbalances): ERC20 and NFT<br />
            [**Transactions**](https://docs.unmarshal.io/reference/get-v3-chain-address-address-transactions) with price annotations<br />
            [**NFT API**](https://docs.unmarshal.io/reference/get-v2-chain-address-address-nft-transactions) (transactions and metadata)</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Zerion](https://zerion.io/)</td>
            <td>✅</td>
            <td>[Docs](https://zerion.io/api)</td>
            <td>[**Wallet info**](https://developers.zerion.io/reference/wallets)<br />
            [**Balances**](https://developers.zerion.io/reference/listwalletpositions) (native, ERC20, and NFTs)<br />
            [**Transactions**](https://developers.zerion.io/reference/listwallettransactions) (multichain with prices)<br />
            **Other:** [Portfolio](https://developers.zerion.io/reference/getwalletportfolio), [PNL](https://developers.zerion.io/reference/getwalletpnl#/) and [Historical Positions](https://developers.zerion.io/reference/getwalletchart)<br />
            [Notification Webhooks](https://developers.zerion.io/v1.0-subscriptions/reference/createsubscriptionwallettransactions)</td>
            <td>API; Webhooks</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Supported services</th>
            <th>Access model</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Allium](https://www.allium.so/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.allium.so/)</td>
            <td>**Chain data** (blocks, transactions, logs, traces, contracts) (via [Explorer](https://docs.allium.so/app/overview) (historical) and [Datastreams](https://docs.allium.so/realtime/kafka-blockchains-70+) (realtime) products)<br />
            **Transfers** (native, ERC20, and NFTs) (via [Developer](https://docs.allium.so/data-products-real-time/allium-developer/wallet-apis/activities) (realtime) product)</td>
            <td>API, except streaming for Datastreams product</td>
          </tr>

          <tr>
            <td>[Codex](https://www.codex.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.codex.io/)</td>
            <td>Token- and trading-centric data:<br />
            [Token](https://docs.codex.io/recipes/discover-tokens) charts, metadata, prices, events, and detailed stats (see [dashboard](https://www.defined.fi/tokens/discover?network=mon-test))<br />
            [NFT](https://docs.codex.io/api-reference/queries/getnftpool) metadata, events, and detailed stats</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Dune Sim](https://sim.dune.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sim.dune.com/)</td>
            <td>**Chain data:** Transactions, logs (raw or decoded)<br />
            **Balances:** Native, ERC20</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[GoldRush](https://goldrush.dev/) (by Covalent)</td>
            <td>✅</td>
            <td>[Docs](https://goldrush.dev/docs/overview)</td>
            <td>**Chain data:** Blocks, enriched transactions and logs (raw and decoded)<br />
            **Balances:** native, ERC20, NFTs & Portfolio<br />
            **Transactions:** Full historical with decoded transfer events</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Goldsky](https://goldsky.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.goldsky.com/)</td>
            <td>**Chain data:** blocks, enriched transactions, logs, and traces via [Mirror](https://docs.goldsky.com/mirror/introduction). [Fast scan](https://docs.goldsky.com/mirror/sources/direct-indexing#backfill-vs-fast-scan) is supported</td>
            <td>API; Streaming</td>
          </tr>

          <tr>
            <td>[Mobula](https://mobula.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.mobula.io/introduction)</td>
            <td>**Chain data**<br />
            **Balances:** [native, ERC20](https://docs.mobula.io/rest-api-reference/endpoint/wallet-portfolio) and [NFT](https://docs.mobula.io/rest-api-reference/endpoint/wallet-nfts)<br />
            **Transfers:** [native, ERC20](https://docs.mobula.io/rest-api-reference/endpoint/wallet-transactions) and NFT<br />
            [**DEX trades**](https://docs.mobula.io/rest-api-reference/endpoint/market-trades-pair)<br />
            [**Market data**](https://docs.mobula.io/rest-api-reference/endpoint/market-data) for ERC20s</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Moralis](https://moralis.com)</td>
            <td>❌</td>
            <td>[Docs](https://docs.moralis.com/)</td>
            <td>**Chain data**<br />
            **Balances:** [native, ERC20](https://docs.moralis.com/web3-data-api/evm/reference/wallet-api/get-wallet-token-balances-price?address=0xcB1C1FdE09f811B294172696404e88E658659905\&chain=eth\&token_addresses=\[]\&limit=50) and [NFT](https://docs.moralis.com/web3-data-api/evm/reference/wallet-api/get-nfts-by-wallet?address=0xff3879b8a363aed92a6eaba8f61f1a96a9ec3c1e\&chain=eth\&format=decimal\&limit=50\&token_addresses=\[]\&normalizeMetadata=true\&media_items=false\&include_prices=false)<br />
            **Transfers:** [native, ERC20](https://docs.moralis.com/web3-data-api/evm/reference/wallet-api/get-transactions-by-wallet?address=0x1f9090aaE28b8a3dCeaDf281B0F12828e676c326\&chain=eth\&limit=50\&order=DESC)<br /></td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Quicknode](https://www.quicknode.com/)</td>
            <td>✅</td>
            <td>[Docs](https://www.quicknode.com/docs/streams/getting-started)</td>
            <td>[**Streams**](https://www.quicknode.com/streams), [**Webhooks**](https://www.quicknode.com/webhooks)</td>
            <td>Streams, Webhooks</td>
          </tr>

          <tr>
            <td>[Sequence](https://sequence.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sequence.xyz/solutions/indexer/overview)</td>
            <td>**Balances**: native, ERC20, and NFT<br />
            **Transfers**: native, ERC20, and NFTs<br />
            **Other:** Transaction history; webhooks</td>
            <td>API; Streaming (webhooks)</td>
          </tr>

          <tr>
            <td>[SQD](https://sqd.ai/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sqd.ai/)</td>
            <td>**Chain data:** blocks, transactions, logs, traces, state diffs (via [Portal](https://docs.sqd.dev/en/portal/evm/overview) and [Subsquid SDK](https://github.com/subsquid/squid-sdk))<br />
            **Other:** [MCP server](https://docs.sqd.dev/en/ai/mcp-server) for AI agent integration</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[SonarX](https://sonarx.com)</td>
            <td>✅</td>

            <td />

            <td>**Chain data:** blocks, transactions, logs, traces<br />
            **Transfers:** tokens, NFTs, internal transfers, net internal transfers (with/without pricing)<br />
            **Balances:** PIT and current balances<br />
            **DEX trades** and balances<br />
            **Other:** Approvals and failed transactions</td>
            <td>Cloud Platforms Data Shares (Snowflake, BigQuery, Azure, Databricks); Streaming (Kafka); File delivery (CSV, Parquet, Iceberg); API</td>
          </tr>

          <tr>
            <td>[thirdweb](https://thirdweb.com/)</td>
            <td>✅</td>
            <td>[Docs](https://insight-api.thirdweb.com/guide/getting-started)</td>
            <td>**Chain data:** [blocks](https://insight-api.thirdweb.com/reference#tag/blocks), [transactions](https://insight-api.thirdweb.com/guide/blueprints#transactions-blueprint), [logs](https://insight-api.thirdweb.com/guide/blueprints#events-blueprint), [contracts](https://insight-api.thirdweb.com/reference#tag/contracts)<br />
            [**Balances**](https://insight-api.thirdweb.com/guide/blueprints#tokens-blueprint): native, ERC20, NFTs<br />
            **Other:** [NFTs](https://insight-api.thirdweb.com/reference#tag/nfts)</td>
            <td>API</td>
          </tr>

          <tr>
            <td>[Zerion](https://zerion.io/)</td>
            <td>✅</td>
            <td>[Docs](https://zerion.io/api)</td>
            <td>[**Wallet info**](https://developers.zerion.io/reference/wallets)<br />
            [**Balances**](https://developers.zerion.io/reference/listwalletpositions) (native, ERC20, and NFTs)<br />
            [**Transactions**](https://developers.zerion.io/reference/listwallettransactions) (multichain with prices)<br />
            **Other:** [Portfolio](https://developers.zerion.io/reference/getwalletportfolio), [PNL](https://developers.zerion.io/reference/getwalletpnl#/) and [Historical Positions](https://developers.zerion.io/reference/getwalletchart)<br />
            [Notification Webhooks](https://developers.zerion.io/v1.0-subscriptions/reference/createsubscriptionwallettransactions)</td>
            <td>API; Webhooks</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Allium

[Allium](https://www.allium.so/) is an Enterprise Data Platform that serves accurate, fast, and simple blockchain data. Allium offers near real-time Monad Testnet data for infrastructure needs and enriched Monad Testnet data (NFT, DEX, Decoded) for research and analytics.

Allium supports data delivery to multiple [destinations](https://docs.allium.so/integrations/overview), including Snowflake, Bigquery, Databricks, and AWS S3. To get started, contact Allium [here](https://www.allium.so/contact).

| Product                                                                          | Description / mechanism                            | Monad Testnet data supported                                                                                          |
| -------------------------------------------------------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [Explorer](https://docs.allium.so/app/overview)                                  | Historical data (postgres/API)                     | Chain data: blocks, transactions, logs, traces, contracts                                                             |
| [Developer](https://docs.allium.so/data-products-real-time/allium-developer)     | Real-time data (postgres/API)                      | [Transfers](https://docs.allium.so/products/allium-developer/wallet-apis/activities) (native, ERC20, ERC721, ERC1155) |
| [Datastreams](https://docs.allium.so/data-products-real-time/allium-datastreams) | Real-time data (streaming - Kafka, PubSub, or SNS) | Chain data: blocks, transactions, logs, traces, contracts                                                             |

### Birdeye Data Services

[Birdeye Data Services](https://bds.birdeye.so/) (BDS) provides comprehensive multi-market data APIs for cryptocurrency tokens, pulling information from decentralized exchanges (DEX). BDS offers real-time and historical token prices, market data, OHLCV charts, trade history, and token metadata.

To get started, visit the [documentation](https://docs.birdeye.so/) or sign up at [bds.birdeye.so](https://bds.birdeye.so/).

### Codex

[Codex](https://www.codex.io/) API provides fast and accurate enriched data, meticulously structured to easily plug straight into your application.

To get started, visit the [documentation](https://docs.codex.io/) or sign up for an API key at [dashboard.codex.io](https://dashboard.codex.io/).

### Dune Sim

[Dune Sim](https://sim.dune.com/) makes building multi-chain application seamless. These APIs power
several of the best teams building on crypto.

Available APIs:

* **Token Balances**: Access accurate and fast real time balances of native and ERC20 tokens of
  accounts on EVM blockchains.
* **Transactions**: Access transactions for accounts in real time across EVM blockchains.

To get started, visit the [documentation](https://docs.sim.dune.com/).

### GoldRush (by Covalent)

[GoldRush](https://goldrush.dev/) provides multichain data APIs and toolkits for easy web3 development across 100+ chains including Monad.

GoldRush offers structured onchain data, including multichain wallet balances, full transaction histories and decoded log events, for building apps and powering AI Agents. Join hundreds of top teams that leverage GoldRush to cut down their development time and scale their multichain offerings with enterprise-grade onchain data.

To get started, visit the [documentation](https://goldrush.dev/docs/overview) or [sign up](https://goldrush.dev/platform/auth/register/) for an API key.

### Goldsky

[Goldsky](https://goldsky.com/) is the go-to data indexer for web3 builders, offering high-performance subgraph hosting and realtime data replication pipelines.

Goldsky offers two core self-serve products that can be used independently or in conjunction to power your data stack.

* **Subgraphs**: Flexible indexing with typescript, with support for webhooks and more.
* **Mirror**: Get live blockchain data in your database or message queues with a single yaml config.

To get started, visit the [documentation](https://docs.goldsky.com/) or follow the [quickstart](https://docs.goldsky.com/subgraphs/guides/create-a-no-code-subgraph) guide.

### Mobula

[Mobula](https://mobula.io/) provides curated datasets for builders: market data with Octopus, wallets data, metadata with Metacore, alongside with REST, GraphSQL & SQL interfaces to query them.

You can get started playing around with the [API endpoints](https://docs.mobula.io/rest-api-reference/introduction) for free, and sign-up to the API dashboard once you need API keys (queries without API keys aren’t production-ready).

To get started, visit the [documentation](https://docs.mobula.io/introduction).

### Moralis

[Moralis](https://moralis.com) is the unified way to fetch, stream, and export onchain data. Access fast, enriched Data APIs for wallets, tokens, prices, holders, NFTs, transfers, liquidity, and full transaction & wallet history - plus real-time Streams and RPC nodes. Teams use Moralis as their crypto data layer to get complete, reliable onchain data without running indexers or maintaining pipelines.

To get started, visit the [documentation](https://docs.moralis.com) or [sign up](https://admin.moralis.com/register) for a free API key.

### Quicknode

[Streams](https://www.quicknode.com/streams) is a managed, push-based service for blockchain data streaming with guaranteed delivery of live and sequential historical data. Receive raw or filtered data (e.g., specific contract events) pushed to your destination: webhook, S3, Postgres, or Snowflake.

To get started, visit the [documentation](https://www.quicknode.com/docs/streams) for detailed instructions.

[Webhooks](https://www.quicknode.com/webhooks) provide real-time notifications for blockchain events on Monad. Track smart contract activity, wallet transactions, and more using ready-to-use templates or your own custom JavaScript.

To get started, visit the [documentation](https://www.quicknode.com/docs/webhooks) for detailed instructions.

### Rarible

[Rarible](https://rarible.org) offers an comprehensive toolkit for anyone interacting with
NFTs, including marketplaces and wallets. Rarible's API for NFT data includes collection/item
metadata, trades, holdings by account (both current and historical), and spam scoring.

Rarible also offers aggregated order books from major NFT marketplaces like OpenSea, Rarible, and
Blur, as well as an NFT trading SDK.

To get started, check out the [documentation](https://docs.rarible.org/).

### Sequence

[Sequence](https://sequence.xyz) [Indexer](https://docs.sequence.xyz/solutions/indexer/overview)
offers real-time balances, transfers, NFTs, prices, and contract events across EVM chains with
webhooks and subscriptions and sub-300 ms queries. Use it as your production read layer for on-chain
apps.

Indexer gives you low-latency reads across EVM chains: balances and portfolio, token and NFT
ownership, transfers and logs, prices, and contract events. It is built for enterprise-grade
production and supports developers of all sizes. Cursor-based pagination, filters, webhooks,
and event subscriptions: All in a scalable, 99.99% uptime service.

To get started, visit the
[quickstart](https://docs.sequence.xyz/solutions/indexer/overview#quickstart) guide.

### SQD

[SQD](https://sqd.ai/) is a decentralized data indexing platform (formerly Subsquid) that provides access to onchain data through its permissionless data lake. SQD offers chain data (blocks, transactions, logs, traces, state diffs) for Monad via the [Portal API](https://docs.sqd.dev/en/portal/evm/overview) and the [Subsquid SDK](https://github.com/subsquid/squid-sdk) for building custom indexers.

SQD also offers a [Portal MCP server](https://docs.sqd.dev/en/ai/mcp-server) that enables AI agents to query onchain data directly.

To get started, visit the [documentation](https://docs.sqd.ai/) or explore the [Portal API](https://docs.sqd.dev/en/portal/evm/overview).

### SonarX

[SonarX](https://sonarx.com) delivers structured blockchain data with historical and real-time coverage across 100+ blockchains with a focus on data quality, in line with our proprietary Data Quality Framework.

Enterprises, Institutions and Builders can query full historical datasets in their preferred cloud warehouse (Snowflake, BigQuery, Azure), receive file drops in csv, parquet, iceberg formats, or run real-time pipelines with Kafka streaming. Supported services include chain data (blocks, transactions, logs, traces, decoded logs and traces), staking, and DEX trades and balances.

With ready-to-use tables and flexible delivery, SonarX helps power analytics, trading, accounting, and applications without the burden of maintaining indexing pipelines.

To get started, visit the console at [console.sonarx.com](https://console.sonarx.com).

### thirdweb

thirdweb [Insight](https://thirdweb.com/insight) is a fast, reliable and fully customizable way for developers to index, transform & query onchain data across 30+ chains. Insight includes out-of-the-box APIs for transactions, events, tokens. Developers can also define custom API schemas, or blueprints, without the need for ABIs, decoding, RPC, or web3 knowledge to fetch blockchain data.

thirdweb Insight can be used to fetch:

* all assets (ERC20, ERC721, ERC115) for a given wallet address
* all sales of skins on your in-game marketplace
* monthly protocol fees in the last 12 months
* the total cost of all accounts created using ERC-4337
* metadata for a given token (ERC20, ERC721, ERC115)
* daily active wallets for your application or game
* and so much more

To get started, sign up for a [free thirdweb account](https://thirdweb.com/team) and visit the [thirdweb Insight documentation](https://insight.thirdweb.com/reference)

### Unmarshal

[Unmarshal](https://unmarshal.io/) is a leading decentralized multi-chain data network, enabling Web3 projects to access accurate, real-time blockchain data across 55+ chains (including Monad Testnet).

Leveraging AI-driven solutions, Unmarshal enhances data accessibility and insights for RWA, DePIN, AI Agents, DeFi, NFT, and GameFi platforms. Through robust APIs, notification services, and no-code indexers, it empowers dApps to deliver seamless user experiences while ensuring transparency, scalability, and innovation at the forefront of Web3 advancements.

To get started, visit the [documentation](https://docs.unmarshal.io) or reach out at [support@unmarshal.io](mailto:support@unmarshal.io).

### Zerion

The [Zerion API](https://zerion.io/api) can be used to build feature-rich web3 apps, wallets, and protocols with ease. Across all major blockchains, you can access wallets, assets, and chain data for web3 portfolios. Zerion's infrastructure supports all major chains!

To get started, visit the [documentation](https://zerion.io/api).


# Indexers
Source: https://docs.monad.xyz/tooling-and-infra/indexers/index



<CardGroup>
  <Card title="Common Data" href="/tooling-and-infra/indexers/common-data">
    Raw transactional data and frequently-used derived data like balances, transfers, and DEX trades
  </Card>

  <Card title="Indexing Frameworks" href="/tooling-and-infra/indexers/indexing-frameworks">
    Tools that allow developers to build custom calculators in response to events
  </Card>
</CardGroup>

<br />

The blockchain can be thought of as a list of blocks, transactions, and logs, as well as a series of global states. Indexers compute common transformations on this data to save downstream consumers the cost and complexity of doing so.

There are two main types of indexer services:

1. **[Data for common use cases](/tooling-and-infra/indexers/common-data)**: raw data (blocks, transactions, logs, traces) and derived data for common use cases (token balances, NFT holdings, DEX trades), computed across the entire blockchain
2. **[Indexing Frameworks](/tooling-and-infra/indexers/indexing-frameworks)** enable devleopers to build custom calculators for a specific smart contract

## Data for common use cases

Data providers offer raw and transformed data for common use cases via API or by streaming to your local environment.

Raw data includes:

* blocks, transactions, logs, traces (potentially decoded using contract ABIs)

Transformed data includes:

* balances (native tokens, ERC20s, NFTs)
* transfers (native tokens, ERC20s, NFTs)
* DEX trades
* market data
* and more

See [Common Data](/tooling-and-infra/indexers/common-data) for a fuller list of features and providers.

## Indexing Frameworks

Smart contract indexers are custom off-chain calculators for a specific smart contract. They maintain additional off-chain state and perform additional computation. Since blockchain data is public, anyone may deploy a subgraph involving state or logs from any smart contract.

See [Indexing Frameworks](/tooling-and-infra/indexers/indexing-frameworks) for a list of features and providers.


# Indexing Frameworks
Source: https://docs.monad.xyz/tooling-and-infra/indexers/indexing-frameworks



## Background

**Smart contract indexers** are off-chain calculators that compute additional metrics specific to one smart contract. Calculators can be thought of as extensions to a smart contract that do additional off-chain computation and maintain additional off-chain state.

*Simple example:* the [UniswapV2Pair contract](https://github.com/Uniswap/v2-core/blob/master/contracts/UniswapV2Pair.sol) maintains minimal state for the pool and emits `Mint`, `Burn`, and `Swap` events. If we wanted to know the cumulative number and volume of swaps on the pair, we could write and deploy a custom indexer instead of adding additional state variables and computation to the contract.

Smart contract indexers typically produce object schemas using the [GraphQL](https://graphql.org/) schema language.

Smart contract indexing services usually provide a hosted service so that users can deploy their indexers without having to run their own infrastructure.

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Language</th>
            <th>Framework</th>
            <th>Known for</th>
            <th>Hosted service</th>
            <th>Decen- tralized hosted service</th>
            <th>Onchain & offchain data</th>
            <th>Web- socket subscr- iptions</th>
            <th>Query layer</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Envio](https://envio.dev/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.envio.dev/docs/HyperIndex/overview)</td>
            <td>JavaScript, TypeScript, Rescript</td>
            <td>[HyperIndex](https://github.com/enviodev/hyperindex)</td>
            <td>Performance and scale</td>
            <td>✅</td>
            <td>❌</td>
            <td>✅</td>
            <td>✅</td>
            <td>GraphQL</td>
          </tr>

          <tr>
            <td>[Ghost](https://tryghost.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.tryghost.xyz/ghostgraph/overview)</td>
            <td>Solidity</td>
            <td>GhostGraph</td>
            <td>Solidity development</td>
            <td>✅</td>
            <td>❌</td>
            <td>❌</td>
            <td>❌</td>
            <td>GraphQL</td>
          </tr>

          <tr>
            <td>[Goldsky](https://goldsky.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.goldsky.com/)</td>
            <td>AssemblyScript, SQL, TypeScript</td>
            <td>[subgraph](https://github.com/graphprotocol/graph-node), [ETL pipelines](https://docs.goldsky.com/mirror/introduction)</td>
            <td>Real-time data streaming</td>
            <td>✅</td>
            <td>❌</td>
            <td>✅ (with [Compose](https://docs.goldsky.com/compose/introduction))</td>
            <td>❌</td>
            <td>GraphQL and SQL ([in your db](https://docs.goldsky.com/mirror/sinks/postgres))</td>
          </tr>

          <tr>
            <td>[Ormi](https://ormilabs.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.ormilabs.com/)</td>
            <td>Assembly- Script</td>
            <td>[subgraph](https://github.com/graphprotocol/graph-node)</td>
            <td>High performance and custom environments</td>
            <td>✅</td>
            <td>❌</td>
            <td>❌</td>
            <td>❌</td>
            <td>Custom GraphQL</td>
          </tr>

          <tr>
            <td>[Sentio](https://www.sentio.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sentio.xyz/docs/quickstart)</td>
            <td>JavaScript, TypeScript</td>
            <td>[sentio-sdk](https://github.com/sentioxyz/sentio-sdk)</td>
            <td>Performance; integrated alerting and visualization</td>
            <td>✅</td>
            <td>❌</td>
            <td>✅</td>
            <td>❌</td>
            <td>GraphQL & SQL</td>
          </tr>

          <tr>
            <td>[SQD](https://sqd.ai/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sqd.ai)</td>
            <td>TypeScript</td>
            <td>[squid-sdk](https://github.com/subsquid/squid-sdk)</td>
            <td>Performance, decentralization</td>
            <td>✅</td>
            <td>Partial[^1]</td>
            <td>✅</td>
            <td>✅</td>
            <td>GraphQL</td>
          </tr>

          <tr>
            <td>[Streamingfast](https://thegraph.market/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.substreams.dev/tutorials/intro-to-tutorials/monad)</td>
            <td>Rust</td>
            <td>[Substreams](https://substreams.dev)</td>
            <td>Performance, low latency and custom sinks</td>
            <td>✅</td>
            <td>❌</td>
            <td>❌</td>
            <td>✅ (gRPC subscription)</td>
            <td>gRPC, 20+ db types supported</td>
          </tr>

          <tr>
            <td>[SubQuery](https://subquery.network/)</td>
            <td>✅</td>
            <td>[Docs](https://academy.subquery.network/)</td>
            <td>TypeScript</td>
            <td>[subql](https://github.com/subquery/subql)</td>
            <td>Decentral- ization</td>
            <td>✅</td>
            <td>✅</td>
            <td>✅</td>
            <td>❌</td>
            <td>GraphQL</td>
          </tr>

          <tr>
            <td>[The Graph](https://thegraph.com/)</td>
            <td>✅</td>
            <td>[Docs](https://thegraph.com/docs/en/subgraphs/quick-start/)</td>
            <td>Assembly- Script</td>
            <td>[subgraph](https://github.com/graphprotocol/graph-node)</td>
            <td>The original indexer</td>
            <td>✅</td>
            <td>✅</td>
            <td>❌</td>
            <td>❌</td>
            <td>Custom GraphQL</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*

    [^1]: SQD hosted service is semi-decentralized: the data lake is decentralized, but indexers run on proprietary infra.
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Language</th>
            <th>Framework</th>
            <th>Known for</th>
            <th>Hosted service</th>
            <th>Decen- tralized hosted service</th>
            <th>Onchain & offchain data</th>
            <th>Web- socket subscr- iptions</th>
            <th>Query layer</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Envio](https://envio.dev/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.envio.dev/docs/HyperIndex/overview)</td>
            <td>JavaScript, TypeScript, Rescript</td>
            <td>[HyperIndex](https://github.com/enviodev/hyperindex)</td>
            <td>Performance and scale</td>
            <td>✅</td>
            <td>❌</td>
            <td>✅</td>
            <td>✅</td>
            <td>GraphQL</td>
          </tr>

          <tr>
            <td>[Ghost](https://tryghost.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.tryghost.xyz/ghostgraph/overview)</td>
            <td>Solidity</td>
            <td>GhostGraph</td>
            <td>Solidity development</td>
            <td>✅</td>
            <td>❌</td>
            <td>❌</td>
            <td>❌</td>
            <td>GraphQL</td>
          </tr>

          <tr>
            <td>[Goldsky](https://goldsky.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.goldsky.com/)</td>
            <td>AssemblyScript, SQL, TypeScript</td>
            <td>[subgraph](https://github.com/graphprotocol/graph-node), [ETL pipelines](https://docs.goldsky.com/mirror/introduction)</td>
            <td>Real-time data streaming</td>
            <td>✅</td>
            <td>❌</td>
            <td>✅ (with [Compose](https://docs.goldsky.com/compose/introduction))</td>
            <td>❌</td>
            <td>GraphQL and SQL ([in your db](https://docs.goldsky.com/mirror/sinks/postgres))</td>
          </tr>

          <tr>
            <td>[Ormi](https://ormilabs.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.ormilabs.com/)</td>
            <td>Assembly- Script</td>
            <td>[subgraph](https://github.com/graphprotocol/graph-node)</td>
            <td>High performance and custom environments</td>
            <td>✅</td>
            <td>❌</td>
            <td>❌</td>
            <td>❌</td>
            <td>Custom GraphQL</td>
          </tr>

          <tr>
            <td>[SQD](https://sqd.ai/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sqd.ai)</td>
            <td>TypeScript</td>
            <td>[squid-sdk](https://github.com/subsquid/squid-sdk)</td>
            <td>Performance, decentralization</td>
            <td>✅</td>
            <td>Partial[^1]</td>
            <td>✅</td>
            <td>✅</td>
            <td>GraphQL</td>
          </tr>

          <tr>
            <td>[SubQuery](https://subquery.network/)</td>
            <td>✅</td>
            <td>[Docs](https://academy.subquery.network/)</td>
            <td>TypeScript</td>
            <td>[subql](https://github.com/subquery/subql)</td>
            <td>Decentral- ization</td>
            <td>✅</td>
            <td>✅</td>
            <td>✅</td>
            <td>❌</td>
            <td>GraphQL</td>
          </tr>

          <tr>
            <td>[The Graph](https://thegraph.com/)</td>
            <td>✅</td>
            <td>[Docs](https://thegraph.com/docs/en/subgraphs/quick-start/)</td>
            <td>Assembly- Script</td>
            <td>[subgraph](https://github.com/graphprotocol/graph-node)</td>
            <td>The original indexer</td>
            <td>✅</td>
            <td>✅</td>
            <td>❌</td>
            <td>❌</td>
            <td>Custom GraphQL</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*

    [^1]: SQD hosted service is semi-decentralized: the data lake is decentralized, but indexers run on proprietary infra.
  </Tab>
</Tabs>

## Provider Details

### Envio

[Envio](https://envio.dev/) is a full-featured data indexing solution that provides application developers with a seamless and efficient way to index and aggregate real-time and historical blockchain data for Monad Testnet. The indexed data is easily accessible through custom GraphQL queries, providing developers with the flexibility and power to retrieve specific information.

[Envio HyperSync](https://docs.envio.dev/docs/HyperIndex/hypersync) is an indexed layer of the Monad Testnet blockchain for the hyper-speed syncing of historical data (JSON-RPC bypass). What would usually take hours to sync \~100,000 events can now be done in the order of less than a minute.

Designed to optimize the user experience, Envio offers automatic code generation, flexible language support, multi-chain data aggregation, and a reliable, cost-effective hosted service.

To get started, visit the [documentation](https://docs.envio.dev/docs/HyperIndex/overview) or follow the [quickstart](https://docs.envio.dev/docs/HyperIndex/contract-import) guide.

### Ghost

With [GhostGraph](https://tryghost.xyz/graph), you can write your indexers in the same language as your contracts: Solidity. This means less context switching and faster time to market.

To get started, visit the [documentation](https://docs.tryghost.xyz/ghostgraph/overview/) or check out the [tutorial](/guides/indexers/ghost).

Services supported:

* GhostGraph

### Goldsky

[Goldsky](https://goldsky.com/) handles the hard parts of building on crypto rails: real-time data and reliable connectivity, so you can ship better products, faster.

Goldsky offers two core self-serve products that can be used independently or in conjunction to power your data stack.

* [**Subgraphs**](https://docs.goldsky.com/subgraphs/deploying-subgraphs): Instant GraphQL APIs for Monad data with zero maintenance.
* [**Mirror**](https://docs.goldsky.com/mirror/create-a-pipeline): Stream realtime Monad data directly into your database.

To take your app to the next level, build using Goldsky’s next gen data pipeline engine:

* [**Turbo**](https://docs.goldsky.com/turbo-pipelines/introduction): *Really fast decoding*, infinite filters, dynamic tables, and live data inspection.

To get started, visit the [documentation](https://docs.goldsky.com/introduction) for guided walkthroughs.

### Ormi

[Ormi](https://ormilabs.com/) delivers real-time blockchain data that is fast, accurate, and ready for production.

It keeps data synced to the tip of the chain and makes it instantly accessible through Subgraphs and APIs without the need to manage indexing infrastructure.

Ormi provides two core products:

* **Subgraphs**: Smart contract data at sub-second latency with zero throttling.
* **Data API**: Real-time and historical blockchain data delivered through flexible, high-speed API endpoints.

Ormi supports shared, dedicated, and fully custom environments that provide isolated performance for high-demand workloads.

Start building by exploring the [documentation](https://docs.ormilabs.com/) or following the [Quickstart Guide](https://docs.ormilabs.com/subgraphs/quickstart).

### Sentio

[Sentio](https://www.sentio.xyz/) offers blazing-fast native processors and seamless subgraph hosting on Monad. With powerful database capabilities, intuitive dashboards, and comprehensive API functionalities, Sentio is built to provide an exceptional developer experience.

To get started, check out the [docs](https://docs.sentio.xyz/docs/readme) or visit the [quickstart](https://docs.sentio.xyz/docs/quickstart) guide.

### SQD

[SQD](https://sqd.ai/) enables permissionless, cost-efficient access to petabytes of high-value Web3 data.

SQD is a decentralized hyper-scalable data platform optimized for providing efficient, permissionless access to large volumes of data. It currently serves historical on-chain data, including event logs, transaction receipts, traces, and per-transaction state diffs.

To get started, visit the [documentation](https://docs.sqd.ai) or see this [quickstart](https://docs.sqd.ai/sdk/quickstart/) with [examples](https://docs.sqd.ai/sdk/examples) on how to easily create subgraphs via Subsquid.

### Streamingfast

[Streamingfast](https://thegraph.market/) builds massively scalable software
for processing and indexing blockchain data. StreamingFast has built two
foundational technologies:

* [Firehose](https://firehose.streamingfast.io/): a blockchain data extraction layer designed to
  process complete blockchain histories using a files-based and streaming-first approach.
* [Substreams](https://docs.substreams.dev/): a data transformation layer which   allows developers
  to write rust modules that can be composed like building blocks, building upon community-developed
  modules. Substreams can output data to various destinations including PosgreSQL, MongoDB\< Kafka,
  and flat files.

To get started, check out the [docs](https://docs.substreams.dev/), or visit the
[tutorial](https://docs.substreams.dev/tutorials/intro-to-tutorials/monad) for generating your
first substream on Monad.

### SubQuery

[SubQuery](https://subquery.network/) is a leading blockchain data indexer that provides developers with fast, flexible, universal, open source and decentralised APIs for web3 projects. SubQuery SDK allows developers to get rich indexed data and build intuitive and immersive decentralised applications in a faster and more efficient way. SubQuery supports many ecosystems including Monad, Ethereum, Cosmos, Near, Polygon, Polkadot, Algorand, and more.

One of SubQuery's advantages is the ability to aggregate data not only within a chain but across multiple blockchains all within a single project. This allows the creation of feature-rich dashboard analytics and multi-chain block scanners.

#### Useful resources:

* [SubQuery Academy (Documentation)](https://academy.subquery.network/)
* [Monad Testnet Starter](https://github.com/subquery/ethereum-subql-starter/tree/main/Monad/monad-testnet-starter)
* [Monad Testnet Quick Start Guide](https://academy.subquery.network/indexer/quickstart/quickstart_chains/monad.html)

For technical questions and support reach out to us `start@subquery.network`

### The Graph

[The Graph](https://thegraph.com/) is an indexing protocol that provides an easy way to query blockchain data through APIs known as subgraphs.

With The Graph, you can benefit from:

* **Decentralized Indexing**: Enables indexing blockchain data through multiple indexers, thus eliminating any single point of failure
* **GraphQL Queries**: Provides a powerful GraphQL interface for querying indexed data, making data retrieval super simple.
* **Customization**: Define your own logic for transforming & storing blockchain data. Reuse subgraphs published by other developers on The Graph Network.

Follow this [quick-start](https://thegraph.com/docs/en/subgraphs/quick-start/) guide to create, deploy, and query a subgraph within 5 minutes.


# Onramps
Source: https://docs.monad.xyz/tooling-and-infra/onramps



Onramps are services that allow users to convert fiat currency into cryptocurrency. They serve
as an entrypoint for users who want to participate in the Monad ecosystem.

**See also:** [Payment Orchestrators](/tooling-and-infra/payment-orchestrators).

## Provider Summary

<div>
  <table>
    <thead>
      <tr>
        <th>Provider</th>
        <th>Status</th>
        <th>Docs</th>
        <th>Support notes</th>
        <th>Regions supported</th>
        <th>Currencies & Countries Supported</th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td>[AhoraCrypto](https://ahoracrypto.com/)</td>
        <td>✅</td>
        <td>[Docs](https://ahoracrypto.gitbook.io/ahoracrypto)</td>
        <td>[Onramp API](https://ahoracrypto.gitbook.io/ahoracrypto/api/payment-intent)<br />
        Offramp docs coming soon<br />
        [Widget](https://ahoracrypto.gitbook.io/ahoracrypto/widget/web-widget)</td>
        <td>Africa, APAC, Europe, LATAM, Middle East, North America, South Asia</td>
        <td>14+ local payment methods, 50+ cryptocurrencies, 50+ countries</td>
      </tr>

      <tr>
        <td>[Alchemy Pay](https://alchemypay.org/)</td>
        <td>✅</td>
        <td>[Docs](https://alchemypay.readme.io/)</td>
        <td>[Onramp](https://alchemypay.readme.io/docs/alchemypay-on-ramp)<br />
        [NFT Checkout](https://alchemypay.readme.io/docs/alchemy-pay-nft-checkout)<br />
        [Crypto Payment](https://alchemypay.readme.io/docs/alchemy-pay-crypto-payment)</td>
        <td>APAC, Africa, LATAM</td>
        <td>[Payment Methods](https://alchemypay.notion.site/Payment-Methods-Coverages-Other-Details-Table-fb3b4f5c68c04b9b8619c48aad31277d)</td>
      </tr>

      <tr>
        <td>[alfred](https://www.alfredpay.io/)</td>
        <td>⌛️</td>
        <td>[Docs](https://alfredpay.readme.io/docs/overview)</td>
        <td>[API Endpoints](https://alfredpay.readme.io/reference/customers-1)</td>
        <td>LATAM, US, EU, APAC</td>
        <td>[Supported Currencies](https://alfredpay.readme.io/docs/payment-methods-supported)</td>
      </tr>

      <tr>
        <td>[Banxa](https://banxa.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.banxa.com/)</td>
        <td>[Onramp API](https://docs.banxa.com/docs/tutorial)<br />
        [Offramp API](https://docs.banxa.com/docs/off-ramp)</td>
        <td>US, Canada, UK, EU, Australia</td>
        <td>[Supported Currencies](https://support.banxa.com/en/support/solutions/articles/44002280809-which-fiat-currencies-does-banxa-support-)<br />
        [Supported Countries](https://support.banxa.com/en/support/solutions/articles/44002216505-what-countries-are-supported-by-banxa-)</td>
      </tr>

      <tr>
        <td>[Blink](https://blink.cash/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.blink.cash/introduction)</td>
        <td>[Quickstart](https://docs.blink.cash/quickstart)<br />
        [Web SDK + Mobile SDK](https://docs.blink.cash/integration/supported-networks-and-wallets)</td>
        <td>Worldwide</td>
        <td>One tap deposits for 136+ tokens across 45+ chains<br />
        [Supported Networks](https://docs.blink.cash/integration/supported-networks-and-wallets)</td>
      </tr>

      <tr>
        <td>[Brale](https://brale.xyz/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.brale.xyz/)</td>
        <td>[Onramp](https://docs.brale.xyz/guides/fiat-to-stablecoin-onramp)<br />
        [Offramp](https://docs.brale.xyz/guides/stablecoin-to-fiat-offramp)</td>

        <td />

        <td>[Supported Currencies](https://docs.brale.xyz/coverage/value-types)</td>
      </tr>

      <tr>
        <td>[Bridge](https://www.bridge.xyz/)</td>
        <td>✅</td>
        <td>[Docs](https://apidocs.bridge.xyz/)</td>
        <td>[Onramp](https://apidocs.bridge.xyz/get-started/guides/wallets/onramp)<br />
        [Offramp](https://apidocs.bridge.xyz/get-started/guides/wallets/offramp)<br />
        [Orchestration API](https://apidocs.bridge.xyz/platform/orchestration/overview)</td>
        <td>US, EU, UK, LATAM, Global</td>
        <td>USD (ACH & wire), EUR (SEPA), GBP, MXN (SPEI) & more via [virtual accounts](https://apidocs.bridge.xyz/get-started/guides/move-money/virtualaccounts)</td>
      </tr>

      <tr>
        <td>[BTC Direct](https://onramp.btcdirect.eu/)</td>
        <td>✅</td>
        <td>[Docs](https://developer.btcdirect.eu/)</td>
        <td>[Onramp](https://developer.btcdirect.eu/api/v1/#/Buy)<br />
        [Offramp](https://developer.btcdirect.eu/api/v1/#/Sell)<br />
        [Widget](https://developer.btcdirect.eu/widget/getting-started)</td>
        <td>SEPA / Europe</td>
        <td>EUR<br />
        [Supported Cryptocurrencies](https://developer.btcdirect.eu/widget/supported-cryptocurrencies.html)</td>
      </tr>

      <tr>
        <td>[Capa](https://capa.fi/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.capa.fi/docs/getting-started)</td>
        <td>[Onramp API](https://docs.capa.fi/docs/on-ramp)<br />
        [Offramp API](https://docs.capa.fi/docs/off-ramp)</td>
        <td>LATAM</td>
        <td>[Supported Currencies](https://docs.capa.fi/docs/on-ramp#select-the-fiat-currency%3A)</td>
      </tr>

      <tr>
        <td>[Chainrails](https://chainrails.io)</td>
        <td>✅</td>
        <td>[Docs](https://docs.chainrails.io)</td>
        <td>[API Endpoints](https://docs.chainrails.io/api-reference/introduction)</td>
        <td>Africa, APAC, LATAM, EU, US, Australia</td>
        <td>[Supported Currencies](https://docs.chainrails.io/essentials/integrations)</td>
      </tr>

      <tr>
        <td>[Coinbase Onramp & Offramp](https://docs.cdp.coinbase.com/onramp/introduction/welcome)</td>
        <td>✅</td>
        <td>[Docs](https://docs.cdp.coinbase.com/onramp/introduction/welcome)</td>
        <td>[Onramp API](https://docs.cdp.coinbase.com/onramp-&-offramp/onramp-apis/onramp-overview)<br />
        [Offramp API](https://docs.cdp.coinbase.com/onramp-&-offramp/offramp-apis/offramp-overview)</td>
        <td>US, Canada, Brazil, EU, Singapore, Australia, New Zealand</td>
        <td>ACH, debit cards, Apple Pay, and cash/crypto balances are supported in the US. Debit cards and cash/crypto balances are supported everywhere else.</td>
      </tr>

      <tr>
        <td>[Coindisco](https://coindisco.com/)</td>
        <td>✅</td>
        <td>[Docs](https://coindisco.gitbook.io/coindisco)</td>
        <td>[Buy|Sell Widget](https://coindisco.gitbook.io/coindisco/widget-integration/widget-integration-methods)<br />
        [White Label API](https://coindisco.gitbook.io/coindisco/widget-integration/white-label-api-integration)</td>
        <td>240+ countries and territories</td>
        <td>[Supported Payment Methods](https://coindisco.gitbook.io/coindisco/platform-support/supported-payment-methods)<br />
        [Supported Fiat Currencies](https://coindisco.gitbook.io/coindisco/supported-fiat-currencies)<br />
        [Supported Countries](https://coindisco.gitbook.io/coindisco/supported-countries)</td>
      </tr>

      <tr>
        <td>[Coinflow](https://coinflow.cash/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.coinflow.cash/)</td>
        <td>[API Endpoints](https://docs.coinflow.cash/guides/getting-started/getting-started-with-checkout)</td>
        <td>APAC, LATAM, US, EU</td>
        <td>[Supported Countries - Withdraw](https://docs.coinflow.cash/guides/payouts/available-countries)<br />
        [Supported Countries - Global Push Card](https://docs.coinflow.cash/guides/payouts/available-countries/supported-countries-for-global-push-to-card)</td>
      </tr>

      <tr>
        <td>[Daimo](https://daimo.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.daimo.com/introduction)</td>
        <td>[Quickstart](https://docs.daimo.com/quickstart)</td>
        <td>Canada, US</td>
        <td>[Payment Methods](https://docs.daimo.com/guides/fiat#supported-rails)</td>
      </tr>

      <tr>
        <td>[El Dorado](https://eldorado.io/)</td>
        <td>✅</td>
        <td>[Docs](https://api.eldorado.io/)</td>
        <td>[API Overview](https://api.eldorado.io/#api-overview)</td>
        <td>LATAM</td>
        <td>[Supported Countries](https://api.eldorado.io/concepts/countries)<br />
        [Supported Currencies](https://api.eldorado.io/concepts/currencies)</td>
      </tr>

      <tr>
        <td>[FinchPay](https://finchpay.io/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.finchpay.io/)</td>
        <td>[Widget URL](https://docs.finchpay.io/docs/url-structure)<br />
        [API](https://docs.finchpay.io/docs/partners-api)</td>
        <td>EU, 150+ countries</td>
        <td>Local payment methods: Brazil (PicPay, PIX), Mexico (SPEI and OXXO), Indonesia (virtual accounts BRI & Mandiri, e-wallets DANA/OVO)</td>
      </tr>

      <tr>
        <td>[Flashnet](https://flashnet.xyz/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.flashnet.xyz/products/orchestration/overview)</td>

        <td />

        <td>US Only, no NY</td>
        <td>[Supported Chains & Assets](https://docs.flashnet.xyz/products/orchestration/overview#which-chains-and-assets-are-supported)</td>
      </tr>

      <tr>
        <td>[Fonbnk](https://www.fonbnk.com/)</td>
        <td>⌛️</td>
        <td>[Docs](https://docs.fonbnk.com/)</td>
        <td>[Onramp](https://docs.fonbnk.com/on-ramp)<br />
        [Offramp](https://docs.fonbnk.com/off-ramp)</td>
        <td>Africa, LATAM</td>
        <td>[Supported Countries & Payment Methods](https://www.fonbnk.com/)</td>
      </tr>

      <tr>
        <td>[Fun.xyz](https://fun.xyz/)</td>
        <td>✅</td>
        <td>[Contact](https://fun.xyz/contact)</td>

        <td />

        <td>✅</td>

        <td />
      </tr>

      <tr>
        <td>[Guardarian](https://guardarian.com/)</td>
        <td>✅</td>
        <td>[Docs](https://guardarian.com/api-doc)</td>
        <td>[API](https://guardarian.com/api-doc)</td>
        <td>LATAM, EU, Africa, APAC</td>
        <td>[Supported Countries & Payment Methods](https://guardarian.com/payment-methods)<br />
        [Supported Countries Fees](https://guardarian.notion.site/guardarian-supported-countries-fees)<br />
        [Supported Currencies](https://guardarian.com/currencies)</td>
      </tr>

      <tr>
        <td>[Halliday](https://halliday.xyz/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.halliday.xyz/pages/home)</td>
        <td>[API Quickstart](https://docs.halliday.xyz/pages/api-quickstart)<br />
        [Payments SDK](https://docs.halliday.xyz/pages/payments-sdk-docs)</td>
        <td>US, EU, LATAM, APAC</td>
        <td>Credit or debit card, ACH, Apple Pay, Google Pay, or a CEX balance</td>
      </tr>

      <tr>
        <td>[HoneyCoin](https://honeycoin.app/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.honeycoin.app/reference/welcome)</td>
        <td>[Onramp](https://docs.honeycoin.app/reference/onramp)<br />
        [Offramp](https://docs.honeycoin.app/reference/crypto-off-ramp)</td>
        <td>Africa</td>
        <td>[Supported Countries & Limits](https://docs.honeycoin.app/docs/supported-countries-limits)</td>
      </tr>

      <tr>
        <td>[Koywe](https://koywe.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.koywe.com/crypto/introduction/%F0%9F%91%8B-welcome-to-koywe-%F0%9F%8C%B3)</td>
        <td>[Widget Ramp Demo](https://widget.koywe.com/)</td>
        <td>LATAM</td>
        <td>[Supported Currencies](https://docs.koywe.com/documentation/supported-currencies-payment-methods#supported-currencies-by-country)<br />
        [Supported Countries](https://docs.koywe.com/documentation/supported-currencies-payment-methods#supported-payment-methods-by-country)</td>
      </tr>

      <tr>
        <td>[Meld](https://www.meld.io/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.meld.io/docs/getting-started) (pw protected)</td>

        <td />

        <td>225+ Countries</td>

        <td />
      </tr>

      <tr>
        <td>[Mercuryo](https://mercuryo.io/)</td>
        <td>✅</td>
        <td>[Docs](https://oor-redirect.redoc.ly/)</td>
        <td>[Onramp API Endpoints](https://oor-redirect.redoc.ly/#section/On-Ramp.-Crypto-Purchase)<br />
        [Offramp API Endpoints](https://oor-redirect.redoc.ly/#section/Off-Ramp.-Crypto-Sell.)</td>
        <td>US, EU</td>
        <td>[Supported Currencies](https://help.mercuryo.io/hc/en-gb/articles/14495507502749-Which-fiat-currencies-are-supported)<br />
        [Supported Countries](https://help.mercuryo.io/hc/en-gb/articles/15265851177245-Where-does-Mercuryo-operate)</td>
      </tr>

      <tr>
        <td>[MoonPay](https://www.moonpay.com/)</td>
        <td>✅</td>
        <td>[Docs](https://dev.moonpay.com/)</td>
        <td>[Onramp](https://dev.moonpay.com/docs/on-ramp-overview)<br />
        [Offramp](https://dev.moonpay.com/docs/off-ramp-overview)</td>
        <td>US, EU, Canada, LATAM, APAC, Africa</td>
        <td>[Supported Currencies](https://support.moonpay.com/en/articles/362475-moonpay-s-supported-currencies)<br />
        [Supported Payment Methods](https://support.moonpay.com/en/articles/380823-moonpay-s-supported-payment-methods)<br />
        [Unsupported Countries](https://support.moonpay.com/en/articles/380968-moonpay-s-unsupported-countries)</td>
      </tr>

      <tr>
        <td>[Onramp Money](https://onramp.money/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.onramp.money/onramp/)</td>

        <td />

        <td>APAC, Africa, EU, US, LATAM</td>

        <td />
      </tr>

      <tr>
        <td>[Onramper](https://www.onramper.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.onramper.com/docs/getting-started)</td>
        <td>[API Endpoints](https://docs.onramper.com/reference/get_supported)</td>
        <td>190+ Countries</td>
        <td>[Payment Methods](https://docs.onramper.com/docs/supported-payment-methods)</td>
      </tr>

      <tr>
        <td>[OSL Pay](https://www.osl-pay.com/)</td>
        <td>✅</td>
        <td>[Docs](https://www.osl-pay.com/api-doc/startHere/quickStart)</td>
        <td>[Onramp](https://www.osl-pay.com/api-doc/product/onRamp)</td>
        <td>134+ Countries</td>
        <td>[Supported Currencies & Countries](https://docs.pay.osl.com/docs/overview)</td>
      </tr>

      <tr>
        <td>[Paj](https://paj.cash/)</td>
        <td>✅</td>
        <td>[Docs](https://github.com/paj-cash/paj_ramp/tree/main/examples)</td>
        <td>[Support notes](https://github.com/paj-cash/paj_ramp)</td>
        <td>Africa</td>
        <td>[Supported Currencies & Countries](https://github.com/paj-cash/paj_ramp)</td>
      </tr>

      <tr>
        <td>[Peer](https://peer.xyz/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.peer.xyz/)</td>
        <td>[Onramp](https://docs.peer.xyz/developer/integrate-zkp2p/integrate-redirect-onramp)<br />
        [Offramp](https://docs.peer.xyz/developer/developer/offramp)</td>
        <td>US, EU, Africa, LATAM, APAC</td>
        <td>Venmo, Cash App, Wise, Revolut, PayPal, Mercado Pago, etc.</td>
      </tr>

      <tr>
        <td>[Ramp Network](https://rampnetwork.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.rampnetwork.com/)</td>
        <td>[Getting Started](https://docs.rampnetwork.com/getting-started)</td>
        <td>US, EU, LATAM, APAC & 150+ countries</td>
        <td>[Supported Currencies & Countries](https://support.rampnetwork.com/en/articles/433-which-countries-and-us-states-are-unsupported-for-buying-and-selling-crypto)</td>
      </tr>

      <tr>
        <td>[Rampnow](https://app.rampnow.io)</td>
        <td>✅</td>
        <td>[Docs](https://docs.rampnow.io)</td>

        <td />

        <td>US, EU, EEA, LATAM, ASIA, South Africa, Nigeria</td>
        <td>[Payment Methods](https://docs.rampnow.io/quickstart/onramp/payment-methods)</td>
      </tr>

      <tr>
        <td>[Suby](https://suby.fi)</td>
        <td>✅</td>
        <td>[Docs](https://documentation.suby.fi/)</td>
        <td>[Crypto Payment Link](https://documentation.suby.fi/docs/payment/stablecoins)</td>
        <td>Global</td>
        <td>[Supported Countries](https://documentation.suby.fi/docs/merchants/supported-countries)</td>
      </tr>

      <tr>
        <td>[Swapped](https://swapped.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.swapped.com/)</td>
        <td>[Onramp Endpoints](https://docs.swapped.com/swapped-ramp/endpoints/onramp-endpoints)<br />
        [Offramp Endpoints](https://docs.swapped.com/swapped-ramp/endpoints/offramp-endpoints)</td>
        <td>150+ countries</td>
        <td>[Supported Payment Methods](https://swapped.com/payment-methods)<br />
        [Supported Countries](https://swapped.com/supported-countries)</td>
      </tr>

      <tr>
        <td>[Swapper Finance](https://swapper.finance/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.swapper.finance/)</td>
        <td>[Onramp Widget SDK](https://docs.swapper.finance/quick-start)</td>
        <td>Global</td>
        <td>ACH, credit cards, Apple Pay, Google Pay, UnionPay, and other major payment methods</td>
      </tr>

      <tr>
        <td>[Switch](https://onswitch.xyz/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.onswitch.xyz/introduction)</td>
        <td>[API Reference](https://docs.onswitch.xyz/api-reference/introduction)</td>
        <td>Europe, UK, Africa, APAC, India, China</td>
        <td>USDC and USDT0 on Monad, settled in local currency (EUR, GBP, NGN, KES, GHS, INR, CNY, etc.) via bank transfer, mobile money, and SWIFT</td>
      </tr>

      <tr>
        <td>[Transak](https://transak.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.transak.com/)</td>
        <td>[API endpoints](https://docs.transak.com/reference/end-points)</td>
        <td>US, UK, EU, Australia, Canada, APAC</td>
        <td>[Supported Countries](https://transak.com/global-coverage)</td>
      </tr>

      <tr>
        <td>[Unlimit](https://www.unlimit.com/)</td>
        <td>⌛️</td>
        <td>[Docs](https://integration.unlimit.com/doc-guides/mylvyrw7nxiom-homepage)</td>
        <td>[API Endpoints](https://integration.unlimit.com/api-reference/6nk7rnnwnafo0-environments)</td>
        <td>LATAM, Africa, India, EU, UK, APAC</td>
        <td>[Payment Methods](https://integration.unlimit.com/doc-guides/ci8k5zm86k3ny-card-methods)<br />
        [Payout Methods](https://integration.unlimit.com/doc-guides/m2mtijltdzphg-card-methods)</td>
      </tr>

      <tr>
        <td>[UR](https://ur.app/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.ur.app/)</td>

        <td />

        <td>APAC, EU</td>
        <td>[Supported Countries](https://support.ur.app/hc/en-us/articles/12862724456207-Countries-and-Territories-Supported-By-UR)</td>
      </tr>

      <tr>
        <td>[Walapay](https://www.walapay.io/)</td>
        <td>⌛️</td>
        <td>[Docs](https://docs.walapay.io/docs/introduction)</td>

        <td />

        <td>Africa, APAC, EU, US, Canada, LATAM</td>
        <td>[Supported Countries & Currencies](https://docs.walapay.io/docs/countries-and-rails)<br />
        [Prohibited Countries](https://docs.walapay.io/docs/onboarding-regions)</td>
      </tr>

      <tr>
        <td>[zerohash](https://zerohash.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.zerohash.com/)</td>
        <td>[On and Off Ramps](https://docs.zerohash.com/docs/convert-withdraw-1)</td>
        <td>US, Canada, EU, Africa, Australia, APAC</td>
        <td>[Supported Countries](https://docs.zerohash.com/docs/supported-regions)</td>
      </tr>
    </tbody>
  </table>
</div>

## Provider details

### AhoraCrypto

[AhoraCrypto](https://ahoracrypto.com/) is the crypto infrastructure built around the best-in-market UX: fast compliant KYC, responsive checkout, and 14+ local payment methods to maximize conversion. Revenue share is settled instantly to your wallet on every transaction, with no minimums, waiting periods, or fees. Supporting 14 blockchains, 50+ cryptocurrencies, and 50+ countries, go live in hours via white-label widget or REST API.

To get started, visit the [documentation](https://ahoracrypto.gitbook.io/ahoracrypto).

### Alchemy Pay

[Alchemy Pay](https://alchemypay.org/) is a payment gateway that seamlessly connects crypto with traditional fiat currencies for businesses, developers, and end users. With its offerings including On & Off Ramp, Crypto Card, Web3 Digital Bank, NFT Checkout, and Crypto Payments, Alchemy Pay supports payments in 173 countries.

To get started, visit the [documentation](https://alchemypay.readme.io/docs/alchemypay-on-ramp).

### alfred

With [alfred](https://www.alfredpay.io/), settle international payments in real time. Move money over stablecoin rails and give your business global coverage without the use of intermediary banks resulting in faster transfers at lower costs compared to traditional banking.

To get started, visit the [documentation](https://alfredpay.readme.io/docs/overview).

### Banxa

[Banxa](https://banxa.com/) powers one of the largest digital asset platforms by providing payments infrastructure and regulatory compliance across global markets. Banxa's mission and vision is to build the bridge that provides people in every part of the world access to a fairer and more equitable financial system.

To get started, visit the [documentation](https://docs.banxa.com/).

### Blink

[Blink](https://blink.cash/) is a deposit SDK for crypto apps, letting users fund your app easily with FaceID. Blink handles auth, wallet connections, and cross-chain bridging, supporting 136+ tokens across 45+ chains with native USDC and MON routes on Monad.

To get started, visit the [documentation](https://docs.blink.cash/introduction).

### Brale

[Brale](https://brale.xyz) is a stablecoin infrastructure platform that enables developers to onramp fiat to stablecoins, offramp stablecoins back to fiat, swap between [stablecoins](https://docs.brale.xyz/coverage/value-types) and [networks](https://docs.brale.xyz/coverage/transfer-types), and issue branded stablecoins, all through a single unified API. Brale handles regulatory compliance, reserves, and multi-chain orchestration so builders can focus on their product. Brale also provides payment orchestration — see [Payment Orchestrators](/tooling-and-infra/payment-orchestrators).

To get started, visit the [Brale documentation](https://docs.brale.xyz/).

### Bridge

[Bridge](https://www.bridge.xyz/) (a Stripe company) is a stablecoin payments platform whose orchestration APIs let developers build onramps, offramps, and crypto-to-crypto transfers, alongside virtual accounts, stablecoin issuance, wallets, and card products. Bridge also provides payment orchestration — see [Payment Orchestrators](/tooling-and-infra/payment-orchestrators).

To get started, visit the [documentation](https://apidocs.bridge.xyz/).

### BTC Direct

[BTC Direct](https://onramp.btcdirect.eu/) provides a suite of tools to integrate cryptocurrency services into your platform. Their API supports [buying (onramp)](https://developer.btcdirect.eu/api/v1/#/Buy) and [selling (offramp)](https://developer.btcdirect.eu/api/v1/#/Sell) digital assets, with support for EUR via SEPA across Europe.

To get started, visit the [documentation](https://developer.btcdirect.eu/).

### Capa

[Capa](https://capa.fi/) is your one-stop solution to send and receive payments between Latin America and the world through their all-in-one API, making cross-border transactions fast, simple, and cost-effective.

To get started, visit the [documentation](https://docs.capa.fi/docs/getting-started).

### Chainrails

[Chainrails](https://chainrails.io) enables you to accept crypto payments/deposits from any chain, in any token or currency, instantly.

To get started, visit the [documentation](https://docs.chainrails.io).

### Coinbase Onramp & Offramp

[Coinbase Onramp & Offramp](https://docs.cdp.coinbase.com/onramp/introduction/welcome) by [Coinbase Developer Platform (CDP)](https://www.coinbase.com/developer-platform) empowers enterprises and developers with seamless onchain solutions. The Onramp & Offramp APIs and SDKs enable developers to move money seamlessly between fiat and onchain economies.

To get started, visit the [documentation](https://docs.cdp.coinbase.com/onramp/introduction/welcome).

### Coindisco

[Coindisco](https://coindisco.com/) is an onramp aggregator that provides access to crypto purchases across 240+ countries and territories through a unified widget and white label API integration.

To get started, visit the [documentation](https://coindisco.gitbook.io/coindisco).

### Coinflow

[Coinflow](https://coinflow.cash/) enables businesses to grow faster with instant settlement, fraud & chargeback indemnity, global pay-in, multi-currency FX, and unified payouts---all in one intuitive platform.

To get started, visit the [documentation](https://docs.coinflow.cash/).

### Daimo

[Daimo](https://daimo.com/) is the ramp for stablecoin apps. Integrate once, accept deposits from any wallet, any chain, any token. Funds arrive as the stablecoin you want, on the chain you want.

To get started, visit the [documentation](https://docs.daimo.com/introduction).

### El Dorado

[El Dorado](https://eldorado.io/) is an on/off ramp solution for Latin America, enabling seamless conversion between fiat currencies and cryptocurrency in the LATAM region.

To get started, visit the [documentation](https://api.eldorado.io/).

### FinchPay

[FinchPay](https://finchpay.io/) is an EU-regulated global fiat on-ramp and payment infrastructure for Web3, that lets users buy crypto with cards or local payment methods in 150+ countries.

To get started, visit the [documentation](https://docs.finchpay.io/).

### Flashnet

[Flashnet](https://flashnet.xyz/) builds Bitcoin exchange infrastructure. Its Orchestra product enables Bitcoin orchestration, moving Bitcoin to/from any asset/chain. Orchestra also powers a novel CashApp onramp, which can pull fiat and push stables on the other side. It's instant, low-cost, and the best onramp UX for US persons.

To get started, visit the [documentation](https://docs.flashnet.xyz/products/orchestration/overview).

### Fonbnk

[Fonbnk](https://www.fonbnk.com/) bridges mobile-first, cash-based economies to Web3 by converting prepaid payments into stablecoins, enabling frictionless FX, cross-border treasury flows, and instant liquidity.

To get started, visit the [documentation](https://docs.fonbnk.com/).

### Fun.xyz

[Fun.xyz](https://fun.xyz/)'s platform provides API-driven deposit and withdraw flows for secure, cross-chain, programmable experiences.

To get started, [contact](https://fun.xyz/contact) Fun.xyz.

### Guardarian

[Guardarian](https://guardarian.com/) is a fully licensed, non-custodial crypto payment infrastructure provider that enables both individuals and businesses to seamlessly buy, sell, and swap 1000+ cryptocurrencies using popular payment methods like Visa, Mastercard, Apple Pay, and Google Pay, offering fast low-KYC processing and support for 50+ fiat currencies across 150+ countries.

To get started, visit the [documentation](https://guardarian.com/api-doc).

### Halliday

With [Halliday](https://halliday.xyz/) Payments, users can acquire any token on any chain with minimal effort. Seamlessly onramp from fiat, cross arbitrary bridges, and swap assets from an existing wallet (e.g., MetaMask), into whatever form. Connect with an exchange account (e.g., Coinbase, Binance) to transfer digital assets onto any chain.

To get started, visit the [documentation](https://docs.halliday.xyz/pages/home).

### HoneyCoin

[HoneyCoin](https://honeycoin.app/) is a crypto onramp and offramp service focused on Africa, enabling seamless conversion between fiat currencies and cryptocurrency across the African continent.

To get started, visit the [documentation](https://docs.honeycoin.app/reference/welcome).

### Koywe

[Koywe](https://koywe.com/) is services and interface that make it easier and simpler to buy and sell crypto in Latin America for the fairest price while using local currency and payment methods.

To get started, visit the [documentation](https://docs.koywe.com/crypto/introduction/%F0%9F%91%8B-welcome-to-koywe-%F0%9F%8C%B3).

### Meld

[Meld](https://www.meld.io/) is an infrastructure to move money across Web2 and Web3 rails. fiat \<> fiat | fiat \<> crypto

To get started, [contact](https://www.meld.io/contact) Meld.

### Mercuryo

[Mercuryo](https://mercuryo.io/) enables efficient capital flow within the DeFi ecosystem and consolidates various payment and banking solutions into a single, user-centric interface.

To get started, visit the [documentation](https://oor-redirect.redoc.ly/).

### MoonPay

[MoonPay](https://www.moonpay.com/) simplifies access to buy, sell and trade crypto using everyday payment methods like cards, Apple Pay, PayPal and Venmo, while also providing simple tools to send, receive and manage stablecoins.

To get started, visit the [documentation](https://dev.moonpay.com/).

### Onramp Money

[Onramp Money](https://onramp.money/) is a comprehensive fiat-to-crypto infrastructure that empowers businesses and their users to buy and sell crypto using local fiat, swap crypto-to-crypto, spend crypto on gift cards instantly, and more.

To get started, visit the [documentation](https://docs.onramp.money/onramp/).

### Onramper

[Onramper](https://www.onramper.com/) is a fiat onramp aggregator. All fiat onramps in a single integration, unlocking the lowest fees and highest transaction success rates on the market.

To get started, visit the [documentation](https://docs.onramper.com/docs/getting-started).

### OSL Pay

[OSL Pay](https://www.osl-pay.com/) is the payment infrastructure arm of OSL Group, providing licensed and compliant solutions for seamless conversion between digital assets and fiat currencies.

To get started, visit the [documentation](https://www.osl-pay.com/api-doc/startHere/quickStart).

### Paj

[Paj](https://paj.cash/) abstracts global payments into wallet addresses by representing user bank accounts on-chain. Deterministic wallet addresses derived from users' bank accounts enable users to receive any crypto token converted directly into fiat automatically in their local bank account. This means that any bank account can receive on-chain money and anyone can send crypto to a bank account.

To get started, visit the [documentation](https://github.com/paj-cash/paj_ramp/tree/main/examples).

### Peer

[Peer](https://peer.xyz/) (formerly ZKP2P) is the first trustless P2P on/offramping bulletin board powered by zero-knowledge proofs. This enables a fast, cheap, and DeFi-composable buying and selling crypto experience. Peer supports multiple payment methods including Venmo, Cash App, Wise, Revolut, PayPal, and Mercado Pago across 20+ chains.

To get started, visit the [documentation](https://docs.peer.xyz/).

### Ramp Network

[Ramp Network](https://rampnetwork.com/) is a non-custodial fiat\<>crypto infrastructure that makes it easy for users to jump on and off of Web3 from anywhere.

To get started, visit the [documentation](https://docs.rampnetwork.com/).

### Rampnow

[Rampnow](https://app.rampnow.io) is a global blockchain on-ramp and off-ramp infrastructure provider connecting fiat and blockchain liquidity for businesses, developers, and end users. It supports 125+ blockchains, 20,000+ tokens, and major payment methods across multiple regions through a single API and widget.

To get started, visit the [documentation](https://docs.rampnow.io).

### Suby

[Suby](https://suby.fi) enables merchants to accept stablecoin payments through crypto checkout payment links, with global coverage.

To get started, visit the [documentation](https://documentation.suby.fi/).

### Swapped

[Swapped](https://swapped.com/) offers On-Ramp, Connect, and Commerce solutions, enabling customers to move funds onchain, receive crypto payments, and build full financial platforms, games, and consumer experiences.

To get started, visit the [documentation](https://docs.swapped.com/).

### Swapper Finance

[Swapper Finance](https://swapper.finance/) is the fiat-to-DeFi infrastructure for one-click onboarding to any protocol. Built to bring 3.5+ billion users to DeFi.

To get started, visit the [documentation](https://docs.swapper.finance/).

### Switch

[Switch](https://onswitch.xyz/) is a stablecoin settlement layer that lets businesses accept stablecoin deposits and pay out in local currency across multiple markets via bank transfer, mobile money, and SWIFT. Switch supports USDC and USDT0 on Monad and settles in currencies including EUR, GBP, NGN, KES, GHS, INR, and CNY.

To get started, visit the [documentation](https://docs.onswitch.xyz/introduction).

### Transak

[Transak](https://transak.com/) is a developer integration toolkit that enables you as an app developer to onboard your users to buy/sell crypto in any blockchain app, website or web plugin. With Transak you can onboard mainstream users into your dApp, protocol, game or wallet app and also increase your revenue.

To get started, visit the [documentation](https://docs.transak.com/docs/what-is-transak).

### Unlimit

[Unlimit](https://www.unlimit.com/)'s mission is to provide innovators with a convenient and simple financial interface that enables payments to flow freely and invisibly across borders. They offer a wide range of services, including payment gateway, card acquiring, business accounts, card issuing, alternative payment methods, and more.

To get started, visit the [documentation](https://integration.unlimit.com/doc-guides/mylvyrw7nxiom-homepage).

### UR

[UR](https://ur.app/) is a borderless smart money app built on the blockchain. Your go-to unified crypto and fiat account with 0 off-ramp fees and access to multiple currencies.

To get started, visit the [documentation](https://docs.ur.app/).

### Walapay

[Walapay](https://www.walapay.io/) is a global money movement platform that is building the future of cross-border payments.

To get started, visit the [documentation](https://www.walapay.io/).

### zerohash

[zerohash](https://zerohash.com/) is a B2B2C embedded infrastructure platform that provides APIs and SDKs, enabling businesses to integrate digital asset trading, custody, and fiat-to-crypto on-ramps directly into their applications. zerohash also provides payment orchestration — see [Payment Orchestrators](/tooling-and-infra/payment-orchestrators).

To get started, visit the [documentation](https://docs.zerohash.com/).


# Oracles
Source: https://docs.monad.xyz/tooling-and-infra/oracles



Oracles make off-chain data accessible on chain.

## Definitions

| Term                             | Description                                                          |
| -------------------------------- | -------------------------------------------------------------------- |
| Push oracle                      | Provider regularly pushes price data to the oracle contract on chain |
| Pull (on-demand) oracle          | User triggers price data update while calling a smart contract       |
| Custom oracle                    | A custom calculator                                                  |
| VRF (Verifiable Random Function) | Provides random numbers on chain                                     |

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Contract addresses</th>
            <th>Live data</th>
            <th>Support notes</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Chainlink](https://chain.link/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.chain.link/)</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/chainlink.jsonc)</td>
            <td>[Live data](https://data.chain.link/streams)</td>

            <td>
              * Push oracle ([Price Feeds](https://docs.chain.link/data-feeds/price-feeds))
              * Pull oracle ([Data Streams](https://docs.chain.link/data-streams))
            </td>
          </tr>

          <tr>
            <td>[Chronicle](https://chroniclelabs.org/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.chroniclelabs.org/)</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/chronicle.jsonc)</td>

            <td />

            <td>Push oracle; custom oracles</td>
          </tr>

          <tr>
            <td>[Pyth](https://www.pyth.network/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.pyth.network/)</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/pyth.jsonc)</td>
            <td>[Live data](https://www.pyth.network/price-feeds)</td>
            <td>[Pull oracle](https://docs.pyth.network/price-feeds/pull-updates);<br />
            [VRF](https://docs.pyth.network/entropy)</td>
          </tr>

          <tr>
            <td>[Redstone](https://www.redstone.finance/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.redstone.finance/)</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/redstone.jsonc)</td>
            <td>[Live data](https://app.redstone.finance/app/tokens/)</td>
            <td>[Push oracle](https://app.redstone.finance/app/feeds/?networks=10143);<br />
            [pull oracle](https://app.redstone.finance/app/pull-model/redstone-primary-prod)</td>
          </tr>

          <tr>
            <td>[Stork](https://stork.network/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.stork.network/)</td>

            <td>
              * See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/stork.jsonc)<br />
              * [Addresses](https://docs.stork.network/resources/contract-addresses/evm); [APIs](https://docs.stork.network/api-reference/contract-apis/evm); [Asset ID Registry](https://docs.stork.network/resources/asset-id-registry)
            </td>

            <td>[Live Data](https://data.stork.network)</td>
            <td>[Push oracle](https://docs.stork.network/resources/stork-pushed-assets);<br />[Pull oracle](https://docs.stork.network/introduction/core-concepts)</td>
          </tr>

          <tr>
            <td>[Supra](https://supra.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.supra.com/)</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/supra_oracles.jsonc)</td>
            <td>[Live data](https://supra.com/data)</td>
            <td>[Push oracle](https://docs.supra.com/oracles/data-feeds/push-oracle);<br />[Pull oracle](https://docs.supra.com/oracles/data-feeds/pull-oracle);<br />[dVRF](https://docs.supra.com/oracles/dvrf)</td>
          </tr>

          <tr>
            <td>[Switchboard](https://switchboard.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.switchboard.xyz/)</td>

            <td>
              * See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/switchboard.jsonc)
              * More info: [Deployments](https://docs.switchboard.xyz/docs-by-chain/evm)
            </td>

            <td />

            <td>[Pull oracle](https://docs.switchboard.xyz/docs-by-chain/evm);<br />
            [Oracle aggregator](https://docs.switchboard.xyz/custom-feeds/advanced-feed-configuration/oracle-aggregator);<br />
            [VRF](https://docs.switchboard.xyz/docs-by-chain/evm/randomness)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Contract addresses</th>
            <th>Live data</th>
            <th>Support notes</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Chainlink](https://chain.link/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.chain.link/)</td>

            <td>
              Price Feeds \[push oracle]:<br />

              * BTC / USD: [`0x2Cd9D7E85494F68F5aF08EF96d6FD5e8F71B4d31`](https://testnet.monadvision.com/address/0x2Cd9D7E85494F68F5aF08EF96d6FD5e8F71B4d31)
              * ETH / USD: [`0x0c76859E85727683Eeba0C70Bc2e0F5781337818`](https://testnet.monadvision.com/address/0x0c76859E85727683Eeba0C70Bc2e0F5781337818)
              * LINK / USD: [`0x4682035965Cd2B88759193ee2660d8A0766e1391`](https://testnet.monadvision.com/address/0x4682035965Cd2B88759193ee2660d8A0766e1391)
              * USDC / USD: [`0x70BB0758a38ae43418ffcEd9A25273dd4e804D15`](https://testnet.monadvision.com/address/0x70BB0758a38ae43418ffcEd9A25273dd4e804D15)
              * USDT / USD: [`0x14eE6bE30A91989851Dc23203E41C804D4D71441`](https://testnet.monadvision.com/address/0x14eE6bE30A91989851Dc23203E41C804D4D71441)
              * [general reference](https://docs.chain.link/data-feeds/price-feeds/addresses?page=1\&testnetPage=1\&network=monad) <br /><br />

              Data Streams \[pull oracle]:<br />

              * Data stream verifier proxy address: [`0xC539169910DE08D237Df0d73BcDa9074c787A4a1`](https://testnet.monadvision.com/address/0xC539169910DE08D237Df0d73BcDa9074c787A4a1)
            </td>

            <td>[Live data](https://data.chain.link/streams)</td>

            <td>
              * Push oracle ([Price Feeds](https://docs.chain.link/data-feeds/price-feeds))
              * Pull oracle ([Data Streams](https://docs.chain.link/data-streams))
            </td>
          </tr>

          <tr>
            <td>[Chronicle](https://chroniclelabs.org/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.chroniclelabs.org/)</td>
            <td>[Address reference](https://docs.chroniclelabs.org/Developers/testnet)</td>
            <td>[Dashboard](https://chroniclelabs.org/dashboard/oracles?blockchain=MON-TESTNET) (toggle dev mode)</td>
            <td>Push oracle; custom oracles</td>
          </tr>

          <tr>
            <td>[eOracle](https://eo.app/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.eo.app/docs)</td>

            <td>
              * Update conditions: 0.5% deviation & 24h heartbeat
            </td>

            <td>[Dashboard](https://data.eo.app/)</td>
            <td>Push oracle</td>
          </tr>

          <tr>
            <td>[Gelato VRF](https://docs.gelato.network/web3-services/vrf/quick-start)</td>
            <td>✅</td>
            <td>[Docs](https://docs.gelato.network/web3-services/vrf/quick-start)</td>

            <td />

            <td />

            <td>VRF</td>
          </tr>

          <tr>
            <td>[Pyth](https://www.pyth.network/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.pyth.network/)</td>

            <td>
              * Price feeds: [`0x2880aB155794e7179c9eE2e38200202908C17B43`](https://testnet.monadvision.com/address/0x2880aB155794e7179c9eE2e38200202908C17B43)<br /><br />
              * Beta price feeds (incl MON/USDC): [`0xad2B52D2af1a9bD5c561894Cdd84f7505e1CD0B5`](https://testnet.monadvision.com/address/0xad2B52D2af1a9bD5c561894Cdd84f7505e1CD0B5)<br /><br />
              * Entropy: [`0x36825bf3Fbdf5a29E2d5148bfe7Dcf7B5639e320`](https://testnet.monadvision.com/address/0x36825bf3Fbdf5a29E2d5148bfe7Dcf7B5639e320)
            </td>

            <td>[Live data](https://www.pyth.network/price-feeds)<br /><br />
            [Beta live data](https://www.pyth.network/developers/price-feed-ids#beta) (includes MON / USDC)</td>
            <td>[Pull oracle](https://docs.pyth.network/price-feeds/pull-updates);<br />
            [VRF](https://docs.pyth.network/entropy)</td>
          </tr>

          <tr>
            <td>[Redstone](https://www.redstone.finance/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.redstone.finance/)</td>

            <td>
              * Push oracle [addresses](https://app.redstone.finance/app/feeds/?networks=10143)<br />
              * Update conditions for all: 0.5% deviation & 6h heartbeat
            </td>

            <td>[Live data](https://app.redstone.finance/app/tokens/)</td>
            <td>[Push oracle](https://app.redstone.finance/app/feeds/?networks=10143);<br />
            [pull oracle](https://app.redstone.finance/app/pull-model/redstone-primary-prod)</td>
          </tr>

          <tr>
            <td>[Stork](https://stork.network/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.stork.network/)</td>

            <td>
              * Pull oracle (includes MON/USD): [`0xacC0a0cF13571d30B4b8637996F5D6D774d4fd62`](https://testnet.monadvision.com/address/0xacC0a0cF13571d30B4b8637996F5D6D774d4fd62)<br />
              * [Addresses](https://docs.stork.network/resources/contract-addresses/evm); [APIs](https://docs.stork.network/api-reference/contract-apis/evm); [Asset ID Registry](https://docs.stork.network/resources/asset-id-registry)
            </td>

            <td>[Live Data](https://data.stork.network)</td>
            <td>[Pull oracle](https://docs.stork.network/introduction/core-concepts)</td>
          </tr>

          <tr>
            <td>[Supra](https://supra.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.supra.com/)</td>

            <td>
              * Storage: [`0xf0e852BC3F940447862D6b67e5B9807E64B433F6`](https://testnet.monadvision.com/address/0xf0e852BC3F940447862D6b67e5B9807E64B433F6)
              * Pull: [`0xF8522B7fcE37439b98A2be282d413A44269028bE`](https://testnet.monadvision.com/address/0xF8522B7fcE37439b98A2be282d413A44269028bE)
              * Router: [`0x5CbC3Dfa33223884E7752a833Fa6aD28Ee015FC4`](https://testnet.monadvision.com/address/0x5CbC3Dfa33223884E7752a833Fa6aD28Ee015FC4)
              * Deposit: [`0x95bfe6e94D5ff9e9d087647bc589acC9E3D31619`](https://testnet.monadvision.com/address/0x95bfe6e94D5ff9e9d087647bc589acC9E3D31619)
            </td>

            <td>[Live data](https://supra.com/data)</td>
            <td>[Push oracle](https://docs.supra.com/oracles/data-feeds/push-oracle);<br />[Pull oracle](https://docs.supra.com/oracles/data-feeds/pull-oracle);<br />[dVRF](https://docs.supra.com/oracles/dvrf)</td>
          </tr>

          <tr>
            <td>[Switchboard](https://switchboard.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.switchboard.xyz/)</td>

            <td>
              * Pull oracle: [`0xD3860E2C66cBd5c969Fa7343e6912Eff0416bA33`](https://testnet.monadvision.com/address/0xD3860E2C66cBd5c969Fa7343e6912Eff0416bA33)<br /><br />
              * More info: [Deployments](https://docs.switchboard.xyz/docs-by-chain/evm)
            </td>

            <td>[Live data](https://explorer.switchboardlabs.xyz/)</td>
            <td>[Pull oracle](https://docs.switchboard.xyz/docs-by-chain/evm);<br />
            [Oracle aggregator](https://docs.switchboard.xyz/custom-feeds/advanced-feed-configuration/oracle-aggregator);<br />
            [VRF](https://docs.switchboard.xyz/docs-by-chain/evm/randomness)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Chainlink

#### Chainlink Data Streams

[Chainlink Data Streams](https://docs.chain.link/data-streams) deliver low-latency market data offchain, which can be verified onchain. This approach provides decentralized applications (dApps) with on-demand access to high-frequency market data backed by decentralized, fault-tolerant, and transparent infrastructure.

Traditional push-based oracles update onchain data at set intervals or when certain price thresholds are met. In contrast, Chainlink Data Streams uses a pull-based design that preserves trust-minimization with onchain verification.

To get started, check out the [documentation](https://docs.chain.link/data-streams).

#### Chainlink Price Feeds

[Chainlink Price Feeds](https://docs.chain.link/data-feeds) are the quickest way to connect your smart contracts to real-world data such as asset prices.

Data Feeds aggregate many data sources and publish them onchain using a combination of the [Decentralized Data Model](https://docs.chain.link/architecture-overview/architecture-decentralized-model?parent=dataFeeds) and [Offchain Reporting](https://docs.chain.link/architecture-overview/off-chain-reporting?parent=dataFeeds).

To get started, check out the [documentation](https://docs.chain.link/data-feeds).

### Chronicle

Chronicle's decentralized oracle network was originally built within MakerDAO for the development of DAI and is now available to builders on Monad.

* **Data Feeds**: Builders can choose from 90+ data feeds, including crypto assets, yield rates, and RWAs. Chronicle's data is sourced via custom-built data models, only utilizing Tier 1 sources.
* **Transparency & Integrity**: Chronicle's oracle network is fully transparent and verifiable via the [Chronicle dashboard](https://chroniclelabs.org/dashboard/oracles?blockchain=MON-TESTNET). Users can cryptographically challenge the integrity of every oracle update using the 'verify' feature. Data is independently sourced by a [community of Validators](https://chroniclelabs.org/validators) including Gitcoin, Etherscan, Infura, DeFi Saver, and MakerDAO.
* **Gas Efficiency**: Pioneering the Schnorr-based oracle architecture, Chronicle's oracles use 60-80% less gas per update than other oracle providers. This lowest cost per update allows Push oracle updates to be made more frequently, enabling granular data reporting.
* Every oracle implementation is customized to fit your needs. Implement one of our existing data models or contact Chronicle to develop custom oracle data feeds via [Discord](https://discord.gg/CjgvJ9EspJ).

Developers can dive deeper into Chronicle Protocol's architecture and unique design choices via the [docs](https://docs.chroniclelabs.org/).

### Pyth

The [Pyth Network](https://www.pyth.network/) is one of the largest first-party oracle networks, delivering real-time data across a number of chains. Pyth introduces a low-latency [pull oracle](https://docs.pyth.network/price-feeds/pull-updates) design. Data providers push price updates to [Pythnet](https://docs.pyth.network/price-feeds/how-pyth-works/pythnet) every 400 ms. Users pull aggregated prices from Pythnet onto Monad when needed, enabling everyone in the onchain environment to access that data point most efficiently.

Pyth Price Feeds features:

* 400ms latency
* [First-party](https://www.pyth.network/publishers) data sourced directly from financial institutions
* [Price feeds](https://www.pyth.network/developers/price-feed-ids) ranging from crypto, stocks, FX, and metals
  * See also: [beta price feeds](https://www.pyth.network/developers/price-feed-ids#beta) (testnet MON/USD is a beta price feed)
* Available on [many](https://docs.pyth.network/price-feeds/contract-addresses) major chains

Contract Addresses for Monad Testnet:

* Price feeds: [`0x2880aB155794e7179c9eE2e38200202908C17B43`](https://testnet.monadvision.com/address/0x2880aB155794e7179c9eE2e38200202908C17B43)
  * Beta price feeds: [`0xad2B52D2af1a9bD5c561894Cdd84f7505e1CD0B5`](https://testnet.monadvision.com/address/0xad2B52D2af1a9bD5c561894Cdd84f7505e1CD0B5) (testnet MON/USD is a beta price feed)
* Entropy: [`0x36825bf3Fbdf5a29E2d5148bfe7Dcf7B5639e320`](https://testnet.monadvision.com/address/0x36825bf3Fbdf5a29E2d5148bfe7Dcf7B5639e320)

<Note>
  The testnet `MON/USD` price feed is currently a beta feed on Pyth Network. To use the MON/USD feed, integrate the [beta price feed](https://testnet.monadvision.com/address/0xad2B52D2af1a9bD5c561894Cdd84f7505e1CD0B5) contract instead of the primary price feed contract.

  To get the MON/USD price feed offchain, use the beta hermes endpoint: [https://hermes-beta.pyth.network](https://hermes-beta.pyth.network)
</Note>

### Redstone

[RedStone](https://www.redstone.finance/) is the fastest-growing modular oracle, specializing in yield-bearing collateral for lending markets, such as LSTs, LRTs and BTCFi.

To get started, visit the [Redstone documentation](https://docs.redstone.finance/docs/introduction).

### Stork

[Stork](https://stork.network/) is an oracle protocol that enables ultra low latency connections between data providers and both on and off-chain applications. The most common use-case for Stork is pulling and consuming market data in the form of real time price feeds for DeFi.

Stork is implemented as a [pull oracle](https://docs.stork.network/introduction/core-concepts#docs-internal-guid-4b312e7b-7fff-1147-c04b-bbaadec1a82a). Stork continuously aggregates, verifies, and audits data from trusted publishers, and makes that aggregated data available at sub-second latency and frequency. This data can then be pulled into any on or off-chain application as often as needed.

To learn more about how Stork works, visit [Core Concepts](https://docs.stork.network/introduction/core-concepts) and [How It Works](https://docs.stork.network/introduction/how-it-works).

### Supra

[Supra](https://supra.com) provides VRF and decentralized oracle price feeds (push and pull based) that can be used for onchain and offchain use-cases such as spot and perpetual DEXes, lending protocols, and payments protocols.

To get started, visit the [Supra documentation](https://docs.supra.com)

### Switchboard

[Switchboard](https://switchboard.xyz/) is a permissionless oracle protocol that enables developers to bring any off-chain or cross-chain data onto Monad through verifiable, ultra-low-latency feeds.

Switchboard features:

* Fully permissionless feed creation via the [Feed Builder](https://explorer.switchboardlabs.xyz/feed-builder): deploy custom oracles in minutes
* [Switchboard Surge](https://docs.switchboard.xyz/docs-by-chain/evm/surge): Low-latency data feeds with sub-10 ms updates for high-performance applications
* Enterprise-grade reliability
* [Aggregator](https://docs.switchboard.xyz/custom-feeds/advanced-feed-configuration/oracle-aggregator): access multiple oracle sources (like the ones on this page) in a single transaction
* [Data Feed Variables](https://docs.switchboard.xyz/product-documentation/data-feeds/designing-feeds/data-feed-variable-overrides): bring API-gated or confidential data on-chain without exposing API keys
* Customizable feeds: adjust feed parameters (confidence intervals, deviation thresholds, and more) to your dapp's needs
* Decentralized oracle network secured by globally distributed validator set
* Verifiable Randomness: generate secure, verifiable random numbers for games, lotteries, and more
* Supports any data type: prices, prediction markets, sports, weather, RWAs, etc

Contract Address for Monad Mainnet: [`0xB7F03eee7B9F56347e32cC71DaD65B303D5a0E67`](https://monadvision.com/address/0xB7F03eee7B9F56347e32cC71DaD65B303D5a0E67)

For more details, check out [Switchboard's detailed EVM documentation](https://docs.switchboard.xyz/docs-by-chain/evm).


# Payment Orchestrators
Source: https://docs.monad.xyz/tooling-and-infra/payment-orchestrators



Payment orchestrators connect multiple providers, rails, and chains behind a single API — routing
stablecoin and fiat flows (onramps, offramps, transfers, payouts, and swaps) across networks so
builders can move money without managing fragmented integrations.

**See also:** [Onramps](/tooling-and-infra/onramps).

## Provider Summary

<div>
  <table>
    <thead>
      <tr>
        <th>Provider</th>
        <th>Status</th>
        <th>Docs</th>
        <th>Support notes</th>
        <th>Currencies & Countries Supported</th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td>[Brale](https://brale.xyz/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.brale.xyz/)</td>

        <td>
          [Orchestration](https://docs.brale.xyz/documentation/platform/stablecoin-orchestration):

          <ul>
            <li>[Unified transfers](https://docs.brale.xyz/key-concepts/transfers) (one <code>address\_id</code> across on- and off-chain rails)</li>
            <li>[Multi-rail transfer types](https://docs.brale.xyz/coverage/transfer-types): ACH, wire, plus onchain rails</li>
            <li>[Virtual-account automations](https://docs.brale.xyz/key-concepts/automations)</li>
            <li>[ACH payout branding](https://docs.brale.xyz/key-concepts/transfers)</li>
            <li>Program controls: [idempotency](https://docs.brale.xyz/key-concepts/idempotency), scoped credentials, and [webhooks](https://docs.brale.xyz/webhooks/overview)</li>
          </ul>
        </td>

        <td>[Supported Currencies](https://docs.brale.xyz/coverage/value-types)</td>
      </tr>

      <tr>
        <td>[Bridge](https://www.bridge.xyz/)</td>
        <td>✅</td>
        <td>[Docs](https://apidocs.bridge.xyz/)</td>

        <td>
          [Orchestration](https://apidocs.bridge.xyz/platform/orchestration/overview):

          <ul>
            <li>[Transfers](https://apidocs.bridge.xyz/platform/orchestration/transfers/transfer) (one-time fiat or stablecoin)</li>
            <li>[Static Template Transfers](https://apidocs.bridge.xyz/platform/orchestration/transfers/static-templates) (reusable instructions)</li>
            <li>[Virtual Accounts](https://apidocs.bridge.xyz/get-started/guides/move-money/virtualaccounts) (fiat deposit addresses)</li>
            <li>[Liquidation Address](https://apidocs.bridge.xyz/platform/orchestration/liquidation_address/liquidation_address) (map an on-chain address to a fiat/crypto destination)</li>
          </ul>
        </td>

        <td>USD (ACH & wire), EUR (SEPA), GBP, MXN (SPEI) & more via [virtual accounts](https://apidocs.bridge.xyz/get-started/guides/move-money/virtualaccounts)</td>
      </tr>

      <tr>
        <td>[Checker](https://www.checker.finance/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.checker.finance/)</td>

        <td>
          [Orchestration](https://docs.checker.finance/docs/getting-started):

          <ul>
            <li>[Order management & trade execution](https://docs.checker.finance/docs/creating-a-trade-order)</li>
            <li>[RFQ](https://docs.checker.finance/docs/request-for-quote-rfq) + [liquidity-provider quotes](https://docs.checker.finance/docs/get-prices-from-venues)</li>
            <li>[Asset coverage](https://docs.checker.finance/docs/supported-currencies) plus [deposits](https://docs.checker.finance/reference/create_2) and [withdrawals](https://docs.checker.finance/reference/create_4)</li>
            <li>[Cross-border payments (FX)](https://docs.checker.finance/docs/currency-conversion) and [FX quote requests](https://docs.checker.finance/reference/create_3)</li>
            <li>[Market data coverage](https://docs.checker.finance/docs/data-coverage) and [waterfall pricing](https://docs.checker.finance/reference/getprice)</li>
            <li>[Custodian ops & PSP pay-in/pay-out](https://docs.checker.finance/docs/payments-sequence-diagram) (launching)</li>
          </ul>
        </td>

        <td>75+ currencies via 50+ integrated providers (banks, exchanges, OTC desks, payment providers)</td>
      </tr>

      <tr>
        <td>[zerohash](https://zerohash.com/)</td>
        <td>✅</td>
        <td>[Docs](https://docs.zerohash.com/)</td>

        <td>
          [Orchestration](https://docs.zerohash.com/docs/getting-started):

          <ul>
            <li>Transact: [payins](https://docs.zerohash.com/docs/payins), [payouts](https://docs.zerohash.com/docs/payouts), [on/off ramps](https://docs.zerohash.com/docs/on-off-ramps), and [fiat rails](https://docs.zerohash.com/docs/fiat)</li>
            <li>Trade: [buy/sell](https://docs.zerohash.com/docs/buysell), [order management](https://docs.zerohash.com/docs/supported-orders), and [RFQ](https://docs.zerohash.com/docs/request-for-quote)</li>
            <li>Tokenize: [payment rails](https://docs.zerohash.com/docs/tokenization-payment-rails) and [tokenization engine](https://docs.zerohash.com/docs/tokenization-engine)</li>
            <li>Stablecoins: [issuer fees](https://docs.zerohash.com/docs/issuer-fees)</li>
            <li>[Onboarding](https://docs.zerohash.com/docs/onboarding-experience-sample), [SDK](https://docs.zerohash.com/docs/sdk), [Client Portal](https://docs.zerohash.com/docs/onboarding), and [Tax](https://docs.zerohash.com/docs/crypto-tax-overview)</li>
          </ul>
        </td>

        <td>[Supported Countries](https://docs.zerohash.com/docs/supported-regions)</td>
      </tr>
    </tbody>
  </table>
</div>

## Provider details

### Brale

[Brale](https://brale.xyz) is a stablecoin infrastructure platform that enables developers to onramp fiat to stablecoins, offramp stablecoins back to fiat, swap between [stablecoins](https://docs.brale.xyz/coverage/value-types) and [networks](https://docs.brale.xyz/coverage/transfer-types), and issue branded stablecoins, all through a single unified API. Brale handles regulatory compliance, reserves, and multi-chain orchestration so builders can focus on their product. Brale also provides fiat onramps and offramps — see [Onramps](/tooling-and-infra/onramps).

To get started, visit the [Brale documentation](https://docs.brale.xyz/).

### Bridge

[Bridge](https://www.bridge.xyz/) (a Stripe company) is a stablecoin payments platform whose orchestration APIs let developers build onramps, offramps, and crypto-to-crypto transfers, alongside virtual accounts, stablecoin issuance, wallets, and card products. Bridge also provides fiat onramps and offramps — see [Onramps](/tooling-and-infra/onramps).

To get started, visit the [documentation](https://apidocs.bridge.xyz/).

### Checker

[Checker](https://www.checker.finance/) is a digital asset orchestration platform that unifies stablecoin and digital asset operations for financial institutions through a single API. It connects 50+ providers---exchanges, OTC desks, banks, and payment providers---into one programmable network, giving institutions access to trading, payments, treasury, and credit without managing fragmented integrations.

To get started, visit the [documentation](https://docs.checker.finance/).

### zerohash

[zerohash](https://zerohash.com/) is a B2B2C embedded infrastructure platform that provides APIs and SDKs, enabling businesses to integrate digital asset trading, custody, and fiat-to-crypto on-ramps directly into their applications. zerohash also provides fiat onramps and offramps — see [Onramps](/tooling-and-infra/onramps).

To get started, visit the [documentation](https://docs.zerohash.com/).


# RPC Providers
Source: https://docs.monad.xyz/tooling-and-infra/rpc-providers



<Note>
  See also: [API reference](/reference/json-rpc)
</Note>

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Notes</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Alchemy](https://www.alchemy.com/)</td>
            <td>✅</td>
            <td>Alchemy Monad [docs](https://www.alchemy.com/docs/reference/monad-api-quickstart)</td>
          </tr>

          <tr>
            <td>[Ankr](https://www.ankr.com/)</td>
            <td>✅</td>
            <td>Ankr Monad [docs](https://www.ankr.com/web3-api/chains-list/monad/)</td>
          </tr>

          <tr>
            <td>[Blockdaemon](https://www.blockdaemon.com)</td>
            <td>✅</td>
            <td>Blockdaemon Monad [docs](https://www.blockdaemon.com/protocols/monad)</td>
          </tr>

          <tr>
            <td>[BlockPI](https://blockpi.io/)</td>
            <td>✅</td>
            <td>BlockPI Monad [docs](https://blockpi.io/chain/monad)</td>
          </tr>

          <tr>
            <td>[Chainstack](https://chainstack.com/build-better-with-monad/)</td>
            <td>✅</td>
            <td>Chainstack Monad [docs](https://docs.chainstack.com/reference/monad-getting-started)</td>
          </tr>

          <tr>
            <td>[dRPC NodeCloud](https://drpc.org/)</td>
            <td>✅</td>
            <td>dRPC NodeCloud Monad [docs](https://drpc.org/chainlist/monad-mainnet-rpc)</td>
          </tr>

          <tr>
            <td>[Dwellir](https://dwellir.com/)</td>
            <td>✅</td>
            <td>Dwellir Monad [docs](https://dwellir.com/networks/monad)</td>
          </tr>

          <tr>
            <td>[Envio](https://envio.dev/)</td>
            <td>✅</td>
            <td>HyperRPC is a performant read-only RPC. See [docs](https://docs.envio.dev/docs/HyperRPC/overview-hyperrpc)</td>
          </tr>

          <tr>
            <td>[GetBlock](https://getblock.io/)</td>
            <td>✅</td>
            <td>GetBlock Monad [docs](https://getblock.io/nodes/monad/)</td>
          </tr>

          <tr>
            <td>[OnFinality](https://onfinality.io/)</td>
            <td>✅</td>
            <td>OnFinality Monad [docs](https://onfinality.io/en/networks/monad-mainnet)</td>
          </tr>

          <tr>
            <td>[Quicknode](https://www.quicknode.com/)</td>
            <td>✅</td>
            <td>Quicknode Monad [docs](https://www.quicknode.com/chains/monad)</td>
          </tr>

          <tr>
            <td>[Spectrum](https://spectrumnodes.com/)</td>
            <td>✅</td>

            <td />
          </tr>

          <tr>
            <td>[Tatum](https://tatum.io)</td>
            <td>✅</td>
            <td>Tatum Monad [docs](https://tatum.io/exclusive/monad)</td>
          </tr>

          <tr>
            <td>[thirdweb](https://thirdweb.com)</td>
            <td>✅</td>
            <td>thirdweb RPC Edge [docs](https://portal.thirdweb.com/infrastructure/rpc-edge/overview)</td>
          </tr>

          <tr>
            <td>[Triton One](https://triton.one/)</td>
            <td>✅</td>
            <td>Triton One Monad [docs](https://docs.triton.one/chains/monad)</td>
          </tr>

          <tr>
            <td>[Validation Cloud](https://validationcloud.io/)</td>
            <td>✅</td>
            <td>Validation Cloud Monad [docs](https://docs.validationcloud.io/monad)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Notes</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Alchemy](https://www.alchemy.com/)</td>
            <td>✅</td>
            <td>Alchemy Monad [docs](https://www.alchemy.com/docs/reference/monad-api-quickstart)</td>
          </tr>

          <tr>
            <td>[Ankr](https://www.ankr.com/)</td>
            <td>✅</td>
            <td>Ankr Monad [docs](https://www.ankr.com/web3-api/chains-list/monad/)</td>
          </tr>

          <tr>
            <td>[Blockdaemon](https://www.blockdaemon.com)</td>
            <td>✅</td>
            <td>Blockdaemon Monad [docs](https://www.blockdaemon.com/protocols/monad)</td>
          </tr>

          <tr>
            <td>[BlockPI](https://blockpi.io/)</td>
            <td>✅</td>
            <td>BlockPI Monad [docs](https://blockpi.io/chain/monad)</td>
          </tr>

          <tr>
            <td>[Chainstack](https://chainstack.com/build-better-with-monad/)</td>
            <td>✅</td>
            <td>Chainstack Monad [docs](https://docs.chainstack.com/reference/monad-getting-started)</td>
          </tr>

          <tr>
            <td>[dRPC NodeCloud](https://drpc.org/)</td>
            <td>✅</td>
            <td>dRPC NodeCloud Monad [docs](https://drpc.org/chainlist/monad-testnet-rpc)</td>
          </tr>

          <tr>
            <td>[Dwellir](https://dwellir.com/)</td>
            <td>✅</td>
            <td>Dwellir Monad [docs](https://dwellir.com/networks/monad)</td>
          </tr>

          <tr>
            <td>[Envio](https://envio.dev/)</td>
            <td>✅</td>
            <td>HyperRPC is a performant read-only RPC. See [docs](https://docs.envio.dev/docs/HyperRPC/overview-hyperrpc)</td>
          </tr>

          <tr>
            <td>[GetBlock](https://getblock.io/)</td>
            <td>✅</td>
            <td>GetBlock Monad [docs](https://getblock.io/nodes/monad/)</td>
          </tr>

          <tr>
            <td>[OnFinality](https://onfinality.io/)</td>
            <td>✅</td>
            <td>OnFinality Monad [docs](https://onfinality.io/en/networks/monad-mainnet)</td>
          </tr>

          <tr>
            <td>[Quicknode](https://www.quicknode.com/)</td>
            <td>✅</td>
            <td>Quicknode Monad [docs](https://www.quicknode.com/chains/monad)</td>
          </tr>

          <tr>
            <td>[Spectrum](https://spectrumnodes.com/)</td>
            <td>✅</td>

            <td />
          </tr>

          <tr>
            <td>[Tatum](https://tatum.io)</td>
            <td>✅</td>
            <td>Tatum Monad [docs](https://tatum.io/chain/monad)</td>
          </tr>

          <tr>
            <td>[thirdweb](https://thirdweb.com)</td>
            <td>✅</td>
            <td>thirdweb RPC Edge [docs](https://portal.thirdweb.com/infrastructure/rpc-edge/overview)</td>
          </tr>

          <tr>
            <td>[Validation Cloud](https://validationcloud.io/)</td>
            <td>✅</td>
            <td>Validation Cloud Monad [docs](https://docs.validationcloud.io/monad)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Alchemy

[Alchemy](https://www.alchemy.com/) is a popular API provider and developer platform. Its robust, free tier offers access to JSON-RPC APIs, and hosted testnet nodes for Monad Testnet.

### Ankr

[Ankr](https://www.ankr.com/web3-api/) provides private and public RPC endpoints for Monad, powered by a globally distributed and decentralized network of nodes.

### Blockdaemon

[Blockdaemon](https://www.blockdaemon.com/) provides enterprise-grade web3 infrastructure, including dedicated nodes, APIs, staking, liquid staking, MPC wallets, and more.

To get started, visit the [Blockdaemon documentation](https://docs.blockdaemon.com/).

### BlockPI

[BlockPI](https://blockpi.io/) provides enterprise-grade, high-performance RPC services for both Monad Mainnet and Testnet. Whatever you're building on Monad, we offer this premium service at a fraction of the market average price, making high-quality RPC access affordable for everyone.

To get started, visit [BlockPI's Monad page](https://blockpi.io/chain/monad).

### Chainstack

[Chainstack](https://chainstack.com/build-better-with-monad/) provides low-latency, highly reliable, and scalable RPC infrastructure for Monad.

You can deploy robust Monad Mainnet and Testnet nodes and access [geo-balanced RPC endpoints](https://chainstack.com/global-nodes/) on a secure, SOC 2–certified platform.

To get started, create a free account with a [Monad RPC node](https://chainstack.com/).

### dRPC NodeCloud

[dRPC NodeCloud](https://drpc.org/) delivers robust, low-latency RPC for Monad. Free accounts & paid plans from \$10. Full speed. No limits, build confidently.

To get started, visit the [dRPC's Monad page](https://drpc.org/chainlist/monad-testnet-rpc).

### Dwellir

[Dwellir](https://dwellir.com/) supports Monad Mainnet and Testnet endpoints as well as over 100+ other blockchain networks. And best of all: every response costs the same—no compute units.

To get started, visit the [Dwellir Monad page](https://dwellir.com/networks/monad).

### Envio

[Envio](https://envio.dev) has a free read only RPC that supports a subset of data intensive [methods](https://docs.envio.dev/docs/HyperRPC/overview-hyperrpc#supported-methods), Envio's purpose built rust node supports historical data allowing you to query past 10,000 blocks into the past.

To get started, visit the [Envio documentation](https://docs.envio.dev/docs/HyperRPC/overview-hyperrpc)

### GetBlock

[GetBlock](https://getblock.io/) provides reliable RPC endpoints for Monad, offering shared and dedicated nodes with high availability and performance.

To get started, visit the [GetBlock Monad page](https://getblock.io/nodes/monad/).

### OnFinality

[OnFinality](https://onfinality.io/) provides high performance RPC for Monad Mainnet and Testnet, along with support for many other leading networks so teams can build cross chain from Monad with ease. OnFinality infrastructure delivers 99.99% uptime, fast response times, and pricing that is friendly for teams of every size.

Start building on Monad today with reliable and scalable RPC from [OnFinality](https://onfinality.io/en/networks/monad-mainnet).

### Quicknode

[Quicknode](https://www.quicknode.com/) offers access to their [Core RPC API](https://www.quicknode.com/core-api) for both Monad Testnet and Mainnet. Quicknode provides managed, high-performance RPC endpoints with instant access.

To get started, visit [Quicknode's Monad page](https://www.quicknode.com/chains/monad).

### Spectrum

[Spectrum](https://spectrumnodes.com/) is an enterprise-grade RPC Infrastructure provider that
makes it easy to deploy and manage dedicated RPC endpoints to over 150 networks.  Sign up today
to get started on Monad.

To get started, visit the [Spectrum dashboard](https://dashboard.spectrumnodes.com/auth/signup).

### Tatum

[Tatum](https://tatum.io/) provides RPC nodes, blockchain data, and real-time notifications.

To get started, visit the [Tatum documentation](https://docs.tatum.io/).

### thirdweb

[thirdweb](https://thirdweb.com/)'s [RPC Edge](https://portal.thirdweb.com/infrastructure/rpc-edge/overview) provides an RPC endpoint for developers building on Monad.

To get started, visit the [Thirdweb RPC Edge documentation](https://portal.thirdweb.com/infrastructure/rpc-edge/overview).

### Triton One

[Triton One](https://triton.one/triton-rpc/) is a reliable, globally distributed Monad RPC provider built
for teams that need consistent performance under load, high throughput, and uninterrupted uptime.

To get started, visit the Triton One Monad [docs](https://docs.triton.one/chains/monad).

### Validation Cloud

[Validation Cloud](https://validationcloud.io/) is the world's fastest node provider according to Compare Nodes. With 50 million compute units available for use without a credit card and a scale tier that never has rate limits, Validation Cloud is built to support your most rigorous and low-latency workloads.

To get started, visit the [Validation Cloud Monad documentation](https://docs.validationcloud.io/monad).


# Hardhat
Source: https://docs.monad.xyz/tooling-and-infra/toolkits/hardhat



[Hardhat](https://hardhat.org/docs) is a Solidity development framework paired with a JavaScript testing framework.

When configuring your Hardhat project for Monad, set the EVM version to `prague` in your `hardhat.config.js`:

```javascript theme={null}
module.exports = {
  solidity: {
    version: "0.8.28",
    settings: {
      evmVersion: "prague",
    },
  },
};
```

For deployment and verification guides using Hardhat, see:

* [Deploy a Contract with Hardhat](/guides/deploy-smart-contract/hardhat)
* [Verify a Contract with Hardhat](/guides/verify-smart-contract/hardhat)


# Toolkits
Source: https://docs.monad.xyz/tooling-and-infra/toolkits/index



Development toolkits for building on Monad.

## Summary

| Toolkit                                                    | Description                                                                                                                                     |
| ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| [Monad Foundry](/tooling-and-infra/toolkits/monad-foundry) | Custom fork of Foundry with Monad EVM, staking precompile support, and human-readable trace decoding. **Recommended for Solidity development.** |
| [Hardhat](/tooling-and-infra/toolkits/hardhat)             | JavaScript-based Solidity development framework with Monad compatibility.                                                                       |
| [Monad Solonet](/tooling-and-infra/toolkits/monad-solonet) | Run a local Monad network for development and testing.                                                                                          |


# Monad Foundry
Source: https://docs.monad.xyz/tooling-and-infra/toolkits/monad-foundry



[Monad Foundry](https://github.com/category-labs/foundry/tree/monad) is a custom fork of [Foundry](https://book.getfoundry.sh/) that integrates Monad features directly into the familiar Foundry developer workflow. It uses [monad-revm](https://github.com/category-labs/monad-revm), to ensure that `forge test`, `forge script`, `cast`, `anvil`, and `chisel` all execute with Monad's gas model, opcode pricing, and precompile behavior — so your local development environment matches Monad's on-chain behavior.

For general Foundry usage (writing tests, scripts, deployments, configuration, cheatcodes), refer to the [Foundry Docs](https://book.getfoundry.sh/).

## Installation

Install the Monad Foundry installer:

```sh theme={null}
curl -L https://foundry.category.xyz | bash
```

Then install Monad Foundry:

```sh theme={null}
foundryup --network monad
```

This installs all four binaries — `forge`, `cast`, `anvil`, and `chisel` — with Monad support.

<Note>
  The same installer also supports standard Foundry. Running `foundryup` without `--network monad` will install the official upstream Foundry release, so you can use both side by side.
</Note>

## Features

| Feature                   | Description                                                                    |
| ------------------------- | ------------------------------------------------------------------------------ |
| **Monad EVM Execution**   | Monad gas model, 128KB code size limit, no gas refunds, repriced precompiles   |
| **Staking Precompile**    | All staking view functions work locally at address `0x1000`                    |
| **Human-Readable Traces** | Staking calls decoded with function names; address labeled "Staking" in traces |
| **Anvil with Monad**      | `anvil --monad` for a local Monad EVM node                                     |
| **Contract Verification** | `forge verify-contract` uses Monad EVM for bytecode comparison                 |

## Monad EVM Execution

`forge test` and `forge script` execute with Monad EVM by default. The following differences from Ethereum are applied automatically:

* **Gas charging**: Gas is charged based on `gas_limit`, not `gas_used`. There are no gas refunds. See [Gas Pricing](/developer-essentials/gas-pricing) for details.
* **Contract size**: Max contract size is 128KB
* **Initcode size**: Max initcode size is 256KB
* **Precompile gas costs**: See [Opcode Pricing](/developer-essentials/opcode-pricing).
* **No blob transactions**: EIP-4844 (type 3) transactions are not supported.

For the complete list of differences, see [Differences between Monad and Ethereum](/developer-essentials/differences).

## Staking Precompile Support

All [staking precompile](/reference/staking/api) view functions work in `forge test` at address `0x1000`:

### Trace Decoding

When running tests with verbose output (`forge test -vvvv`), staking calls are decoded with human-readable function names and parameters. The address `0x1000` is labeled as **"Staking"** in trace output.

All staking state-changing functions (`addValidator`, `delegate`, `undelegate`, `withdraw`, `compound`, `claimRewards`, `changeCommission`, `externalReward`) and events (`ValidatorRewarded`, `Delegate`, `Undelegate`, `Withdraw`, `ClaimRewards`, `CommissionChanged`, `EpochChanged`, `ValidatorStatusChanged`) are decoded in traces.

Example trace output:

```
├─ [16200] Staking::getEpoch()
│   └─ ← [Return] 42, false
```

## Anvil with Monad EVM

Use `anvil --monad` to run a local development node with Monad EVM:

```sh theme={null}
# Local Monad node
anvil --monad

# Fork Monad Testnet
anvil --fork-url https://testnet-rpc.monad.xyz

# Fork Monad Mainnet
anvil --fork-url https://rpc.monad.xyz
```

Monad EVM activates automatically when forking a Monad RPC endpoint (detected via chain ID), so you don't need the `--monad` flag when forking.

## Cast & Chisel

`cast` and `chisel` execute with Monad EVM by default. All standard commands work the same as upstream Foundry.

## CI Integration

Use the [Monad Foundry GitHub Action](https://github.com/category-labs/foundry-toolchain) to install Monad Foundry in your CI workflows:

```yaml theme={null}
- name: Install Monad Foundry
  uses: category-labs/foundry-toolchain@v1
```

This installs the latest stable Monad Foundry (`stable-monad`) by default. You can also pin a specific version:

```yaml theme={null}
- name: Install Monad Foundry
  uses: category-labs/foundry-toolchain@v1
  with:
    version: v1.5.0-monad.0.1.0
```

Full workflow example:

```yaml theme={null}
name: CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
        with:
          submodules: recursive

      - name: Install Monad Foundry
        uses: category-labs/foundry-toolchain@v1

      - name: Run tests
        run: forge test -vvv
```

The action supports caching and works on all platforms (Linux, macOS, Windows). See the [foundry-toolchain repo](https://github.com/category-labs/foundry-toolchain) for all available options.

## Releases & Versioning

Monad Foundry uses a `v{upstream}-monad.{monad_version}` versioning scheme. For example, `v1.5.0-monad.0.1.0` is based on upstream Foundry v1.5.0 with Monad fork version 0.1.0.

See the [GitHub Releases](https://github.com/category-labs/foundry/releases) for full release history.


# Monad Solonet
Source: https://docs.monad.xyz/tooling-and-infra/toolkits/monad-solonet



[Monad Solonet](https://github.com/monad-crypto/monad-solonet) is an official tool for running a local Monad network. Unlike `anvil --monad`, which simulates Monad EVM behavior, Solonet runs actual Monad nodes — giving you a local environment that more closely matches testnet and mainnet.

Use Solonet when you need full node behavior locally: consensus, staking, or accurate block production timing.

## Installation & usage

See the [Monad Solonet README](https://github.com/monad-crypto/monad-solonet#readme) for setup instructions and configuration options.


# Account Abstraction Providers
Source: https://docs.monad.xyz/tooling-and-infra/wallet-infra/account-abstraction



Account Abstraction Providers provide bundler and paymaster services, enabling features like
sponsored transactions or payment via custom tokens.

## Definitions

| Service   | Description                                                                                     |
| --------- | ----------------------------------------------------------------------------------------------- |
| Bundler   | Operates a custom mempool for UserOperations; simulates and assembles bundles of UserOperations |
| Paymaster | Enables sponsored transactions; enables users to pay for gas with a custom token                |

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Supported services</th>
            <th>How to get started</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Alchemy](https://www.alchemy.com/smart-wallets)</td>
            <td>✅</td>
            <td>[Docs](https://accountkit.alchemy.com/)</td>
            <td>[Gas Manager](https://docs.alchemy.com/docs/gas-manager-services) (aka Paymaster)<br />
            [Bundler](https://docs.alchemy.com/docs/bundler-services)</td>
            <td>[Dashboard](https://dashboard.alchemy.com/accounts?a=smart-wallets\&utm_source=chain_partner\&utm_medium=referral\&utm_campaign=monad)</td>
          </tr>

          <tr>
            <td>[Biconomy](https://biconomy.io)</td>
            <td>✅</td>
            <td>[Docs](https://docs.biconomy.io)</td>
            <td>[Orchestration Infrastructure](https://docs.biconomy.io/new/learn-about-biconomy/what-is-mee)</td>
            <td>[Getting started](https://docs.biconomy.io/supertransaction-api/getting-started)</td>
          </tr>

          <tr>
            <td>[FastLane](https://www.fastlane.xyz/)</td>
            <td>❓</td>
            <td>[Docs](https://docs.shmonad.xyz/)</td>
            <td>[Paymaster and Bundler](https://github.com/FastLane-Labs/4337-bundler-paymaster-script/tree/main)</td>
            <td>[Dashboard](https://shmonad.xyz/)</td>
          </tr>

          <tr>
            <td>[Pimlico](https://pimlico.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.pimlico.io/)</td>
            <td>[Paymaster](https://docs.pimlico.io/infra/paymaster)<br />
            [Bundler](https://docs.pimlico.io/infra/bundler)</td>
            <td>[Tutorial](https://docs.pimlico.io/permissionless/tutorial/tutorial-1)</td>
          </tr>

          <tr>
            <td>[Sequence](https://sequence.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sequence.xyz/solutions/infrastructure/transaction-api)</td>
            <td>Relayer: gasless, batched, parallelized transactions</td>
            <td>[Quickstart](https://docs.sequence.xyz/solutions/builder/gas-sponsorship)</td>
          </tr>

          <tr>
            <td>[thirdweb](https://thirdweb.com/)</td>
            <td>✅</td>
            <td>[Docs](https://portal.thirdweb.com/)</td>
            <td>[Paymaster and Bundler](https://portal.thirdweb.com/connect/account-abstraction/infrastructure)</td>
            <td>[Quickstart](https://portal.thirdweb.com/typescript/v5/account-abstraction/get-started)</td>
          </tr>

          <tr>
            <td>[ZeroDev](https://zerodev.app/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.zerodev.app/)</td>
            <td>[Meta AA infrastructure](https://docs.zerodev.app/meta-infra/intro) for bundlers and paymasters</td>
            <td>[Dashboard](https://dashboard.zerodev.app/)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Supported services</th>
            <th>How to get started</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Alchemy](https://www.alchemy.com/smart-wallets)</td>
            <td>✅</td>
            <td>[Docs](https://accountkit.alchemy.com/)</td>
            <td>[Gas Manager](https://docs.alchemy.com/docs/gas-manager-services) (aka Paymaster)<br />
            [Bundler](https://docs.alchemy.com/docs/bundler-services)</td>
            <td>[Dashboard](https://dashboard.alchemy.com/accounts?a=smart-wallets\&utm_source=chain_partner\&utm_medium=referral\&utm_campaign=monad)</td>
          </tr>

          <tr>
            <td>[Biconomy](https://biconomy.io)</td>
            <td>✅</td>
            <td>[Docs](https://docs.biconomy.io)</td>
            <td>[Orchestration Infrastructure](https://docs.biconomy.io/new/learn-about-biconomy/what-is-mee)</td>
            <td>[Getting started](https://docs.biconomy.io/supertransaction-api/getting-started)</td>
          </tr>

          <tr>
            <td>[FastLane](https://www.fastlane.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.shmonad.xyz/)</td>
            <td>[Paymaster and Bundler](https://github.com/FastLane-Labs/4337-bundler-paymaster-script/tree/main)</td>
            <td>[Dashboard](https://shmonad.xyz/)</td>
          </tr>

          <tr>
            <td>[Gelato](https://docs.gelato.cloud/paymaster-&-bundler/introduction/overview)</td>
            <td>✅</td>
            <td>[Docs](https://docs.gelato.cloud/paymaster-&-bundler/introduction/overview)</td>
            <td>[Paymaster and Bundler](https://docs.gelato.cloud/paymaster-&-bundler/introduction/overview)</td>
            <td>[Quickstart](https://docs.gelato.cloud/paymaster-&-bundler/how-to-guides/overview)</td>
          </tr>

          <tr>
            <td>[Openfort](https://openfort.io/)</td>
            <td>✅</td>
            <td>[Docs](https://www.openfort.io/docs)</td>
            <td>[Paymaster and Bundler](https://www.openfort.io/docs/overview)</td>
            <td>[Quickstart](https://www.openfort.io/docs/overview/start)</td>
          </tr>

          <tr>
            <td>[Pimlico](https://pimlico.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.pimlico.io/)</td>
            <td>[Paymaster](https://docs.pimlico.io/infra/paymaster)<br />
            [Bundler](https://docs.pimlico.io/infra/bundler)</td>
            <td>[Tutorial](https://docs.pimlico.io/permissionless/tutorial/tutorial-1)</td>
          </tr>

          <tr>
            <td>[Sequence](https://sequence.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sequence.xyz/solutions/infrastructure/transaction-api)</td>
            <td>Relayer: gasless, batched, parallelized transactions</td>
            <td>[Quickstart](https://docs.sequence.xyz/solutions/builder/gas-sponsorship)</td>
          </tr>

          <tr>
            <td>[thirdweb](https://thirdweb.com/)</td>
            <td>✅</td>
            <td>[Docs](https://portal.thirdweb.com/)</td>
            <td>[Paymaster and Bundler](https://portal.thirdweb.com/connect/account-abstraction/infrastructure)</td>
            <td>[Quickstart](https://portal.thirdweb.com/typescript/v5/account-abstraction/get-started)</td>
          </tr>

          <tr>
            <td>[ZeroDev](https://zerodev.app/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.zerodev.app/)</td>
            <td>[Meta AA infrastructure](https://docs.zerodev.app/meta-infra/intro) for bundlers and paymasters</td>
            <td>[Dashboard](https://dashboard.zerodev.app/)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Alchemy

Alchemy powers the [#1 most used](https://www.bundlebear.com/erc4337-overview/all) smart accounts today with account abstraction that eliminates gas fees and signing for users. Their accounts support ERC-4337, EIP-7702, and ERC-6900, a modular account standard co-authored with the Ethereum Foundation, Circle, and Trust Wallet.

To get started, sign up for an [Alchemy account](https://dashboard.alchemy.com/accounts?utm_source=chain_partner\&utm_medium=referral\&utm_campaign=monad), visit the [documentation](https://accountkit.alchemy.com/), follow the [quickstart](https://accountkit.alchemy.com/react/quickstart) guide. To learn more, check out their [smart wallets](https://www.alchemy.com/smart-wallets) and demo [here](https://demo.alchemy.com/).

### Biconomy

[Biconomy](https://biconomy.io) is the most comprehensive smart account and execution infrastructure platform that enables seamless, user-friendly experiences across single or multiple chains. With Biconomy, developers can build superior onchain UX through gas abstraction, sessions, batching, and one-click signatures for complex actions on any number of networks.

To get started, visit the [documentation](https://docs.biconomy.io/).

### FastLane

[FastLane](https://www.fastlane.xyz/) is an MEV protocol for validators + apps with an integrated 4337 bundler, an on-chain task scheduler, and the first holistic LST.

To get started, vist the [shMonad](https://docs.shmonad.xyz/) Documentation or try the shMonad bundler using the following example [project](https://github.com/FastLane-Labs/4337-bundler-paymaster-script/tree/main).

### Gelato

[Gelato](https://docs.gelato.cloud/paymaster-&-bundler/introduction/overview) provides Paymaster and Bundler services that enable sponsored transactions and Account Abstraction, allowing you to cover gas costs on behalf of users and enable seamless onchain experiences.

To get started, visit the [documentation](https://docs.gelato.cloud/paymaster-&-bundler/introduction/overview) or follow the [quickstart](https://docs.gelato.cloud/paymaster-&-bundler/how-to-guides/overview) guide.

### Openfort

[Openfort](https://openfort.io) is a developer platform that helps projects onboard and and activates wallets. It does so by creating wallets with it’s SSS and passkeys,sending transactions via sponsored paymasters and session keys or directly using backend wallets for automated onchain actions.

To get started, visit the [documentation](https://www.openfort.io/docs/overview/start) or follow the [quickstart](https://www.openfort.io/docs/guides/react) guide.

### Pimlico

[Pimlico](https://pimlico.io/) is the world's most advanced ERC-4337 account abstraction infrastructure platform. Pimlico provides a suite of tools and services to help you build, deploy, and manage smart accounts on Ethereum and other EVM-compatible chains.

To get started, visit the [documentation](https://docs.pimlico.io/) or follow the [quickstart](https://docs.pimlico.io/permissionless/tutorial/tutorial-1) guide.

### Sequence

The [Sequence](https://sequence.xyz)
[Transaction API](https://docs.sequence.xyz/solutions/infrastructure/transaction-api) is a unified
relayer that dispatches transactions on EVM chains with:

* Gas sponsorship
* Fee abstraction
* Batching
* Parallel processing

It manages nonces, estimates optimal gas, and resubmits transactions when needed, so you can focus
on your business logic. [Sequence Builder](https://sequence.build/) offers a Gas Sponsorship feature
that allows project owners to easily sponsor gas for their users in web3 apps. By covering
transaction fees, users can enjoy a seamless experience without worrying about obtaining crypto
for fees which is seamlessly integrated with our suite of smart contract wallets.

To get started, visit the gas sponsorship [docs](https://docs.sequence.xyz/solutions/builder/gas-sponsorship).

### thirdweb

[thirdweb](https://portal.thirdweb.com/connect/account-abstraction/overview) offers a complete platform to leverage account abstraction.

Remove the clunky user experience of requiring gas & signatures for every onchain action:

* Abstract away gas
* Pre-audited account factory contracts
* Built-in infra:
* Sponsorship policies

To get started:

1. Sign up for a [free thirdweb account](https://thirdweb.com/team)
2. Visit [Account Abstraction Documentation](https://portal.thirdweb.com/connect/account-abstraction/how-it-works) and [Account Abstraction Playground](https://playground.thirdweb.com/connect/account-abstraction/connect)

### Zerodev

[ZeroDev](https://zerodev.app) is the most powerful smart account development platform. With ZeroDev, you can build Web3 experiences without gas, confirmations, seed phrases, and bridging.

To get started, visit the [documentation](https://docs.zerodev.app/) or follow the [quickstart](https://docs.zerodev.app/sdk/getting-started/quickstart) guide.


# Embedded Wallets
Source: https://docs.monad.xyz/tooling-and-infra/wallet-infra/embedded-wallets



## Background

Some developers want to "embed" a wallet into their application. Here are a few possible reasons
they might want to do this:

* to allow users to sign in with email or another social sign-in method
* to allow users to take actions within the app without signing a new transaction each time.

Generally speaking, embedded wallet services provide this by utilizing advanced cryptographic
techniques to shard keys. Some keys are stored user-side while others are stored on
the application developer's server or the embedded wallet provider's server.

This page attempts a toplogy of authentication and key management features over the set of
providers supporting Monad.

### Authentication Features

| Features        | Description                                                                                                       |
| --------------- | ----------------------------------------------------------------------------------------------------------------- |
| Passkey sign-in | Authentication with [WebAuthn](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API) (passkey) |
| Social sign-in  | Authentication with social accounts (google, X, etc)                                                              |
| Email sign-in   | Authentication with OTP via email                                                                                 |
| SMS sign-in     | Authentication with OTP via SMS                                                                                   |

### Key Management Features

| Features                 | Description                                                                                     |
| ------------------------ | ----------------------------------------------------------------------------------------------- |
| MPC                      | Multi-party computation                                                                         |
| SSS                      | Shamir's Secret Sharing                                                                         |
| TEE                      | Storage of private keys in a cloud-based Trusted Execution Environment, like AWS Nitro Enclaves |
| TSS                      | Threshold Signature Scheme                                                                      |
| Embedded wallet          | A wallet interface local to a website or mobile app, utilizing browser session keys for signing |
| Server-delegated actions | Allow app to request permission to sign on the user's behalf                                    |
| Session keys             | Scoped keys that grant access only for specific apps, useful for bots/AI agents                 |

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Supported services</th>
            <th>Security Method</th>
            <th>How to get started</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Alchemy](https://www.alchemy.com/smart-wallets)</td>
            <td>✅</td>
            <td>[Docs](https://accountkit.alchemy.com/)</td>
            <td>[Embedded wallets](https://accountkit.alchemy.com/react/quickstart)<br />
            Auth: [passkey](https://accountkit.alchemy.com/signer/authentication/passkey-signup), [social](https://accountkit.alchemy.com/signer/authentication/social-login), [email](https://accountkit.alchemy.com/signer/authentication/email-otp) sign-in</td>

            <td />

            <td>[Quickstart](https://accountkit.alchemy.com/react/quickstart)</td>
          </tr>

          <tr>
            <td>[Coinbase Developer Platform (CDP)](https://www.coinbase.com/developer-platform/products/embeddedwallets)</td>
            <td>✅</td>
            <td>[Docs](https://docs.cdp.coinbase.com/embedded-wallets/welcome)</td>
            <td>[Embedded wallets](https://docs.cdp.coinbase.com/embedded-wallets/welcome)<br />
            Auth: [email/social/SMS](https://docs.cdp.coinbase.com/embedded-wallets/authentication-methods)</td>
            <td>Device-based secure enclaves</td>
            <td>[Quickstart](https://docs.cdp.coinbase.com/embedded-wallets/quickstart)</td>
          </tr>

          <tr>
            <td>[Crossmint](https://www.crossmint.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.crossmint.com/)</td>
            <td>[Embedded wallets](https://docs.crossmint.com/wallets/overview) (smart contract wallets with modular signers)<br />
            Auth: [device](https://docs.crossmint.com/wallets/concepts/signers#device-signer), [passkey](https://docs.crossmint.com/wallets/concepts/signers#passkey-signer), [server](https://docs.crossmint.com/wallets/concepts/signers#server-signer), [email](https://docs.crossmint.com/wallets/concepts/signers#email-otp-signer), [SMS](https://docs.crossmint.com/wallets/concepts/signers#sms--phone-otp-signer) sign-in</td>
            <td>Smart wallets; device secure enclave</td>
            <td>[Quickstart](https://docs.crossmint.com/wallets/quickstarts/react)</td>
          </tr>

          <tr>
            <td>[Cubist](https://cubist.dev/)</td>
            <td>✅</td>

            <td />

            <td>[Embedded wallets](https://cubist.dev/products/cubesigner-end-user-custody) (CubeSigner); non-custodial signing & key management<br />
            Auth: social (Google, Apple, X, Telegram) sign-in; MFA: passkeys, YubiKeys, authenticator apps</td>
            <td>HSM + TEE (Nitro Enclaves)</td>
            <td>[Quickstart](https://github.com/cubist-labs/CubeSigner-TypeScript-SDK)</td>
          </tr>

          <tr>
            <td>[Dynamic](https://dynamic.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.dynamic.xyz/)</td>
            <td>[Embedded wallets](https://docs.dynamic.xyz/wallets/embedded-wallets/dynamic-embedded-wallets)<br />
            Auth: [passkey](https://docs.dynamic.xyz/wallets/v1-embedded/transactional-mfa/passkeys#passkeys), [email/social/SMS](https://docs.dynamic.xyz/authentication-methods/email-social-sms) sign-in</td>
            <td>TEE; TSS-MPC (just added)</td>
            <td>[Get started](https://www.dynamic.xyz/get-started)</td>
          </tr>

          <tr>
            <td>[Fordefi](https://fordefi.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.fordefi.com/)</td>
            <td>[Products and Services](https://docs.fordefi.com/user-guide/welcome/products-and-services)</td>
            <td>MPC</td>
            <td>[Quickstart](https://docs.fordefi.com/user-guide/quickstart)</td>
          </tr>

          <tr>
            <td>[MetaMask Embedded Wallet](https://docs.metamask.io/embedded-wallets/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.metamask.io/embedded-wallets/)</td>
            <td>Embedded wallet<br />
            Auth: [passkey](https://docs.metamask.io/embedded-wallets/authentication/), [social](https://docs.metamask.io/embedded-wallets/authentication/social-logins/google/), [email](https://docs.metamask.io/embedded-wallets/authentication/basic-logins/email-passwordless/), [SMS](https://docs.metamask.io/embedded-wallets/authentication/basic-logins/sms-otp/)</td>
            <td>MPC-SSS/TSS</td>
            <td>[Quickstart](https://docs.metamask.io/embedded-wallets/connect-blockchain/evm/monad)</td>
          </tr>

          <tr>
            <td>[Openfort](https://openfort.io/)</td>
            <td>✅</td>
            <td>[Docs](https://www.openfort.io/docs)</td>
            <td>[Embedded wallets](https://www.openfort.io/docs/guides/react/configuration), [Backend wallets](https://www.openfort.io/docs/guides/server/dev), [Ecosystem wallets](https://www.openfort.io/docs/guides/ecosystem)<br />
            Auth: [passkeys](https://www.openfort.io/docs/products/embedded-wallet/react/auth), [social](https://www.openfort.io/docs/products/embedded-wallet/react/auth), [email](https://www.openfort.io/docs/products/embedded-wallet/react/auth)</td>
            <td>SSS</td>
            <td>[Quickstart](https://www.openfort.io/docs/guides/react)</td>
          </tr>

          <tr>
            <td>[Para](https://www.getpara.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.getpara.com/)</td>
            <td>[Embedded wallets](https://docs.getpara.com/getting-started/initial-setup/react-nextjs); robust policy engine for sessions<br />
            Auth: [email and phone](https://docs.getpara.com/v2/swift/guides/email-phone-login#email-and-phone-login), [social](https://docs.getpara.com/customize-para/oauth-social-logins), [SMS](https://docs.getpara.com/customize-para/phone-login) sign-in</td>
            <td>MPC + DKG</td>
            <td>[Quickstart](https://docs.getpara.com/v1/web/guides/evm/overview#evm-overview)</td>
          </tr>

          <tr>
            <td>[Portal](https://www.portalhq.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.portalhq.io/)</td>
            <td>[Integration overview](https://docs.portalhq.io/integrations)</td>
            <td>TSS MPC</td>
            <td>[API Quickstart](https://docs.portalhq.io/apis/quickstart), [SDK Quickstart](https://docs.portalhq.io/sdks/quickstart)</td>
          </tr>

          <tr>
            <td>[Privy](https://privy.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.privy.io/)</td>
            <td>[Embedded wallets](https://docs.privy.io/guide/embedded-wallets), [server wallets](https://docs.privy.io/guide/overview-server-wallets), server-delegated actions<br />
            Auth: [passkey](https://docs.privy.io/guide/authentication), [social](https://docs.privy.io/guide/authentication), [email](https://docs.privy.io/guide/authentication), [SMS](https://docs.privy.io/guide/authentication)</td>
            <td>TEE + SSS</td>
            <td>[Quickstart](https://docs.privy.io/guide/react/quickstart)</td>
          </tr>

          <tr>
            <td>[Reown](https://reown.com/) (formerly WalletConnect)</td>
            <td>✅</td>
            <td>[Docs](https://docs.reown.com/)</td>
            <td>Popular UI component for selecting a wallet<br />
            Embedded wallet with social/email sign-in</td>

            <td />

            <td>[Overview](https://docs.reown.com/appkit/overview)</td>
          </tr>

          <tr>
            <td>[Sequence](https://sequence.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sequence.xyz/solutions/wallets/overview)</td>
            <td>[Embedded wallets](https://docs.sequence.xyz/solutions/wallets/developers/embedded-wallet/overview),
            [ecosystem wallets](https://docs.sequence.xyz/solutions/wallets/developers/overview)<br />Auth: Passkey, Google, Apple, Twitter, email, Facebook, Twitch, Epic Games, Playfab, Stych, Standard OAuth</td>
            <td>TEE; Sandboxed Smart Sessions</td>
            <td>[Ecosystem quickstart](https://docs.sequence.xyz/solutions/wallets/developers/overview)<br /><br />
            [Embedded quickstart](https://docs.sequence.xyz/solutions/wallets/developers/embedded-wallet/quickstart)</td>
          </tr>

          <tr>
            <td>[thirdweb](https://thirdweb.com/)</td>
            <td>✅</td>
            <td>[Docs](https://portal.thirdweb.com/connect/wallet/overview)</td>
            <td>Embedded wallets<br />
            Auth: [passkey](https://portal.thirdweb.com/connect/wallet/sign-in-methods/configure), [social](https://portal.thirdweb.com/connect/wallet/sign-in-methods/configure), [email](https://portal.thirdweb.com/connect/wallet/sign-in-methods/configure), [SMS](https://portal.thirdweb.com/connect/wallet/sign-in-methods/configure), OIDC, or generic auth</td>

            <td />

            <td>[Quickstart](https://portal.thirdweb.com/connect/wallet/get-started)</td>
          </tr>

          <tr>
            <td>[Turnkey](https://www.turnkey.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.turnkey.com/)</td>
            <td>[Embedded wallet](https://docs.turnkey.com/reference/embedded-wallet-kit), [policy engine](https://docs.turnkey.com/concepts/policies/overview), [delegated access](https://docs.turnkey.com/concepts/policies/delegated-access-frontend), [signing automation](https://docs.turnkey.com/signing-automation/overview), [sessions](https://docs.turnkey.com/authentication/sessions)<br />
            [Server-side SDKs](https://docs.turnkey.com/sdks/introduction) for auth, wallet management, and policies<br />
            Auth: [passkey](https://docs.turnkey.com/authentication/passkeys/introduction), [social](https://docs.turnkey.com/authentication/social-logins), [email](https://docs.turnkey.com/authentication/email), [SMS](https://docs.turnkey.com/authentication/sms) login</td>
            <td>TEE</td>
            <td>[Quickstart](https://docs.turnkey.com/getting-started/quickstart)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Supported services</th>
            <th>Security Method</th>
            <th>How to get started</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Alchemy](https://www.alchemy.com/smart-wallets)</td>
            <td>✅</td>
            <td>[Docs](https://accountkit.alchemy.com/)</td>
            <td>[Embedded wallets](https://accountkit.alchemy.com/react/quickstart)<br />
            Auth: [passkey](https://accountkit.alchemy.com/signer/authentication/passkey-signup), [social](https://accountkit.alchemy.com/signer/authentication/social-login), [email](https://accountkit.alchemy.com/signer/authentication/email-otp) sign-in</td>

            <td />

            <td>[Quickstart](https://accountkit.alchemy.com/react/quickstart)</td>
          </tr>

          <tr>
            <td>[Coinbase Developer Platform (CDP)](https://www.coinbase.com/developer-platform/products/embeddedwallets)</td>
            <td>✅</td>
            <td>[Docs](https://docs.cdp.coinbase.com/embedded-wallets/welcome)</td>
            <td>[Embedded wallets](https://docs.cdp.coinbase.com/embedded-wallets/welcome)<br />
            Auth: [email/social/SMS](https://docs.cdp.coinbase.com/embedded-wallets/authentication-methods)</td>
            <td>Device-based secure enclaves</td>
            <td>[Quickstart](https://docs.cdp.coinbase.com/embedded-wallets/quickstart)</td>
          </tr>

          <tr>
            <td>[Crossmint](https://www.crossmint.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.crossmint.com/)</td>
            <td>[Embedded wallets](https://docs.crossmint.com/wallets/overview) (smart contract wallets with modular signers)<br />
            Auth: [device](https://docs.crossmint.com/wallets/concepts/signers#device-signer), [passkey](https://docs.crossmint.com/wallets/concepts/signers#passkey-signer), [server](https://docs.crossmint.com/wallets/concepts/signers#server-signer), [email](https://docs.crossmint.com/wallets/concepts/signers#email-otp-signer), [SMS](https://docs.crossmint.com/wallets/concepts/signers#sms--phone-otp-signer) sign-in</td>
            <td>Smart wallets; device secure enclave</td>
            <td>[Quickstart](https://docs.crossmint.com/wallets/quickstarts/react)</td>
          </tr>

          <tr>
            <td>[Cubist](https://cubist.dev/)</td>
            <td>✅</td>

            <td />

            <td>[Embedded wallets](https://cubist.dev/products/cubesigner-end-user-custody) (CubeSigner); non-custodial signing & key management<br />
            Auth: social (Google, Apple, X, Telegram) sign-in; MFA: passkeys, YubiKeys, authenticator apps</td>
            <td>HSM + TEE (Nitro Enclaves)</td>
            <td>[Quickstart](https://github.com/cubist-labs/CubeSigner-TypeScript-SDK)</td>
          </tr>

          <tr>
            <td>[Dynamic](https://dynamic.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.dynamic.xyz/)</td>
            <td>[Embedded wallets](https://docs.dynamic.xyz/wallets/embedded-wallets/dynamic-embedded-wallets)<br />
            Auth: [passkey](https://docs.dynamic.xyz/wallets/v1-embedded/transactional-mfa/passkeys#passkeys), [email/social/SMS](https://docs.dynamic.xyz/authentication-methods/email-social-sms) sign-in</td>
            <td>TEE; TSS-MPC (just added)</td>
            <td>[Get started](https://www.dynamic.xyz/get-started)</td>
          </tr>

          <tr>
            <td>[Fordefi](https://fordefi.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.fordefi.com/)</td>
            <td>[Products and Services](https://docs.fordefi.com/user-guide/welcome/products-and-services)</td>
            <td>MPC</td>
            <td>[Quickstart](https://docs.fordefi.com/user-guide/quickstart)</td>
          </tr>

          <tr>
            <td>[MetaMask Embedded Wallet](https://docs.metamask.io/embedded-wallets/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.metamask.io/embedded-wallets/)</td>
            <td>Embedded wallet<br />
            Auth: [passkey](https://docs.metamask.io/embedded-wallets/authentication/), [social](https://docs.metamask.io/embedded-wallets/authentication/social-logins/google/), [email](https://docs.metamask.io/embedded-wallets/authentication/basic-logins/email-passwordless/), [SMS](https://docs.metamask.io/embedded-wallets/authentication/basic-logins/sms-otp/)</td>
            <td>MPC-SSS/TSS</td>
            <td>[Quickstart](https://docs.metamask.io/embedded-wallets/connect-blockchain/evm/monad)</td>
          </tr>

          <tr>
            <td>[Openfort](https://openfort.io/)</td>
            <td>✅</td>
            <td>[Docs](https://www.openfort.io/docs)</td>
            <td>[Embedded wallets](https://www.openfort.io/docs/guides/react/configuration), [Backend wallets](https://www.openfort.io/docs/guides/server/dev), [Ecosystem wallets](https://www.openfort.io/docs/guides/ecosystem)<br />
            Auth: [passkeys](https://www.openfort.io/docs/products/embedded-wallet/react/auth), [social](https://www.openfort.io/docs/products/embedded-wallet/react/auth), [email](https://www.openfort.io/docs/products/embedded-wallet/react/auth)</td>
            <td>SSS</td>
            <td>[Quickstart](https://www.openfort.io/docs/guides/react)</td>
          </tr>

          <tr>
            <td>[Para](https://www.getpara.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.getpara.com/)</td>
            <td>[Embedded wallets](https://docs.getpara.com/getting-started/initial-setup/react-nextjs); robust policy engine for sessions<br />
            Auth: [email and phone](https://docs.getpara.com/v2/swift/guides/email-phone-login#email-and-phone-login), [social](https://docs.getpara.com/customize-para/oauth-social-logins), [SMS](https://docs.getpara.com/customize-para/phone-login) sign-in</td>
            <td>MPC + DKG</td>
            <td>[Quickstart](https://docs.getpara.com/v1/web/guides/evm/overview#evm-overview)</td>
          </tr>

          <tr>
            <td>[Phantom](https://phantom.com/learn/developers)</td>
            <td>✅</td>
            <td>[Docs](https://docs.phantom.com/)</td>
            <td>[Embedded wallets](https://github.com/phantom/wallet-sdk) (Web SDK & Native Mobile SDK)<br />
            Auth: [Google](https://phantom.com/learn/blog/deep-dive-log-in-to-phantom-with-email) sign-in</td>
            <td>SSS</td>
            <td>[Quickstart](https://docs.phantom.com/introduction)</td>
          </tr>

          <tr>
            <td>[Portal](https://www.portalhq.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.portalhq.io/)</td>
            <td>[Integration overview](https://docs.portalhq.io/integrations)</td>
            <td>TSS MPC</td>
            <td>[API Quickstart](https://docs.portalhq.io/apis/quickstart), [SDK Quickstart](https://docs.portalhq.io/sdks/quickstart)</td>
          </tr>

          <tr>
            <td>[Privy](https://privy.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.privy.io/)</td>
            <td>[Embedded wallets](https://docs.privy.io/guide/embedded-wallets), [server wallets](https://docs.privy.io/guide/overview-server-wallets), server-delegated actions<br />
            Auth: [passkey](https://docs.privy.io/guide/authentication), [social](https://docs.privy.io/guide/authentication), [email](https://docs.privy.io/guide/authentication), [SMS](https://docs.privy.io/guide/authentication)</td>
            <td>TEE + SSS</td>
            <td>[Quickstart](https://docs.privy.io/guide/react/quickstart)</td>
          </tr>

          <tr>
            <td>[Reown](https://reown.com/) (formerly WalletConnect)</td>
            <td>✅</td>
            <td>[Docs](https://docs.reown.com/)</td>
            <td>Popular UI component for selecting a wallet<br />
            Embedded wallet with social/email sign-in</td>

            <td />

            <td>[Overview](https://docs.reown.com/appkit/overview)</td>
          </tr>

          <tr>
            <td>[Sequence](https://sequence.xyz/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.sequence.xyz/solutions/wallets/overview)</td>
            <td>[Embedded wallets](https://docs.sequence.xyz/solutions/wallets/developers/embedded-wallet/overview),
            [ecosystem wallets](https://docs.sequence.xyz/solutions/wallets/developers/overview)<br />Auth: Passkey, Google, Apple, Twitter, email, Facebook, Twitch, Epic Games, Playfab, Stych, Standard OAuth</td>
            <td>TEE; Sandboxed Smart Sessions</td>
            <td>[Ecosystem quickstart](https://docs.sequence.xyz/solutions/wallets/developers/overview)<br /><br />
            [Embedded quickstart](https://docs.sequence.xyz/solutions/wallets/developers/embedded-wallet/quickstart)</td>
          </tr>

          <tr>
            <td>[thirdweb](https://thirdweb.com/)</td>
            <td>✅</td>
            <td>[Docs](https://portal.thirdweb.com/connect/wallet/overview)</td>
            <td>Embedded wallets<br />
            Auth: [passkey](https://portal.thirdweb.com/connect/wallet/sign-in-methods/configure), [social](https://portal.thirdweb.com/connect/wallet/sign-in-methods/configure), [email](https://portal.thirdweb.com/connect/wallet/sign-in-methods/configure), [SMS](https://portal.thirdweb.com/connect/wallet/sign-in-methods/configure), OIDC, or generic auth</td>

            <td />

            <td>[Quickstart](https://portal.thirdweb.com/connect/wallet/get-started)</td>
          </tr>

          <tr>
            <td>[Turnkey](https://www.turnkey.com/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.turnkey.com/)</td>
            <td>[Embedded wallet](https://docs.turnkey.com/reference/embedded-wallet-kit), [policy engine](https://docs.turnkey.com/concepts/policies/overview), [delegated access](https://docs.turnkey.com/concepts/policies/delegated-access-frontend), [signing automation](https://docs.turnkey.com/signing-automation/overview), [sessions](https://docs.turnkey.com/authentication/sessions)<br />
            [Server-side SDKs](https://docs.turnkey.com/sdks/introduction) for auth, wallet management, and policies<br />
            Auth: [passkey](https://docs.turnkey.com/authentication/passkeys/introduction), [social](https://docs.turnkey.com/authentication/social-logins), [email](https://docs.turnkey.com/authentication/email), [SMS](https://docs.turnkey.com/authentication/sms) login</td>
            <td>TEE</td>
            <td>[Quickstart](https://docs.turnkey.com/getting-started/quickstart)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Providers Offering Subsidized Usage

These WaaS providers are subsidizing usage on Monad Testnet:

| Provider                            | How to access                                                                                                     |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [Privy](https://privy.io/)          | Sign up, then email the Privy team at `monad@privy.io`                                                            |
| [Para](https://www.getpara.com/)    | Sign up via the [Developer Portal](https://developer.getpara.com/) and reach out to the team at `ops@getpara.com` |
| [Turnkey](https://www.turnkey.com/) | Turnkey is free for developers building on Monad Testnet. All you need to do is sign up!                          |

## Provider Details

### Alchemy

[Account Kit](https://accountkit.alchemy.com/) is a complete solution for account abstraction. Using Account Kit, you can create a smart contract wallet for every user that leverages account abstraction to simplify every step of your app's onboarding experience. It also offers Gas Manager and Bundler APIs for sponsoring gas and batching transactions.

To get started, sign up for an [Alchemy account](https://www.alchemy.com/), visit the [documentation](https://accountkit.alchemy.com/), follow the [quickstart](https://accountkit.alchemy.com/react/quickstart) guide or check out the demo [here](https://demo.alchemy.com/).

Alchemy helps you to replace 3rd-party pop-up wallets with native in-app auth. Drop in branded sign-in modals for email, passkeys, and social logins with plug-n-play components.

To get started, sign up for an [Alchemy account](https://dashboard.alchemy.com/accounts?utm_source=chain_partner\&utm_medium=referral\&utm_campaign=monad), visit the [documentation](https://accountkit.alchemy.com/), follow the [quickstart](https://accountkit.alchemy.com/react/quickstart) guide. To further streamline UX with no gas fees or signing for users, see Alchemy's [AA infra offering](/tooling-and-infra/wallet-infra/account-abstraction#alchemy) and a demo [here](https://demo.alchemy.com/).

### Coinbase Developer Platform

[Coinbase Developer Platform](https://www.coinbase.com/developer-platform/) allows developers to
build next-gen on-chain apps. CDP simplifies development by providing services for creating smart
wallets, processing payments, and integrating crypto into existing apps.

With CDP Embedded Wallets, your users can access the full power of blockchains through familiar
authentication methods like email and social logins (no seed phrases, browser extensions, or
pop-ups required).

To get started, visit the [documentation](https://docs.cdp.coinbase.com/embedded-wallets/welcome)
or follow the [quickstart](https://docs.cdp.coinbase.com/embedded-wallets/quickstart) guide.

### Crossmint

[Crossmint](https://www.crossmint.com/) provides smart contract wallets with a modular signer architecture, abstracting away blockchain complexity so you can spin up embedded, invisible wallets for your users, high-throughput treasury wallets, and wallets for AI agents — all from a single SDK and API.

Wallets support email, Google/social, passkey, and SMS sign-in. The default device signer keeps a non-extractable P256 key inside the device's secure hardware (iOS Secure Enclave, Android Keystore, or the browser's Web Crypto API), so the private key never leaves the device.

To get started, visit the [documentation](https://docs.crossmint.com/wallets/overview) or follow the [React quickstart](https://docs.crossmint.com/wallets/quickstarts/react) guide.

### Cubist

[Cubist](https://cubist.dev/) builds [CubeSigner](https://cubist.dev/products/cubesigner-end-user-custody), hardware-backed wallet-as-a-service and embedded wallet infrastructure. Keys are generated and used inside HSM-sealed AWS Nitro Enclaves, combining cold-wallet security with hot-wallet speed — keys never leave secure hardware.

CubeSigner provides non-custodial embedded wallets with social login (Google, Apple, X, Telegram), multi-factor authentication via passkeys, YubiKeys, and authenticator apps, and programmable, policy-based signing for sessions and automation.

To get started, follow the [TypeScript SDK quickstart](https://github.com/cubist-labs/CubeSigner-TypeScript-SDK).

### Dynamic

[Dynamic](https://dynamic.xyz/) offers smart and beautiful login flows for crypto-native users, simple onboarding flows for everyone else, and powerful developer tools that go beyond authentication.

To get started, visit the [documentation](https://docs.dynamic.xyz/) or follow the [quickstart](https://docs.dynamic.xyz/docs/quickstart) guide.

### Fordefi

[Fordefi](https://fordefi.com/) is the first institutional MPC wallet and security platform built for decentralized finance (DeFi), offering MPC key management, self-serve DeFi policy controls, time-of-transaction smart contract insights, transaction simulation, and real-time risk alerts, alongside a full-stack developer suite of native APIs and SDKs.

To get started, visit the [documentation](https://docs.fordefi.com/) or follow the [quickstart](https://docs.fordefi.com/user-guide/quickstart) guide.

### MetaMask Embedded Wallet

[MetaMask Embedded Wallets](https://docs.metamask.io/embedded-wallets/) brings one-click, OAuth-based onboarding to Monad.

Users can log in with Google or Apple and get a non-custodial wallet instantly connected to the network — with no setup or seed phrase required.

Setup is entirely handled in the MetaMask Dashboard — developers just enable Monad, and it works out of the box.

Learn more at [docs.metamask.io/embedded-wallets](https://docs.metamask.io/embedded-wallets/).

To get started, visit the [Monad integration guide](https://docs.metamask.io/embedded-wallets/connect-blockchain/evm/monad).

### Para

<Info>
  Para is free for developers building on Monad Testnet!

  Sign up via the [Developer Portal](https://developer.getpara.com/) and reach out to the team via the below email.

  `ops@getpara.com`
</Info>

[Para](https://www.getpara.com/) is the easiest and most secure way to onboard all your users and support them throughout their crypto journey. We support projects throughout their growth, ranging from personal projects to many of the most trusted teams in crypto and beyond.

Para's cross-app embedded wallets work universally across apps, chains, and ecosystem, so whether users start transacting on EVM, Solana, or Cosmos, they can onboard once and transact forever, all with the same wallet.

To get started, visit the [documentation](https://docs.getpara.com/v1/introduction/welcome#welcome) or follow the [quickstart](https://docs.getpara.com/v2/introduction/welcome) guide.

### Phantom

[Phantom](https://phantom.com/) is the world's leading crypto wallet for managing digital assets and accessing decentralized applications.

Phantom embedded wallets enable seamless, seedless onboarding with in-app, non-custodial access--no app switching or seed phrases required.

To get started, visit the [documentation](https://docs.phantom.com/) or follow the [Introduction](https://docs.phantom.com/introduction) guide.

### Portal

[Portal](https://www.portalhq.io/) is a fast, flexible, and secure stablecoin finance developer platform. Create wallets, move stablecoins, and scale on-chain operations — all with simple SDKs and APIs.

To get started, visit the [documentation](https://docs.portalhq.io/) or follow the [quickstart](https://docs.portalhq.io/apis/quickstart) guide.

### Privy

<Info>
  Privy is subsidizing all Monad Testnet usage!

  For more details reach out to the Privy team via the below email.

  `monad@privy.io`
</Info>

[Privy](https://privy.io/) helps you onboard any user to crypto no matter how familiar they are with the space. Power flexible, powerful wallets under the hood for any application, securely.

To get started, visit the [documentation](https://docs.privy.io/) or follow the [quickstart](https://docs.privy.io/guide/react/quickstart) guide.

### Reown

[Reown](https://reown.com/) gives developers the tools to build user experiences that make digital ownership effortless, intuitive, and secure.

#### AppKit

AppKit is a powerful, free, and fully open-source SDK for developers looking to integrate wallet connections and other Web3 functionalities into their apps on any EVM and non-EVM chain. In just a few simple steps, you can provide your users with seamless wallet access, one-click authentication, social logins, and notifications—streamlining their experience while enabling advanced features like on-ramp functionality, in-app token swaps and smart accounts.

To get started, visit the [documentation](https://docs.reown.com/) or follow the [quickstart](https://reown.com/blog/how-to-get-started-with-reown-appkit-on-monad-testnet) guide.

### Sequence

[Sequence](https://sequence.xyz) provides the industry gold standard in robust open-source,
non-custodial [Embedded](https://docs.sequence.xyz/solutions/wallets/developers/embedded-wallet/overview)
and [Ecosystem](https://docs.sequence.xyz/solutions/wallets/developers/overview)
Wallets.Sequence is the originator of non-custodial smart contract wallets, and authors of
ERC-1271 and ERC-6492.

Embedded and Ecosystem Wallets enable seamless onboarding with user-friendly
email, social, passkey, and guest account logins. Invisible onchain transactions; secure and
compliant non-custodial sovereignty; and cross-platform integrations with SDKs for Unity, Unreal,
Web, and mobile. Fully customizable for developers and ecosystems.

To get started, visit the [Ecosystem Wallet Quickstart](https://docs.sequence.xyz/solutions/wallets/developers/overview#ecosystem-wallet-quickstarts).

### thirdweb

[thirdweb](https://thirdweb.com/) provides client-side SDKs for user onboarding, identity and transactions.

* Onboard new users to your apps with every wallet & login method
* create a complete picture of all your users via user analytics & identity linking
* facilitate onchain transactions via onramps, swaps & bridging

To get started:

1. Sign up for a [free thirdweb account](https://thirdweb.com/team)
2. Visit [Connect Documentation](https://portal.thirdweb.com/connect/sign-in/ConnectButton) and [Connect Playground](https://playground.thirdweb.com/connect/sign-in/button)

### Turnkey

<Info>
  Turnkey is free for developers building on Monad Testnet!
</Info>

[Turnkey](https://www.turnkey.com/) is secure, flexible, and scalable wallet infrastructure. Create millions of embedded wallets, eliminate manual transaction flows, and automate onchain actions - all without compromising on security.

To get started, visit the [documentation](https://docs.turnkey.com/) or follow the [quickstart](https://docs.turnkey.com/getting-started/embedded-wallet-quickstart) guide.


# Wallet Infrastructure
Source: https://docs.monad.xyz/tooling-and-infra/wallet-infra/index



## Summary

Monad features excellent support for developers looking to refine their users' experience
by utilizing modular wallet infrastructure.

These pages survey the supported infrastructure:

* [Embedded Wallets](/tooling-and-infra/wallet-infra/embedded-wallets)
* [Account Abstraction Providers](/tooling-and-infra/wallet-infra/account-abstraction)
* [Smart Account Implementations](/tooling-and-infra/wallet-infra/smart-accounts)

The landscape can be confusing, even to an experienced developer; therefore we include a
rough topology below.

## Background

Wallets allow users to store private keys and sign transactions. The basic setup involves
separation between the wallet and the application: the application presents a transaction
to the wallet for signing, and the wallet submits the transaction to the network, paying
for inclusion and execution with native tokens deducted from its balance.

However, increasingly, developers wish to customize their users' experience, for example by
sponsoring gas for their users or by allowing users to pay fees in an alternate currency. Other
developers want to embed the "wallet" into the app and give the app signing power over that
wallet, so that users don't have to sign a transaction with each action that they take.
Modular wallet infrastructure enables these and other features.

A number of providers are solving for this experience. To simplify understanding of the options,
we suggest the following two-dimensional matrix:

|                   | Freestanding                                                                                                                                                                                                                      | Embedded                                                                                                                                    |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **EOA**           | See [Simple Wallets](/tooling-and-infra/wallets)                                                                                                                                                                                  | See [Embedded Wallets](/tooling-and-infra/wallet-infra/embedded-wallets).<br />Typically utilizes key sharding, e.g. using MPC, SSS, or TEE |
| **Smart Account** | Utilizes Account Abstraction, i.e. developer needs to choose:<br /><ul><li>[AA Providers](/tooling-and-infra/wallet-infra/account-abstraction)</li><li>[Smart Accounts](/tooling-and-infra/wallet-infra/smart-accounts)</li></ul> | See [Embedded Wallets](/tooling-and-infra/wallet-infra/embedded-wallets) and look for "Embedded Smart Accounts"                             |

## EOA-based approach

**(EOA, freestanding)** is the traditional wallet experience powered by browser extension wallets,
mobile wallets, and hardware wallets. It involves a single private key stored within the wallet.
See [Wallets](/tooling-and-infra/wallets) for a survey.

**(EOA, embedded)**: typically uses cryptographic techniques (MPC, SSS, etc) to shard the
signing keys, implementing additional authorization or access control features off-chain, while
presenting to the blockchain as an ordinary EOA. See [Embedded Wallets](/tooling-and-infra/wallet-infra/embedded-wallets)
for a list of providers.

## Smart account (account abstraction) approach

Account Abstraction means using smart contracts in place of simple EOAs. The smart contract
implements the authorization / access control logic, i.e. the logic is on chain.

Historically, smart contracts could not pay for their own transaction costs (although EIP-7702
introduces an exception to this rule). Therefore, the account abstraction path requires
users to sign pseudo-transactions (UserOperations) and submit them to a custom mempool.
Then, a service called the Bundler/Relayer submits UserOperations in a normal Monad transaction
and pays for the execution.

Thus, there are at least two considerations for developers building with smart accounts:

* the Bundler/Relayer service; see [Account Abstraction Providers](/tooling-and-infra/wallet-infra/account-abstraction)
  for a list
* the [Smart Account Implementation](/tooling-and-infra/wallet-infra/smart-accounts)

Some embedded wallet providers support smart accounts. See [Embedded Wallets](/tooling-and-infra/wallet-infra/embedded-wallets)
and look out for "Embedded Smart Accounts".


# Smart Account Implementations
Source: https://docs.monad.xyz/tooling-and-infra/wallet-infra/smart-accounts



## Background

Under ERC-4337, smart wallets perform authentication (signature verification) inside of a smart
contract.  Depending on the signature scheme, signing may be done locally (on the user's computer)
or in a remote environment (e.g. TEEs).

This page lists notable smart account implementations deployed to Monad.

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Supported services</th>
            <th>How to get started</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Biconomy](https://biconomy.io)</td>
            <td>✅</td>
            <td>[Docs](https://docs.biconomy.io)</td>
            <td>[Nexus: Smartest & most gas-efficient smart account](https://docs.biconomy.io/new/learn-about-biconomy/nexus)<br />
            [External Wallets](https://docs.biconomy.io/new/quickstart/external-wallets-quickstart)<br />
            Auth: [privy](https://docs.biconomy.io/new/integration-guides/wallets-and-signers/privy), [turnkey](https://docs.biconomy.io/new/integration-guides/wallets-and-signers/turnkey); [session keys](https://docs.biconomy.io/new/smart-sessions/introduction)</td>
            <td>[Quickstart](https://docs.biconomy.io/new/getting-started/getting-started)</td>
          </tr>

          <tr>
            <td>[MetaMask Smart Accounts Kit](https://docs.metamask.io/smart-accounts-kit)</td>
            <td>✅</td>
            <td>[Embedded Smart Accounts (4337 & 7702)](https://docs.metamask.io/smart-accounts-kit#smart-account-implementation-types)<br />
            Auth: Signer agnostic, bring any signer<br />
            Features: WebAuthn, Multisig, [ERC-7710 delegations support](https://eips.ethereum.org/EIPS/eip-7710)</td>

            <td />

            <td>[Quickstart](https://docs.metamask.io/smart-accounts-kit/get-started/smart-account-quickstart/)</td>
          </tr>

          <tr>
            <td>[Pimlico](https://pimlico.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.pimlico.io/)</td>
            <td>[permissionless.js](https://docs.pimlico.io/permissionless), a flexible SDK for interfacing with various smart accounts, bundlers/paymasters, and signers.</td>
            <td>[Tutorial](https://docs.pimlico.io/permissionless/tutorial/tutorial-1)</td>
          </tr>

          <tr>
            <td>[ZeroDev](https://zerodev.app/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.zerodev.app/)</td>
            <td>[Smart contract accounts](https://docs.zerodev.app/sdk/core-api/create-account)<br />
            [Session keys](https://docs.zerodev.app/sdk/permissions/intro) with several options for signature schemes (ECDSA, Passkey, Multisig), policies, and actions.</td>
            <td>[Quickstart](https://docs.zerodev.app/sdk/getting-started/quickstart)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Provider</th>
            <th>Status</th>
            <th>Docs</th>
            <th>Supported services</th>
            <th>How to get started</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Biconomy](https://biconomy.io)</td>
            <td>✅</td>
            <td>[Docs](https://docs.biconomy.io)</td>
            <td>[Nexus: Smartest & most gas-efficient smart account](https://docs.biconomy.io/new/learn-about-biconomy/nexus)<br />
            [External Wallets](https://docs.biconomy.io/new/quickstart/external-wallets-quickstart)<br />
            Auth: [privy](https://docs.biconomy.io/new/integration-guides/wallets-and-signers/privy), [turnkey](https://docs.biconomy.io/new/integration-guides/wallets-and-signers/turnkey); [session keys](https://docs.biconomy.io/new/smart-sessions/introduction)</td>
            <td>[Quickstart](https://docs.biconomy.io/new/getting-started/getting-started)</td>
          </tr>

          <tr>
            <td>[MetaMask Smart Accounts Kit](https://docs.metamask.io/smart-accounts-kit)</td>
            <td>✅</td>
            <td>[Embedded Smart Accounts (4337 & 7702)](https://docs.metamask.io/smart-accounts-kit#smart-account-implementation-types)<br />
            Auth: Signer agnostic, bring any signer<br />
            Features: WebAuthn, Multisig, [ERC-7710 delegations support](https://eips.ethereum.org/EIPS/eip-7710)</td>

            <td />

            <td>[Quickstart](https://docs.metamask.io/smart-accounts-kit/get-started/smart-account-quickstart/)</td>
          </tr>

          <tr>
            <td>[Pimlico](https://pimlico.io/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.pimlico.io/)</td>
            <td>[permissionless.js](https://docs.pimlico.io/permissionless), a flexible SDK for interfacing with various smart accounts, bundlers/paymasters, and signers.</td>
            <td>[Tutorial](https://docs.pimlico.io/permissionless/tutorial/tutorial-1)</td>
          </tr>

          <tr>
            <td>[ZeroDev](https://zerodev.app/)</td>
            <td>✅</td>
            <td>[Docs](https://docs.zerodev.app/)</td>
            <td>[Smart contract accounts](https://docs.zerodev.app/sdk/core-api/create-account)<br />
            [Session keys](https://docs.zerodev.app/sdk/permissions/intro) with several options for signature schemes (ECDSA, Passkey, Multisig), policies, and actions.</td>
            <td>[Quickstart](https://docs.zerodev.app/sdk/getting-started/quickstart)</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Biconomy

[Biconomy](https://biconomy.io) is the most comprehensive smart account and execution infrastructure platform that enables seamless, user-friendly experiences across single or multiple chains. With Biconomy, developers can build superior onchain UX through gas abstraction, sessions, batching, and one-click signatures for complex actions on any number of networks.

Additionally, you can use Biconomy's [Nexus](https://docs.biconomy.io/new/learn-about-biconomy/nexus):

* Directly as a smart account with passkeys or embedded wallets
* [Directly via 7702 with embedded wallets](https://docs.biconomy.io/new/quickstart/embedded-wallets-quickstart)
* [With all EOA wallets such as Metamask, Rabby and more](https://docs.biconomy.io/new/quickstart/external-wallets-quickstart)

[Session keys](https://docs.biconomy.io/new/smart-sessions/introduction) are available for all the above methods.

To get started, visit the [documentation](https://docs.biconomy.io/).

### MetaMask Smart Accounts Kit

The [MetaMask Smart Accounts Kit](https://docs.metamask.io/smart-accounts-kit) enables developers to create and interact with MetaMask Smart Accounts, unlocking new programmable account behaviors and granular permission sharing. The toolkit allows developers to build on embedded MetaMask Smart Accounts and request Advanced Permissions ([ERC-7715](https://eips.ethereum.org/EIPS/eip-7715)) from MetaMask users.

To get started, visit the [documentation](https://docs.metamask.io/smart-accounts-kit) or follow the [quickstart](https://docs.metamask.io/smart-accounts-kit/get-started/smart-account-quickstart/) guide.

### Pimlico

[Pimlico](https://pimlico.io/) is the world's most advanced ERC-4337 account abstraction infrastructure platform. Pimlico provides a suite of tools and services to help you build, deploy, and manage smart accounts on Ethereum and other EVM-compatible chains.

To get started, visit the [documentation](https://docs.pimlico.io/) or follow the [quickstart](https://docs.pimlico.io/permissionless/tutorial/tutorial-1) guide.

### Zerodev

[ZeroDev](https://zerodev.app) is the most powerful smart account development platform. With ZeroDev, you can build Web3 experiences without gas, confirmations, seed phrases, and bridging.

To get started, visit the [documentation](https://docs.zerodev.app/) or follow the [quickstart](https://docs.zerodev.app/sdk/getting-started/quickstart) guide.


# Hardware Wallets
Source: https://docs.monad.xyz/tooling-and-infra/wallets/hardware-wallets



## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Wallet</th>
            <th>Status</th>
            <th>Other Features</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Ledger](https://www.ledger.com)</td>
            <td>✅</td>

            <td />
          </tr>

          <tr>
            <td>[Safepal](https://www.safepal.com)</td>
            <td>✅</td>
            <td>Support for multiple cryptocurrencies, Secure element chip</td>
          </tr>

          <tr>
            <td>[Tangem](https://tangem.com/en/)</td>
            <td>✅</td>
            <td>Card-shaped, self-custodial hardware wallet designed for secure, offline storage of cryptocurrencies.</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Wallet</th>
            <th>Status</th>
            <th>Other Features</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[D'Cent Wallet](https://dcentwallet.com)</td>
            <td>✅</td>
            <td>Biometric authentication, Bluetooth connectivity</td>
          </tr>

          <tr>
            <td>[Ledger](https://www.ledger.com)</td>
            <td>❌</td>

            <td />
          </tr>

          <tr>
            <td>[Safepal](https://www.safepal.com)</td>
            <td>✅</td>
            <td>Support for multiple cryptocurrencies, Secure element chip</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### D'Cent Wallet

[D'Cent Wallet](https://dcentwallet.com) is a hardware wallet featuring biometric authentication for enhanced security. It uses a secure chip to protect private keys and offers Bluetooth connectivity for convenient mobile device pairing. D'Cent provides a balance of security and usability with its fingerprint recognition technology and support for multiple cryptocurrencies.

To get started, learn more about D'Cent Wallet [here](https://store.dcentwallet.com/) or visit the [user guide](https://userguide.dcentwallet.com/).

### Ledger

Ledger is a leading company in cryptocurrency security, best known for its hardware wallets that
keep digital assets safe through offline (cold) storage. These wallets use a secure element chip
and custom operating system to protect private keys, while requiring users to confirm transactions
directly on the device for added safety.

Learn more about Ledger [here](https://www.ledger.com/).

### Safepal

[Safepal](https://www.safepal.com) offers hardware wallet solutions that combine security with user-friendly features. Their hardware wallets utilize secure element chips to protect private keys and support a wide range of cryptocurrencies. Safepal hardware wallets are designed to be affordable while maintaining high security standards, making them accessible to both new and experienced crypto users.

To get started, learn more about Safepal hardware wallets [here](https://www.safepal.com/s1) or visit the [documentation](https://docs.safepal.io).

### Tangem

[Tangem Wallet](https://tangem.com/en/) is a card-shaped, self-custodial hardware wallet designed for secure, offline storage of cryptocurrencies. It is roughly the size of a standard credit card and uses NFC (Near Field Communication) to connect to a smartphone.


# Wallets
Source: https://docs.monad.xyz/tooling-and-infra/wallets/index



<CardGroup>
  <Card title="Software Wallets" href="/tooling-and-infra/wallets/software-wallets">
    Browser extension wallets and mobile wallets
  </Card>

  <Card title="Hardware Wallets" href="/tooling-and-infra/wallets/hardware-wallets">
    Offline wallets
  </Card>

  <Card title="Institutional Wallets" href="/tooling-and-infra/wallets/institutional-wallets" />

  <Card title="Multisig Wallets" href="/tooling-and-infra/wallets/multisig-wallets" />
</CardGroup>

<br />

For developers looking for advanced functionality such as embedded wallets or account
abstraction, see [Wallet Infrastructure](/tooling-and-infra/wallet-infra).


# Institutional Wallets
Source: https://docs.monad.xyz/tooling-and-infra/wallets/institutional-wallets



<Note>
  See also [Custody](/tooling-and-infra/custody).
</Note>

## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Wallet</th>
            <th>Status</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Cubist](https://cubist.dev/products/cubesigner-self-custody)</td>
            <td>✅</td>
          </tr>

          <tr>
            <td>[Porto by Anchorage Digital](https://www.anchorage.com/platform/self-custody)</td>
            <td>✅</td>
          </tr>

          <tr>
            <td>[Utila](https://utila.io/)</td>
            <td>✅</td>
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Cubist

[Cubist](https://cubist.dev/products/cubesigner-self-custody)'s CubeSigner gives teams and protocols self-custody key management backed by FIPS-certified hardware, SSO authentication, and a programmable policy engine with role-based access control and multi-party approvals. It secures treasury, trading, payments, staking and validator, and cross-chain bridge operations across Bitcoin, Ethereum and EVM chains, Solana, and Sui — and is trusted by leading institutions.

### Porto by Anchorage Digital

[Porto](https://www.anchorage.com/platform/self-custody) by Anchorage Digital empowers institutions to confidently engage with a wide variety of DeFi protocols, execute native swaps, and deploy sophisticated on-chain strategies directly from a self-custody wallet.

### Utila

Securely build, manage, and scale digital asset operations with [Utila](https://utila.io/)'s enterprise-grade wallet platform. Trusted by leading institutions to power stablecoin payments, treasury, trading, and beyond.

To get started, visit the [documentation](https://docs.utila.io/reference/api-overview) or follow the [quickstart](https://support.utila.io/en/collections/13931663-getting-started) guide.


# Multisig Wallets
Source: https://docs.monad.xyz/tooling-and-infra/wallets/multisig-wallets



## Provider Summary

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Wallet</th>
            <th>Status</th>
            <th>Contract addresses</th>
            <th>Other Features</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Safe](https://safe.global/wallet)</td>
            <td>✅</td>
            <td>See [contract addresses](https://github.com/monad-crypto/protocols/blob/main/mainnet/safe.jsonc)</td>

            <td />
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Wallet</th>
            <th>Status</th>
            <th>Other Features</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Safe](https://safe.global/wallet)</td>
            <td>✅</td>

            <td />
          </tr>
        </tbody>
      </table>
    </div>

    *✅ = supported, ⌛️ = in progress, ❓ = unknown, ❌ = won't support*
  </Tab>
</Tabs>

## Provider Details

### Safe Wallet

[Safe Wallet](https://safe.global/wallet) is a secure, non-custodial cryptocurrency wallet that
allows users to manage, store, and interact with digital assets like tokens and NFTs. It is built
on the Safe (formerly Gnosis Safe) smart contract infrastructure, offering advanced features like
multisig control, transaction batching, and custom permissions. Designed for both individuals and
organizations, Safe Wallet emphasizes security, transparency, and decentralized asset management.

Access Safe Wallet [here](https://safe.global/wallet).

<Tip>
  [safe-tx-hashes-util](https://github.com/pcaversaccio/safe-tx-hashes-util) is a tool for
  independently computing Safe transaction hashes based on transaction details from the
  Safe transaction service UI.

  [safe-tx-hashes-util](https://github.com/pcaversaccio/safe-tx-hashes-util) supports Monad.
</Tip>


# Software Wallets
Source: https://docs.monad.xyz/tooling-and-infra/wallets/software-wallets



## Provider Summary

Monad is supported on most EVM-compatible wallets, including the below. To add Monad to an EVM-compatible wallet, use the wallet's network selector, or use [this tool](/guides/add-monad-to-wallet/mainnet).

<Tabs>
  <Tab title="Mainnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Wallet</th>
            <th>Status</th>
            <th>Available on</th>
            <th>Autodetect Tokens and NFTs</th>
            <th>Other Features</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Ambire Wallet](https://www.ambire.com)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens</td>
            <td>Smart accounts (EIP-7702), Open source, Gas Tank, DApp connectivity</td>
          </tr>

          <tr>
            <td>[Backpack](https://backpack.app)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens, NFTs</td>
            <td>DApp browser, Built-in exchange, Futures trading, Portfolio tracking</td>
          </tr>

          <tr>
            <td>[Binance Wallet](https://www.binance.com/en/web3wallet)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens, NFTs</td>
            <td>DApp browser, Token swaps, Multi-chain support, Binance exchange integration</td>
          </tr>

          <tr>
            <td>[Bitget Wallet](https://web3.bitget.com/en?source=bitget)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>❌</td>
            <td>DApp browser, NFT Market, DApp Browser, and Launchpad</td>
          </tr>

          <tr>
            <td>[Coin98 Wallet](https://coin98.com)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>Multi-chain support, DApp browser, Cross-chain swaps, NFT Gallery</td>
          </tr>

          <tr>
            <td>[Exodus](https://www.exodus.com)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens, NFTs</td>
            <td>Token swaps, Staking, Portfolio tracking, NFT support, Buy crypto</td>
          </tr>

          <tr>
            <td>[HaHa](https://www.haha.me)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>DeFi integrations, AA, Monad Native, trading, hardware wallet support</td>
          </tr>

          <tr>
            <td>[imToken](https://token.im)</td>
            <td>✅</td>
            <td>Mobile</td>
            <td>Tokens</td>
            <td>Multi-chain support, DApp browser, Token swaps, Staking</td>
          </tr>

          <tr>
            <td>[Keplr](https://www.keplr.app)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>❌</td>
            <td>Multi-chain support, Open source, Portfolio tracking, Transaction History, In-app browser</td>
          </tr>

          <tr>
            <td>[MetaMask](https://metamask.io)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>NFTs</td>
            <td>NFT support, DApp browser, Open source, Token swaps, portfolio tracking</td>
          </tr>

          <tr>
            <td>[OKX Wallet](https://web3.okx.com/)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>DApp browser, Portfolio tracking, Cross-chain swaps, Biometric Login</td>
          </tr>

          <tr>
            <td>[Rabby Wallet](https://rabby.io/)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>Portfolio tracking, Biometric login</td>
          </tr>

          <tr>
            <td>[Safepal](https://www.safepal.com)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>NFT support, DApp browser, Token swaps, Hardware wallet support</td>
          </tr>

          <tr>
            <td>[Trust Wallet](https://trustwallet.com)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens, NFTs</td>
            <td>Multi-chain support, NFT support, DApp browser, Token swaps, Staking, Buy crypto</td>
          </tr>

          <tr>
            <td>[Uniswap Wallet](https://wallet.uniswap.org)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens</td>
            <td>Token swaps, Built-in bridge, DApp connectivity</td>
          </tr>

          <tr>
            <td>[Zerion](https://zerion.io)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens, NFTs</td>
            <td>Portfolio tracking, DeFi, DApp browser, NFT support</td>
          </tr>
        </tbody>
      </table>
    </div>
  </Tab>

  <Tab title="Testnet">
    <div>
      <table>
        <thead>
          <tr>
            <th>Wallet</th>
            <th>Status</th>
            <th>Available on</th>
            <th>Autodetect Tokens and NFTs</th>
            <th>Other Features</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>[Backpack](https://backpack.app)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens, NFTs</td>
            <td>DApp browser, Built-in exchange, Futures trading, Portfolio tracking</td>
          </tr>

          <tr>
            <td>[Bitget Wallet](https://web3.bitget.com/en?source=bitget)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>❌</td>
            <td>DApp browser, NFT Market, DApp Browser, and Launchpad</td>
          </tr>

          <tr>
            <td>[Coin98 Wallet](https://coin98.com)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>Multi-chain support, DApp browser, Cross-chain swaps, NFT Gallery</td>
          </tr>

          <tr>
            <td>[HaHa](https://www.haha.me)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>DeFi integrations, AA, Monad Native, trading, hardware wallet support</td>
          </tr>

          <tr>
            <td>[imToken](https://token.im)</td>
            <td>✅</td>
            <td>Mobile</td>
            <td>Tokens</td>
            <td>Multi-chain support, DApp browser, Token swaps, Staking</td>
          </tr>

          <tr>
            <td>[MetaMask](https://metamask.io)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>NFTs</td>
            <td>NFT support, DApp browser, Open source, Token swaps, portfolio tracking</td>
          </tr>

          <tr>
            <td>[OKX Wallet](https://www.okx.com/en-us/help/section/faq-web3-wallet)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>DApp browser, Portfolio tracking, Cross-chain swaps, Biometric Login</td>
          </tr>

          <tr>
            <td>[Rabby Wallet](https://rabby.io/)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>Portfolio tracking, Biometric login</td>
          </tr>

          <tr>
            <td>[Safepal](https://www.safepal.com)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>✅</td>
            <td>NFT support, DApp browser, Token swaps, Hardware wallet support</td>
          </tr>

          <tr>
            <td>[Trust Wallet](https://trustwallet.com)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens, NFTs</td>
            <td>Multi-chain support, NFT support, DApp browser, Token swaps, Staking, Buy crypto</td>
          </tr>

          <tr>
            <td>[Uniswap Wallet](https://wallet.uniswap.org)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens</td>
            <td>Token swaps, Built-in bridge, DApp connectivity</td>
          </tr>

          <tr>
            <td>[Zerion](https://zerion.io)</td>
            <td>✅</td>
            <td>Desktop, Mobile</td>
            <td>Tokens, NFTs</td>
            <td>Portfolio tracking, DeFi, DApp browser, NFT support</td>
          </tr>
        </tbody>
      </table>
    </div>
  </Tab>
</Tabs>

## Provider Details

### Ambire Wallet

[Ambire Wallet](https://www.ambire.com) is an open-source, self-custodial wallet with smart-account features via EIP-7702, supporting EOAs, smart accounts, and hardware wallets across many EVM networks. It includes a Gas Tank and built-in DApp connectivity.

To get started, get Ambire Wallet [here](https://www.ambire.com) or visit the [documentation](https://help.ambire.com).

### Backpack

[Backpack](https://backpack.app) is a next-level wallet and exchange. Buy tokens, trade futures, and explore on-chain apps—seamlessly and securely. 🎒

To get started, download the Backpack wallet [here](https://backpack.app) or visit the [documentation](https://docs.backpack.app/).

### Binance Wallet

[Binance Wallet](https://www.binance.com/en/web3wallet) is a self-custodial Web3 wallet built into the Binance app and browser extension. It uses keyless (MPC) security and lets users hold assets, swap tokens, and explore DApps across multiple chains, with easy transfers to and from the Binance exchange.

To get started, get the Binance Wallet [here](https://www.binance.com/en/web3wallet).

### Bitget Wallet

[Bitget Wallet](https://web3.bitget.com/en?source=bitget) is a non-custodial wallet with advanced multi-chain capabilities and powerful swap function

To get started, download the Bitget wallet [here](https://web3.bitget.com/en/wallet-download?type=2) or visit the [documentation](https://web3.bitget.com/en/docs/).

### Coin98 Wallet

[Coin98 Wallet](https://coin98.com) is a multi-chain wallet that connects users to numerous blockchains, allowing for seamless asset management and DeFi interactions. It features cross-chain swaps, an integrated DApp browser, and comprehensive portfolio tracking across multiple networks.

To get started, download Coin98 Wallet [here](https://coin98.com/wallet) or visit the [documentation](https://docs.coin98.com).

### Exodus

[Exodus](https://www.exodus.com) is a multi-asset, self-custodial wallet available on desktop, mobile, and as a browser extension. It supports thousands of assets across many networks, with built-in swaps, staking, and NFT support.

To get started, download Exodus [here](https://www.exodus.com/download) or visit the [documentation](https://www.exodus.com/support).

### HaHa Wallet

[HaHa](https://www.haha.me) is a next-gen smart wallet with DeFi capabilities.

To get started, download the HaHa wallet [here](https://www.haha.me).

### imToken

[imToken](https://token.im) is a widely used multi-chain, self-custodial wallet with native Monad support alongside many other networks. It offers asset management, a built-in DApp browser, token swaps, and staking.

To get started, download imToken [here](https://token.im) or visit the [documentation](https://support.token.im).

### Keplr Wallet

[Keplr Wallet](https://www.keplr.app/) is an open-source, multichain wallet supporting Cosmos, Bitcoin, Ethereum, Starknet, and more.

Download Keplr [here](https://www.keplr.app/get) or visit the [documentation](https://docs.keplr.app/api/intro).

### MetaMask

[MetaMask](https://metamask.io) is a secure and easy-to-use wallet with native support for Monad, letting you swap and bridge on Monad directly in the wallet.

To get started, download the MetaMask wallet [here](https://metamask.io/download) or visit the [documentation](https://docs.metamask.io).

### OKX Wallet

[OKX Wallet](https://www.okx.com/en-us/help/section/faq-web3-wallet) is your all-in-one gateway to the Web3 world.

To get started, download the OKX Wallet [here](https://chromewebstore.google.com/detail/okx-wallet/mcohilncbfahbmgdjkbpemcciiolgcge) or visit the [documentation](https://www.okx.com/web3/build/docs/sdks/okx-wallet-integration-introduction).

### Rabby Wallet

[Rabby Wallet](https://rabby.io/) is a non-custodial, multi-chain Web3 wallet created by DeBank that makes using decentralized apps easier and safer. It supports Monad and many other blockchains, automatically detects networks, and shows transaction simulations with risk alerts to help prevent mistakes or scams. Users keep full control of their keys.

Download Rabby wallet and learn more about it [here](https://rabby.io/).

### Safepal

[Safepal](https://www.safepal.com) is a cryptocurrency wallet that offers both software and hardware wallet solutions. It provides secure storage for digital assets with features like token swaps, NFT management, and DApp browsing. Safepal emphasizes security while maintaining user-friendly access to DeFi and Web3 applications.

To get started, download the Safepal wallet [here](https://www.safepal.com/download) or visit the [documentation](https://docs.safepal.io).

### Trust Wallet

[Trust Wallet](https://trustwallet.com) is a popular multi-chain cryptocurrency wallet that supports millions of assets and blockchains. It provides a secure, decentralized platform for storing, sending, and receiving cryptocurrencies, with built-in features for staking, NFT management, and accessing DApps.

To get started, download Trust Wallet [here](https://trustwallet.com/download) or visit the [documentation](https://developer.trustwallet.com).

### Uniswap Wallet

[Uniswap Wallet](https://wallet.uniswap.org) is the self-custodial wallet from Uniswap, available on mobile and as a browser extension, with built-in token swapping and bridging across supported networks including Monad.

To get started, get the Uniswap Wallet [here](https://wallet.uniswap.org).

### Zerion

[Zerion](https://zerion.io) is a self-custodial wallet and DeFi portfolio manager supporting Monad and many other networks, with full portfolio tracking, swaps, and DApp access.

To get started, download Zerion [here](https://zerion.io) or visit the [documentation](https://help.zerion.io).


