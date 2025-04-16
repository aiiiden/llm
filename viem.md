<page>
  <title>Viem · TypeScript Interface for Ethereum</title>
  <url>https://viem.sh/</url>
  <content>Build reliable apps & libraries with lightweight, composable, and type-safe modules that interface with Ethereum

    // 1. Import modules.
    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    // 2. Set up your client with desired chain & transport.
    const client = createPublicClient({
      chain: mainnet,
      transport: http(),
    })
     
    // 3. Consume an action!
    const blockNumber = await client.getBlockNumber()

viem supports all these features out-of-the-box:

*   Abstractions over the [JSON-RPC API](https://ethereum.org/en/developers/docs/apis/json-rpc/) to make your life easier
*   First-class APIs for interacting with [Smart Contracts](https://ethereum.org/en/glossary/#smart-contract)
*   Language closely aligned to official [Ethereum terminology](https://ethereum.org/en/glossary/)
*   Import your Browser Extension, WalletConnect or Private Key Wallet
*   Browser native [BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt), instead of large BigNumber libraries
*   Utilities for working with [ABIs](https://ethereum.org/en/glossary/#abi) (encoding/decoding/inspection)
*   TypeScript ready ([infer types](https://viem.sh/docs/typescript) from ABIs and EIP-712 Typed Data)
*   First-class support for [Anvil](https://book.getfoundry.sh/), [Hardhat](https://hardhat.org/) & [Ganache](https://trufflesuite.com/ganache/)
*   Test suite running against [forked](https://ethereum.org/en/glossary/#fork) Ethereum network

Check out the following places for more wagmi-related content:

*   Follow [@wevm\_dev](https://twitter.com/wevm_dev), [@\_jxom](https://twitter.com/_jxom), and [@awkweb](https://twitter.com/awkweb) on Twitter for project updates
*   Join the [discussions on GitHub](https://github.com/wevm/viem/discussions)
*   [Share your project/organization](https://github.com/wevm/viem/discussions/104) that uses viem

Help support future development and make wagmi a sustainable open-source project:

*   [GitHub Sponsors](https://github.com/sponsors/wevm?metadata_campaign=docs_support)
*   [Gitcoin Grant](https://wagmi.sh/gitcoin)
*   [wevm.eth](https://etherscan.io/enslookup-search?search=wevm.eth)</content>
</page>

<page>
  <title>Why Viem</title>
  <url>https://viem.sh/docs/introduction</url>
  <content>The Problems
------------

The current state of low-level Ethereum interface abstractions lack in at least one of the following four areas: **developer experience**, **stability**, **bundle size** and/or **performance** — a quadrilemma.

As the authors of [wagmi](https://wagmi.sh/), a popular React Hooks library for Ethereum, we struggled to work with the existing low-level TypeScript Ethereum libraries. We wanted to provide the users of wagmi with the best possible developer experience, but we were limited by the underlying technologies wagmi was built on. We knew an _always_ stable, predictable implementation with a tiny bundle size and performant modules was paramount to interacting with the world's largest blockchain ecosystem.

So we created **viem**: a TypeScript Interface for Ethereum that provides low-level stateless primitives for interacting with Ethereum. An alternative to ethers.js and web3.js with a focus on reliability, efficiency, and excellent developer experience.

Developer Experience
--------------------

viem delivers a great developer experience through modular and composable APIs, comprehensive documentation, and automatic type safety and inference.

It provides developers with intuitive building blocks to build their Ethereum apps and libraries. While viem's APIs may be more verbose than alternative libraries, we believe this is the right trade-off as it makes viem's modular building blocks extremely flexible. Easy to move around, change, and remove. It also allows the developers to better understand Ethereum concepts as well as understand _what_ and _why_ certain properties are being passed through. Learning how to use viem is a great way to learn how to interact with Ethereum in general.

We aim to provide extensive API documentation and usage for _every_ module in viem. viem uses a [documentation](https://gist.github.com/zsup/9434452) and [test driven](https://en.wikipedia.org/wiki/Test-driven_development#:~:text=Test%2Ddriven%20development%20\(TDD\),software%20against%20all%20test%20cases.) development approach to building modules, which leads to predictable and stable APIs.

viem also provides consumers with [strongly typed APIs](https://viem.sh/docs/typescript), allowing consumers to get the best possible experience through [autocomplete](https://twitter.com/awkweb/status/1555678944770367493), [type inference](https://twitter.com/_jxom/status/1570244174502588417?s=20), as well as static validation.

Stability
---------

Stability is a fundamental principle for viem. As the authors of [wagmi](https://wagmi.sh/), we have many organizations, large and small, that rely heavily on the library and expect it to be entirely stable for their users.

viem takes the following steps to ensure stability:

*   We run our test suite against a forked Ethereum node
*   We aim for complete test coverage and test all potential behavioral cases
*   We build deterministic and pure APIs

Bundle Size
-----------

Maintaining a low bundle size is critical when building web applications. End users should not be required to download a module of over 100kB in order to interact with Ethereum. On a slow 3G mobile network loading a 100kB library would take at least **two seconds** (plus additional time to establish an HTTP connection).

Furthermore, viem is tree-shakable, meaning only the modules you use are included in your final bundle.

Performance
-----------

In addition to the fast load times mentioned above, viem further tunes performance by only executing heavy asynchronous tasks when required and optimized encoding/parsing algorithms. The benchmarks speak for themselves:

Opinions & Escape Hatches
-------------------------

Unlike other low-level interfaces that impose opinions on consumers, viem enables consumers to choose their opinions while still maintaining sensible and secure defaults. This allows consumers to create their own opinionated implementations, such as [wagmi](https://wagmi.sh/), without the need for tedious workarounds.

* * *

**viem** will help developers build with a higher level of accuracy and correctness through type safety and developer experience. It will also integrate extremely well with [wagmi](https://wagmi.sh/) so folks can start using it without much upfront switching cost.</content>
</page>

<page>
  <title>TypeScript</title>
  <url>https://viem.sh/docs/typescript</url>
  <content>viem is designed to be as type-safe as possible! Things to keep in mind:

*   Types currently require using TypeScript v5.0.4 or greater.
*   Changes to types in this repository are considered non-breaking and are usually released as patch semver changes (otherwise every type enhancement would be a major version!).
*   It is highly recommended that you lock your `viem` package version to a specific patch release and upgrade with the expectation that types may be fixed or upgraded between any release.
*   The non-type-related public API of `viem` still follows semver very strictly.

To ensure everything works correctly, make sure that your `tsconfig.json` has [`strict`](https://www.typescriptlang.org/tsconfig#strict) mode set to `true`:

    {
      "compilerOptions": {
        "strict": true
      }
    }

Type Inference
--------------

viem can infer types based on [ABI](https://docs.soliditylang.org/en/v0.8.24/abi-spec.html#json) and [EIP-712](https://eips.ethereum.org/EIPS/eip-712) Typed Data definitions (powered by [ABIType](https://abitype.dev/)), giving you full end-to-end type-safety from your contracts to your frontend and incredible developer experience (e.g. autocomplete ABI function names and catch misspellings, strongly-typed ABI function arguments, etc.).

For this to work, you must either add [const assertions](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4#const-assertions) to specific configuration parameters (more info on those below) or **define them inline**. For example, [`readContract`](https://viem.sh/docs/contract/readContract)'s `abi` configuration parameter:

    const abi = [{ 
      type: 'function', 
      name: 'balanceOf', 
      stateMutability: 'view', 
      inputs: [{ type: 'address' }], 
      outputs: [{ type: 'uint256' }], 
    }] as const
          ↑ const assertion const result = client.readContract({
      address: '0x27a69ffba1e939ddcfecc8c7e0f967b872bac65c',
      abi, 
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']
    })

      ↓ defined inlineconst result = client.readContract({  address: '0x27a69ffba1e939ddcfecc8c7e0f967b872bac65c',
      abi: [{ 
        type: 'function', 
        name: 'balanceOf', 
        stateMutability: 'view', 
        inputs: [{ type: 'address' }], 
        outputs: [{ type: 'uint256' }], 
      }], 
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']
    })

If type inference isn't working, it's likely you forgot to add a `const` assertion or define the configuration parameter inline.

### Contract ABIs

The following actions and utilities support type inference when you add a const assertion to `abi` or define `abi` inline:

#### Actions

*   [`createEventFilter`](https://viem.sh/docs/actions/public/createEventFilter)
*   [`watchEvent`](https://viem.sh/docs/actions/public/watchEvent)
*   [`createContractEventFilter`](https://viem.sh/docs/contract/createContractEventFilter)
*   [`deployContract`](https://viem.sh/docs/contract/deployContract)
*   [`estimateContractGas`](https://viem.sh/docs/contract/estimateContractGas)
*   [`multicall`](https://viem.sh/docs/contract/multicall)
*   [`readContract`](https://viem.sh/docs/contract/readContract)
*   [`simulateContract`](https://viem.sh/docs/contract/simulateContract)
*   [`writeContract`](https://viem.sh/docs/contract/writeContract)
*   [`watchContractEvent`](https://viem.sh/docs/contract/watchContractEvent)

#### Utilities

*   [`decodeEventLog`](https://viem.sh/docs/contract/decodeEventLog)
*   [`decodeFunctionResult`](https://viem.sh/docs/contract/decodeFunctionResult)
*   [`encodeDeployData`](https://viem.sh/docs/contract/encodeDeployData)
*   [`encodeErrorResult`](https://viem.sh/docs/contract/encodeErrorResult)
*   [`encodeEventTopics`](https://viem.sh/docs/contract/encodeEventTopics)
*   [`encodeFunctionData`](https://viem.sh/docs/contract/encodeFunctionData)
*   [`encodeFunctionResult`](https://viem.sh/docs/contract/encodeFunctionResult)
*   [`getAbiItem`](https://viem.sh/docs/abi/getAbiItem)

For example, `readContract`:

    const result = await client.readContract({
     
     
      address: '0xecb504d39723b0be0e3a9aa33d646642d1051ee1',
      abi: erc20Abi,
      functionName: 'balanceOf',
      
      
     
      // ↑ Notice how "transfer" is not included since it is not a "read" function
     
      args: ['0x27a69ffba1e939ddcfecc8c7e0f967b872bac65c'],
    })

### EIP-712 Typed Data

Adding a const assertion to `types` or defining `types` inline adds type inference to [`signTypedData`](https://viem.sh/docs/actions/wallet/signTypedData)'s `value` configuration parameter:

    const result = client.signTypedData({
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
     
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
     
      primaryType: 'Mail',
     
      message: {
     
     
     
     
     
     
     
     
     
     
     
     
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### Other

The following utilities support type inference when you use const assertions or define arguments inline:

*   [`decodeAbiParameters`](https://viem.sh/docs/abi/decodeAbiParameters)
*   [`encodeAbiParameters`](https://viem.sh/docs/abi/encodeAbiParameters)
*   [`encodePacked`](https://viem.sh/docs/abi/encodePacked)
*   [`parseAbi`](https://viem.sh/docs/abi/parseAbi)
*   [`parseAbiItem`](https://viem.sh/docs/abi/parseAbiItem)
*   [`parseAbiParameter`](https://viem.sh/docs/abi/parseAbiParameter)
*   [`parseAbiParameters`](https://viem.sh/docs/abi/parseAbiParameters)

Configuring Internal Types
--------------------------

For advanced use-cases, you may want to configure viem's internal types. Most of viem's types relating to ABIs and EIP-712 Typed Data are powered by [ABIType](https://abitype.dev/). See ABIType's [documentation](https://abitype.dev/config) for more info on how to configure types.

`window` Polyfill
-----------------

By importing the `viem/window` Polyfill, the global `window.ethereum` will typed as an [`EIP1193Provider`](https://github.com/wagmi-dev/viem/blob/4bdbf15be0d61b52a195e11c97201e707fb616cc/src/types/eip1193.ts#L24-L26) (including a fully-typed `request` function & typed events).

    import 'viem/window';
     
    const hash = await window.ethereum.request({
      method: 'eeth_blobBaseFeeeth_blockNumbereth_chainIdeth_coinbaseeth_gasPriceeth_maxPriorityFeePerGaseth_newBlockFiltereth_newPendingTransactionFiltereth_protocolVersioneth_accountseth_requestAccountseth_syncingeth_supportedEntryPoints 
    })
     
     
     
     
     
     
     
     
    const hash = await window.ethereum.request({
      method: 'eth_getTransactionByHash',
      params: [
    })</content>
</page>

<page>
  <title>Platform Compatibility</title>
  <url>https://viem.sh/docs/compatibility</url>
  <content>Platforms compatible with Viem

**Viem supports all modern browsers (Chrome, Edge, Firefox, etc) & runtime environments (Node 18+, Deno, Bun, etc).**

Viem uses modern EcmaScript features such as:

*   [`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)
*   [`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
*   Error [`cause`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error/cause)
*   TextEncoder [`encode`](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder/encode)

You can check support for these features on [Can I use...](https://caniuse.com/)

Polyfills
---------

If your platform does not support one of the required features, it is also possible to import a polyfill.

### `fetch`

*   [isomorphic-unfetch](https://github.com/developit/unfetch/tree/main/packages/isomorphic-unfetch)
*   [node-fetch](https://github.com/node-fetch/node-fetch#providing-global-access)

### Error `cause`

*   [core-js](https://github.com/zloirock/core-js)

### `TextEncoder`

*   [FastestSmallestTextEncoderDecoder](https://github.com/anonyco/FastestSmallestTextEncoderDecoder)</content>
</page>

<page>
  <title>Error Handling</title>
  <url>https://viem.sh/docs/error-handling</url>
  <content>    import { type GetBlockNumberErrorType } from 'viem'
    import { client } from './client'
     
    try {
      const blockNumber = await client.getBlockNumber()
    } catch (e) {
      const error = e as GetBlockNumberErrorType
      error.name: "Error" | "ChainDisconnectedError" | "HttpRequestError" | "InternalRpcError" | "InvalidInputRpcError" | "InvalidParamsRpcError" | "InvalidRequestRpcError" | "JsonRpcVersionUnsupportedError" | ... 16 more ... | "WebSocketRequestError"name 
     
     
     
     
     
     
      if (error.name === 'InternalRpcError')
        error.code: -32603code
     
     
      if (error.name === 'HttpRequestError') {
        error.HttpRequestError.headers?: Headers | undefinedheaders
     
     
        error.HttpRequestError.status?: number | undefinedstatus
      }
    }</content>
</page>

<page>
  <title>Introduction to Clients & Transports</title>
  <url>https://viem.sh/docs/clients/intro</url>
  <content>A **Client** provides access to a subset of **Actions**.

> A **Client** in the context of viem is similar to an [Ethers.js Provider](https://docs.ethers.org/v5/api/providers/).

There are three types of **Clients** in viem:

*   A [Public Client](https://viem.sh/docs/clients/public) which provides access to [Public Actions](https://viem.sh/docs/actions/public/introduction), such as `getBlockNumber` and `getBalance`.
*   A [Wallet Client](https://viem.sh/docs/clients/wallet) which provides access to [Wallet Actions](https://viem.sh/docs/actions/wallet/introduction), such as `sendTransaction` and `signMessage`.
*   A [Test Client](https://viem.sh/docs/clients/test) which provides access to [Test Actions](https://viem.sh/docs/actions/test/introduction), such as `mine` and `impersonate`.

Transports
----------

A **Client** is instantiated with a **Transport**, which is the intermediary layer that is responsible for executing outgoing requests (ie. RPC requests).

There are three types of Transports in viem:

*   A [HTTP Transport](https://viem.sh/docs/clients/transports/http) that executes requests via a HTTP JSON-RPC API.
*   A [WebSocket Transport](https://viem.sh/docs/clients/transports/websocket) that executes requests via a WebSocket JSON-RPC API.
*   A [Custom Transport](https://viem.sh/docs/clients/transports/custom) that executes requests via an [EIP-1193 `request` function](https://eips.ethereum.org/EIPS/eip-1193).</content>
</page>

<page>
  <title>Installation</title>
  <url>https://viem.sh/docs/installation</url>
  <content>Install Viem via your package manager, a `<script>` tag, or build from source.

Package Manager
---------------

Install the required packages.

CDN
---

If you're not using a package manager, you can also use Viem via an ESM-compatible CDN such as [esm.sh](https://esm.sh/). Simply add a `<script type="module">` tag to the bottom of your HTML file with the following content.

    <script type="module">
      import { createClient } from 'https://esm.sh/viem'
    </script>

Using Unreleased Commits
------------------------

If you can't wait for a new release to test the latest features, you can either install from the `canary` tag (tracks the [`main`](https://github.com/wevm/viem/tree/main) branch).

Or clone the [Viem repo](https://github.com/wevm/viem) to your local machine, build, and link it yourself.

    gh repo clone wevm/viem
    cd viem
    pnpm install
    pnpm build
    pnpm link --global

Then go to the project where you are using Viem and run `pnpm link --global viem` (or the package manager that you used to link Viem globally).

Security
--------

Ethereum-related projects are often targeted in attacks to steal users' assets. Make sure you follow security best-practices for your project. Some quick things to get started.

*   Pin package versions, upgrade mindfully, and inspect lockfile changes to minimize the risk of [supply-chain attacks](https://nodejs.org/en/guides/security/#supply-chain-attacks).
*   Install the [Socket Security](https://socket.dev/) [GitHub App](https://github.com/apps/socket-security) to help detect and block supply-chain attacks.
*   Add a [Content Security Policy](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html) to defend against external scripts running in your app.</content>
</page>

<page>
  <title>Ethers v5 → viem Migration Guide</title>
  <url>https://viem.sh/docs/ethers-migration</url>
  <content>This is a long document. Feel free to use the search bar above (⌘ K) or the Table of Contents to the side. If there is an API you need which is missing or cannot find, create a [Parity Request here](https://github.com/wagmi-dev/viem/discussions/new?category=feature-request&title=Parity%20Request:).

You may notice some of the APIs in viem are a little more verbose than Ethers. We prefer boring code and we want to strongly embrace [clarity & composability](https://viem.sh/docs/introduction#developer-experience). We believe that [verbose APIs are more flexible](https://www.youtube.com/watch?v=4anAwXYqLG8&t=789s) to move, change and remove compared to code that is prematurely abstracted and hard to change.

Provider → Client
-----------------

### getDefaultProvider

#### Ethers

    import { getDefaultProvider } from 'ethers'
     
    const provider = getDefaultProvider() 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: http() 
    }) 

> We are more verbose here – we want to be explicit and clear what chain you are connecting to & what transport you are using to avoid any confusion. :)

### JsonRpcProvider

#### Ethers

This is also interchangeable with `StaticJsonRpcProvider`.

    import { providers } from 'ethers'
     
    const provider = new providers.JsonRpcProvider('https://cloudflare-eth.com') 

Custom Chain:

    import { providers } from 'ethers'
     
    const provider = new providers.JsonRpcProvider('https://250.rpc.thirdweb.com', { 
      name: 'Fantom', 
      id: 250
    }) 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: http('https://cloudflare-eth.com') 
    }) 

Custom Chain:

    import { createPublicClient, http } from 'viem'
    import { fantom } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: fantom, 
      transport: http('https://250.rpc.thirdweb.com') 
    }) 

> viem exports custom EVM chains in the `viem/chains` entrypoint.

### InfuraProvider

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.InfuraProvider('homestead', '<apiKey>') 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: http('https://mainnet.infura.io/v3/<apiKey>') 
    }) 

> viem does not have custom API Provider clients – you can just pass in their RPC URL.

### AlchemyProvider

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.AlchemyProvider('homestead', '<apiKey>') 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: http('https://eth-mainnet.g.alchemy.com/v2/<apiKey>') 
    }) 

> viem does not have custom API Provider clients – you can just pass in their RPC URL.

### CloudflareProvider

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.CloudflareProvider() 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: http('https://cloudflare-eth.com/') 
    }) 

> viem does not have custom API Provider clients – you can just pass in their RPC URL.

### PocketProvider

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.PocketProvider('homestead', '<apiKey>') 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: http('https://eth-mainnet.gateway.pokt.network/v1/lb/<apiKey>') 
    }) 

> viem does not have custom API Provider clients – you can just pass in their RPC URL.

### AnkrProvider

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.AnkrProvider('homestead', '<apiKey>') 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: http('https://rpc.ankr.com/eth/<apiKey>') 
    }) 

> viem does not have custom API Provider clients – you can just pass in their RPC URL.

### FallbackProvider

#### Ethers

    import { providers } from 'ethers'
     
    const alchemy = new providers.AlchemyProvider('homestead', '<apiKey>') 
    const infura = new providers.InfuraProvider('homestead', '<apiKey>') 
    const provider = new providers.FallbackProvider([alchemy, infura]) 

#### viem

    import { createPublicClient, http, fallback } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const alchemy = http('https://eth-mainnet.g.alchemy.com/v2/<apiKey>') 
    const infura = http('https://mainnet.infura.io/v3/<apiKey>') 
     
    const client = createPublicClient({
      chain: mainnet,
      transport: fallback([alchemy, infura]) 
    })

### IpcProvider

Coming soon.

### JsonRpcBatchProvider

Coming soon.

### Web3Provider

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.Web3Provider(window.ethereum) 

#### viem

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({ 
      chain: mainnet, 
      transport: custom(window.ethereum) 
    }) 

### WebSocketProvider

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.WebSocketProvider('wss://eth-mainnet.g.alchemy.com/v2/<apiKey>') 

#### viem

    import { createPublicClient, webSocket } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: webSocket('wss://eth-mainnet.g.alchemy.com/v2/<apiKey>') 
    }) 

Signers → Accounts
------------------

### JsonRpcSigner

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.Web3Provider(window.ethereum)
     
    const [address] = await provider.listAccounts() 
    const signer = provider.getSigner(address) 
     
    signer.sendTransaction({ ... })

#### viem

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const [account] = await window.ethereum.request({ method: 'eth_requestAccounts' }) 
     
    const client = createWalletClient({
      account, 
      chain: mainnet,
      transport: custom(window.ethereum)
    })
     
    client.sendTransaction({ ... })

> viem uses the term ["Account"](https://ethereum.org/en/developers/docs/accounts/) rather than "Signer".

### Wallet

#### Ethers

    import { providers, Wallet } from 'ethers'
     
    const provider = new providers.Web3Provider(window.ethereum)
     
    const wallet = new Wallet('0x...', provider) 
     
    wallet.sendTransaction({ ... })

#### viem

    import { createWalletClient, custom } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const account = privateKeyToAccount('0x...') 
     
    const client = createWalletClient({
      account, 
      chain: mainnet,
      transport: custom(window.ethereum)
    })
     
    client.sendTransaction({ ... })

> viem uses the term ["Account"](https://ethereum.org/en/developers/docs/accounts/) rather than "Signer".

Provider Methods
----------------

#### Ethers

    import { getDefaultProvider } from 'ethers'
     
    const provider = getDefaultProvider()
     
    provider.getBlock(...) 
    provider.getTransaction(...) 
    ...

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http()
    })
     
    client.getBlock(...) 
    client.getTransaction(...) 
    ...

> Methods that extend off the Public Client are **Public Actions**. [Read more](https://viem.sh/docs/actions/public/introduction).

> There are API differences in all of these methods. Use the search bar at the top of the page to learn more about them.

Signer Methods
--------------

### JsonRpcSigner

#### Ethers

    import { providers } from 'ethers'
     
    const provider = new providers.Web3Provider(window.ethereum)
     
    const [address] = await provider.listAccounts()
    const signer = provider.getSigner(address)
     
    signer.sendTransaction(...) 
    signer.signMessage(...) 
    ...

#### viem

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const [account] = await window.ethereum.request({ method: 'eth_requestAccounts' })
     
    const client = createWalletClient({
      account,
      chain: mainnet,
      transport: custom(window.ethereum)
    })
     
    client.sendTransaction({ ... }) 
    client.signMessage({ ... }) 
    ...

> Methods that extend off the Wallet Client are **Wallet Actions**. [Read more](https://viem.sh/docs/actions/wallet/introduction).

> There are API differences in all of these methods. Use the search bar at the top of the page to learn more about them.

Contract Interaction
--------------------

### Reading from Contracts

#### Ethers

    import { getDefaultProvider } from 'ethers'
    import { wagmiContractConfig } from './abi'
     
    const provider = getDefaultProvider()
     
    const { abi, address } = wagmiContractConfig 
    const contract = new Contract(address, abi, provider) 
    const supply = await contract.totalSupply() 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
    import { wagmiContractConfig } from './abi'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http()
    })
     
    const supply = await client.readContract({ 
      ...wagmiContractConfig, 
      functionName: 'totalSupply'
    }) 

### Writing to Contracts

#### Ethers

    import { Contract, providers } from 'ethers'
    import { wagmiContractConfig } from './abi'
     
    const provider = new providers.Web3Provider(window.ethereum)
     
    const [address] = await provider.listAccounts()
    const signer = provider.getSigner(address)
     
    const { abi, address } = wagmiContractConfig 
    const contract = new Contract(address, abi, signer) 
    const hash = await contract.mint() 

#### viem

    import { createPublicClient, createWalletClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
    import { wagmiContractConfig } from './abi'
     
    const walletClient = createWalletClient({
      chain: mainnet,
      transport: custom(window.ethereum)
    })
     
    const [address] = await walletClient.getAddresses()
     
    const hash = await walletClient.writeContract({ 
      ...wagmiContractConfig, 
      functionName: 'mint', 
      account: address, 
    }) 

### Deploying Contracts

#### Ethers

    import { ContractFactory, providers } from 'ethers'
    import { abi, bytecode } from './abi'
     
    const provider = new providers.Web3Provider(window.ethereum)
     
    const [address] = await provider.listAccounts()
    const signer = provider.getSigner(address)
     
    const contract = new ContractFactory(abi, bytecode, signer) 
    await contract.deploy() 

#### viem

    import { createWalletClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
    import { abi, bytecode } from './abi'
     
    const walletClient = createWalletClient({
      chain: mainnet,
      transport: custom(window.ethereum)
    })
     
    const [address] = await walletClient.getAddresses()
     
    await walletClient.deployContract({ 
      abi, 
      account: address, 
      bytecode, 
    }) 

### Contract Events

#### Ethers

    import { getDefaultProvider } from 'ethers'
    import { wagmiContractConfig } from './abi'
     
    const provider = getDefaultProvider()
     
    const { abi, address } = wagmiContractConfig 
    const contract = new Contract(address, abi, provider) 
     
    const listener = (from, to, amount, event) => { 
      // ... 
    } 
    contract.on('Transfer', listener) 
     
    // unsubscribe 
    contract.off('Transfer', listener) 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
    import { wagmiContractConfig } from './abi'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http()
    })
     
    const unwatch = client.watchContractEvent({ 
      ...wagmiContractConfig, 
      eventName: 'Transfer', 
      onLogs: logs => { 
        const { args: { from, to, amount }, eventName } = logs[0] 
        // ... 
      }, 
    }) 
     
    // unsubscribe 
    unwatch() 

> Note: Logs are batched between polling intervals in viem to avoid excessive callback invocations. You can disable this behavior with `batch: false` however.

### Gas Estimation

#### Ethers

    import { getDefaultProvider } from 'ethers'
    import { wagmiContractConfig } from './abi'
     
    const provider = getDefaultProvider()
     
    const { abi, address } = wagmiContractConfig 
    const contract = new Contract(address, abi, provider) 
    const gas = await contract.estimateGas.mint() 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
    import { wagmiContractConfig } from './abi'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http()
    })
     
    const gas = await client.estimateContractGas({ 
      ...wagmiContractConfig,  
      functionName: 'mint'
    }) 

### Call

#### Ethers

    import { getDefaultProvider } from 'ethers'
    import { wagmiContractConfig } from './abi'
     
    const provider = getDefaultProvider()
     
    const { abi, address } = wagmiContractConfig 
    const contract = new Contract(address, abi, provider) 
    await contract.callStatic.mint() 

#### viem

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
    import { wagmiContractConfig } from './abi'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http()
    })
     
    await client.simulateContract({ 
      ...wagmiContractConfig,  
      functionName: 'mint'
    }) 

### Contract Instances

#### Ethers

    import { getDefaultProvider } from 'ethers'
    import { wagmiContractConfig } from './abi'
     
    const provider = getDefaultProvider()
     
    const { abi, address } = wagmiContractConfig 
    const contract = new Contract(address, abi, provider) 
     
    const supply = await contract.totalSupply()
    const listener = (from, to, amount, event) => {
      // ...
    }
    contract.on('Transfer', listener)
    contract.off('Transfer', listener)

#### viem

    import { createPublicClient, http, getContract } from 'viem'
    import { mainnet } from 'viem/chains'
    import { wagmiContractConfig } from './abi'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http()
    })
     
    const contract = getContract({ 
      ...wagmiContractConfig, 
      client, 
    }) 
     
    const supply = await contract.read.totalSupply()
    const unwatch = contract.watchEvent.Transfer({
      onLogs: logs => {
        const { args: { from, to, amount }, eventName } = logs[0]
        // ...
      },
    })
    unwatch()

ABI Utilities
-------------

### abiCoder.encode

#### Ethers

    import { utils } from 'ethers'
     
    const abiCoder = utils.defaultAbiCoder()
     
    // Object
    abiCoder.encode(
      [{ type: 'uint', name: 'x' }, { type: 'string', name: 'y' }],
      [1234, 'Hello world']
    )
     
    // Human Readable
    abiCoder.encode(
      ['uint', 'string'], 
      [1234, 'Hello World']
    );

#### viem

    import { encodeAbiParameters, parseAbiParameters } from 'viem'
     
    // Object
    encodeAbiParameters(
      [{ type: 'uint', name: 'x' }, { type: 'string', name: 'y' }],
      [1234, 'Hello world']
    )
     
    // Human Readable
    encodeAbiParameters(
      parseAbiParameters('uint, string'),
      [1234, 'Hello world']
    )

### abiCoder.decode

#### Ethers

    import { utils } from 'ethers'
     
    const abiCoder = utils.defaultAbiCoder()
     
    // Object
    abiCoder.decode(
      [{ type: 'uint', name: 'x' }, { type: 'string', name: 'y' }],
      '0x00000000000000000000000000000000000000000000000000000000000004d20000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000000b48656c6c6f20576f726c64000000000000000000000000000000000000000000'
    )
     
    // Human Readable
    abiCoder.decode(
      ['uint', 'string'], 
      '0x00000000000000000000000000000000000000000000000000000000000004d20000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000000b48656c6c6f20576f726c64000000000000000000000000000000000000000000'
    );

#### viem

    import { decodeAbiParameters, parseAbiParameters } from 'viem'
     
    // Object
    decodeAbiParameters(
      [{ type: 'uint', name: 'x' }, { type: 'string', name: 'y' }],
      '0x00000000000000000000000000000000000000000000000000000000000004d20000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000000b48656c6c6f20576f726c64000000000000000000000000000000000000000000'
    )
     
    // Human Readable
    decodeAbiParameters(
      parseAbiParameters('uint, string'),
      '0x00000000000000000000000000000000000000000000000000000000000004d20000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000000b48656c6c6f20576f726c64000000000000000000000000000000000000000000'
    )

Notice: different from ethers, viem only supports [standard tuple expression](https://docs.soliditylang.org/en/latest/grammar#a4.SolidityParser.tupleExpression) for Human Readable. example: `(uint a, string b)` is valid, but `tuple(uint a, string b)` is not.

### Fragments & Interfaces

In viem, there is no concept of "fragments" & "interfaces". We want to stick as close to the wire as possible and not introduce middleware abstractions and extra layers over ABIs. Instead of working with "fragments", we encourage you to work with the ABI itself. We provide utilities such as `getAbiItem`, `parseAbi` `parseAbiItem`, `parseAbiParameters` and `parseAbiParameter` which covers the use cases of interfaces & fragments.

### Interface.format

viem only supports Human Readable → Object format.

#### Ethers

    import { utils } from 'ethers'
     
    const interface = new Interface([ 
      'constructor(string symbol, string name)', 
      'function transferFrom(address from, address to, uint amount)', 
      'function transferFrom(address from, address to, uint amount, bool x)', 
      'function mint(uint amount) payable', 
      'function balanceOf(address owner) view returns (uint)'
    ]) 
    const json = interface.format(utils.FormatTypes.json) 

#### viem

    import { parseAbi } from 'viem'
     
    const json = parseAbi([ 
      'constructor(string symbol, string name)', 
      'function transferFrom(address from, address to, uint amount)', 
      'function transferFrom(address from, address to, uint amount, bool x)', 
      'function mint(uint amount) payable', 
      'function balanceOf(address owner) view returns (uint)', 
      'event Transfer(address indexed from, address indexed to, uint256 amount)'
    ]) 

### Fragment.from

#### ethers

    import { utils } from 'ethers'
     
    const fragment = utils.Fragment.from('function balanceOf(address owner) view returns (uint)') 

#### viem

    import { parseAbiItem } from 'viem'
     
    const abiItem = parseAbiItem('function balanceOf(address owner) view returns (uint)') 

### ParamType.from

#### ethers

    import { utils } from 'ethers'
     
    const param = utils.ParamType.from('address owner') 

#### viem

    import { parseAbiParameter } from 'viem'
     
    const param = parseAbiParameter('address owner') 

### Fragment Access

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const interface = new utils.Interface(abi)  
    interface.getFunction('transferFrom') 
    interface.getEvent('Transfer') 

#### viem

    import { getAbiItem } from 'viem'
    import { abi } from './abi'
     
    getAbiItem({ abi, name: 'transferFrom' })  
    getAbiItem({ abi, name: 'Transfer' }) 

### Interface.encodeDeploy

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi);  
    const data = iface.encodeDeploy(['SYM', 'Some Name']) 

#### viem

    import { encodeDeployData } from 'viem'
    import { abi, bytecode } from './abi'
     
    const data = encodeDeployData({ 
      abi, 
      bytecode, 
      args: ['SYM', 'Some Name'] 
    }) 

> Note: viem concatenates the contract bytecode onto the ABI encoded data.

### Interface.encodeErrorResult

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi);  
    const data = iface.encodeErrorResult('AccountLocked', [ 
      '0x8ba1f109551bD432803012645Ac136ddd64DBA72', 
      utils.parseEther('1.0') 
    ]); 

#### viem

    import { encodeErrorResult, parseEther } from 'viem'
    import { abi } from './abi'
     
    const data = encodeErrorResult({  
      abi: wagmiAbi, 
      errorName: 'AccountLocked', 
      args: [ 
        '0x8ba1f109551bD432803012645Ac136ddd64DBA72', 
        parseEther('1.0') 
      ] 
    }) 

### Interface.encodeFilterTopics

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi);  
    const data = iface.encodeFilterTopics('Transfer', [ 
      null, 
      '0x8ba1f109551bD432803012645Ac136ddd64DBA72'
    ]) 

#### viem

    import { encodeEventTopics } from 'viem'
    import { abi } from './abi'
     
    const data = encodeEventTopics({ 
      abi, 
      eventName: 'Transfer', 
      args: { 
        to: '0x8ba1f109551bD432803012645Ac136ddd64DBA72'
      } 
    }) 

### Interface.encodeFunctionData

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi); 
    const data = iface.encodeFunctionData('transferFrom', [ 
      '0x8ba1f109551bD432803012645Ac136ddd64DBA72', 
      '0xaB7C8803962c0f2F5BBBe3FA8bf41cd82AA1923C', 
      parseEther('1.0') 
    ]) 

#### viem

    import { encodeFunctionData, parseEther } from 'viem'
    import { abi } from './abi'
     
    const data = encodeFunctionData({  
      abi, 
      functionName: 'transferFrom', 
      args: [ 
        '0x8ba1f109551bD432803012645Ac136ddd64DBA72', 
        '0xaB7C8803962c0f2F5BBBe3FA8bf41cd82AA1923C', 
        parseEther('1.0') 
      ] 
    }) 

### Interface.encodeFunctionResult

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi); 
    const data = iface.encodeFunctionResult('balanceOf', [ 
      '0x8ba1f109551bD432803012645Ac136ddd64DBA72'
    ]) 

#### viem

    import { encodeFunctionResult, parseEther } from 'viem'
    import { abi } from './abi'
     
    const data = encodeFunctionResult({  
      abi, 
      functionName: 'balanceOf', 
      value: ['0x8ba1f109551bD432803012645Ac136ddd64DBA72'] 
    }) 

### Interface.decodeErrorResult

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi); 
    const result = iface.decodeErrorResult("AccountLocked", '0xf7c3865a0000000000000000000000008ba1f109551bd432803012645ac136ddd64dba720000000000000000000000000000000000000000000000000de0b6b3a7640000') 

#### viem

    import { decodeErrorResult, parseEther } from 'viem'
    import { abi } from './abi'
     
    const result = decodeErrorResult({  
      abi, 
      data: '0xf7c3865a0000000000000000000000008ba1f109551bd432803012645ac136ddd64dba720000000000000000000000000000000000000000000000000de0b6b3a7640000'
    }) 

### Interface.decodeEventLog

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi); 
    const result = iface.decodeEventLog( 
      'Transfer', 
      data: '0x0000000000000000000000000000000000000000000000000de0b6b3a7640000', 
      topics: [ 
        '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef', 
        '0x0000000000000000000000008ba1f109551bd432803012645ac136ddd64dba72', 
        '0x000000000000000000000000ab7c8803962c0f2f5bbbe3fa8bf41cd82aa1923c'
      ] 
    ); 

#### viem

    import { decodeEventLog, parseEther } from 'viem'
    import { abi } from './abi'
     
    const result = decodeEventLog({ 
      abi, 
      data: '0x0000000000000000000000000000000000000000000000000de0b6b3a7640000', 
      topics: [ 
        '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef', 
        '0x0000000000000000000000008ba1f109551bd432803012645ac136ddd64dba72', 
        '0x000000000000000000000000ab7c8803962c0f2f5bbbe3fa8bf41cd82aa1923c'
      ] 
    }) 

### Interface.decodeFunctionData

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi); 
    const result = iface.decodeFunctionData('transferFrom', '0x23b872dd0000000000000000000000008ba1f109551bd432803012645ac136ddd64dba72000000000000000000000000ab7c8803962c0f2f5bbbe3fa8bf41cd82aa1923c0000000000000000000000000000000000000000000000000de0b6b3a7640000'); 

#### viem

    import { decodeFunctionData, parseEther } from 'viem'
    import { abi } from './abi'
     
    const result = decodeFunctionData({ 
      abi, 
      data: '0x23b872dd0000000000000000000000008ba1f109551bd432803012645ac136ddd64dba72000000000000000000000000ab7c8803962c0f2f5bbbe3fa8bf41cd82aa1923c0000000000000000000000000000000000000000000000000de0b6b3a7640000', 
    }) 

### Interface.decodeFunctionResult

#### Ethers

    import { utils } from 'ethers'
    import { abi } from './abi'
     
    const iface = new utils.Interface(abi); 
    const result = iface.decodeFunctionResult('balanceOf', '0x0000000000000000000000000000000000000000000000000de0b6b3a7640000'); 

#### viem

    import { decodeFunctionResult, parseEther } from 'viem'
    import { abi } from './abi'
     
    const result = decodeFunctionResult({ 
      abi, 
      functionName: 'balanceOf', 
      data: '0x0000000000000000000000000000000000000000000000000de0b6b3a7640000', 
    }) 

### Interface.getSighash

#### Ethers

    import { Interface, FunctionFragment } from '@ethersproject/abi';
     
    const hash = Interface.getSighash(FunctionFragment.from('function ownerOf(uint256)')); 

#### viem

    import { toFunctionHash } from 'viem'
     
    const hash = toFunctionHash('function ownerOf(uint256)') 

Address Utilities
-----------------

### getAddress

#### Ethers

    import { utils } from 'ethers'
     
    const address = utils.getAddress('0x8ba1f109551bd432803012645ac136ddd64dba72') 

#### viem

    import { getAddress } from 'viem'
     
    const address = getAddress('0x8ba1f109551bd432803012645ac136ddd64dba72') 

### isAddress

#### Ethers

    import { utils } from 'ethers'
     
    const address = utils.isAddress('0x8ba1f109551bd432803012645ac136ddd64dba72') 

#### viem

    import { isAddress } from 'viem'
     
    const address = isAddress('0x8ba1f109551bd432803012645ac136ddd64dba72') 

### getContractAddress

#### Ethers

    import { utils } from 'ethers'
     
    const address = utils.getContractAddress({ from: '0x...', nonce: 5 }); 

#### viem

    import { getContractAddress } from 'viem'
     
    const address = getContractAddress({ from: '0x...', nonce: 5 }) 

### getCreate2Address

#### Ethers

    import { utils } from 'ethers'
     
    const from = '0x8ba1f109551bD432803012645Ac136ddd64DBA72'; 
    const salt = '0x7c5ea36004851c764c44143b1dcb59679b11c9a68e5f41497f6cf3d480715331'; 
    const initCode = '0x6394198df16000526103ff60206004601c335afa6040516060f3'; 
    const initCodeHash = utils.keccak256(initCode); 
     
    const address = utils.getCreate2Address(from, salt, initCodeHash); 

#### viem

    import { getContractAddress } from 'viem'
     
    const address = getContractAddress({ 
      bytecode: '0x6394198df16000526103ff60206004601c335afa6040516060f3', 
      from: '0x8ba1f109551bD432803012645Ac136ddd64DBA72', 
      opcode: 'CREATE2', 
      salt: '0x7c5ea36004851c764c44143b1dcb59679b11c9a68e5f41497f6cf3d480715331', 
    }); 

BigNumber Utilities
-------------------

### Ethers

Many.

### viem

None. We use browser native [BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt).

Byte Manipulation Utilities
---------------------------

### isBytes

#### Ethers

    import { utils } from 'ethers'
     
    utils.isBytes(new Uint8Array([1, 69, 420])) 

#### viem

    import { isBytes } from 'viem'
     
    isBytes(new Uint8Array([1, 69, 420])) 

### isHexString

#### Ethers

    import { utils } from 'ethers'
     
    utils.isHexString('0xdeadbeef') 

#### viem

    import { isHex } from 'viem'
     
    isHex('0xdeadbeef') 

### isBytesLike

#### Ethers

    import { utils } from 'ethers'
     
    utils.isBytesLike('0xdeadbeef') 

#### viem

    import { isBytes, isHex } from 'viem'
     
    isBytes('0xdeadbeef') || isHex('0xdeadbeef') 

### arrayify

#### Ethers

    import { utils } from 'ethers'
     
    utils.arrayify('0xdeadbeef') 

#### viem

    import { toBytes } from 'viem'
     
    toBytes('0xdeadbeef') 

### hexlify

#### Ethers

    import { utils } from 'ethers'
     
    utils.hexlify(new Uint8Array([1, 69, 420])) 

#### viem

    import { toHex } from 'viem'
     
    toHex(new Uint8Array([1, 69, 420])) 

### hexValue

#### Ethers

    import { utils } from 'ethers'
     
    utils.hexValue(1) 

#### viem

    import { toHex } from 'viem'
     
    toHex(1) 

### formatBytes32String

#### Ethers

    import { utils } from 'ethers'
     
    utils.formatBytes32String('Hello world') 
    // 0x48656c6c6f20776f726c642e0000000000000000000000000000000000000000

#### viem

    import { stringToHex } from 'viem'
     
    stringToHex('Hello world', { size: 32 }) 
    // 0x48656c6c6f20776f726c642e0000000000000000000000000000000000000000

### parseBytes32String

#### Ethers

    import { utils } from 'ethers'
     
    utils.parseBytes32String('0x48656c6c6f20776f726c642e0000000000000000000000000000000000000000') 
    // "Hello world"

#### viem

    import { hexToString } from 'viem'
     
    hexToString('0x48656c6c6f20776f726c642e0000000000000000000000000000000000000000', { size: 32 }) 
    // "Hello world"

### concat

#### Ethers

    import { utils } from 'ethers'
     
    utils.concat([new Uint8Array([69]), new Uint8Array([420])]) 

#### viem

    import { concat, toBytes } from 'viem'
     
    concat([new Uint8Array([69]), new Uint8Array([420])]) 

### stripZeros

#### Ethers

    import { utils } from 'ethers'
     
    utils.stripZeros(new Uint8Array([0, 0, 0, 0, 0, 69])) 

#### viem

    import { trim } from 'viem'
     
    trim(new Uint8Array([0, 0, 0, 0, 0, 69])) 

### zeroPad

#### Ethers

    import { utils } from 'ethers'
     
    utils.zeroPad(new Uint8Array([69]), 32) 

#### viem

    import { pad } from 'viem'
     
    pad(new Uint8Array([69]), { size: 32 }) 

### hexConcat

#### Ethers

    import { utils } from 'ethers'
     
    utils.hexConcat(['0x00000069', '0x00000420']) 

#### viem

    import { concat, toBytes } from 'viem'
     
    concat(['0x00000069', '0x00000420']) 

### hexDataLength

#### Ethers

    import { utils } from 'ethers'
     
    utils.hexDataLength('0x00000069') 

#### viem

    import { size } from 'viem'
     
    size('0x00000069') 

### hexDataSlice

#### Ethers

    import { utils } from 'ethers'
     
    utils.hexDataSlice('0x00000069', 4) 

#### viem

    import { slice } from 'viem'
     
    slice('0x00000069', 4) 

### hexStripZeros

#### Ethers

    import { utils } from 'ethers'
     
    utils.hexStripZeros('0x00000069') 

#### viem

    import { trim } from 'viem'
     
    trim('0x00000069') 

### hexZeroPad

#### Ethers

    import { utils } from 'ethers'
     
    utils.hexZeroPad('0x69', 32) 

#### viem

    import { pad } from 'viem'
     
    pad('0x69', { size: 32 }) 

Display Logic & Input Utilities
-------------------------------

### formatUnits

#### Ethers

    import { utils } from 'ethers'
     
    utils.formatUnits(BigNumber.from('1000000000'), 9) 

#### viem

    import { formatUnits } from 'viem'
     
    formatUnits(1000000000n, 9) 

### formatEther

#### Ethers

    import { utils } from 'ethers'
     
    utils.formatEther(BigNumber.from('1000000000000000000')) 

#### viem

    import { formatEther } from 'viem'
     
    formatEther(1000000000000000000n) 

### parseUnits

#### Ethers

    import { utils } from 'ethers'
     
    utils.parseUnits('1.0', 18) 

#### viem

    import { parseUnits } from 'viem'
     
    parseUnits('1', 18) 

### parseEther

#### Ethers

    import { utils } from 'ethers'
     
    utils.parseEther('1.0') 

#### viem

    import { parseEther } from 'viem'
     
    parseEther('1') 

Encoding Utilities
------------------

### RLP.encode

#### Ethers

    import { utils } from 'ethers'
     
    utils.RLP.encode('0x12345678') 

#### viem

    import { toRlp } from 'viem'
     
    toRlp('0x12345678') 

### RLP.decode

#### Ethers

    import { utils } from 'ethers'
     
    utils.RLP.decode('0x8412345678') 

#### viem

    import { fromRlp } from 'viem'
     
    fromRlp('0x8412345678') 

Hashing Utilities
-----------------

### id

#### Ethers

    import { utils } from 'ethers'
     
    utils.id('function ownerOf(uint256 tokenId)') 
     
    // hash utf-8 data
    utils.id('hello world') 

#### viem

    import { toFunctionSelector, keccak256, toHex } from 'viem'
     
    toFunctionSelector('function ownerOf(uint256 tokenId)') 
     
    // hash utf-8 data
    keccak256(toHex('hello world')) 

### keccak256

#### Ethers

    import { utils } from 'ethers'
     
    utils.keccak256(utils.toUtf8Bytes('hello world')) 

#### viem

    import { keccak256, toBytes } from 'viem'
     
    keccak256(toBytes('hello world')) 

### encodeBase64/decodeBase64

viem does not provide Base64 encoding utilities.

You can use browser native [`atob`](https://developer.mozilla.org/en-US/docs/Web/API/atob) and [`btoa`](https://developer.mozilla.org/en-US/docs/Web/API/btoa) instead.

### encodeBase58/decodeBase58

viem does not provide Base58 encoding utilities.

You can use libraries such as [`base58-js`](https://www.npmjs.com/package/base58-js) or [`bs58`](https://github.com/cryptocoinjs/bs58) instead.

### namehash

#### Ethers

    import { utils } from 'ethers'
     
    utils.namehash('awkweb.eth') 

#### viem

    import { namehash } from 'viem'
     
    namehash('awkweb.eth') 

### solidityPack & solidityKeccak256

#### Ethers

    import { utils } from 'ethers'
     
    utils.solidityPack(['int16', 'uint48'], [-1, 12]) 
    utils.solidityKeccak256(['int16', 'uint48'], [-1, 12]) 

#### viem

    import { encodePacked, keccak256 } from 'viem'
     
    encodePacked(['int16', 'uint48'], [-1, 12]) 
    keccak256(encodePacked(['int16', 'uint48'], [-1, 12])) 

String Utilities
----------------

### toUtf8Bytes

#### Ethers

    import { utils } from 'ethers'
     
    utils.toUtf8Bytes('Hello World') 

#### viem

    import { stringToBytes } from 'viem'
     
    stringToBytes('Hello World') 

### toUtf8String

#### Ethers

    import { utils } from 'ethers'
     
    utils.toUtf8String(new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])) 

#### viem

    import { bytesToString } from 'viem'
     
    bytesToString(new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])) 

Transaction Utilities
---------------------

### serializeTransaction

#### Ethers

    import { utils } from 'ethers'
     
    const serialized = utils.serializeTransaction({
      chainId: 1,
      maxFeePerGas: utils.parseGwei('20'),
      maxPriorityFeePerGas: utils.parseGwei('2'),
      nonce: 69,
      to: "0x1234512345123451234512345123451234512345",
      type: 2,
      value: utils.parseEther('0.01'),
    })

#### viem

    import { serializeTransaction, parseEther, parseGwei } from 'viem'
     
    const serialized = serializeTransaction({
      chainId: 1,
      gas: 21001n,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69,
      to: "0x1234512345123451234512345123451234512345",
      value: parseEther('0.01'),
    })

### parseTransaction

#### Ethers

    import { utils } from 'ethers'
     
    const transaction = utils.parseTransaction('0x02ef0182031184773594008477359400809470997970c51812dc3a010c7d01b50e0d17dc79c8880de0b6b3a764000080c0')

#### viem

    import { parseTransaction } from 'viem'
     
    const transaction = parseTransaction('0x02ef0182031184773594008477359400809470997970c51812dc3a010c7d01b50e0d17dc79c8880de0b6b3a764000080c0')</content>
</page>

<page>
  <title>EIP-7702 Overview</title>
  <url>https://viem.sh/docs/eip7702</url>
  <content>EIP-7702 is a proposal to add a new Transaction type to allow an EOA to designate a Smart Contract as its "implementation".

The main difference between an EIP-7702 Transaction and other transactions is the inclusion of a **"authorization list"** property, a set of `(chain_id, contract_address, nonce, y_parity, r, s)` tuples that depict what Contracts should be delegated onto the Externally Owned Account.

Applications of EIP-7702 include:

*   **Batching**: allowing multiple operations from the same user in one atomic transaction. One common example is an ERC-20 approval followed by spending that approval, a common workflow in DEXes that requires two transactions today. Advanced use cases of batching occasionally involve dependencies: the output of the first operation is part of the input to the second operation.
*   **Sponsorship**: account X pays for a transaction on behalf of account Y. Account X could be paid in some other ERC-20 for this service, or it could be an application operator including the transactions of its users for free.
*   **Privilege de-escalation**: users can sign sub-keys, and give them specific permissions that are much weaker than global access to the account. For example, you could imagine a permission to spend ERC-20 tokens but not ETH, or to spend up to 1% of total balance per day, or to interact only with a specific application.

Next Steps
----------

*   [Contract Writes](https://viem.sh/docs/eip7702/contract-writes)
*   [Sending Transactions](https://viem.sh/docs/eip7702/sending-transactions)</content>
</page>

<page>
  <title>Test Client</title>
  <url>https://viem.sh/docs/clients/test</url>
  <content>A Test Client is an interface to "test" JSON-RPC API methods accessible through a local Ethereum test node such as [Anvil](https://book.getfoundry.sh/anvil/) or [Hardhat](https://hardhat.org/) such as mining blocks, impersonating accounts, setting fees, etc through [Test Actions](https://viem.sh/docs/actions/test/introduction).

The `createTestClient` function sets up a Test RPC Client with a given [Transport](https://viem.sh/docs/clients/intro).

Import
------

    import { createTestClient } from 'viem'

Usage
-----

Initialize a Client with your desired [Chain](https://viem.sh/docs/chains/introduction), [Transport](https://viem.sh/docs/clients/intro) (e.g. `http`) and [mode](https://viem.sh/docs/clients/test#mode) (e.g. `"anvil"`).

    import { createTestClient, http } from 'viem'
    import { foundry } from 'viem/chains'
     
    const client = createTestClient({
      chain: foundry,
      mode: 'anvil',
      transport: http(), 
    })

Then you can consume [Test Actions](https://viem.sh/docs/actions/test/introduction):

    const mine = await client.mine({ blocks: 1 }) 

### Extending with Public & Wallet Actions

When interacting with a Ethereum test node, you may also find yourself wanting to interact with [Public Actions](https://viem.sh/docs/actions/public/introduction) and [Wallet Actions](https://viem.sh/docs/actions/wallet/introduction) with the same `chain` and `transport`. Instead of creating three different Clients, you can instead just extend the Test Client with those actions:

    import { createTestClient, http, publicActions, walletActions } from 'viem'
    import { foundry } from 'viem/chains'
     
    const client = createTestClient({
      chain: foundry,
      mode: 'anvil',
      transport: http(), 
    })
      .extend(publicActions) 
      .extend(walletActions) 
     
    const blockNumber = await client.getBlockNumber() // Public Action
    const hash = await client.sendTransaction({ ... }) // Wallet Action
    const mine = await client.mine({ blocks: 1 }) // Test Action

Parameters
----------

### mode

*   **Type:** `"anvil" | "hardhat" | "ganache"`

Mode of the Test Client.

    const client = createTestClient({
      chain: foundry,
      mode: 'anvil', 
      transport: http(), 
    })

### transport

*   **Type:** [Transport](https://viem.sh/docs/glossary/types#transport)

[Transport](https://viem.sh/docs/clients/intro) of the Test Client.

    const client = createTestClient({
      chain: foundry,
      mode: 'anvil', 
      transport: http(),  
    })

### account (optional)

*   **Type:** `Account | Address`

The Account to use for the Client. This will be used for Actions that require an `account` as an argument.

Accepts a [JSON-RPC Account](https://viem.sh/docs/accounts/jsonRpc) or [Local Account (Private Key, etc)](https://viem.sh/docs/accounts/local/privateKeyToAccount).

    import { privateKeyToAccount } from 'viem/accounts'
     
    const client = createTestClient({
      account: privateKeyToAccount('0x...'), 
      chain: foundry,
      mode: 'anvil',
      transport: http(),
    })

### chain (optional)

*   **Type:** [Chain](https://viem.sh/docs/glossary/types#chain)

[Chain](https://viem.sh/docs/chains/introduction) of the Test Client.

    const client = createTestClient({
      chain: foundry, 
      mode: 'anvil',
      transport: http(), 
    })

### cacheTime (optional)

*   **Type:** `number`
*   **Default:** `client.pollingInterval`

Time (in ms) that cached data will remain in memory.

    const client = createTestClient({
      cacheTime: 10_000, 
      chain: foundry,
      mode: 'anvil',
      transport: http(),
    })

### name (optional)

*   **Type:** `string`
*   **Default:** `"Test Client"`

A name for the Client.

    const client = createTestClient({
      chain: foundry,
      mode: 'anvil', 
      name: 'Anvil Client',  
      transport: http(),
    })

### pollingInterval (optional)

*   **Type:** `number`
*   **Default:** `4_000`

Frequency (in ms) for polling enabled Actions.

    const client = createTestClient({
      chain: foundry,
      mode: 'anvil', 
      pollingInterval: 10_000,  
      transport: http(),
    })

### rpcSchema (optional)

*   **Type:** `RpcSchema`
*   **Default:** `TestRpcSchema`

Typed JSON-RPC schema for the client.

    import { rpcSchema } from 'viem'
     
    type CustomRpcSchema = [{ 
      Method: 'eth_wagmi', 
      Parameters: [string] 
      ReturnType: string
    }] 
     
    const client = createTestClient({
      chain: foundry,
      rpcSchema: rpcSchema<CustomRpcSchema>(), 
      transport: http()
    })
     
    const result = await client.request({ 
      method: 'eth_wa // [!code focus] 
      params: ['hello'], 
    })</content>
</page>

<page>
  <title>Blob Transactions</title>
  <url>https://viem.sh/docs/guides/blob-transactions</url>
  <content>Blob Transactions are a new type of transaction in Ethereum (introduced in [EIP-4844](https://eips.ethereum.org/EIPS/eip-4844)) that allows you to broadcast BLObs (Binary Large Objects) to the Ethereum network. Blob Transactions are like any other transaction, but with the added ability to carry a payload of Blobs. Blobs are extremely larger than regular calldata (~128kB), however unlike regular calldata, they are not accessible on the EVM. The EVM can only view the commitments of the blobs. Blobs are also transient, and only last for 4096 epochs (approx. 18 days).

To read more on Blob Transactions and EIP-4844, check out these resources:

*   [EIP-4844 Spec](https://eips.ethereum.org/EIPS/eip-4844)
*   [EIP-4844 Website](https://www.eip4844.com/#faq)
*   [EIP-4844 FAQ](https://notes.ethereum.org/@vbuterin/proto_danksharding_faq#Proto-Danksharding-FAQ)

In this guide, we will walk you through how to send your first Blob Transaction with Viem.

Set up Client
-------------

We will first set up our Viem Client.

Let's create a `client.ts` file that holds our Client.

File

client.ts" filename="client.ts

    import { createWalletClient, http } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    export const account = privateKeyToAccount('0x...')
     
    export const client = createWalletClient({
      account,
      chain: mainnet,
      transport: http()
    })

Install KZG bindings
--------------------

Next, we will need to install some KZG bindings. KZG will be used to compute the commitments of the blobs, and generate proofs from the blobs & commitments. The commitments and proofs are needed to serialize and sign the Blob Transaction before we send it off.

A couple of KZG implementations we recommend are:

*   [c-kzg](https://github.com/ethereum/c-kzg-4844): Node.js bindings to c-kzg.
*   [kzg-wasm](https://github.com/ethereumjs/kzg-wasm): WebAssembly bindings to c-kzg.

    npm i c-kzg
    # or
    npm i kzg-wasm

Set up KZG interface
--------------------

After that, we will need to hook up the KZG bindings to Viem.

Let's create a `kzg.ts` file that holds our KZG interface.

    import * as cKzg from 'c-kzg'
    import { setupKzg } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    export const kzg = setupKzg(cKzg, mainnetTrustedSetupPath)

Send Blob Transaction
---------------------

Now that we have our Client and KZG interface set up, we can send our first Blob Transaction.

For demonstration purposes, we will construct a blob with a simple string: `"hello world"`, and send it to the zero address.

    import { parseGwei, stringToHex, toBlobs } from 'viem'
    import { account, client } from './client'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: stringToHex('hello world') })
     
    const hash = await client.sendTransaction({
      blobs,
      kzg,
      maxFeePerBlobGas: parseGwei('30'),
      to: '0x0000000000000000000000000000000000000000',
    })

That's it!
----------

You've just sent your first Blob Transaction with Viem.

With the `hash` you received in Step 4, you can now track your Blob Transaction on a blob explorer like [Blobscan](https://blobscan.com/).</content>
</page>

<page>
  <title>Frequently Asked Questions</title>
  <url>https://viem.sh/docs/faq</url>
  <content>Frequently asked questions related to viem.

**TL;DR: viem tries to avoid creating unnecessary abstractions on top of existing systems.**

Feel free to add to this document if you notice frequently asked questions that are not covered here.

Why use the terms "Wallet" & "Account" instead of "Signer"
----------------------------------------------------------

viem attempts to align to the "Wallet" and "Account" [terminology on Ethereum.org](https://ethereum.org/en/glossary/). The term "Signer" was adapted from ethers.js.

Let's clear up on some terms before we dive in.

*   Wallet: An application or interface that holds Account(s).
*   Account: An object that represents an address, balance, nonce, and optional storage and code.
*   Private Key: Proves ownership of an Account, and can sign messages & transactions.

In the context of viem, a Wallet Client is an interface that can hold an Account. The Account may or may not hold a Private Key.

In viem, there are two types of Accounts:

*   Local Account: can **synchronously & directly** sign messages and transactions using its Private Key. A signature is guaranteed.
*   JSON-RPC Account: **asynchronously requests** signing of messages and transactions from the target Wallet over JSON-RPC (e.g. Browser Extension or WalletConnect). The target Wallet holds the Account & Private Key. A signature is not guaranteed (the target Wallet may not have permitted the Account, or the Wallet may have rejected the request).

We do not use the term "Signer" because there are noticeable behavioral differences between signing locally and signing over JSON-RPC.

Why are contract function `args` with fully-named inputs represented as unnamed tuple types instead of object types?
--------------------------------------------------------------------------------------------------------------------

Let's look at an example! Suppose I have the following function in my contract:

    function transferFrom(address sender, address recipient, uint256 amount) returns (bool)

All the inputs are named (`sender`, `recipient`, and `amount`) so I might be tempted to represent the parameters as the following TypeScript type:

    type Args = {
      sender: `0x${string}`;
      recipient: `0x${string}`;
      amount: bigint;
    }

This improves developer experience a bit because now I can see the names of the parameters in my editor.

    import { createWalletClient, parseAbi } from 'viem'
     
    const client = createWalletClient(…)
    client.writeContract({
      address: '0x…',
      abi: parseAbi([
        'function transferFrom(address sender, address recipient, uint256 amount) returns (bool)',
      ]),
      functionName: 'transferFrom',
      args: {
        sender: '0x…',
        recipient: '0x…',
        amount: 100n,
      },
    })

However, this only works if all the inputs are named (some compilers will strip names from inputs). If any of the inputs are unnamed, then you'll have to use a tuple instead:

    client.writeContract({
      address: '0x…',
      abi: parseAbi([
        'function transferFrom(address, address, uint256) returns (bool)',
      ]),
      functionName: 'transferFrom',
      args: ['0x…', '0x…', 100n],
    })

This can get even more complicated when a function has overloads:

    function safeTransferFrom(address, address, uint256) {}
    function safeTransferFrom(address from, address to, uint256 tokenId, bytes data) {}

In this case, the type of the overload parameters start to diverge from each other:

    type Args =
      | [`0x${string}`, `0x${string}`, bigint]
      | {
          from: `0x${string}`;
          to: `0x${string}`;
          tokenId: bigint;
          data: string;
        }

If you want to switch between the two overloads in your code, you'll need to completely change the type instead of just adding or removing a single positional argument from the end. (Objects also don't enforce type-level ordering so you can put them in whatever order you want. This would also mean that viem would also need to internally validate order during runtime, adding some extra overhead.)

    client.writeContract({
      address: '0x…',
      abi: parseAbi([
        'function safeTransferFrom(address, address, uint256)',
        'function safeTransferFrom(address from, address to, uint256 tokenId, bytes data)',
      ]),
      functionName: 'safeTransferFrom',
    - args: ['0x…', '0x…', 100n],
    + args: {
    +   from: '0x…',
    +   to: '0x…',
    +   tokenId: 100n,
    +   data: '0x…',
    + },
    })

Even though overloads are an edge case, it would be sufficiently [astonishing](https://en.wikipedia.org/wiki/Principle_of_least_astonishment) to come across this behavior. So what's the best way to represent `args`? Well, they are positional at the contract-level so it makes sense to represent them that way in viem too.

Not all is lost when it comes to developer experience though! Tuple types in TypeScript can have [names](https://www.typescriptlang.org/play?ts=4.0.2#example/named-tuples) attached to them:

    type Args = [from: `0x${string}`, to: `0x${string}`, tokenId: bigint]

These names show up in your editor so you get nice developer experience when using autocomplete, etc. Unfortunately, TypeScript doesn't support dynamic named tuples right now, but we are watching [this issue](https://github.com/microsoft/TypeScript/issues/44939) closely and once it is implemented, we will add it to viem. In the meantime, hang tight!

Why is a contract function return type returning an array instead of an object?
-------------------------------------------------------------------------------

Suppose your ABI looks like this:

    [
      {
        inputs: [],
        name: "latestRoundData",
        outputs: [
          { name: "roundId", type: "uint80" },
          { name: "answer", type: "int256" },
          { name: "startedAt", type: "uint256" },
          { name: "updatedAt", type: "uint256" },
          { name: "answeredInRound", type: "uint80" },
        ],
        stateMutability: "view",
        type: "function",
      }
    ]

You might be confused why the following does not return an object:

    import { createPublicClient, parseAbi } from 'viem'
     
    const client = createPublicClient(…)
    const res = await client.readContract({
      address: '0x…',
      abi: […], // abi from above
      functionName: 'latestRoundData',
    })
    res
    // ^? const res: [bigint, bigint, bigint, bigint, bigint]

This is expected. `"latestRoundData"` `outputs` is an array of types, so you get an array of decoded values as the return type. viem only maps explicitly typed tuples as objects

Why does viem follow this approach? Here is the contract function definition for `latestRoundData` with two different return types:

    function latestRoundData() external view
      returns (
        uint80 roundId,
        int256 answer,
        uint256 startedAt,
        uint256 updatedAt,
        uint80 answeredInRound
      );
     
    struct Data {
      uint80 roundId;
      uint256 answer;
      uint256 startedAt;
      uint256 updatedAt;
      uint80 answeredInRound
    }
     
    function latestRoundData() external view returns (Data data);

The first function returns a set of five items, so viem maps it to an array. The reason why we don't convert it to an object is because things get ambiguous when we come to decode structs. How do you determine the difference between a "return" tuple (first function) and a "struct" tuple (second function).

Another reason is that folks might expect it to be an array (because it is a set of return items). Other libraries, like ethers, mitigate this by returning a hybrid Array/Object type, but that kind of type is not serializable in JavaScript, and viem prefers to not try and "hack" JavaScript types.

Why doesn't Wallet Client support public actions?
-------------------------------------------------

Wallet Client doesn't support public actions because wallet providers (Injected `window.ethereum`, WalletConnect v2, etc.) may not provide a large majority of "node"/"public" RPC methods like `eth_call`, `eth_newFilter`, `eth_getLogs`, etc. This is because these methods are not required for a wallet provider to function properly. For example, a wallet provider may only support `eth_sendTransaction` and `eth_sign` and nothing else.</content>
</page>

<page>
  <title>Build your own Client</title>
  <url>https://viem.sh/docs/clients/custom</url>
  <content>You can build your own viem Client by using the `createClient` function and optionally extending (`.extend`) it – this is how viem's internal Clients ([Public](https://viem.sh/docs/clients/public), [Wallet](https://viem.sh/docs/clients/wallet), and [Test](https://viem.sh/docs/clients/test)) are built.

Building your own Client is useful if you have specific requirements for how the Client should behave, and if you want to extend that Client with custom functionality (ie. create a [geth Debug](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug) Client).

The `createClient` function sets up a base viem Client with a given [Transport](https://viem.sh/docs/clients/intro) configured with a [Chain](https://viem.sh/docs/chains/introduction). After that, you can extend the Client with custom properties (that could be Actions or other configuration).

Import
------

    import { createClient } from 'viem'

Usage
-----

Initialize a Client with your desired [Chain](https://viem.sh/docs/chains/introduction) (e.g. `mainnet`) and [Transport](https://viem.sh/docs/clients/intro) (e.g. `http`).

    import { createClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createClient({ 
      chain: mainnet,
      transport: http()
    })

Next, you can either [extend your Client with Actions or configuration](https://viem.sh/docs/clients/custom#extending-with-actions-or-configuration), or you can use it as-is for the purpose of [maximizing tree-shaking in your app](https://viem.sh/docs/clients/custom#tree-shaking).

### Extending with Actions or configuration

You can extend your Client with custom Actions or configuration by using the `.extend` function.

Below is a naive implementation of implementing a [geth Debug](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug) Client with a `traceCall` Action that uses the `debug_traceCall` RPC method.

    import { 
      createClient, 
      http,
      formatTransactionRequest,
      type CallParameters
    } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const debugClient = createClient({ 
      chain: mainnet,
      transport: http(),
    }).extend(client => ({
      // ...
      async traceCall(args: CallParameters) {
        return client.request({
          method: 'debug_traceCall',
          params: [formatTransactionRequest(args), 'latest', {}]
        })
      },
      // ...
    }))
     
    const response = await debugClient.traceCall({
      account: '0xdeadbeef29292929192939494959594933929292',
      to: '0xde929f939d939d393f939393f93939f393929023',
      gas: 69420n,
      data: '0xf00d4b5d00000000000000000000000001291230982139282304923482304912923823920000000000000000000000001293123098123928310239129839291010293810'
    })
    // { failed: false, gas: 69420, returnValue: '...', structLogs: [] }

For a more succinct implementation of using `.extend`, check out viem's [Public Client implementation](https://github.com/wagmi-dev/viem/blob/29c053f5069a5b44e3791972c221368a2c71a254/src/clients/createPublicClient.ts#L48-L68) extended with [Public Actions](https://github.com/wagmi-dev/viem/blob/29c053f5069a5b44e3791972c221368a2c71a254/src/clients/decorators/public.ts#L1377-L1425).

### Tree-shaking

You can use the Client as-is, with no decorated Actions, to maximize tree-shaking in your app. This is useful if you are pedantic about bundle size and want to only include the Actions you use.

In the example below, instead of calling `getBlock` from the Public Client, we are importing the Action directly from `viem` and then injecting our Client as the first parameter to the Action.

    import { createClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
    import { getBlock, sendTransaction } from 'viem/actions'
     
    const client = createClient({ 
      chain: mainnet,
      transport: http()
    })
     
    const blockNumber = await getBlock(client, { blockTag: 'latest' })
    const hash = await sendTransaction(client, { ... })

Parameters
----------

### transport

*   **Type:** [Transport](https://viem.sh/docs/glossary/types#transport)

The [Transport](https://viem.sh/docs/clients/intro) of the Public Client.

    const client = createClient({
      chain: mainnet,
      transport: http(), 
    })

### account (optional)

*   **Type:** `Account | Address`

The Account to use for the Client. This will be used for Actions that require an `account` as an argument.

Accepts a [JSON-RPC Account](https://viem.sh/docs/accounts/jsonRpc) or [Local Account (Private Key, etc)](https://viem.sh/docs/accounts/local/privateKeyToAccount).

    import { privateKeyToAccount } from 'viem/accounts'
     
    const client = createClient({
      account: privateKeyToAccount('0x...'), 
      chain: mainnet,
      transport: http(),
    })

### chain (optional)

*   **Type:** [Chain](https://viem.sh/docs/glossary/types#chain)

The [Chain](https://viem.sh/docs/chains/introduction) of the Public Client.

    const client = createClient({
      chain: mainnet, 
      transport: http(),
    })

### batch (optional)

Flags for batch settings.

### batch.multicall (optional)

*   **Type:** `boolean | MulticallBatchOptions`
*   **Default:** `false`

Toggle to enable `eth_call` multicall aggregation.

    const client = createClient({
      batch: {
        multicall: true, 
      },
      chain: mainnet,
      transport: http(),
    })

### batch.multicall.batchSize (optional)

*   **Type:** `number`
*   **Default:** `1_024`

The maximum size (in bytes) for each multicall (`aggregate3`) calldata chunk.

> Note: Some RPC Providers limit the amount of calldata that can be sent in a single request. It is best to check with your RPC Provider to see if there are any calldata size limits to `eth_call` requests.

    const client = createClient({
      batch: {
        multicall: {
          batchSize: 512, 
        },
      },
      chain: mainnet,
      transport: http(),
    })

### batch.multicall.wait (optional)

*   **Type:** `number`
*   **Default:** `0` ([zero delay](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop#zero_delays))

The maximum number of milliseconds to wait before sending a batch.

    const client = createClient({
      batch: {
        multicall: {
          wait: 16, 
        },
      },
      chain: mainnet,
      transport: http(),
    })

### key (optional)

*   **Type:** `string`
*   **Default:** `"public"`

A key for the Client.

    const client = createClient({
      chain: mainnet,
      key: 'public', 
      transport: http(),
    })

### name (optional)

*   **Type:** `string`
*   **Default:** `"Public Client"`

A name for the Client.

    const client = createClient({
      chain: mainnet,
      name: 'Public Client', 
      transport: http(),
    })

### pollingInterval (optional)

*   **Type:** `number`
*   **Default:** `4_000`

Frequency (in ms) for polling enabled Actions.

    const client = createClient({
      chain: mainnet,
      pollingInterval: 10_000, 
      transport: http(),
    })

### rpcSchema (optional)

*   **Type:** `RpcSchema`
*   **Default:** `WalletRpcSchema`

Typed JSON-RPC schema for the client.

    import { rpcSchema } from 'viem'
     
    type CustomRpcSchema = [{ 
      Method: 'eth_wagmi', 
      Parameters: [string] 
      ReturnType: string
    }] 
     
    const client = createClient({
      chain: mainnet,
      rpcSchema: rpcSchema<CustomRpcSchema>(), 
      transport: http()
    })
     
    const result = await client.request({ 
      method: 'eth_wa // [!code focus] 
      params: ['hello'], 
    })</content>
</page>

<page>
  <title>Public Client</title>
  <url>https://viem.sh/docs/clients/public</url>
  <content>A Public Client is an interface to "public" [JSON-RPC API](https://ethereum.org/en/developers/docs/apis/json-rpc/) methods such as retrieving block numbers, transactions, reading from smart contracts, etc through [Public Actions](https://viem.sh/docs/actions/public/introduction).

The `createPublicClient` function sets up a Public Client with a given [Transport](https://viem.sh/docs/clients/intro) configured for a [Chain](https://viem.sh/docs/chains/introduction).

Import
------

    import { createPublicClient } from 'viem'

Usage
-----

Initialize a Client with your desired [Chain](https://viem.sh/docs/chains/introduction) (e.g. `mainnet`) and [Transport](https://viem.sh/docs/clients/intro) (e.g. `http`).

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const publicClient = createPublicClient({ 
      chain: mainnet,
      transport: http()
    })

Then you can consume [Public Actions](https://viem.sh/docs/actions/public/introduction):

    const blockNumber = await publicClient.getBlockNumber() 

Optimization
------------

The Public Client also supports [`eth_call` Aggregation](https://viem.sh/docs/clients/public#multicall) for improved performance.

### `eth_call` Aggregation (via Multicall)

The Public Client supports the aggregation of `eth_call` requests into a single multicall (`aggregate3`) request.

This means for every Action that utilizes an `eth_call` request (ie. `readContract`), the Public Client will batch the requests (over a timed period) and send it to the RPC Provider in a single multicall request. This can dramatically improve network performance, and decrease the amount of [Compute Units (CU)](https://docs.alchemy.com/reference/compute-units) used by RPC Providers like Alchemy, Infura, etc.

The Public Client schedules the aggregation of `eth_call` requests over a given time period. By default, it executes the batch request at the end of the current [JavaScript message queue](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop#queue) (a [zero delay](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop#zero_delays)), however, consumers can specify a custom `wait` period (in ms).

You can enable `eth_call` aggregation by setting the `batch.multicall` flag to `true`:

    const publicClient = createPublicClient({
      batch: {
        multicall: true, 
      },
      chain: mainnet,
      transport: http(),
    })

> You can also [customize the `multicall` options](https://viem.sh/docs/clients/public#batchmulticallbatchsize-optional).

Now, when you start to utilize `readContract` Actions, the Public Client will batch and send over those requests at the end of the message queue (or custom time period) in a single `eth_call` multicall request:

    import { getContract } from 'viem'
    import { abi } from './abi'
    import { publicClient } from './client'
     
    const contract = getContract({ address, abi, client: publicClient })
     
    // The below will send a single request to the RPC Provider.
    const [name, totalSupply, symbol, balance] = await Promise.all([
      contract.read.name(),
      contract.read.totalSupply(),
      contract.read.symbol(),
      contract.read.balanceOf([address]),
    ])

> Read more on [Contract Instances](https://viem.sh/docs/contract/getContract).

Parameters
----------

### transport

*   **Type:** [Transport](https://viem.sh/docs/glossary/types#transport)

The [Transport](https://viem.sh/docs/clients/intro) of the Public Client.

    const publicClient = createPublicClient({
      chain: mainnet,
      transport: http(), 
    })

### chain (optional)

*   **Type:** [Chain](https://viem.sh/docs/glossary/types#chain)

The [Chain](https://viem.sh/docs/chains/introduction) of the Public Client.

    const publicClient = createPublicClient({
      chain: mainnet, 
      transport: http(),
    })

### batch (optional)

Flags for batch settings.

### batch.multicall (optional)

*   **Type:** `boolean | MulticallBatchOptions`
*   **Default:** `false`

Toggle to enable `eth_call` multicall aggregation.

    const publicClient = createPublicClient({
      batch: {
        multicall: true, 
      },
      chain: mainnet,
      transport: http(),
    })

### batch.multicall.batchSize (optional)

*   **Type:** `number`
*   **Default:** `1_024`

The maximum size (in bytes) for each multicall (`aggregate3`) calldata chunk.

> Note: Some RPC Providers limit the amount of calldata that can be sent in a single request. It is best to check with your RPC Provider to see if there are any calldata size limits to `eth_call` requests.

    const publicClient = createPublicClient({
      batch: {
        multicall: {
          batchSize: 512, 
        },
      },
      chain: mainnet,
      transport: http(),
    })

### batch.multicall.wait (optional)

*   **Type:** `number`
*   **Default:** `0` ([zero delay](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop#zero_delays))

The maximum number of milliseconds to wait before sending a batch.

    const publicClient = createPublicClient({
      batch: {
        multicall: {
          wait: 16, 
        },
      },
      chain: mainnet,
      transport: http(),
    })

### cacheTime (optional)

*   **Type:** `number`
*   **Default:** `client.pollingInterval`

Time (in ms) that cached data will remain in memory.

    const publicClient = createPublicClient({
      cacheTime: 10_000, 
      chain: mainnet,
      transport: http(),
    })

### ccipRead (optional)

*   **Type:** `(parameters: CcipRequestParameters) => Promise<CcipRequestReturnType> | false`
*   **Default:** `true`

[CCIP Read](https://eips.ethereum.org/EIPS/eip-3668) configuration.

CCIP Read is enabled by default, but if set to `false`, the client will not support offchain CCIP lookups.

    const publicClient = createPublicClient({
      ccipRead: false, 
      chain: mainnet,
      transport: http(),
    })

### ccipRead.request (optional)

*   **Type:** `(parameters: CcipRequestParameters) => Promise<CcipRequestReturnType>`

A function that will be called to make the [offchain CCIP lookup request](https://eips.ethereum.org/EIPS/eip-3668#client-lookup-protocol).

    const publicClient = createPublicClient({
      ccipRead: { 
        async request({ data, sender, urls }) { 
          // ... 
        } 
      }, 
      chain: mainnet,
      transport: http(),
    })

### key (optional)

*   **Type:** `string`
*   **Default:** `"public"`

A key for the Client.

    const publicClient = createPublicClient({
      chain: mainnet,
      key: 'public', 
      transport: http(),
    })

### name (optional)

*   **Type:** `string`
*   **Default:** `"Public Client"`

A name for the Client.

    const publicClient = createPublicClient({
      chain: mainnet,
      name: 'Public Client', 
      transport: http(),
    })

### pollingInterval (optional)

*   **Type:** `number`
*   **Default:** `4_000`

Frequency (in ms) for polling enabled Actions.

    const publicClient = createPublicClient({
      chain: mainnet,
      pollingInterval: 10_000, 
      transport: http(),
    })

### rpcSchema (optional)

*   **Type:** `RpcSchema`
*   **Default:** `PublicRpcSchema`

Typed JSON-RPC schema for the client.

    import { rpcSchema } from 'viem'
     
    type CustomRpcSchema = [{ 
      Method: 'eth_wagmi', 
      Parameters: [string] 
      ReturnType: string
    }] 
     
    const publicClient = createPublicClient({
      chain: mainnet,
      rpcSchema: rpcSchema<CustomRpcSchema>(), 
      transport: http(),
    })
     
    const result = await publicClient.request({ 
      method: 'eth_wa // [!code focus] 
      params: ['hello'], 
    }) 

Live Example
------------

Check out the usage of `createPublicClient` in the live [Public Client Example](https://stackblitz.com/github/wagmi-dev/viem/tree/main/examples/clients_public-client) below.</content>
</page>

<page>
  <title>Viem</title>
  <url>https://viem.sh/docs/migration-guide</url>
  <content>If you are coming from an earlier version of `viem`, you will need to make sure to update the following APIs listed below.

2.x.x Breaking changes
----------------------

The 2.x.x release includes very minor breaking changes to the Contract Instances API, entrypoints, chain modules, and miscellaneous actions + utilities listed below.

Not ready to migrate? [Head to the 1.x.x docs.](https://v1.viem.sh/)

### Actions: Modified `getContract` Client API

The `publicClient` and `walletClient` parameters of the `getContract` API has been removed in favour of `client` to support Client's that [extend](https://viem.sh/docs/clients/wallet#optional-extend-with-public-actions) (ie. [a Wallet Client extended with Public Actions](https://viem.sh/docs/clients/wallet#optional-extend-with-public-actions)).

[Read more.](https://viem.sh/docs/contract/getContract)

    import { getContract } from 'viem'
    import { publicClient, walletClient } from './client'
     
    const contract = getContract({
      abi,
      address,
      publicClient, 
      walletClient, 
      client: { 
        public: publicClient, 
        wallet: walletClient, 
      } 
    })

### Removed entrypoints

The following entrypoints have been removed:

*   `viem/abi`
*   `viem/contract`
*   `viem/public`
*   `viem/test`
*   `viem/wallet`

You can import the entrypoints directly from `viem`:

    import { encodeAbiParameters } from 'viem/abi'
    import { getContract } from 'viem/contract'
    import { getBlock } from 'viem/public'
    import { mine } from 'viem/test'
    import { sendTransaction } from 'viem/wallet'
    import { 
      encodeAbiParameters, 
      getContract, 
      getBlock, 
      mine, 
      sendTransaction, 
    } from 'viem'

### Moved chain-specific exports in `viem/chains/utils`

Chain-specific exports in `viem/chains/utils` have been moved to `viem/{celo|op-stack|zksync}`:

    import {
      parseTransactionCelo,
      parseTransaction 
      serializeTransactionCelo, 
      serializeTransaction 
      // ...
    } from 'viem/chains/utils'
    } from 'viem/celo'
     
    import {
      // ...
    } from 'viem/chains/utils'
    } from 'viem/op-stack'
     
    import {
      parseTransactionZkSync, 
      parseTransaction, 
      serializeTransactionZkSync, 
      serializeTransaction, 
      // ...
    } from 'viem/chains/utils'
    } from 'viem/zksync'

### Actions: `getBlockNumber`

The `maxAge` parameter has been removed in favor of `cacheTime`.

    const blockNumber = await client.getBlockNumber({
      maxAge: 84_600
      cacheTime: 84_600
    })

### Actions: `OnLogFn` & `OnLogParameter` types

The `OnLogFn` & `OnLogParameter` types have been renamed.

    import {
      OnLogFn, 
      WatchEventOnLogsFn, 
      OnLogParameter, 
      WatchEventOnLogsParameter, 
    } from 'viem' 

### Actions: `prepareRequest`

The `prepareRequest` Action has been renamed to `prepareTransactionRequest` and moved to `viem/actions` entrypoint.

    import {
      prepareRequest, 
      prepareTransactionRequest, 
    } from 'viem'
    } from 'viem/actions'

### Actions: `SimulateContractParameters` & `SimulateContractReturnType` types

Note the following breaking generic slot changes:

    type SimulateContractParameters<
      TAbi,
      TFunctionName,
      TArgs, // Args added to Slot 2 
      TChain,
      TChainOverride,
      TAccountOverride,
    >
     
    type SimulateContractReturnType<
      TAbi,
      TFunctionName,
      TArgs, // Args added to Slot 2 
      TChain,
      TAccount, // Account added to Slot 4 
      TChainOverride,
      TAccountOverride,
    >

### Utilities: Removed `extractFunctionParts`, `extractFunctionName`, `extractFunctionParams`, `extractFunctionType`

The `extractFunctionParts`, `extractFunctionName`, `extractFunctionParams`, `extractFunctionType` utility functions have been removed. You can use the [`parseAbiItem` utility function from abitype](https://abitype.dev/api/human#parseabiitem-1) instead.

### Utilities: Renamed `bytesToBigint`

The `bytesToBigint` utility function has been renamed to `bytesToBigInt`.

    import {
      bytesToBigint, 
      bytesToBigInt, 
    } from 'viem'

### Utilities: Renamed chain types

The following chain types have been renamed:

    import {
      Formatter, 
      ChainFormatter, 
      Formatters, 
      ChainFormatters, 
      Serializers, 
      ChainSerializers, 
      ExtractFormatterExclude, 
      ExtractChainFormatterExclude, 
      ExtractFormatterParameters, 
      ExtractChainFormatterParameters, 
      ExtractFormatterReturnType, 
      ExtractChainFormatterReturnType, 
    } from 'viem'

### Utilities: `isAddress` & `getAddress` perform checksum validation

The `isAddress` utility function now performs checksum validation by default.

To opt-out of this behavior, you can pass `strict: false` or lowercase the address.

    import { isAddress } from 'viem'
     
    isAddress('0xa5cc3c03994db5b0d9a5eEdD10Cabab0813678ac', {
      strict: false
    })
     
    isAddress(
      '0xa5cc3c03994db5b0d9a5eEdD10Cabab0813678ac'.toLowerCase() 
    )

1.x.x Breaking changes
----------------------

The 1.x.x release only includes very minor changes to the behavior in event log decoding, and removes the redundant ethers.js Wallet Adapter. If you do not directly use these APIs, you do not need to update any of your code for this version.

### Removed `ethersWalletToAccount`

The `ethersWalletToAccount` adapter has been removed.

This adapter was introduced when viem did not have Private Key & HD Accounts. Since 0.2, viem provides all the utilities needed to create and import [Private Key](https://viem.sh/docs/accounts/local/privateKeyToAccount) & [HD Accounts](https://viem.sh/docs/accounts/local/mnemonicToAccount).

If you still need it, you can copy + paste the [old implementation](https://github.com/wevm/viem/blob/a9a71507032db896295fa1f3fa2dd6c2bdc85137/src/adapters/ethers.ts).

### `logIndex` & `transactionIndex` on Logs

`logIndex` & `transactionIndex` on `Log` now return a `number` instead of a `bigint`.

    const log: Log = {
      ...
      logIndex: 1n, 
      logIndex: 1, 
      transactionIndex: 1n, 
      transactionIndex: 1, 
      ...
    }

### Minor: `decodeEventLog` behavior change

`decodeEventLog` no longer attempts to partially decode events. If the Log does not conform to the ABI (mismatch between the number of indexed/non-indexed arguments to topics/data), it will throw an error.

For example, the following Log will throw an error as there is a mismatch in non-`indexed` arguments & `data` length.

    decodeEventLog({
      abi: parseAbi(['event Transfer(address indexed, address, uint256)']), 
      // `data` should be 64 bytes, but is only 32 bytes. 
      data: '0x0000000000000000000000000000000000000000000000000000000000000001'
      topics: [
        '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
        '0x000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      ]
    })

Previously, the above would only decode the `indexed` arguments.

If you would like to partially decode event logs (previous behavior), you can turn off `strict` mode:

    decodeEventLog({
      abi: parseAbi(['event Transfer(address indexed, address, uint256)']),
      data: '0x0000000000000000000000000000000000000000000000000000000000000001'
      topics: [
        '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
        '0x000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      ],
      strict: false
    })

0.3.x Breaking changes
----------------------

The 0.3.x release only includes breaking changes around RPC errors. If you do not directly use the APIs listed below, you do not need to update any of your code for this version.

### Renamed `RequestError` to `RpcError`

`RequestError` was renamed `RpcError` for clarity.

    import { RequestError } from 'viem'
    import { RpcError } from 'viem'
     
    throw new RequestError(new Error('An error occurred.'))  
    throw new RpcError(new Error('An error occurred.'))  

### Removed `RpcRequestError`

`RpcRequestError` was removed. Use `RpcError` instead.

    import { RpcRequestError } from 'viem'
    import { RpcError } from 'viem'
     
    throw new RpcRequestError(new Error('An error occurred.')) 
    throw new RpcError(new Error('An error occurred.')) 

### Renamed `RpcError` to `RpcRequestError`

`RpcError` was renamed `RpcRequestError` for consistency.

    import { RpcError } from 'viem'
    import { RpcRequestError } from 'viem'
     
    const err = new RpcError({ 
    const err = new RpcRequestError({  
      body: { foo: 'bar' },
      error: { code: 420, message: 'Error' },
      url: 'https://example-rpc.com',
    })

0.2.x Breaking changes
----------------------

### `chain` is required for `sendTransaction`, `writeContract`, `deployContract`

A chain is now required for the `sendTransaction`, `writeContract`, `deployContract` Actions.

You can hoist the Chain on the Client:

    import { createWalletClient, custom, getAccount } from 'viem'
    import { mainnet } from 'viem/chains'
     
    export const walletClient = createWalletClient({
      chain: mainnet, 
      transport: custom(window.ethereum)
    })
     
    const account = getAccount('0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266')
     
    const hash = await walletClient.sendTransaction({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

Alternatively, you can pass the Chain directly to the Action:

    import { createWalletClient, custom, getAccount } from 'viem'
    import { mainnet } from 'viem/chains'
     
    export const walletClient = createWalletClient({
      chain: mainnet, 
      transport: custom(window.ethereum)
    })
     
    const account = getAccount('0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266')
     
    const hash = await walletClient.sendTransaction({ 
      account,
      chain: mainnet, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### `recoverAddress`, `recoverMessageAddress`, `verifyMessage` are now async

The following functions are now `async` functions instead of synchronous functions:

*   `recoverAddress`
*   `recoverMessageAddress`
*   `verifyMessage`

    import { recoverMessageAddress } from 'viem'
     
    recoverMessageAddress({ message: 'hello world', signature: '0x...' }) 
    await recoverMessageAddress({ message: 'hello world', signature: '0x...' }) 

### `assertChain` removed from `sendTransaction`

Removed `assertChain` argument on `sendTransaction`, `writeContract` & `deployContract`. If you wish to bypass the chain check (not recommended unless for testing purposes), you can pass `chain: null`.

    await walletClient.sendTransaction({
      assertChain: false, 
      chain: null, 
      ...
    })

### `getAccount` removed

Removed the `getAccount` function.

#### For JSON-RPC Accounts, use the address itself.

You can now pass the address directly to the `account` option.

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const address = '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
     
    const client = createWalletClient({
      account: getAccount(address), 
      account: address, 
      chain: mainnet,
      transport: custom(window.ethereum)
    })

#### For Ethers Wallet Adapter, use `ethersWalletToAccount`.

If you were using the Ethers Wallet adapter, you can use the `ethersWalletToAccount` function.

> Note: viem 0.2.0 now has a [Private Key](https://viem.sh/docs/accounts/local/privateKeyToAccount) & [Mnemonic Account](https://viem.sh/docs/accounts/local/mnemonicToAccount) implementation. You probably do not need this adapter anymore. This adapter may be removed in a future version.

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
    import { getAccount } from 'viem/ethers'
    import { ethersWalletToAccount } from 'viem/ethers'
    import { Wallet } from 'ethers'
     
    const account = getAccount(new Wallet('0x...')) 
    const account = ethersWalletToAccount(new Wallet('0x...')) 
     
    const client = createWalletClient({
      account,
      chain: mainnet,
      transport: custom(window.ethereum)
    })

#### For Local Accounts, use `toAccount`.

If you are using a custom signing implementation, you can use the `toAccount` function.

    import { createWalletClient, http, getAccount } from 'viem'
    import { createWalletClient, http } from 'viem'
    import { toAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
    import { getAddress, signMessage, signTransaction } from './sign-utils' 
     
    const privateKey = '0x...' 
    const account = getAccount({ 
    const account = toAccount({ 
      address: getAddress(privateKey),
      signMessage(message) {
        return signMessage(message, privateKey)
      },
      signTransaction(transaction) {
        return signTransaction(transaction, privateKey)
      },
      signTypedData(typedData) {
        return signTypedData(typedData, privateKey)
      }
    })
     
    const client = createWalletClient({
      account,
      chain: mainnet,
      transport: http()
    })

### `data` renamed in `signMessage`

Renamed the `data` parameter in `signMessage` to `message`.

    walletClient.signMessage({
      data: 'hello world', 
      message: 'hello world', 
    })</content>
</page>

<page>
  <title>Wallet Client</title>
  <url>https://viem.sh/docs/clients/wallet</url>
  <content>A Wallet Client is an interface to interact with [Ethereum Account(s)](https://ethereum.org/en/glossary/#account) and provides the ability to retrieve accounts, execute transactions, sign messages, etc through [Wallet Actions](https://viem.sh/docs/actions/wallet/introduction).

The `createWalletClient` function sets up a Wallet Client with a given [Transport](https://viem.sh/docs/clients/intro).

The Wallet Client supports signing over:

*   [JSON-RPC Accounts](https://viem.sh/docs/clients/wallet#json-rpc-accounts) (e.g. Browser Extension Wallets, WalletConnect, etc.).
*   [Local Accounts](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc) (e.g. private key/mnemonic wallets).

Import
------

    import { createWalletClient } from 'viem'

JSON-RPC Accounts
-----------------

A [JSON-RPC Account](https://viem.sh/docs/accounts/jsonRpc) **defers** signing of transactions & messages to the target Wallet over JSON-RPC. An example could be sending a transaction via a Browser Extension Wallet (e.g. MetaMask) with the `window.ethereum` Provider.

Below is an example of how you can set up a JSON-RPC Account.

#### 1: Initialize a Wallet Client

Before we set up our Account and start consuming Wallet Actions, we will need to set up our Wallet Client with the [`custom` Transport](https://viem.sh/docs/clients/transports/custom), where we will pass in the `window.ethereum` Provider:

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: custom(window.ethereum!)
    })

#### 2: Set up your JSON-RPC Account

We will want to retrieve an address that we can access in our Wallet (e.g. MetaMask).

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: custom(window.ethereum!)
    })
     
    const [address] = await client.getAddresses() 
    // or: const [address] = await client.requestAddresses() 

> Note: Some Wallets (like MetaMask) may require you to request access to Account addresses via [`client.requestAddresses`](https://viem.sh/docs/actions/wallet/requestAddresses) first.

#### 3: Consume [Wallet Actions](https://viem.sh/docs/actions/wallet/introduction)

Now you can use that address within Wallet Actions that require a signature from the user:

    import { createWalletClient, custom, parseEther } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: custom(window.ethereum!)
    })
     
    const [address] = await client.getAddresses()
     
    const hash = await client.sendTransaction({ 
      account: address,
      to: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: parseEther('0.001')
    })

#### Optional: Hoist the Account

If you do not wish to pass an account around to every Action that requires an `account`, you can also hoist the account into the Wallet Client.

    import { createWalletClient, http, parseEther } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const [account] = await window.ethereum!.request({ method: 'eth_requestAccounts' })
     
    const client = createWalletClient({ 
      account, 
      chain: mainnet,
      transport: http()
    })
     
    const hash = await client.sendTransaction({
      account, 
      to: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: parseEther('0.001')
    })

Local Accounts (Private Key, Mnemonic, etc)
-------------------------------------------

A Local Account performs signing of transactions & messages with a private key **before** executing a method over JSON-RPC.

There are three types of Local Accounts in viem:

*   [Private Key Account](https://viem.sh/docs/accounts/local/privateKeyToAccount)
*   [Mnemonic Account](https://viem.sh/docs/accounts/local/mnemonicToAccount)
*   [Hierarchical Deterministic (HD) Account](https://viem.sh/docs/accounts/local/hdKeyToAccount)

Below are the steps to integrate a **Private Key Account**, but the same steps can be applied to **Mnemonic & HD Accounts**.

#### 1: Initialize a Wallet Client

Before we set up our Account and start consuming Wallet Actions, we will need to set up our Wallet Client with the [`http` Transport](https://viem.sh/docs/clients/transports/http):

    import { createWalletClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: http()
    })

#### 2: Set up your Local Account

Next, we will instantiate a Private Key Account using `privateKeyToAccount`:

    import { createWalletClient, http } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: http()
    })
     
    const account = privateKeyToAccount('0x...') 

#### 3: Consume [Wallet Actions](https://viem.sh/docs/actions/wallet/introduction)

Now you can use that Account within Wallet Actions that need a signature from the user:

    import { createWalletClient, http, parseEther } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: http()
    })
     
    const account = privateKeyToAccount('0x...')
     
    const hash = await client.sendTransaction({ 
      account,
      to: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: parseEther('0.001')
    })

#### Optional: Hoist the Account

If you do not wish to pass an account around to every Action that requires an `account`, you can also hoist the account into the Wallet Client.

    import { createWalletClient, http, parseEther } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const account = privateKeyToAccount('0x...')
     
    const client = createWalletClient({ 
      account, 
      chain: mainnet,
      transport: http()
    })
     
    const hash = await client.sendTransaction({
      account, 
      to: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: parseEther('0.001')
    })

#### Optional: Extend with Public Actions

When using a Local Account, you may be finding yourself using a [Public Client](https://viem.sh/docs/clients/public) instantiated with the same parameters (`transport`, `chain`, etc) as your Wallet Client.

In this case, you can extend your Wallet Client with [Public Actions](https://viem.sh/docs/actions/public/introduction) to avoid having to handle multiple Clients.

    import { createWalletClient, http, publicActions } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const account = privateKeyToAccount('0x...')
     
    const client = createWalletClient({ 
      account,
      chain: mainnet,
      transport: http()
    }).extend(publicActions) 
     
    const { request } = await client.simulateContract({ ... }) // Public Action 
    const hash = await client.writeContract(request) // Wallet Action 

Parameters
----------

### account (optional)

*   **Type:** `Account | Address`

The Account to use for the Wallet Client. This will be used for Actions that require an `account` as an argument.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    import { createWalletClient, custom, parseEther } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      account: '0x...', 
      chain: mainnet,
      transport: custom(window.ethereum!)
    })
     
    const hash = await client.sendTransaction({
      to: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: parseEther('0.001')
    })

### chain (optional)

*   **Type:** [Chain](https://viem.sh/docs/glossary/types#chain)

The [Chain](https://viem.sh/docs/chains/introduction) of the Wallet Client.

Used in the [`sendTransaction`](https://viem.sh/docs/actions/wallet/sendTransaction) & [`writeContract`](https://viem.sh/docs/contract/writeContract) Actions to assert that the chain matches the wallet's active chain.

    const client = createWalletClient({
      chain: mainnet, 
      transport: custom(window.ethereum!)
    })

### cacheTime (optional)

*   **Type:** `number`
*   **Default:** `client.pollingInterval`

Time (in ms) that cached data will remain in memory.

    const client = createWalletClient({
      cacheTime: 10_000, 
      chain: mainnet,
      transport: custom(window.ethereum!)
    })

### ccipRead (optional)

*   **Type:** `(parameters: CcipRequestParameters) => Promise<CcipRequestReturnType> | false`
*   **Default:** `true`

[CCIP Read](https://eips.ethereum.org/EIPS/eip-3668) configuration.

CCIP Read is enabled by default, but if set to `false`, the client will not support offchain CCIP lookups.

    const client = createWalletClient({
      ccipRead: false, 
      transport: custom(window.ethereum!)
    })

### ccipRead.request (optional)

*   **Type:** `(parameters: CcipRequestParameters) => Promise<CcipRequestReturnType>`

A function that will be called to make the [offchain CCIP lookup request](https://eips.ethereum.org/EIPS/eip-3668#client-lookup-protocol).

    const client = createWalletClient({
      ccipRead: { 
        async request({ data, sender, urls }) { 
          // ... 
        } 
      }, 
      transport: custom(window.ethereum!)
    })

### key (optional)

*   **Type:** `string`
*   **Default:** `"wallet"`

A key for the Client.

    const client = createWalletClient({
      key: 'foo', 
      transport: custom(window.ethereum!)
    })

### name (optional)

*   **Type:** `string`
*   **Default:** `"Wallet Client"`

A name for the Client.

    const client = createWalletClient({
      name: 'Foo Wallet Client', 
      transport: custom(window.ethereum!)
    })

### pollingInterval (optional)

*   **Type:** `number`
*   **Default:** `4_000`

Frequency (in ms) for polling enabled Actions.

    const client = createWalletClient({
      pollingInterval: 10_000, 
      transport: custom(window.ethereum!)
    })

### rpcSchema (optional)

*   **Type:** `RpcSchema`
*   **Default:** `WalletRpcSchema`

Typed JSON-RPC schema for the client.

    import { rpcSchema } from 'viem'
     
    type CustomRpcSchema = [{ 
      Method: 'eth_wagmi', 
      Parameters: [string] 
      ReturnType: string
    }] 
     
    const client = createWalletClient({
      rpcSchema: rpcSchema<CustomRpcSchema>(), 
      transport: custom(window.ethereum!)
    })
     
    const result = await client.request({ 
      method: 'eth_wa // [!code focus] 
      params: ['hello'], 
    })</content>
</page>

<page>
  <title>HTTP Transport</title>
  <url>https://viem.sh/docs/clients/transports/http</url>
  <content>The `http` Transport connects to a JSON-RPC API via HTTP.

Import
------

    import { http } from 'viem'

Usage
-----

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http('https://1.rpc.thirdweb.com/...'), 
    })

### Batch JSON-RPC

The `http` Transport supports Batch JSON-RPC. This means that multiple JSON-RPC requests can be sent in a single HTTP request.

The Transport will batch up Actions over a given period and execute them in a single Batch JSON-RPC HTTP request. By default, this period is a [zero delay](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop#zero_delays) meaning that the batch request will be executed at the end of the current [JavaScript message queue](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop#queue). Consumers can specify a custom time period `wait` (in ms).

You can enable Batch JSON-RPC by setting the `batch` flag to `true`:

    const transport = http('https://1.rpc.thirdweb.com/...', {
      batch: true
    })

Now when you invoke Actions, the `http` Transport will batch and send over those requests at the end of the message queue (or custom time period) in a single Batch JSON-RPC HTTP request:

    // The below will send a single Batch JSON-RPC HTTP request to the RPC Provider.
    const [blockNumber, balance, ensName] = await Promise.all([
      client.getBlockNumber(),
      client.getBalance({ address: '0xd2135CfB216b74109775236E36d4b433F1DF507B' }),
      client.getEnsName({ address: '0xd2135CfB216b74109775236E36d4b433F1DF507B' }),
    ])

Parameters
----------

### url (optional)

*   **Type:** `string`
*   **Default:** `chain.rpcUrls.default.http[0]`

URL of the JSON-RPC API.

    const transport = http('https://1.rpc.thirdweb.com/...')

### batch (optional)

*   **Type:** `boolean | BatchOptions`
*   **Default:** `false`

Toggle to enable Batch JSON-RPC

    const transport = http('https://1.rpc.thirdweb.com/...', {
      batch: true
    })

### batch.batchSize (optional)

*   **Type:** `number`
*   **Default:** `1_000`

The maximum number of JSON-RPC requests to send in a batch.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      batch: {
        batchSize: 2_000
      }
    })

### batch.wait (optional)

*   **Type:** `number`
*   **Default:** `0` ([zero delay](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop#zero_delays))

The maximum number of milliseconds to wait before sending a batch.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      batch: {
        wait: 16
      }
    })

### fetchOptions (optional)

*   **Type:** [`RequestInit`](https://developer.mozilla.org/en-US/docs/Web/API/fetch)

[Fetch options](https://developer.mozilla.org/en-US/docs/Web/API/fetch) to pass to the internal `fetch` function. Useful for passing auth headers or cache options.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      fetchOptions: { 
        headers: {
          'Authorization': 'Bearer ...'
        }
      }
    })

### key (optional)

*   **Type:** `string`
*   **Default:** `"http"`

A key for the Transport.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      key: 'alchemy', 
    })

### methods (optional)

*   **Type:** `{ include?: string[], exclude?: string[] }`

Methods to include or exclude from sending RPC requests.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      methods: {
        include: ['eth_sendTransaction', 'eth_signTypedData_v4'],
      },
    })

### name (optional)

*   **Type:** `string`
*   **Default:** `"HTTP JSON-RPC"`

A name for the Transport

    const transport = http('https://1.rpc.thirdweb.com/...', {
      name: 'Alchemy HTTP Provider', 
    })

### onFetchRequest (optional)

*   **Type:** `(request: Request) => void`

A callback to handle the fetch request. Useful for logging or debugging.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      onFetchRequest(request) {
        console.log(request) 
      }
    })

### onFetchResponse (optional)

*   **Type:** `(response: Response) => void`

A callback to handle the fetch response. Useful for logging or debugging.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      onFetchResponse(response) {
        console.log(response) 
      }
    })

### retryCount (optional)

*   **Type:** `number`
*   **Default:** `3`

The max number of times to retry when a request fails.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      retryCount: 5, 
    })

### retryDelay (optional)

*   **Type:** `number`
*   **Default:** `150`

The base delay (in ms) between retries. By default, the Transport will use [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff) (`~~(1 << count) * retryDelay`), which means the time between retries is not constant.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      retryDelay: 100, 
    })

### timeout (optional)

*   **Type:** `number`
*   **Default:** `10_000`

The timeout for requests.

    const transport = http('https://1.rpc.thirdweb.com/...', {
      timeout: 60_000, 
    })</content>
</page>

<page>
  <title>Getting Started</title>
  <url>https://viem.sh/docs/getting-started</url>
  <content>Overview
--------

viem is a TypeScript interface for Ethereum that provides low-level stateless primitives for interacting with Ethereum. viem is focused on developer experience, stability, bundle size, and performance:

*   **Developer experience** Automatic [type safety and inference](https://viem.sh/docs/typescript), comprehensive documentation, composable APIs.
*   **Stability** Test suite runs against forked Ethereum networks, complete [test coverage](https://app.codecov.io/gh/wevm/viem).
*   **Bundle size** Tree-shakable lightweight modules.
*   **Performance** Optimized encoding/parsing, async tasks only when necessary.

You can learn more about the rationale behind the project in the [Why viem](https://viem.sh/docs/introduction) section.

Installation
------------

Quick Start
-----------

### 1\. Set up your Client & Transport

Firstly, set up your [Client](https://viem.sh/docs/clients/intro) with a desired [Transport](https://viem.sh/docs/clients/intro) & [Chain](https://viem.sh/docs/chains/introduction).

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: mainnet, 
      transport: http(), 
    }) 

### 2\. Consume Actions

Now that you have a Client set up, you can now interact with Ethereum and consume [Actions](https://viem.sh/docs/actions/public/introduction)!

    import { createPublicClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http(),
    })
     
    const blockNumber = await client.getBlockNumber() 

Live example
------------</content>
</page>

<page>
  <title>WebSocket Transport</title>
  <url>https://viem.sh/docs/clients/transports/websocket</url>
  <content>The `webSocket` Transport connects to a JSON-RPC API via a WebSocket.

Import
------

    import { webSocket } from 'viem'

Usage
-----

    import { createPublicClient, webSocket } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({
      chain: mainnet, 
      transport: webSocket('wss://1.rpc.thirdweb.com/...'), 
    })

Parameters
----------

### url

*   **Type:** `string`

URL of the JSON-RPC API.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...')

### keepAlive (optional)

*   **Type:** `boolean | { interval?: number }`
*   **Default:** `true`

Whether or not to send keep-alive ping messages.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', {
      keepAlive: { interval: 1_000 }, 
    })

### key (optional)

*   **Type:** `string`
*   **Default:** `"webSocket"`

A key for the Transport.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', { 
      key: 'alchemy',  
    })

### methods (optional)

*   **Type:** `{ include?: string[], exclude?: string[] }`

Methods to include or exclude from sending RPC requests.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', {
      methods: {
        include: ['eth_sendTransaction', 'eth_signTypedData_v4'],
      },
    })

### name (optional)

*   **Type:** `string`
*   **Default:** `"WebSocket JSON-RPC"`

A name for the Transport

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', { 
      name: 'Alchemy WebSocket Provider',  
    })

### reconnect (optional)

*   **Type:** `boolean | { maxAttempts?: number, delay?: number }`
*   **Default:** `true`

Whether or not to attempt to reconnect on socket failure.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', {
      reconnect: false, 
    })

#### reconnect.attempts (optional)

*   **Type:** `number`
*   **Default:** `5`

The max number of times to attempt to reconnect.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', {
      reconnect: {
        attempts: 10, 
      }
    })

#### reconnect.delay (optional)

*   **Type:** `number`
*   **Default:** `2_000`

Retry delay (in ms) between reconnect attempts.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', {
      reconnect: {
        delay: 1_000, 
      }
    })

### retryCount (optional)

*   **Type:** `number`
*   **Default:** `3`

The max number of times to retry when a request fails.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', {
      retryCount: 5, 
    })

### retryDelay (optional)

*   **Type:** `number`
*   **Default:** `150`

The base delay (in ms) between retries. By default, the Transport will use [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff) (`~~(1 << count) * retryDelay`), which means the time between retries is not constant.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', {
      retryDelay: 100, 
    })

### timeout (optional)

*   **Type:** `number`
*   **Default:** `10_000`

The timeout for async WebSocket requests.

    const transport = webSocket('wss://1.rpc.thirdweb.com/...', {
      timeout: 60_000, 
    })</content>
</page>

<page>
  <title>Custom Transport</title>
  <url>https://viem.sh/docs/clients/transports/custom</url>
  <content>The `custom` Transport accepts an [EIP-1193 `request` function](https://eips.ethereum.org/EIPS/eip-1193#request-1) as a parameter. This transport is useful for integrating with injected wallets, wallets that provide an EIP-1193 provider (eg. WalletConnect or Coinbase SDK), or even providing your own custom `request` function.

Import
------

    import { custom } from 'viem'

Usage
-----

You can use any [EIP-1193 compatible](https://eips.ethereum.org/EIPS/eip-1193) Ethereum Provider with the `custom` Transport:

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: custom(window.ethereum!)
    })

Or you can define your own:

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
    import { customRpc } from './rpc'
     
    const client = createWalletClient({ 
      chain: mainnet,
      transport: custom({
        async request({ method, params }) {
          const response = await customRpc.request(method, params)
          return response
        }
      })
    })

Parameters
----------

### provider

*   **Type:** `custom`

An [EIP-1193 `request` function](https://eips.ethereum.org/EIPS/eip-1193#request) function.

    import { customRpc } from './rpc'
     
    const transport = custom({
      async request({ method, params }) { 
        const response = await customRpc.request(method, params)
        return response
      }
    })

### key (optional)

*   **Type:** `string`
*   **Default:** `"custom"`

A key for the Transport.

    const transport = custom(
      window.ethereum!,
      { 
        key: 'windowProvider', 
      }
    )

### name (optional)

*   **Type:** `string`
*   **Default:** `"Ethereum Provider"`

A name for the Transport

    const transport = custom(
      window.ethereum!,
      { 
        name: 'Window Ethereum Provider', 
      }
    )

### retryCount (optional)

*   **Type:** `number`
*   **Default:** `3`

The max number of times to retry when a request fails.

    const transport = custom(window.ethereum!, {
      retryCount: 5, 
    })

### retryDelay (optional)

*   **Type:** `number`
*   **Default:** `150`

The base delay (in ms) between retries. By default, the Transport will use [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff) (`~~(1 << count) * retryDelay`), which means the time between retries is not constant.

    const transport = custom(window.ethereum!, {
      retryDelay: 100, 
    })

Gotchas
-------

*   If you are pairing the `custom` Transport with a [Public Client](https://viem.sh/docs/clients/public), ensure that your provider supports [Public Actions](https://viem.sh/docs/actions/public/introduction).</content>
</page>

<page>
  <title>IPC Transport</title>
  <url>https://viem.sh/docs/clients/transports/ipc</url>
  <content>The `ipc` Transport connects to a JSON-RPC API via IPC (inter-process communication).

Import
------

    import { ipc } from 'viem/node'

Usage
-----

    import { createPublicClient } from 'viem'
    import { ipc } from 'viem/node'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({
      chain: mainnet, 
      transport: ipc('/tmp/reth.ipc'), 
    })

Parameters
----------

### path

*   **Type:** `string`

IPC Path the transport should connect to.

    const transport = ipc('/tmp/reth.ipc')

### key (optional)

*   **Type:** `string`
*   **Default:** `"ipc"`

A key for the Transport.

    const transport = ipc('/tmp/reth.ipc', { 
      key: 'reth-ipc',  
    })

### methods (optional)

*   **Type:** `{ include?: string[], exclude?: string[] }`

Methods to include or exclude from sending RPC requests.

    const transport = ipc('/tmp/reth.ipc', {
      methods: {
        include: ['eth_sendTransaction', 'eth_signTypedData_v4'],
      },
    })

### name (optional)

*   **Type:** `string`
*   **Default:** `"IPC JSON-RPC"`

A name for the Transport

    const transport = ipc('/tmp/reth.ipc', { 
      name: 'Reth IPC',  
    })

### reconnect (optional)

*   **Type:** `boolean | { maxAttempts?: number, delay?: number }`
*   **Default:** `true`

Whether or not to attempt to reconnect on socket failure.

    const transport = ipc('/tmp/reth.ipc', {
      reconnect: false, 
    })

#### reconnect.attempts (optional)

*   **Type:** `number`
*   **Default:** `5`

The max number of times to attempt to reconnect.

    const transport = ipc('/tmp/reth.ipc', {
      reconnect: {
        attempts: 10, 
      }
    })

#### reconnect.delay (optional)

*   **Type:** `number`
*   **Default:** `2_000`

Retry delay (in ms) between reconnect attempts.

    const transport = ipc('/tmp/reth.ipc', {
      reconnect: {
        delay: 1_000, 
      }
    })

### retryCount (optional)

*   **Type:** `number`
*   **Default:** `3`

The max number of times to retry when a request fails.

    const transport = ipc('/tmp/reth.ipc', {
      retryCount: 5, 
    })

### retryDelay (optional)

*   **Type:** `number`
*   **Default:** `150`

The base delay (in ms) between retries. By default, the Transport will use [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff) (`~~(1 << count) * retryDelay`), which means the time between retries is not constant.

    const transport = ipc('/tmp/reth.ipc', {
      retryDelay: 100, 
    })

### timeout (optional)

*   **Type:** `number`
*   **Default:** `10_000`

The timeout for async IPC requests.

    const transport = ipc('/tmp/reth.ipc', {
      timeout: 60_000, 
    })</content>
</page>

<page>
  <title>Introduction to Public Actions</title>
  <url>https://viem.sh/docs/actions/public/introduction</url>
  <content>A Public Action is an action that maps one-to-one with a "public" Ethereum RPC method (`eth_blockNumber`, `eth_getBalance`, etc). They are used with a [Public Client](https://viem.sh/docs/clients/public).

Public Actions do not require any special permissions nor do they provide signing capabilities to the user. Examples of Public Actions include [getting the balance of an account](https://viem.sh/docs/actions/public/getBalance), [retrieving the details of a specific transaction](https://viem.sh/docs/actions/public/getTransactionReceipt), and [getting the current block number](https://viem.sh/docs/actions/public/getBlockNumber) of the network.

Public Actions provide a simple and secure way to access public data on the Ethereum blockchain. They are widely used by dapps and other applications that need to retrieve information about transactions, accounts, blocks and other data on the network.</content>
</page>

<page>
  <title>Chains</title>
  <url>https://viem.sh/docs/chains/introduction</url>
  <content>The `viem/chains` entrypoint contains references to popular EVM-compatible chains such as: Polygon, Optimism, Avalanche, Base, Zora, and more.

Usage
-----

Import your chain from the entrypoint and use them in the consuming viem code:

    import { createPublicClient, http } from 'viem'
    import { zora } from 'viem/chains'
     
    const client = createPublicClient({
      chain: zora, 
      transport: http()
    })

[See here for a list of supported chains](https://github.com/wagmi-dev/viem/tree/main/src/chains/index.ts).

> Want to add a chain that's not listed in viem? Read the [Contributing Guide](https://github.com/wagmi-dev/viem/blob/main/.github/CONTRIBUTING.md#chains), and then open a Pull Request with your chain.

Custom Chains
-------------

You can also extend viem to support other EVM-compatible chains by building your own chain object that inherits the `Chain` type.

    import { defineChain } from 'viem'
     
    export const zora = defineChain({
      id: 7777777,
      name: 'Zora',
      nativeCurrency: {
        decimals: 18,
        name: 'Ether',
        symbol: 'ETH',
      },
      rpcUrls: {
        default: {
          http: ['https://rpc.zora.energy'],
          webSocket: ['wss://rpc.zora.energy'],
        },
      },
      blockExplorers: {
        default: { name: 'Explorer', url: 'https://explorer.zora.energy' },
      },
      contracts: {
        multicall3: {
          address: '0xcA11bde05977b3631167028862bE2a173976CA11',
          blockCreated: 5882,
        },
      },
    })</content>
</page>

<page>
  <title>Fallback Transport</title>
  <url>https://viem.sh/docs/clients/transports/fallback</url>
  <content>The `fallback` Transport consumes **multiple** Transports. If a Transport request fails, it will fall back to the next one in the list.

Import
------

    import { fallback } from 'viem'

Usage
-----

    import { createPublicClient, fallback, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: fallback([ 
        http('https://1.rpc.thirdweb.com/...'), 
        http('https://mainnet.infura.io/v3/...') 
      ]), 
    })

### Transport Ranking

Transport Ranking enables each of the Transports passed to the `fallback` Transport are automatically ranked based on their **latency** & **stability** via a weighted moving score algorithm.

Every 10 seconds (`interval`), the `fallback` Transport will ping each transport in the list. For the past 10 pings (`sampleCount`), they will be ranked based on if they responded (stability) and how fast they responded (latency). The algorithm applies a weight of `0.7` to the stability score, and a weight of `0.3` to the latency score to derive the final score which it is ranked on.

The Transport that has the best latency & stability score over the sample period is prioritized first.

You can turn on automated ranking with the `rank` option:

    const client = createPublicClient({
      chain: mainnet,
      transport: fallback([ 
        http('https://1.rpc.thirdweb.com/...'), 
        http('https://mainnet.infura.io/v3/...') 
      ], { rank: true }), 
    })

You can also modify the default rank config:

    const client = createPublicClient({
      chain: mainnet,
      transport: fallback(
        [
          http('https://1.rpc.thirdweb.com/...'), 
          http('https://mainnet.infura.io/v3/...') 
        ],
        { 
          rank: {
            interval: 60_000,
            sampleCount: 5,
            timeout: 500,
            weights: {
              latency: 0.3,
              stability: 0.7
            }
          }
        }
      ),
    })

Parameters
----------

### rank (optional)

*   **Type:** `boolean | RankOptions`
*   **Default:** `false`

Whether or not to automatically rank the Transports based on their latency & stability. Set to `false` to disable automatic ranking.

    const transport = fallback([thirdweb, infura], {
      rank: false, 
    })

### rank.interval (optional)

*   **Type:** `number`
*   **Default:** `client.pollingInterval`

The polling interval (in ms) at which the ranker should ping the RPC URL.

    const transport = fallback([thirdweb, infura], {
      rank: { 
        interval: 5_000
      },
    })

### rank.ping (optional)

*   **Type:** `({ transport }: { transport: Transport }) => Promise<unknown>`
*   **Default:** `({ transport }) => transport.request({ method: 'net_listening' })`

Function to call to ping the Transport. Defaults to calling the `net_listening` method to check if the Transport is online.

    const transport = fallback([thirdweb, infura], {
      rank: { 
        ping: ({ transport }) => transport.request({ method: 'eth_blockNumber' })
      },
    })

### rank.sampleCount (optional)

*   **Type:** `number`
*   **Default:** `10`

The number of previous samples to perform ranking on.

    const transport = fallback([thirdweb, infura], {
      rank: { 
        sampleCount: 10
      },
    })

### rank.timeout (optional)

*   **Type:** `number`
*   **Default:** `1_000`

Timeout when sampling transports.

    const transport = fallback([thirdweb, infura], {
      rank: { 
        timeout: 500
      },
    })

### rank.weights.latency (optional)

*   **Type:** `number`
*   **Default:** `0.3`

The weight to apply to the latency score. The weight is proportional to the other values in the `weights` object.

    const transport = fallback([thirdweb, infura], {
      rank: {
        weights: {
          latency: 0.4, 
          stability: 0.6
        }
      },
    })

### rank.weights.stability (optional)

*   **Type:** `number`
*   **Default:** `0.7`

The weight to apply to the stability score. The weight is proportional to the other values in the `weights` object.

    const transport = fallback([thirdweb, infura], {
      rank: {
        weights: {
          latency: 0.4,
          stability: 0.6
        }
      },
    })

### retryCount (optional)

*   **Type:** `number`
*   **Default:** `3`

The max number of times to retry when a request fails.

> Note: The fallback will first try all the Transports before retrying.

    const transport = fallback([thirdweb, infura], {
      retryCount: 5, 
    })

### retryDelay (optional)

*   **Type:** `number`
*   **Default:** `150`

The base delay (in ms) between retries. By default, the Transport will use [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff) (`~~(1 << count) * retryDelay`), which means the time between retries is not constant.

    const transport = fallback([thirdweb, infura], {
      retryDelay: 100, 
    })

### shouldThrow (optional)

*   **Type:** `function`

Whether the `fallback` Transport should immediately throw an error, or continue and try the next Transport.

    const transport = fallback([thirdweb, infura], {
      shouldThrow: (err: Error) => { 
        return err.message.includes('sad times') 
      }, 
    })</content>
</page>

<page>
  <title>multicall</title>
  <url>https://viem.sh/docs/contract/multicall</url>
  <content>Similar to [`readContract`](https://viem.sh/docs/contract/readContract), but batches up multiple functions on a contract in a single RPC call via the [`multicall3` contract](https://github.com/mds1/multicall).

Usage
-----

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const wagmiContract = {
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi
    } as const
     
    const results = await publicClient.multicall({
      contracts: [
        {
          ...wagmiContract,
          functionName: 'totalSupply',
        },
        {
          ...wagmiContract,
          functionName: 'ownerOf',
          args: [69420n]
        },
        {
          ...wagmiContract,
          functionName: 'mint'
        }
      ]
    })
    /**
     * [
     *  { result: 424122n, status: 'success' },
     *  { result: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b', status: 'success' },
     *  { error: [ContractFunctionExecutionError: ...], status: 'failure' }
     * ]
     */

Return Value
------------

`({ data: <inferred>, status: 'success' } | { error: string, status: 'reverted' })[]`

An array of results with accompanying status.

Additionally, when [`allowFailure`](https://viem.sh/docs/contract/multicall#allowfailure-optional) is set to `false`, it directly returns an array of inferred data:

`(<inferred>)[]`

Parameters
----------

### contracts.address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const results = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
          abi: wagmiAbi,
          functionName: 'totalSupply',
        },
        ...
      ]
    })

### contracts.abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract ABI.

    const results = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi: wagmiAbi, 
          functionName: 'totalSupply',
        },
        ...
      ]
    })

### contracts.functionName

*   **Type**: `string`

The function name to call.

    const results = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi: wagmiAbi,
          functionName: 'totalSupply', 
        },
        ...
      ]
    })

### contracts.args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const results = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi: wagmiAbi,
          functionName: 'balanceOf',
          args: ['0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b'] 
        },
        ...
      ]
    })

### allowFailure (optional)

*   **Type:** `boolean`
*   **Default:** `true`

Whether or not the `multicall` function should throw if a call reverts. If set to `true` (default), and a call reverts, then `multicall` will fail silently and its error will be logged in the `results` array.

    const results = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi: wagmiAbi,
          functionName: 'totalSupply',
        },
        ...
      ],
      allowFailure: false
    })

### batchSize (optional)

*   **Type:** `number`
*   **Default:** [`client.batch.multicall.batchSize`](https://viem.sh/docs/clients/public#batch-multicall-batchsize-optional) (if set) or `1024`

The maximum size (in bytes) for each calldata chunk. Set to `0` to disable the size limit.

> Note: Some RPC Providers limit the amount of calldata (`data`) that can be sent in a single `eth_call` request. It is best to check with your RPC Provider to see if there are any calldata size limits to `eth_call` requests.

    const results = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi: wagmiAbi,
          functionName: 'totalSupply',
        },
        ...
      ],
      batchSize: 4096 // 4kB 
    })

### blockNumber (optional)

*   **Type:** `number`

The block number to perform the read against.

    const results = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi: wagmiAbi,
          functionName: 'totalSupply',
        },
        ...
      ],
      blockNumber: 15121123n, 
    })

### multicallAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)
*   **Default:** `client.chain.contracts.multicall3.address`

Address of Multicall Contract.

    const results = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi: wagmiAbi,
          functionName: 'totalSupply',
        },
        ...
      ],
      multicallAddress: '0xca11bde05977b3631167028862be2a173976ca11'
    })

### stateOverride (optional)

*   **Type:** [`StateOverride`](https://viem.sh/docs/glossary/types#stateoverride)

The state override set is an optional address-to-state mapping, where each entry specifies some state to be ephemerally overridden prior to executing the call.

    const data = await publicClient.multicall({
      contracts: [
        {
          address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi: wagmiAbi,
          functionName: 'totalSupply',
        },
        ...
      ],
      stateOverride: [ 
        { 
          address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
          balance: parseEther('1'), 
          stateDiff: [ 
            { 
              slot: '0x3ea2f1d0abf3fc66cf29eebb70cbd4e7fe762ef8a09bcc06c8edf641230afec0', 
              value: '0x00000000000000000000000000000000000000000000000000000000000001a4', 
            }, 
          ], 
        } 
      ], 
    })

Live Example
------------

Check out the usage of `multicall` in the live [Multicall Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/contracts_multicall) below.</content>
</page>

<page>
  <title>readContract</title>
  <url>https://viem.sh/docs/contract/readContract</url>
  <content>Calls a read-only function on a contract, and returns the response.

A "read-only" function (constant function) on a Solidity contract is denoted by a `view` or `pure` keyword. They can only read the state of the contract, and cannot make any changes to it. Since read-only methods do not change the state of the contract, they do not require any gas to be executed, and can be called by any user without the need to pay for gas.

Internally, `readContract` uses a [Public Client](https://viem.sh/docs/clients/public) to call the [`call` action](https://viem.sh/docs/actions/public/call) with [ABI-encoded `data`](https://viem.sh/docs/contract/encodeFunctionData).

Usage
-----

Below is a very basic example of how to call a read-only function on a contract (with no arguments).

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'totalSupply',
    })
    // 69420n

### Passing Arguments

If your function requires argument(s), you can pass them through with the `args` attribute.

TypeScript types for `args` will be inferred from the function name & ABI, to guard you from inserting the wrong values.

For example, the `balanceOf` function name below requires an **address** argument, and it is typed as `["0x${string}"]`.

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']
    })

### Deployless Reads

It is possible to call a function on a contract that has not been deployed yet. For instance, we may want to call a function on an [ERC-4337 Smart Account](https://eips.ethereum.org/EIPS/eip-4337) contract which has not been deployed.

Viem offers two ways of performing a Deployless Call, via:

*   [Bytecode](https://viem.sh/docs/contract/readContract#bytecode)
*   a [Deploy Factory](https://viem.sh/docs/contract/readContract#deploy-factory): "temporarily deploys" a contract with a provided [Deploy Factory](https://docs.alchemy.com/docs/create2-an-alternative-to-deriving-contract-addresses#create2-contract-factory), and calls the function on the deployed contract.

#### Bytecode

The example below demonstrates how we can utilize a Deployless Call **via Bytecode** to call the `name` function on the [Wagmi Example ERC721 contract](https://etherscan.io/address/0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2#code) which has not been deployed:

    import { parseAbi } from 'viem'
    import { publicClient } from './config'
     
    const data = await publicClient.readContract({
      abi: parseAbi(['function name() view returns (string)']),
      code: '0x...', // Accessible here: https://etherscan.io/address/0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2#code
      functionName: 'name'
    })

#### Deploy Factory

The example below demonstrates how we can utilize a Deployless Call **via a [Deploy Factory](https://docs.alchemy.com/docs/create2-an-alternative-to-deriving-contract-addresses#create2-contract-factory)** to call the `entryPoint` function on an [ERC-4337 Smart Account](https://eips.ethereum.org/EIPS/eip-4337) which has not been deployed:

    import { encodeFunctionData, parseAbi } from 'viem'
    import { account, publicClient } from './config'
     
    const data = await publicClient.readContract({
      // Address of the Smart Account deployer (factory).
      factory: '0xE8Df82fA4E10e6A12a9Dab552bceA2acd26De9bb',
     
      // Function to execute on the factory to deploy the Smart Account.
      factoryData: encodeFunctionData({
        abi: parseAbi(['function createAccount(address owner, uint256 salt)']),
        functionName: 'createAccount',
        args: [account, 0n],
      }),
     
      // Function to call on the Smart Account.
      abi: account.abi,
      address: account.address,
      functionName: 'entryPoint',
    })

Return Value
------------

The response from the contract. Type is inferred.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'totalSupply',
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'totalSupply',
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'totalSupply', 
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const data = await publicClient.readContract({
      address: '0x1dfe7ca09e99d10835bf73044a23b73fc20623df',
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'] 
    })

### account (optional)

*   **Type:** `Account | Address`

Optional Account sender override.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'totalSupply',
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### blockNumber (optional)

*   **Type:** `number`

The block number to perform the read against.

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'totalSupply',
      blockNumber: 15121123n, 
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

The block tag to perform the read against.

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'totalSupply',
      blockTag: 'safe', 
    })

### factory (optional)

*   **Type:**

Contract deployment factory address (ie. Create2 factory, Smart Account factory, etc).

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'totalSupply',
      factory: '0x0000000000ffe8b47b3e2130213b802212439497', 
      factoryData: '0xdeadbeef',
    })

### factoryData (optional)

*   **Type:**

Calldata to execute on the factory to deploy the contract.

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'totalSupply',
      factory: '0x0000000000ffe8b47b3e2130213b802212439497',
      factoryData: '0xdeadbeef', 
    })

### stateOverride (optional)

*   **Type:** [`StateOverride`](https://viem.sh/docs/glossary/types#stateoverride)

The state override set is an optional address-to-state mapping, where each entry specifies some state to be ephemerally overridden prior to executing the call.

    const data = await publicClient.readContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'totalSupply',
      stateOverride: [ 
        { 
          address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
          balance: parseEther('1'), 
          stateDiff: [ 
            { 
              slot: '0x3ea2f1d0abf3fc66cf29eebb70cbd4e7fe762ef8a09bcc06c8edf641230afec0', 
              value: '0x00000000000000000000000000000000000000000000000000000000000001a4', 
            }, 
          ], 
        } 
      ], 
    })

Live Example
------------

Check out the usage of `readContract` in the live [Reading Contracts Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/contracts_reading-contracts) below.</content>
</page>

<page>
  <title>createEventFilter</title>
  <url>https://viem.sh/docs/actions/public/createEventFilter</url>
  <content>Creates a Filter to listen for new events that can be used with [`getFilterChanges`](https://viem.sh/docs/actions/public/getFilterChanges).

Usage
-----

By default, an Event Filter with no arguments will query for/listen to all events.

    import { publicClient } from './client'
     
    const filter = await publicClient.createEventFilter()
    { id: "0x345a6572337856574a76364e457a4366", type: 'event' }

Scoping
-------

You can also scope a Filter to a set of given attributes (listed below).

### Address

A Filter can be scoped to an **address**:

    import { publicClient } from './client'
     
    const filter = await publicClient.createEventFilter({
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2'
    })

### Event

A Filter can be scoped to an **event**.

The `event` argument takes in an event in ABI format – we have a [`parseAbiItem` utility](https://viem.sh/docs/abi/parseAbiItem) that you can use to convert from a human-readable event signature → ABI.

    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
     
    const filter = await publicClient.createEventFilter({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'), 
    })

By default, `event` accepts the [`AbiEvent`](https://viem.sh/docs/glossary/types#abievent) type:

    import { publicClient } from './client'
     
    const filter = await publicClient.createEventFilter(publicClient, {
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: { 
        name: 'Transfer', 
        inputs: [
          { type: 'address', indexed: true, name: 'from' },
          { type: 'address', indexed: true, name: 'to' },
          { type: 'uint256', indexed: false, name: 'value' }
        ] 
      }
    })

### Arguments

A Filter can be scoped to given **_indexed_ arguments**:

    import { parseAbiItem } from 'viem'
     
    const filter = await publicClient.createEventFilter({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      }
    })

Only indexed arguments in `event` are candidates for `args`.

A Filter Argument can also be an array to indicate that other values can exist in the position:

    import { parseAbiItem } from 'viem'
     
    const filter = await publicClient.createEventFilter({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      args: { 
        // '0xd8da...' OR '0xa5cc...' OR '0xa152...'
        from: [
          '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
          '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac',
          '0xa152f8bb749c55e9943a3a0a3111d18ee2b3f94e',
        ],
      }
    })

### Block Range

A Filter can be scoped to a **block range**:

    import { parseAbiItem } from 'viem'
     
    const filter = await publicClient.createEventFilter({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      fromBlock: 16330000n, 
      toBlock: 16330050n
    })

### Multiple Events

A Filter can be scoped to **multiple events**:

    import { parseAbi } from 'viem'
     
    const filter = await publicClient.createEventFilter({
      events: parseAbi([ 
        'event Approval(address indexed owner, address indexed sender, uint256 value)',
        'event Transfer(address indexed from, address indexed to, uint256 value)',
      ]),
    })

Note: A Filter scoped to multiple events cannot be also scoped with [indexed arguments](https://viem.sh/docs/actions/public/createEventFilter#arguments) (`args`).

### Strict Mode

By default, `createEventFilter` will include logs that [do not conform](https://viem.sh/docs/glossary/terms#non-conforming-log) to the indexed & non-indexed arguments on the `event`. viem will not return a value for arguments that do not conform to the ABI, thus, some arguments on `args` may be undefined.

    import { parseAbiItem } from 'viem'
     
    const filter = await publicClient.createEventFilter({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
    })
    const logs = await publicClient.getFilterLogs({ filter })
     
    logs[0].args
     

You can turn on `strict` mode to only return logs that conform to the indexed & non-indexed arguments on the `event`, meaning that `args` will always be defined. The trade-off is that non-conforming logs will be filtered out.

    import { parseAbiItem } from 'viem'
     
    const filter = await publicClient.createEventFilter({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      strict: true
    })
    const logs = await publicClient.getFilterLogs({ filter })
     
    logs[0].args
     

Returns
-------

[`Filter`](https://viem.sh/docs/glossary/types#filter)

Parameters
----------

### address (optional)

*   **Type:** `Address | Address[]`

The contract address or a list of addresses from which Logs should originate.

    const filter = await publicClient.createEventFilter({
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2'
    })

### event (optional)

*   **Type:** [`AbiEvent`](https://viem.sh/docs/glossary/types#abievent)

The event in ABI format.

A [`parseAbiItem` utility](https://viem.sh/docs/abi/parseAbiItem) is exported from viem that converts from a human-readable event signature → ABI.

    import { parseAbiItem } from 'viem'
     
    const filter = await publicClient.createEventFilter({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'), 
    })

### args (optional)

*   **Type:** Inferred.

A list of _indexed_ event arguments.

    import { parseAbiItem } from 'viem'
     
    const filter = await publicClient.createEventFilter({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      }
    })

### fromBlock (optional)

*   **Type:** `bigint`

Block to start querying/listening from.

    const filter = await publicClient.createEventFilter({
      fromBlock: 69420n
    })

### toBlock (optional)

*   **Type:** `bigint`

Block to query/listen until.

    const filter = await publicClient.createEventFilter({
      toBlock: 70120n
    })

JSON-RPC Methods
----------------

[`eth_newFilter`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_newfilter)</content>
</page>

<page>
  <title>watchEvent</title>
  <url>https://viem.sh/docs/actions/public/watchEvent</url>
  <content>Watches and returns emitted [Event Logs](https://viem.sh/docs/glossary/terms#event-log).

This Action will batch up all the Event Logs found within the [`pollingInterval`](https://viem.sh/docs/actions/public/watchEvent#pollinginterval-optional), and invoke them via [`onLogs`](https://viem.sh/docs/actions/public/watchEvent#onlogs).

`watchEvent` will attempt to create an [Event Filter](https://viem.sh/docs/actions/public/createEventFilter) and listen to changes to the Filter per polling interval, however, if the RPC Provider does not support Filters (ie. `eth_newFilter`), then `watchEvent` will fall back to using [`getLogs`](https://viem.sh/docs/actions/public/getLogs) instead.

Usage
-----

By default, you can watch all broadcasted events to the blockchain by just passing `onLogs`.

These events will be batched up into [Event Logs](https://viem.sh/docs/glossary/terms#event-log) and sent to `onLogs`:

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const unwatch = publicClient.watchEvent({
      onLogs: logs => console.log(logs)
    })
    > [{ ... }, { ... }, { ... }] > [{ ... }, { ... }] > [{ ... }, { ... }, { ... }, { ... }]

Scoping
-------

You can also scope `watchEvent` to a set of given attributes (listed below).

### Address

`watchEvent` can be scoped to an **address**:

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const unwatch = publicClient.watchEvent({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48', 
      onLogs: logs => console.log(logs)
    })
    > [{ ... }, { ... }, { ... }] > [{ ... }, { ... }] > [{ ... }, { ... }, { ... }, { ... }]

### Event

`watchEvent` can be scoped to an **event**.

The `event` argument takes in an event in ABI format – we have a [`parseAbiItem` utility](https://viem.sh/docs/abi/parseAbiItem) that you can use to convert from a human-readable event signature → ABI.

    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const unwatch = publicClient.watchEvent({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'), 
      onLogs: logs => console.log(logs)
    })
    > [{ ... }, { ... }, { ... }] > [{ ... }, { ... }] > [{ ... }, { ... }, { ... }, { ... }]

By default, `event` accepts the [`AbiEvent`](https://viem.sh/docs/glossary/types#abievent) type:

    import { publicClient } from './client'
     
    const unwatch = publicClient.watchEvent(publicClient, {
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: { 
        name: 'Transfer', 
        inputs: [
          { type: 'address', indexed: true, name: 'from' },
          { type: 'address', indexed: true, name: 'to' },
          { type: 'uint256', indexed: false, name: 'value' }
        ] 
      },
      onLogs: logs => console.log(logs)
    })

### Arguments

`watchEvent` can be scoped to given **_indexed_ arguments** on the event:

    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
     
    const unwatch = publicClient.watchEvent({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      },
      onLogs: logs => console.log(logs)
    })
    // > [{ ... }, { ... }, { ... }]
    // > [{ ... }, { ... }]
    // > [{ ... }, { ... }, { ... }, { ... }]

Only indexed arguments in `event` are candidates for `args`.

These arguments can also be an array to indicate that other values can exist in the position:

    import { parseAbiItem } from 'viem'
     
    const unwatch = publicClient.watchEvent({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      args: { 
        // '0xd8da...' OR '0xa5cc...' OR '0xa152...'
        from: [
          '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
          '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac',
          '0xa152f8bb749c55e9943a3a0a3111d18ee2b3f94e',
        ],
      },
      onLogs: logs => console.log(logs)
    })

### Multiple Events

`watchEvent` can be scoped to **multiple events**:

    import { parseAbi } from 'viem'
     
    const unwatch = publicClient.watchEvent({
      events: parseAbi([ 
        'event Approval(address indexed owner, address indexed sender, uint256 value)',
        'event Transfer(address indexed from, address indexed to, uint256 value)',
      ]),
      onLogs: logs => console.log(logs)
    })

Note: `watchEvent` scoped to multiple events cannot be also scoped with [indexed arguments](https://viem.sh/docs/actions/public/watchEvent#arguments) (`args`).

Returns
-------

`UnwatchFn`

A function that can be invoked to stop watching for new Event Logs.

Parameters
----------

### onLogs

*   **Type:** `(logs: Log[]) => void`

The new Event Logs.

    const unwatch = publicClient.watchEvent(
      { onLogs: logs => console.log(logs) } 
    )

### address (optional)

*   **Type:** `Address | Address[]`

The contract address or a list of addresses from which Logs should originate.

    const unwatch = publicClient.watchEvent(
      { 
        address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2', 
        onLogs: logs => console.log(logs) 
      }
    )

### event (optional)

*   **Type:** [`AbiEvent`](https://viem.sh/docs/glossary/types#abievent)

The event in ABI format.

A [`parseAbiItem` utility](https://viem.sh/docs/abi/parseAbiItem) is exported from viem that converts from a human-readable event signature → ABI.

    import { parseAbiItem } from 'viem'
     
    const unwatch = publicClient.watchEvent(
      { 
        address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2',
        event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'), 
        onLogs: logs => console.log(logs) 
      }
    )

### args (optional)

*   **Type:** Inferred.

A list of _indexed_ event arguments.

    import { parseAbiItem } from 'viem'
     
    const unwatch = publicClient.watchEvent(
      { 
        address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2',
        event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
        args: { 
          from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
          to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
        },
        onLogs: logs => console.log(logs) 
      }
    )

### batch (optional)

*   **Type:** `boolean`
*   **Default:** `true`

Whether or not to batch the Event Logs between polling intervals.

    const unwatch = publicClient.watchEvent(
      { 
        batch: false, 
        onLogs: logs => console.log(logs),
      }
    )

### onError (optional)

*   **Type:** `(error: Error) => void`

Error thrown from listening for new Event Logs.

    const unwatch = publicClient.watchEvent(
      { 
        onError: error => console.log(error), 
        onLogs: logs => console.log(logs),
      }
    )

### poll (optional)

*   **Type:** `boolean`
*   **Default:** `false` for WebSocket Clients, `true` for non-WebSocket Clients

Whether or not to use a polling mechanism to check for new logs instead of a WebSocket subscription.

This option is only configurable for Clients with a [WebSocket Transport](https://viem.sh/docs/clients/transports/websocket).

    import { createPublicClient, webSocket } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const publicClient = createPublicClient({
      chain: mainnet,
      transport: webSocket()
    })
     
    const unwatch = publicClient.watchEvent(
      { 
        onLogs: logs => console.log(logs),
        poll: true, 
      }
    )

### pollingInterval (optional)

*   **Type:** `number`

Polling frequency (in ms). Defaults to the Client's `pollingInterval` config.

    const unwatch = publicClient.watchEvent(
      { 
        pollingInterval: 1_000, 
        onLogs: logs => console.log(logs),
      }
    )

### fromBlock (optional)

*   **Type:** `bigint`

The block number to start listening for logs from.

    const unwatch = publicClient.watchEvent(
      { 
        fromBlock: 1n, 
        onLogs: logs => console.log(logs),
      }
    )

Live Example
------------

Check out the usage of `watchEvent` in the live [Event Logs Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/logs_event-logs) below.

JSON-RPC Methods
----------------

**When poll `true` and RPC Provider supports `eth_newFilter`:**

*   Calls [`eth_newFilter`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_newfilter) to create a filter (called on initialize).
*   On a polling interval, it will call [`eth_getFilterChanges`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getfilterchanges).

**When poll `true` RPC Provider does not support `eth_newFilter`:**

*   Calls [`eth_getLogs`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getlogs) for each block between the polling interval.

**When poll `false` and WebSocket Transport:**

*   Uses a WebSocket subscription via `eth_subscribe` and the "logs" event.</content>
</page>

<page>
  <title>deployContract</title>
  <url>https://viem.sh/docs/contract/deployContract</url>
  <content>Deploys a contract to the network, given bytecode & constructor arguments.

Usage
-----

    import { wagmiAbi } from './abi'
    import { account, walletClient } from './config'
     
    const hash = await walletClient.deployContract({
      abi,
      account,
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
    })

### Deploying with Constructor Args

    import { deployContract } from 'viem'
    import { wagmiAbi } from './abi'
    import { account, walletClient } from './config'
     
    const hash = await walletClient.deployContract({
      abi,
      account,
      args: [69420],
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
    })

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const hash = await walletClient.deployContract({
      abi: wagmiAbi, 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
    })

### account

*   **Type:** `Account | Address`

The Account to deploy the contract from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await walletClient.deployContract({
      abi: wagmiAbi, 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
    })

### bytecode

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The contract's bytecode.

    const hash = await walletClient.deployContract({
      abi: wagmiAbi,
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...', 
    })

### args (if required)

*   **Type:** Inferred from ABI.

Constructor arguments to call upon deployment.

    const hash = await walletClient.deployContract({
      abi: wagmiAbi,
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      args: [69] 
    })

Live Example
------------

Check out the usage of `deployContract` in the live [Deploying Contracts Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/contracts_deploying-contracts) below.</content>
</page>

<page>
  <title>createContractEventFilter</title>
  <url>https://viem.sh/docs/contract/createContractEventFilter</url>
  <content>Creates a Filter to retrieve event logs that can be used with [`getFilterChanges`](https://viem.sh/docs/actions/public/getFilterChanges) or [`getFilterLogs`](https://viem.sh/docs/actions/public/getFilterLogs).

Usage
-----

By default, an Event Filter with an ABI (`abi`) will retrieve events defined on the ABI.

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi
    })
    /**
     *  {
     *    abi: [...],
     *    id: '0x345a6572337856574a76364e457a4366',
     *    type: 'event'
     *  }
     */

Scoping
-------

You can also scope a Filter to a set of given attributes (listed below).

### Address

A Filter can be scoped to an **address**:

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2'
    })

### Event

A Filter can be scoped to an **event**:

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2',
      eventName: 'Transfer'
    })

### Arguments

A Filter can be scoped to given **_indexed_ arguments**:

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2',
      eventName: 'Transfer',
      args: {  
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      }
    })

Only indexed arguments in `event` are candidates for `args`.

A Filter Argument can also be an array to indicate that other values can exist in the position:

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2',
      eventName: 'Transfer',
      args: { 
        // '0xd8da...' OR '0xa5cc...' OR '0xa152...'
        from: [
          '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
          '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac',
          '0xa152f8bb749c55e9943a3a0a3111d18ee2b3f94e',
        ],
      }
    })

### Block Range

A Filter can be scoped to a **block range**:

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2',
      eventName: 'Transfer',
      fromBlock: 16330000n, 
      toBlock: 16330050n
    })

### Strict Mode

By default, `createContractEventFilter` will include logs that [do not conform](https://viem.sh/docs/glossary/terms#non-conforming-log) to the indexed & non-indexed arguments on the `event`. viem will not return a value for arguments that do not conform to the ABI, thus, some arguments on `args` may be undefined.

    const filter = await publicClient.createContractEventFilter({
      eventName: 'Transfer',
    })
    const logs = await publicClient.getFilterLogs({ filter })
     
    logs[0].args 
    //      ^? { address?: Address, to?: Address, value?: bigint } 

You can turn on `strict` mode to only return logs that conform to the indexed & non-indexed arguments on the `event`, meaning that `args` will always be defined. The trade-off is that non-conforming logs will be filtered out.

    const filter = await publicClient.createContractEventFilter({
      eventName: 'Transfer',
      strict: true
    })
    const logs = await publicClient.getFilterLogs({ filter })
     
    logs[0].args 
    //      ^? { address: Address, to: Address, value: bigint } 

Returns
-------

[`Filter`](https://viem.sh/docs/glossary/types#filter)

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi, 
    })

### address (optional)

*   **Type:** `Address | Address[]`

The contract address or a list of addresses from which Logs should originate. If no addresses are provided, then it will query all events matching the event signatures on the ABI.

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2'
    })

### eventName (optional)

*   **Type:** `string`

The event name.

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      eventName: 'Transfer'
    })

### args (optional)

*   **Type:** Inferred.

A list of _indexed_ event arguments.

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      eventName: 'Transfer',
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      }
    })

### fromBlock (optional)

*   **Type:** `bigint`

Block to start querying/listening from.

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      fromBlock: 69420n
    })

### toBlock (optional)

*   **Type:** `bigint`

Block to query/listen until.

    const filter = await publicClient.createContractEventFilter({
      abi: wagmiAbi,
      toBlock: 70120n
    })</content>
</page>

<page>
  <title>estimateContractGas</title>
  <url>https://viem.sh/docs/contract/estimateContractGas</url>
  <content>Estimates the gas required to successfully execute a contract write function call.

Internally, `estimateContractGas` uses a [Public Client](https://viem.sh/docs/clients/public) to call the [`estimateGas` action](https://viem.sh/docs/actions/public/estimateGas) with [ABI-encoded `data`](https://viem.sh/docs/contract/encodeFunctionData).

Usage
-----

Below is a very basic example of how to estimate gas (with no arguments).

The `mint` function accepts no arguments, and returns a token ID.

    import { account, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })
    // 69420n

### Passing Arguments

If your function requires argument(s), you can pass them through with the `args` attribute.

TypeScript types for `args` will be inferred from the function name & ABI, to guard you from inserting the wrong values.

For example, the `mint` function name below requires a **tokenId** argument, and it is typed as `[number]`.

    import { account, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account,
    })
    // 69420n

Return Value
------------

`bigint`

The gas estimate.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'mint',
      account,
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint', 
      account,
    })

### account

*   **Type:** `Account | Address`

The Account to estimate gas from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      accessList: [{ 
        address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
        storageKeys: ['0x1'],
      }],
      account,
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const gas = await publicClient.estimateContractGas({
      address: '0x1dfe7ca09e99d10835bf73044a23b73fc20623df',
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'], 
      account,
    })

### dataSuffix (optional)

*   **Type:** `Hex`

Data to append to the end of the calldata. Useful for adding a ["domain" tag](https://opensea.notion.site/opensea/Seaport-Order-Attributions-ec2d69bf455041a5baa490941aad307f).

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      dataSuffix: '0xdeadbeef'
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account,
      gasPrice: parseGwei('20'), 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account,
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account,
      nonce: 69
    })

### value (optional)

*   **Type:** `number`

Value in wei sent with this transaction.

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account,
      value: parseEther('1') 
    })

### blockNumber (optional)

*   **Type:** `number`

The block number to perform the read against.

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
      blockNumber: 15121123n, 
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

The block tag to perform the read against.

    const gas = await publicClient.estimateContractGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
      blockTag: 'safe', 
    })</content>
</page>

<page>
  <title>simulateContract</title>
  <url>https://viem.sh/docs/contract/simulateContract</url>
  <content>The `simulateContract` function **simulates**/**validates** a contract interaction. This is useful for retrieving **return data** and **revert reasons** of contract write functions.

This function does not require gas to execute and _**does not**_ change the state of the blockchain. It is almost identical to [`readContract`](https://viem.sh/docs/contract/readContract), but also supports contract write functions.

Internally, `simulateContract` uses a [Public Client](https://viem.sh/docs/clients/public) to call the [`call` action](https://viem.sh/docs/actions/public/call) with [ABI-encoded `data`](https://viem.sh/docs/contract/encodeFunctionData).

Usage
-----

Below is a very basic example of how to simulate a write function on a contract (with no arguments).

The `mint` function accepts no arguments, and returns a token ID.

    import { account, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })

### Passing Arguments

If your function requires argument(s), you can pass them through with the `args` attribute.

TypeScript types for `args` will be inferred from the function name & ABI, to guard you from inserting the wrong values.

For example, the `mint` function name below requires a **tokenId** argument, and it is typed as `[number]`.

    import { account, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420], 
      account,
    })

### Pairing with `writeContract`

The `simulateContract` function also pairs well with `writeContract`.

In the example below, we are **validating** if the contract write will be successful via `simulateContract`. If no errors are thrown, then we are all good. After that, we perform a contract write to execute the transaction.

    import { account, walletClient, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const { request } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })
    const hash = await walletClient.writeContract(request)

### Handling Custom Errors

In the example below, we are **catching** a [custom error](https://blog.soliditylang.org/2021/04/21/custom-errors/) thrown by the `simulateContract`. It is important to include the custom error item in the contract `abi`.

You can access the custom error through the `data` attribute of the error:

    import { BaseError, ContractFunctionRevertedError } from 'viem';
    import { account, walletClient, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    try {
      await publicClient.simulateContract({
        address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
        abi: wagmiAbi,
        functionName: 'mint',
        account,
      })
    } catch (err) {
      if (err instanceof BaseError) {
        const revertError = err.walk(err => err instanceof ContractFunctionRevertedError)
        if (revertError instanceof ContractFunctionRevertedError) {
          const errorName = revertError.data?.errorName ?? ''
          // do something with `errorName`
        }
      }
    }

### State Overrides

When using `simulateContract`, there sometimes needs to be an initial state change to make the transaction pass. A common use case would be an approval. For that, there are [state overrides](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-eth#eth-call). In the example below, we are simulating sending a token on behalf of another user. To do this, we need to modify the state of the token contract to have maximum approve from the token owner.

    import { account, publicClient } from './config'
    import { abi, address } from './contract'
     
    // Allowance slot: A 32 bytes hex string representing the allowance slot of the sender.
    const allowanceSlot = '0x....'
     
    // Max allowance: A 32 bytes hex string representing the maximum allowance (2^256 - 1)
    const maxAllowance = numberToHex(maxUint256)
     
    const { result } = await publicClient.simulateContract({
      abi,
      address,
      account,
      functionName: 'transferFrom',
      args: [
        '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
        account.address, 
        69420n
      ],
      stateOverride: [ 
        { 
          // modifying the state of the token contract 
          address, 
          stateDiff: [ 
            { 
              slot: allowanceSlot, 
              value: maxAllowance, 
            }, 
          ], 
        }, 
      ], 
    })
     
    console.log(result)
    Output: true

Return Value
------------

The simulation result and write request. Type is inferred.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'mint',
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### account

*   **Type:** `Account | Address | null`

The Account to simulate the contract method from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc). If set to `null`, it is assumed that the transport will handle the filling the sender of the transaction.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      accessList: [{ 
        address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
        storageKeys: ['0x1'],
      }],
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### authorizationList (optional)

*   **Type:** `AuthorizationList`

Signed EIP-7702 Authorization list.

    const authorization = await walletClient.signAuthorization({ 
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
    }) 
     
    const { result } = await publicClient.simulateContract({
      address: account.address,
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      authorizationList: [authorization], 
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const { result } = await publicClient.simulateContract({
      address: '0x1dfe7ca09e99d10835bf73044a23b73fc20623df',
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'], 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### blockNumber (optional)

*   **Type:** `number`

The block number to perform the read against.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      blockNumber: 15121123n, 
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

The block tag to perform the read against.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      blockTag: 'safe', 
    })

### dataSuffix (optional)

*   **Type:** `Hex`

Data to append to the end of the calldata. Useful for adding a ["domain" tag](https://opensea.notion.site/opensea/Seaport-Order-Attributions-ec2d69bf455041a5baa490941aad307f).

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      dataSuffix: '0xdeadbeef'
    })

### gas (optional)

*   **Type:** `bigint`

The gas limit for the transaction.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      gas: 69420n, 
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      gasPrice: parseGwei('20'), 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      nonce: 69
    })

### stateOverride (optional)

*   **Type:** [`StateOverride`](https://viem.sh/docs/glossary/types#stateoverride)

The state override set is an optional address-to-state mapping, where each entry specifies some state to be ephemerally overridden prior to executing the call.

> Note: By using state overrides, you simulate the contract based on a fake state. Using this is useful for testing purposes, but making a transaction based on the returned `request` object might fail regardless of the simulation result.

    const data = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      stateOverride: [ 
        { 
          address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
          balance: parseEther('1'), 
          stateDiff: [ 
            { 
              slot: '0x3ea2f1d0abf3fc66cf29eebb70cbd4e7fe762ef8a09bcc06c8edf641230afec0', 
              value: '0x00000000000000000000000000000000000000000000000000000000000001a4', 
            }, 
          ], 
        } 
      ], 
    })

### value (optional)

*   **Type:** `number`

Value in wei sent with this transaction.

    const { result } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      value: parseEther('1') 
    })

Live Example
------------

Check out the usage of `simulateContract` in the live [Writing to Contracts Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/contracts_writing-to-contracts) below.</content>
</page>

<page>
  <title>decodeEventLog</title>
  <url>https://viem.sh/docs/contract/decodeEventLog</url>
  <content>Decodes ABI encoded event topics & data (from an [Event Log](https://viem.sh/docs/glossary/terms#event-log)) into an event name and structured arguments (both indexed & non-indexed).

Install
-------

    import { decodeEventLog } from 'viem'

Usage
-----

    import { decodeEventLog } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const topics = decodeEventLog({
      abi: wagmiAbi,
      data: '0x0000000000000000000000000000000000000000000000000000000000000001',
      topics: [
        '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
        '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
        '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
      ]
    })
    /**
     *  {
     *    eventName: 'Transfer',
     *    args: {
     *      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
     *      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
     *      value: 1n
     *    }
     *  }
     */

### Partial Decode

By default, if the `topics` and `data` does not conform to the ABI (a mismatch between the number of indexed/non-indexed arguments), `decodeEventLog` will throw an error.

For example, the following will throw an error as there is a mismatch in non-`indexed` arguments & `data` length.

    decodeEventLog({
      abi: parseAbi(['event Transfer(address indexed, address, uint256)']), 
      // `data` should be 64 bytes, but is only 32 bytes. 
      data: '0x0000000000000000000000000000000000000000000000000000000000000001', 
      topics: [
        '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
        '0x000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      ]
    })
    // [DecodeLogDataMismatch]: Data size of 32 bytes is too small for non-indexed event parameters.

It is possible for `decodeEventLog` to try and partially decode the Log, this can be done by setting the `strict` argument to `false`:

    decodeEventLog({ 
      abi: parseAbi(['event Transfer(address indexed, address, uint256)']), 
      data: '0x0000000000000000000000000000000000000000000000000000000000000001', 
      topics: [
        '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
        '0x000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      ],
      strict: false
    })
    /**
     * {
     *   eventName: 'Transfer',
     *   args: ['0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266']
     * }
     */

Return Value
------------

    {
      eventName: string;
      args: Inferred;
    }

Decoded ABI event topics.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const topics = decodeEventLog({
      abi: wagmiAbi, 
      data: '0x0000000000000000000000000000000000000000000000000000000000000001',
      topics: [
        '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
        '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
        '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
      ]
    })

### topics

*   **Type:** `[Hex, ...(Hex | Hex[] | null)[]]`

A set of topics (encoded indexed args) from the [Event Log](https://viem.sh/docs/glossary/terms#event-log).

    const topics = decodeEventLog({
      abi: wagmiAbi,
      data: '0x0000000000000000000000000000000000000000000000000000000000000001',
      topics: [ 
        '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
        '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
        '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
      ]
    })

### data (optional)

*   **Type:** `string`

The data (encoded non-indexed args) from the [Event Log](https://viem.sh/docs/glossary/terms#event-log).

    const topics = decodeEventLog({
      abi: wagmiAbi,
      data: '0x0000000000000000000000000000000000000000000000000000000000000001', 
      topics: [
        '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
        '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
        '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
      ]
    })

### eventName (optional)

*   **Type:** `string`

An event name from the ABI. Provide an `eventName` to infer the return type of `decodeEventLog`.

    const topics = decodeEventLog({
      abi: wagmiAbi,
      eventName: 'Transfer', 
      topics: [
        '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
        '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
        '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
      ]
    })

### strict (optional)

*   **Type:** `boolean`
*   **Default:** `true`

If `true`, `decodeEventLog` will throw an error if the `data` & `topics` lengths to not conform to the event on the ABI. If `false`, `decodeEventLog` will try and [partially decode](https://viem.sh/docs/contract/decodeEventLog#partial-decode).

    const topics = decodeEventLog({
      abi: wagmiAbi,
      strict: false, 
      topics: [
        '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
        '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
        '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
      ]
    })</content>
</page>

<page>
  <title>writeContract</title>
  <url>https://viem.sh/docs/contract/writeContract</url>
  <content>Executes a write function on a contract.

A "write" function on a Solidity contract modifies the state of the blockchain. These types of functions require gas to be executed, and hence a [Transaction](https://viem.sh/docs/glossary/terms) is needed to be broadcast in order to change the state.

Internally, `writeContract` uses a [Wallet Client](https://viem.sh/docs/clients/wallet) to call the [`sendTransaction` action](https://viem.sh/docs/actions/wallet/sendTransaction) with [ABI-encoded `data`](https://viem.sh/docs/contract/encodeFunctionData).

Usage
-----

Below is a very basic example of how to execute a write function on a contract (with no arguments).

While you can use `writeContract` [by itself](https://viem.sh/docs/contract/writeContract#standalone), it is highly recommended to pair it with [`simulateContract`](https://viem.sh/docs/contract/simulateContract) to validate that the contract write will execute without errors.

    import { account, publicClient, walletClient } from './config'
    import { wagmiAbi } from './abi'
     
    const { request } = await publicClient.simulateContract({
      account,
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
    })
    await walletClient.writeContract(request)

### Passing Arguments

If your function requires argument(s), you can pass them through with the `args` attribute.

TypeScript types for `args` will be inferred from the function name & ABI, to guard you from inserting the wrong values.

For example, the `mint` function name below requires a **tokenId** argument, and it is typed as `[number]`.

    import { account, walletClient } from './client'
    import { wagmiAbi } from './abi'
     
    const { request } = await publicClient.simulateContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account
    })
    await walletClient.writeContract(request)

### Standalone

If you don't need to perform validation on the contract write, you can also use it by itself:

    import { account, walletClient } from './config'
    import { wagmiAbi } from './abi'
     
    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })

Return Value
------------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

A [Transaction Hash](https://viem.sh/docs/glossary/terms#hash).

Unlike [`readContract`](https://viem.sh/docs/contract/readContract), `writeContract` only returns a [Transaction Hash](https://viem.sh/docs/glossary/terms#hash). If you would like to retrieve the return data of a write function, you can use the [`simulateContract` action](https://viem.sh/docs/contract/simulateContract) – this action does not execute a transaction, and does not require gas (it is very similar to `readContract`).

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420]
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'mint',
      args: [69420]
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint', 
      args: [69420]
    })

### account

*   **Type:** `Account | Address | null`

The Account to write to the contract from.

Accepts a [JSON-RPC Account (or Address)](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc). If set to `null`, it is assumed that the transport will handle the filling the sender of the transaction.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      accessList: [{ 
        address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
        storageKeys: ['0x1'],
      }],
    })

### authorizationList (optional)

*   **Type:** `AuthorizationList`

Signed EIP-7702 Authorization list.

    const authorization = await walletClient.signAuthorization({ 
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
    }) 
     
    await walletClient.writeContract({
      address: account.address,
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      authorizationList: [authorization], 
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420] 
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

The chain is also used to infer its request type (e.g. the Celo chain has a `gatewayFee` that you can pass through to `sendTransaction`).

    import { optimism } from 'viem/chains'
     
    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      chain: optimism, 
    })

### dataSuffix

*   **Type:** `Hex`

Data to append to the end of the calldata. Useful for adding a ["domain" tag](https://opensea.notion.site/opensea/Seaport-Order-Attributions-ec2d69bf455041a5baa490941aad307f).

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      dataSuffix: '0xdeadbeef'
    })

### gas (optional)

*   **Type:** `bigint`

The gas limit for the transaction. Note that passing a gas limit also skips the gas estimation step.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      gas: 69420n, 
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      gasPrice: parseGwei('20'), 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      nonce: 69
    })

### value (optional)

*   **Type:** `number`

Value in wei sent with this transaction.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      value: parseEther('1') 
    })

Live Example
------------

Check out the usage of `writeContract` in the live [Writing to Contracts Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/contracts_writing-to-contracts) below.</content>
</page>

<page>
  <title>watchContractEvent</title>
  <url>https://viem.sh/docs/contract/watchContractEvent</url>
  <content>Watches and returns emitted contract event logs.

This Action will batch up all the event logs found within the [`pollingInterval`](https://viem.sh/docs/contract/watchContractEvent#pollinginterval-optional), and invoke them via [`onLogs`](https://viem.sh/docs/contract/watchContractEvent#onlogs).

`watchContractEvent` will attempt to create an [Event Filter](https://viem.sh/docs/contract/createContractEventFilter) and listen to changes to the Filter per polling interval, however, if the RPC Provider does not support Filters (ie. `eth_newFilter`), then `watchContractEvent` will fall back to using [`getLogs`](https://viem.sh/docs/actions/public/getLogs) instead.

Usage
-----

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      onLogs: logs => console.log(logs)
    })
    // > [{ ... }, { ... }, { ... }]
    // > [{ ... }, { ... }]
    // > [{ ... }, { ... }, { ... }, { ... }]

### Scoping to an Event Name

You can scope to an event on the given ABI.

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      eventName: 'Transfer',
      onLogs: logs => console.log(logs)
    })
    // > [{ ... }, { ... }, { ... }]
    // > [{ ... }, { ... }]
    // > [{ ... }, { ... }, { ... }, { ... }]

### Scoping to Event Arguments

You can scope to given **indexed event arguments**.

In the example below, we want to filter out `Transfer`s that were sent by the address `"0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b"`.

> Only **`indexed`** arguments on the event ABI are candidates for `args` (see `abi.ts`).

    import { publicClient } from './client'
    import { wagmiAbi } from './abi'
     
    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      eventName: 'Transfer',
      args: { from: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b' },
      onLogs: logs => console.log(logs)
    })
    // > [{ ... }, { ... }, { ... }]
    // > [{ ... }, { ... }]
    // > [{ ... }, { ... }, { ... }, { ... }]

Returns
-------

`UnwatchFn`

A function that can be invoked to stop watching for new event logs.

Arguments
---------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      onLogs: logs => console.log(logs)
    })

### onLogs

*   **Type:** `(Log[]) => void`

The new event logs.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      onLogs: logs => console.log(logs) 
    })

### address (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address. If no address is provided, then it will emit all events matching the event signatures on the ABI.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      onLogs: logs => console.log(logs)
    })

### args (optional)

*   **Type:** Inferred from ABI.

Event arguments to filter logs.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      eventName: 'Transfer', 
      args: ['0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b'], 
      onLogs: logs => console.log(logs)
    })

### eventName (optional)

*   **Type:** `string`

An event name to filter logs.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      eventName: 'Transfer', 
      onLogs: logs => console.log(logs)
    })

### batch (optional)

*   **Type:** `boolean`
*   **Default:** `true`

Whether or not to batch logs between polling intervals.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      batch: false, 
      onLogs: logs => console.log(logs)
    })

### onError (optional)

*   **Type:** `(error: Error) => void`

Error thrown from listening for new event logs.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      onError: error => console.log(error), 
      onLogs: logs => console.log(logs)
    })

### poll (optional)

*   **Type:** `boolean`
*   **Default:** `false` for WebSocket Clients, `true` for non-WebSocket Clients

Whether or not to use a polling mechanism to check for new logs instead of a WebSocket subscription.

This option is only configurable for Clients with a [WebSocket Transport](https://viem.sh/docs/clients/transports/websocket).

    import { createPublicClient, webSocket } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const publicClient = createPublicClient({
      chain: mainnet,
      transport: webSocket()
    })
     
    const unwatch = publicClient.watchContractEvent(
      { 
        address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
        abi: wagmiAbi,
        poll: true, 
      }
    )

### pollingInterval (optional)

*   **Type:** `number`

Polling frequency (in ms). Defaults to the Client's `pollingInterval` config.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      pollingInterval: 1_000, 
      onLogs: logs => console.log(logs)
    })

### fromBlock (optional)

*   **Type:** `bigint`

The block number to start listening for logs from.

    const unwatch = publicClient.watchContractEvent({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      onLogs: logs => console.log(logs),
      fromBlock: 1n
    })

JSON-RPC Methods
----------------

**When poll `true` and RPC Provider supports `eth_newFilter`:**

*   Calls [`eth_newFilter`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_newfilter) to create a filter (called on initialize).
*   On a polling interval, it will call [`eth_getFilterChanges`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getfilterchanges).

**When poll `true` RPC Provider does not support `eth_newFilter`:**

*   Calls [`eth_getLogs`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getlogs) for each block between the polling interval.

**When poll `false` and WebSocket Transport:**

*   Uses a WebSocket subscription via `eth_subscribe` and the "logs" event.</content>
</page>

<page>
  <title>encodeDeployData</title>
  <url>https://viem.sh/docs/contract/encodeDeployData</url>
  <content>Encodes deploy data (bytecode & constructor args) into an ABI encoded value.

Install
-------

    import { encodeDeployData } from 'viem'

Usage
-----

Below is a very basic example of how to encode deploy data.

    import { encodeDeployData } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const data = encodeDeployData({
      abi: wagmiAbi,
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...'
    })
    // 0x608060405260405161083e38038061083e833981016040819052610...

### Passing Arguments

If your constructor requires argument(s), you can pass them through with the `args` attribute.

TypeScript types for `args` will be inferred from the constructor & ABI, to guard you from inserting the wrong values.

For example, the `constructor` below requires an **address** argument, and it is typed as `["0x${string}"]`.

    import { encodeDeployData } from 'viem'
    import { wagmiAbi } from './abi'
     
    const data = encodeDeployData({
      abi: wagmiAbi,
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']
    })
    // 0x608060405260405161083e38038061083e833981016040819052610...00000000000000000000000000000000a5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC

Return Value
------------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

ABI encoded data (bytecode & constructor arguments).

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const data = encodeDeployData({
      abi: wagmiAbi, 
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']
    })

### bytecode

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

Contract bytecode.

    const data = encodeDeployData({
      abi: wagmiAbi,
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...', 
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const data = encodeDeployData({
      abi: wagmiAbi,
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'] 
    })</content>
</page>

<page>
  <title>decodeFunctionResult</title>
  <url>https://viem.sh/docs/contract/decodeFunctionResult</url>
  <content>Decodes the result of a function call on a contract.

Install
-------

    import { decodeFunctionResult } from 'viem'

Usage
-----

Given an ABI (`abi`) and a function (`functionName`), pass through the encoded calldata (`data`) to retrieve the decoded value:

    import { decodeFunctionResult } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const value = decodeFunctionResult({
      abi: wagmiAbi,
      functionName: 'ownerOf',
      data: '0x000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac'
    })
    // '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'

### Without `functionName`

If your `abi` contains only one ABI item, you can omit the `functionName` (it becomes optional):

    import { decodeFunctionResult } from 'viem'
    import { abiItem } from './abi.ts'
     
    const value = decodeFunctionResult({
      abi: [abiItem],
      functionName: 'ownerOf', 
      data: '0x000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac'
    })
    // '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'

### A more complex example

    import { decodeFunctionResult } from 'viem'
     
    const value = decodeFunctionResult({
      abi: wagmiAbi,
      functionName: 'getInfo',
      data: '0x000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac0000000000000000000000000000000000000000000000000000000000010f2c0000000000000000000000000000000000000000000000000000000000000001000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac0000000000000000000000000000000000000000000000000000000000000045'
    })
    /**
     * {
     *  foo: {
     *    sender: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
     *    x: 69420n,
     *    y: true
     *  },
     *  sender: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
     *  z: 69
     * }
     */

Return Value
------------

The decoded data. Type is inferred from the ABI.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const value = decodeFunctionResult({
      abi: wagmiAbi, 
      functionName: 'ownerOf',
      data: '0x000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac'
    })

### functionName

*   **Type:** `string`

The function to encode from the ABI.

    const value = decodeFunctionResult({
      abi: wagmiAbi,
      functionName: 'ownerOf', 
      data: '0x000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac'
    })

### data

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The calldata.

    const value = decodeFunctionResult({
      abi: wagmiAbi,
      functionName: 'ownerOf',
      data: '0x000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac'
    })</content>
</page>

<page>
  <title>encodeErrorResult</title>
  <url>https://viem.sh/docs/contract/encodeErrorResult</url>
  <content>    import { decodeErrorResult } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const value = encodeErrorResult({
      abi: wagmiAbi,
      errorName: 'InvalidTokenError',
      args: ['sold out']
    })
    // 0xb758934b000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000b68656c6c6f20776f726c64000000000000000000000000000000000000000000</content>
</page>

<page>
  <title>encodeEventTopics</title>
  <url>https://viem.sh/docs/contract/encodeEventTopics</url>
  <content>[Skip to content](https://viem.sh/docs/contract/encodeEventTopics#vocs-content)

Encodes an event (with optional arguments) into filter topics.

Install
-------

    import { encodeEventTopics } from 'viem'

Usage
-----

Below is a very basic example of how to encode event topics without arguments.

    import { encodeEventTopics } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const topics = encodeEventTopics({
      abi: wagmiAbi,
      eventName: 'Transfer'
    })
    // ["0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0"]

### Passing Arguments

If your event has indexed parameters, you can pass their values through with the `args` attribute.

TypeScript types for `args` will be inferred from the event name & ABI, to guard you from inserting the wrong values.

For example, the `Transfer` event below accepts an **address** argument for the `from` and `to` attributes, and it is typed as `"0x${string}"`.

    import { encodeEventTopics } from 'viem'
     
    const topics = encodeEventTopics({
      abi: wagmiAbi,
      eventName: 'Transfer'
      args: {
        from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
      }
    })
    // ["0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0", "0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266", "0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8"]

### Without `eventName`

If your `abi` contains only one ABI item, you can omit the `eventName` (it becomes optional):

    import { encodeEventTopics } from 'viem'
     
    const abiItem = {
      inputs: [
        {
          indexed: true,
          name: 'from',
          type: 'address',
        },
        { indexed: true, name: 'to', type: 'address' },
        {
          indexed: false,
          name: 'value',
          type: 'uint256',
        },
      ],
      name: 'Transfer',
      type: 'event',
    }
     
    const topics = encodeEventTopics({
      abi: [abiItem],
      eventName: 'Transfer'
    })
    // ["0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0"]

Return Value
------------

Encoded topics.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const data = encodeEventTopics({
      abi: wagmiAbi, 
      functionName: 'Transfer',
    })

### eventName

*   **Type:** `string`

Name of the event.

    const data = encodeEventTopics({
      abi: wagmiAbi,
      eventName: 'Transfer', 
    })

### args (optional)

*   **Type:** `string`

A list of _indexed_ event arguments.

    const data = encodeEventTopics({
      abi: wagmiAbi,
      eventName: 'Transfer',
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      }
    })</content>
</page>

<page>
  <title>encodeFunctionData</title>
  <url>https://viem.sh/docs/contract/encodeFunctionData</url>
  <content>[Skip to content](https://viem.sh/docs/contract/encodeFunctionData#vocs-content)

Encodes the function name and parameters into an ABI encoded value (4 byte selector & arguments).

Install
-------

    import { encodeFunctionData } from 'viem'

Usage
-----

Below is a very basic example of how to encode a function to calldata.

    import { encodeFunctionData } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const data = encodeFunctionData({
      abi: wagmiAbi,
      functionName: 'totalSupply'
    })

### Passing Arguments

If your function requires argument(s), you can pass them through with the `args` attribute.

TypeScript types for `args` will be inferred from the function name & ABI, to guard you from inserting the wrong values.

For example, the `balanceOf` function name below requires an **address** argument, and it is typed as `["0x${string}"]`.

    import { encodeFunctionData } from 'viem'
    import { wagmiAbi } from './abi'
     
    const data = encodeFunctionData({
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']
    })

### Without `functionName`

If your `abi` contains only one ABI item, you can omit the `functionName` (it becomes optional):

    import { encodeFunctionData } from 'viem'
     
    const abiItem = {
      inputs: [{ name: 'owner', type: 'address' }],
      name: 'balanceOf',
      outputs: [{ name: '', type: 'uint256' }],
      stateMutability: 'view',
      type: 'function',
    }
     
    const data = encodeFunctionData({
      abi: [abiItem],
      functionName: 'balanceOf', 
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']
    })

### Preparation (Performance Optimization)

If you are calling the same function multiple times, you can prepare the function selector once and reuse it.

    import { prepareEncodeFunctionData, encodeFunctionData } from 'viem'
     
    const transfer = prepareEncodeFunctionData({
      abi: erc20Abi,
      functionName: 'transfer',
    })
     
    for (const address of addresses) {
      const data = encodeFunctionData({
        ...transfer,
        args: [address, 69420n],
      })
    }

Return Value
------------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

ABI encoded data (4byte function selector & arguments).

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const data = encodeFunctionData({
      abi: wagmiAbi, 
      functionName: 'totalSupply',
    })

### functionName

*   **Type:** `string`

The function to encode from the ABI.

    const data = encodeFunctionData({
      abi: wagmiAbi,
      functionName: 'totalSupply', 
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const data = encodeFunctionData({
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'] 
    })</content>
</page>

<page>
  <title>encodePacked</title>
  <url>https://viem.sh/docs/abi/encodePacked</url>
  <content>Generates [ABI non-standard packed encoded data](https://docs.soliditylang.org/en/v0.8.18/abi-spec#non-standard-packed-mode) given a set of solidity types compatible with packed encoding.

Import
------

    import { encodePacked } from 'viem'

Usage
-----

    encodePacked(
      ['address', 'string', 'bytes16[]'], 
      [
        '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
        'hello world',
        ['0xdeadbeefdeadbeefdeadbeefdeadbeef', '0xcafebabecafebabecafebabecafebabe']
      ]
    )
    // 0xd8da6bf26964af9d7eed9e03e53415d37aa9604568656c6c6f20776f726c64deadbeefdeadbeefdeadbeefdeadbeef00000000000000000000000000000000cafebabecafebabecafebabecafebabe00000000000000000000000000000000

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The encoded packed data.

Parameters
----------

### types

*   **Type**: `PackedAbiType[]`

Set of ABI types to pack encode.

    encodePacked(
      ['address', 'string', 'bytes16[]'], 
      [
        '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
        'hello world',
        ['0xdeadbeefdeadbeefdeadbeefdeadbeef', '0xcafebabecafebabecafebabecafebabe']
      ]
    )

### values

*   **Type**: [`AbiParametersToPrimitiveTypes<PackedAbiType[]>`](https://viem.sh/docs/glossary/terms#abiparameterstoprimitivetypes)

The set of primitive values that correspond to the ABI types defined in `types`.

    encodePacked(
      ['address', 'string', 'bytes16[]'],
      [ 
        '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
        'hello world',
        ['0xdeadbeefdeadbeefdeadbeefdeadbeef', '0xcafebabecafebabecafebabecafebabe']
      ]
    )</content>
</page>

<page>
  <title>getAbiItem</title>
  <url>https://viem.sh/docs/abi/getAbiItem</url>
  <content>Retrieves an item from the ABI.

Import
------

    import { getAbiItem } from 'viem'

Usage
-----

    import { getAbiItem } from 'viem'
     
    const encodedData = getAbiItem({
      abi: [
        { 
          name: 'x', 
          type: 'function', 
          inputs: [{ type: 'uint256' }], 
          outputs: [],
          stateMutability: 'payable'
        },
        { 
          name: 'y', 
          type: 'event', 
          inputs: [{ type: 'address' }], 
          outputs: [{ type: 'uint256' }],
          stateMutability: 'view'
        },
        { 
          name: 'z', 
          type: 'function', 
          inputs: [{ type: 'string' }],
          outputs: [{ type: 'uint256' }],
          stateMutability: 'view'
        }
      ],
      name: 'y',
    })
    /**
     * { 
     *  name: 'y', 
     *  type: 'event', 
     *  inputs: [{ type: 'address' }], 
     *  outputs: [{ type: 'uint256' }],
     *  stateMutability: 'view'
     * }
     */

Returns
-------

`AbiItem`

The ABI item.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const encodedData = getAbiItem({
      abi: [...], 
      name: 'x',
    })

### name

*   **Type:** `string`

Name of the ABI item to extract.

    const encodedData = getAbiItem({
      abi: [...],
      name: 'x', 
    })

You can also provide the ABI item's 4byte selector:

    const encodedData = getAbiItem({
      abi: [...],
      name: '0x70a08231', 
    })

### args (optional)

*   **Type:** Inferred.

Optional arguments to identify function overrides.

    const encodedData = getAbiItem({
      abi: [...],
      name: 'y',
      args: ['0x0000000000000000000000000000000000000000'], 
    })</content>
</page>

<page>
  <title>encodeFunctionResult</title>
  <url>https://viem.sh/docs/contract/encodeFunctionResult</url>
  <content>    import { decodeFunctionResult } from 'viem'
     
    const data = decodeFunctionResult({
      abi: wagmiAbi,
      functionName: 'getInfo',
      value: [
        {
          foo: {
            sender: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
            x: 69420n,
            y: true
          },
          sender: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
          z: 69
        }
      ]
    })
    // 0x000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac0000000000000000000000000000000000000000000000000000000000010f2c0000000000000000000000000000000000000000000000000000000000000001000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac0000000000000000000000000000000000000000000000000000000000000045</content>
</page>

<page>
  <title>decodeAbiParameters</title>
  <url>https://viem.sh/docs/abi/decodeAbiParameters</url>
  <content>[Skip to content](https://viem.sh/docs/abi/decodeAbiParameters#vocs-content)

Decodes ABI encoded data using the [ABI specification](https://solidity.readthedocs.io/en/latest/abi-spec), given a set of ABI parameters (`inputs`/`outputs`) and the encoded ABI data.

The `decodeAbiParameters` function is used by the other contract decoding utilities (ie. `decodeFunctionData`, `decodeEventLog`, etc).

Install
-------

    import { decodeAbiParameters } from 'viem'

Usage
-----

The `decodeAbiParameters` function takes in two parameters:

*   a set of ABI Parameters (`params`), that can be in the shape of the `inputs` or `outputs` attribute of an ABI Item.
*   the ABI encoded data (`data`) that correspond to the given `params`.

    import { decodeAbiParameters } from 'viem'
     
    const values = decodeAbiParameters(
      [
        { name: 'x', type: 'string' },
        { name: 'y', type: 'uint' },
        { name: 'z', type: 'bool' }
      ],
      '0x000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000001a4000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000057761676d69000000000000000000000000000000000000000000000000000000',
    )
    // ['wagmi', 420n, true]

### Human Readable

You can also pass in [Human Readable](https://viem.sh/docs/glossary/terms#human-readable-abi) parameters with the [`parseAbiParameters` utility](https://viem.sh/docs/abi/parseAbiParameters).

    import { decodeAbiParameters, parseAbiParameters } from 'viem'
     
    const values = decodeAbiParameters(
      parseAbiParameters('string x, uint y, bool z'),
      '0x000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000001a4000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000057761676d69000000000000000000000000000000000000000000000000000000'
    )
    // ['wagmi', 420n, true]

Return Value
------------

The decoded data. Type is inferred from the ABI.

Parameters
----------

### params

*   **Type**: [`AbiParameter[]`](https://viem.sh/docs/glossary/types#abiparameter)

The set of ABI parameters to decode against `data`, in the shape of the `inputs` or `outputs` attribute of an ABI event/function.

These parameters must include valid [ABI types](https://docs.soliditylang.org/en/develop/abi-spec#types).

    const values = decodeAbiParameters(
      [{ name: 'x', type: 'uint32' }], 
      '0x0000000000000000000000000000000000000000000000000000000000010f2c',
    )

### data

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The ABI encoded data.

    const values = decodeAbiParameters(
      [{ name: 'x', type: 'uint32' }],
      '0x0000000000000000000000000000000000000000000000000000000000010f2c', 
    )

More Examples
-------------

### Simple struct

    import { abi } from './abi'
     
    const values = decodeAbiParameters(
      abi[0].outputs,
      '0x00000000000000000000000000000000000000000000000000000000000001a40000000000000000000000000000000000000000000000000000000000000001000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac',
    )
    // { x: 420n, y: true, z: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC' }

### Simple bytes

A simple `bytes` that contains an ABI-encoded `uint256` value.

    const values = decodeAbiParameters(
      [
        { name: "response", type: "bytes" },
      ],
      '0x' +
      '0000000000000000000000000000000000000000000000000000000000000020' + // offset pointer
      '0000000000000000000000000000000000000000000000000000000000000020' + // length
      '0000000000000000000000000000000000000000000000000000000000000001',  // data
    )
    // 0x0000000000000000000000000000000000000000000000000000000000000001</content>
</page>

<page>
  <title>encodeAbiParameters</title>
  <url>https://viem.sh/docs/abi/encodeAbiParameters</url>
  <content>Generates ABI encoded data using the [ABI specification](https://docs.soliditylang.org/en/latest/abi-spec.html), given a set of ABI parameters (`inputs`/`outputs`) and their corresponding values.

The `encodeAbiParameters` function is used by the other contract encoding utilities (ie. `encodeFunctionData`, `encodeEventTopics`, etc).

Import
------

    import { encodeAbiParameters } from 'viem'

Usage
-----

The `encodeAbiParameters` function takes in two parameters:

*   a set of ABI Parameters (`params`), that can be in the shape of the `inputs` or `outputs` attribute of an ABI Item.
*   a set of values (`values`) that correspond to the given `params`.

    import { encodeAbiParameters } from 'viem'
     
    const encodedData = encodeAbiParameters(
      [
        { name: 'x', type: 'string' },
        { name: 'y', type: 'uint' },
        { name: 'z', type: 'bool' }
      ],
      ['wagmi', 420n, true]
    )
    // 0x000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000001a4000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000057761676d69000000000000000000000000000000000000000000000000000000

### Human Readable

You can also pass in [Human Readable](https://viem.sh/docs/glossary/terms#human-readable-abi) parameters with the [`parseAbiParameters` utility](https://viem.sh/docs/abi/parseAbiParameters).

    import { encodeAbiParameters, parseAbiParameters } from 'viem'
     
    const encodedData = encodeAbiParameters(
      parseAbiParameters('string x, uint y, bool z'),
      ['wagmi', 420n, true]
    )
    // 0x000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000001a4000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000057761676d69000000000000000000000000000000000000000000000000000000

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The ABI encoded data.

Parameters
----------

### params

*   **Type**: [`AbiParameter[]`](https://viem.sh/docs/glossary/terms#abiparameter)

The set of ABI parameters to encode, in the shape of the `inputs` or `outputs` attribute of an ABI event/function.

These parameters must include valid [ABI types](https://docs.soliditylang.org/en/develop/abi-spec#types).

    encodeAbiParameters(
      [{ name: 'x', type: 'uint32' }], 
      [69420]
    )

### values

*   **Type**: [`AbiParametersToPrimitiveTypes<AbiParameter[]>`](https://viem.sh/docs/glossary/terms#abiparameterstoprimitivetypes)

The set of primitive values that correspond to the ABI types defined in `params`.

    encodeAbiParameters(
      [{ name: 'x', type: 'uint32' }],
      [69420] 
    )

More Examples
-------------

### Simple struct

    import { abi } from './abi'
     
    const encodedData = encodeAbiParameters(
      abi[0].inputs,
      [{
        x: 420n,
        y: true,
        z: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      }],
    )
    // 0x00000000000000000000000000000000000000000000000000000000000001a40000000000000000000000000000000000000000000000000000000000000001000000000000000000000000a5cc3c03994db5b0d9a5eedd10cabab0813678ac</content>
</page>

<page>
  <title>parseAbi</title>
  <url>https://viem.sh/docs/abi/parseAbi</url>
  <content>Parses human-readable ABI into JSON [`Abi`](https://viem.sh/docs/glossary/types#abi). Re-exported from [ABIType](https://abitype.dev/api/human#parseabi-1).

Import
------

    import { parseAbi } from 'viem'

Usage
-----

    import { parseAbi } from 'viem'
     
    const abi = parseAbi([
      //  ^? const abi: readonly [{ name: "balanceOf"; type: "function"; stateMutability:...
      'function balanceOf(address owner) view returns (uint256)',
      'event Transfer(address indexed from, address indexed to, uint256 amount)',
    ])

Returns
-------

[`Abi`](https://viem.sh/docs/glossary/types#abi)

The JSON ABI.

Parameters
----------

### signatures

*   **Type:** `string[]`

Human-readable ABI.

    import { parseAbi } from 'viem'
     
    const abi = parseAbi([
      //  ^? const abi: readonly [{ name: "balanceOf"; type: "function"; stateMutability:...
      'function balanceOf(address owner) view returns (uint256)',
      'event Transfer(address indexed from, address indexed to, uint256 amount)',
    ])</content>
</page>

<page>
  <title>signTypedData</title>
  <url>https://viem.sh/docs/actions/wallet/signTypedData</url>
  <content>[Skip to content](https://viem.sh/docs/actions/wallet/signTypedData#vocs-content)

Signs typed data and calculates an Ethereum-specific signature in [https://eips.ethereum.org/EIPS/eip-712](https://eips.ethereum.org/EIPS/eip-712): `sign(keccak256("\x19\x01" ‖ domainSeparator ‖ hashStruct(message)))`

Usage
-----

    import { account, walletClient } from './config'
    import { domain, types } from './data'
     
    const signature = await walletClient.signTypedData({
      account,
      domain,
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### Account Hoisting

If you do not wish to pass an `account` to every `signTypedData`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#withaccount).

    import { walletClient } from './config'
    import { domain, types } from './data'
     
    const signature = await walletClient.signTypedData({
      domain,
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

Returns
-------

`0x${string}`

The signed data.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to use for signing.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const signature = await walletClient.signTypedData({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### domain

**Type:** `TypedDataDomain`

The typed data domain.

    const signature = await walletClient.signTypedData({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### types

The type definitions for the typed data.

    const signature = await walletClient.signTypedData({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: { 
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### primaryType

**Type:** Inferred `string`.

The primary type to extract from `types` and use in `value`.

    const signature = await walletClient.signTypedData({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [ 
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### message

**Type:** Inferred from `types` & `primaryType`.

    const signature = await walletClient.signTypedData({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: { 
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

Live Example
------------

Check out the usage of `signTypedData` in the live [Sign Typed Data Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/signing_typed-data) below.

JSON-RPC Methods
----------------

*   JSON-RPC Accounts:
    *   [`eth_signTypedData_v4`](https://docs.metamask.io/guide/signing-data#signtypeddata-v4)
*   Local Accounts
    *   Signs locally. No JSON-RPC request.</content>
</page>

<page>
  <title>parseAbiItem</title>
  <url>https://viem.sh/docs/abi/parseAbiItem</url>
  <content>Parses human-readable ABI item (e.g. error, event, function) into ABI item. Re-exported from [ABIType](https://abitype.dev/api/human#parseabiitem-1).

Import
------

    import { parseAbiItem } from 'viem'

Usage
-----

    import { parseAbiItem } from 'viem'
     
    const abiItem = parseAbiItem(
      //  ^? const abiItem: { name: "balanceOf"; type: "function"; stateMutability: "view";...
      'function balanceOf(address owner) view returns (uint256)',
    )

Returns
-------

[`Abi`](https://viem.sh/docs/glossary/types#abi)

Parsed ABI item.

Parameters
----------

### signatures

*   **Type:** `string[]`

Human-Readable ABI item.

    import { parseAbiItem } from 'viem'
     
    const abiItem = parseAbiItem([
      //  ^? const abiItem: { name: "foo"; type: "function"; stateMutability: "view"; inputs:...
      'function foo(Baz bar) view returns (string)',
      'struct Baz { string name; }',
    ])</content>
</page>

<page>
  <title>parseAbiParameter</title>
  <url>https://viem.sh/docs/abi/parseAbiParameter</url>
  <content>Parses human-readable ABI parameter into [`AbiParameter`](https://viem.sh/docs/glossary/types#abiparameter). Re-exported from [ABIType](https://abitype.dev/api/human#parseabiparameter-1).

Import
------

    import { parseAbiParameter } from 'viem'

Usage
-----

    import { parseAbiParameter } from 'viem'
     
    const abiParameter = parseAbiParameter('address from')
    //    ^? const abiParameter: { type: "address"; name: "from"; }

Returns
-------

[`Abi`](https://viem.sh/docs/glossary/types#abi)

Parsed ABI parameter.

Parameters
----------

### signature

*   **Type:** `string | string[]`

Human-Readable ABI parameter.

    import { parseAbiParameter } from 'viem'
     
    const abiParameter = parseAbiParameter([
      //  ^? const abiParameter: { type: "tuple"; components: [{ type: "string"; name:...
      'Baz bar',
      'struct Baz { string name; }',
    ])</content>
</page>

<page>
  <title>Introduction to Wallet Actions</title>
  <url>https://viem.sh/docs/actions/wallet/introduction</url>
  <content>Wallet Actions are actions that map one-to-one with a "wallet" or "signable" Ethereum RPC method (`eth_requestAccounts`, `eth_sendTransaction`, etc). They are used with a [Wallet Client](https://viem.sh/docs/clients/wallet).

Wallet Actions require special permissions and provide signing capabilities. Examples of Wallet Actions include [retrieving the user's account addresses](https://viem.sh/docs/actions/wallet/getAddresses), [sending a transaction](https://viem.sh/docs/actions/wallet/sendTransaction), and [signing a message](https://viem.sh/docs/actions/wallet/signMessage).

Wallet Actions provide a secure and flexible way to access the user's accounts and perform actions on the Ethereum network. They are commonly used by dapps and other applications that need to execute transactions, interact with smart contracts, or sign messages.</content>
</page>

<page>
  <title>Introduction to Test Actions</title>
  <url>https://viem.sh/docs/actions/test/introduction</url>
  <content>Test Actions are actions that map one-to-one with "test" Ethereum RPC methods (`evm_mine`, `anvil_setBalance`, `anvil_impersonate`, etc). They are used with a [Test Client](https://viem.sh/docs/clients/test).

Test Actions are used for testing and simulation purposes. Examples of Test Actions include [mining a block](https://viem.sh/docs/actions/test/mine), [setting the balance of an account](https://viem.sh/docs/actions/test/setBalance), and [impersonating accounts](https://viem.sh/docs/actions/test/impersonateAccount).

Test Actions are an essential part of viem, as they provide a way to test and simulate different scenarios on the Ethereum network. They are commonly used by developers who are building dapps and other applications that need to be tested before they are deployed to the network. By using Test Actions, developers can test the behavior of their applications in a controlled environment, without the need for a real balance or real users. This makes it easier to identify and fix bugs, and it ensures that the application will work as expected when it is deployed to the network.</content>
</page>

<page>
  <title>parseAbiParameters</title>
  <url>https://viem.sh/docs/abi/parseAbiParameters</url>
  <content>Parses human-readable ABI parameters into [`AbiParameter`s](https://viem.sh/docs/glossary/types#abiparameter). Re-exported from [ABIType](https://abitype.dev/api/human#parseabiparameters-1).

Import
------

    import { parseAbiParameters } from 'viem'

Usage
-----

    import { parseAbiParameters } from 'viem'
     
    const abiParameters = parseAbiParameters(
      //  ^? const abiParameters: [{ type: "address"; name: "from"; }, { type: "address";...
      'address from, address to, uint256 amount',
    )

Returns
-------

[`Abi`](https://viem.sh/docs/glossary/types#abi)

Parsed ABI parameters.

Parameters
----------

### params

*   **Type:** `string | string[]`

Human-Readable ABI parameters.

    import { parseAbiParameters } from 'viem'
     
    const abiParameters = parseAbiParameters([
      //  ^? const abiParameters: [{ type: "tuple"; components: [{ type: "string"; name:...
      'Baz bar',
      'struct Baz { string name; }',
    ])</content>
</page>

<page>
  <title>Contract Writes with EIP-7702</title>
  <url>https://viem.sh/docs/eip7702/contract-writes</url>
  <content>The guide below demonstrates how to perform Contract Writes with EIP-7702 to invoke Contract functions on an Externally Owned Account (EOA).

Overview
--------

Here is an end-to-end overview of how to perform a Contract Write to send a batch of Calls. We will break it down into [Steps](https://viem.sh/docs/eip7702/contract-writes#steps) below.

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './config'
    import { abi, contractAddress } from './contract'
     
    const eoa = privateKeyToAccount('0x...')
     
    // 1. Authorize designation of the Contract onto the EOA.
    const authorization = await walletClient.signAuthorization({
      account: eoa,
      contractAddress,
    })
     
    // 2. Designate the Contract on the EOA, and invoke the 
    //    `initialize` function.
    const hash = await walletClient.writeContract({
      abi,
      address: eoa.address,
      authorizationList: [authorization],
      //                  ↑ 3. Pass the Authorization as a parameter.
      functionName: 'initialize',
    })

Steps
-----

### 1\. Set up Smart Contract

We will need to set up a Smart Contract to designate on the Account. For the purposes of this guide, we will [create](https://book.getfoundry.sh/reference/forge/forge-init) and [deploy](https://book.getfoundry.sh/forge/deploying) a simple demonstration `Delegation.sol` contract, however, you can use any existing deployed contract.

Firstly, [deploy a Contract](https://book.getfoundry.sh/forge/deploying) to the Network with the following source:

    pragma solidity ^0.8.20;
     
    contract Delegation {
      event Log(string message);
     
      function initialize() external payable {
        emit Log('Hello, world!');
      }
     
      function ping() external pure {
        emit Log('Pong!');
      }
    }

### 2\. Set up Client & Account

Next, we will need to set up a Client and a "Relay Account" that will be responsible for executing the EIP-7702 Contract Write.

    import { createWalletClient, http } from 'viem'
    import { sepolia } from 'viem/chains'
    import { privateKeyToAccount } from 'viem/accounts'
     
    export const relay = privateKeyToAccount('0x...')
     
    export const walletClient = createWalletClient({
      account: relay,
      chain: sepolia,
      transport: http(),
    })

### 3\. Authorize Contract Designation

We will need to sign an Authorization to designate the Contract to the Account.

In the example below, we are instantiating an existing EOA (`account`) and using it to sign the Authorization – this will be the Account that will be used for delegation.

    import { walletClient } from './config'
    import { contractAddress } from './contract'
     
    const eoa = privateKeyToAccount('0x...') 
     
    const authorization = await walletClient.signAuthorization({ 
      account: eoa, 
      contractAddress, 
    }) 

### 4\. Execute Contract Write

We can now designate the Contract on the Account (and execute the `initialize` function) by sending an EIP-7702 Contract Write.

    import { walletClient } from './config'
    import { abi, contractAddress } from './contract'
     
    const eoa = privateKeyToAccount('0x...')
     
    const authorization = await walletClient.signAuthorization({
      account: eoa,
      contractAddress,
    })
     
    const hash = await walletClient.writeContract({ 
      abi, 
      address: eoa.address, 
      authorizationList: [authorization], 
      functionName: 'initialize', 
    }) 

### 5\. (Optional) Interact with the Delegated Account

Now that we have designated a Contract onto the Account, we can interact with it by invoking its functions.

Note that we no longer need to use an Authorization!

    import { walletClient } from './config'
    import { abi } from './contract'
     
    const eoa = privateKeyToAccount('0x...')
     
    const hash = await walletClient.writeContract({
      abi,
      address: eoa.address,
      functionName: 'ping', 
    })

### Note: Self-executing EIP-7702

If the signer of the Authorization (ie. the EOA) is also executing the Transaction, you will need to pass `executor: 'self'` to `signAuthorization`.

This is because `authorization.nonce` must be incremented by 1 over `transaction.nonce`, so we will need to hint to `signAuthorization` that this is the case.

    import { walletClient } from './config'
    import { abi, contractAddress } from './contract'
     
    const authorization = await walletClient.signAuthorization({
      account: eoa, 
      contractAddress,
      executor: 'self', 
    })
     
    const hash = await walletClient.writeContract({
      abi,
      address: eoa.address, 
      address: walletClient.account.address, 
      authorizationList: [authorization],
      functionName: 'initialize',
    })</content>
</page>

<page>
  <title>Sending Transactions with EIP-7702</title>
  <url>https://viem.sh/docs/eip7702/sending-transactions</url>
  <content>The guide below demonstrates how to send EIP-7702 Transactions to invoke Contract functions on an Externally Owned Account (EOA).

Overview
--------

Here is an end-to-end overview of how to execute an EIP-7702 Transaction to emit a simple event on the EOA's designated contract. We will break it down into [Steps](https://viem.sh/docs/eip7702/sending-transactions#steps) below.

    import { encodeFunctionData } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './config'
    import { abi, contractAddress } from './contract'
     
    const eoa = privateKeyToAccount('0x...')
     
    // 1. Authorize designation of the Contract onto the EOA.
    const authorization = await walletClient.signAuthorization({
      account: eoa,
      contractAddress,
    })
     
    // 2. Designate the Contract on the EOA, and invoke the 
    //    `initialize` function.
    const hash = await walletClient.sendTransaction({
      authorizationList: [authorization],
      //                  ↑ 3. Pass the Authorization as a parameter.
      data: encodeFunctionData({
        abi,
        functionName: 'initialize',
      }),
      to: eoa.address,
    })

Steps
-----

### 1\. Set up Smart Contract

We will need to set up a Smart Contract to designate on the Account. For the purposes of this guide, we will [create](https://book.getfoundry.sh/reference/forge/forge-init) and [deploy](https://book.getfoundry.sh/forge/deploying) a simple demonstration `Delegation.sol` contract, however, you can use any existing deployed contract.

Firstly, [deploy a Contract](https://book.getfoundry.sh/forge/deploying) to the Network with the following source:

    pragma solidity ^0.8.20;
     
    contract Delegation {
      event Log(string message);
     
      function initialize() external payable {
        emit Log('Hello, world!');
      }
     
     
      function ping() external pure {
        emit Log('Pong!');
      }
    }

### 2\. Set up Client & Account

Next, we will need to set up a Client and a "Relay Account" that will be responsible for executing the EIP-7702 Transaction.

    import { createWalletClient, http } from 'viem'
    import { sepolia } from 'viem/chains'
    import { privateKeyToAccount } from 'viem/accounts'
     
    export const relay = privateKeyToAccount('0x...')
     
    export const walletClient = createWalletClient({
      account: relay,
      chain: sepolia,
      transport: http(),
    })

### 3\. Authorize Contract Designation

We will need to sign an Authorization to designate the Contract to the Account.

In the example below, we are instantiating an existing EOA (`account`) and using it to sign the Authorization – this will be the Account that will be used for delegation.

    import { walletClient } from './config'
    import { contractAddress } from './contract'
     
    const eoa = privateKeyToAccount('0x...') 
     
    const authorization = await walletClient.signAuthorization({ 
      account: eoa, 
      contractAddress, 
    }) 

### 4\. Execute Transaction

We can now designate the Contract on the Account (and execute the `initialize` function) by sending an EIP-7702 Transaction.

    import { encodeFunctionData } from 'viem'
    import { walletClient } from './config'
    import { contractAddress } from './contract'
     
    const eoa = privateKeyToAccount('0x...')
     
    const authorization = await walletClient.signAuthorization({
      account: eoa,
      contractAddress,
    })
     
    const hash = await walletClient.sendTransaction({ 
      authorizationList: [authorization], 
      data: encodeFunctionData({ 
        abi, 
        functionName: 'initialize', 
      }), 
      to: eoa.address, 
    }) 

### 5\. (Optional) Interact with the Delegated Account

Now that we have designated a Contract onto the Account, we can interact with it by invoking its functions.

Note that we no longer need to use an Authorization!

    import { encodeFunctionData } from 'viem'
    import { walletClient } from './config'
     
    const eoa = privateKeyToAccount('0x...')
     
    const hash = await walletClient.sendTransaction({
      data: encodeFunctionData({
        abi,
        functionName: 'ping',
      }),
      to: eoa.address,
    })

### Note: Self-executing EIP-7702

If the signer of the Authorization (ie. the EOA) is also executing the Transaction, you will need to pass `executor: 'self'` to `signAuthorization`.

This is because `authorization.nonce` must be incremented by 1 over `transaction.nonce`, so we will need to hint to `signAuthorization` that this is the case.

    import { encodeFunctionData } from 'viem'
    import { walletClient } from './config'
    import { contractAddress } from './contract'
     
    const authorization = await walletClient.signAuthorization({
      account: eoa, 
      contractAddress,
      executor: 'self', 
    })
     
    const hash = await walletClient.sendTransaction({
      authorizationList: [authorization],
      data: encodeFunctionData({
        abi,
        functionName: 'initialize',
      }),
      to: eoa.address, 
      to: walletClient.account.address, 
    })</content>
</page>

<page>
  <title>prepareAuthorization</title>
  <url>https://viem.sh/docs/eip7702/prepareAuthorization</url>
  <content>[Skip to content](https://viem.sh/docs/eip7702/prepareAuthorization#vocs-content)

Prepares an [EIP-7702 Authorization](https://eips.ethereum.org/EIPS/eip-7702) for signing. This Action will fill the required fields of the Authorization object if they are not provided (e.g. `nonce` and `chainId`).

With the prepared Authorization object, you can use [`signAuthorization`](https://viem.sh/docs/eip7702/signAuthorization) to sign over it.

Usage
-----

    import { walletClient } from './client'
     
    const authorization = await walletClient.prepareAuthorization({ 
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
    }) 
    {   chainId: 1,   contractAddress: "0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2",   nonce: 1, } const signedAuthorization = await walletClient.signAuthorization(authorization)

### Explicit Scoping

We can explicitly set a `nonce` and/or `chainId` by supplying them as parameters:

    import { walletClient } from './client'
     
    const authorization = await walletClient.prepareAuthorization({
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      chainId: 10, 
    })
    {   chainId: 10,   contractAddress: "0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2",   nonce: 420, } const signedAuthorization = await walletClient.signAuthorization(authorization)

Returns
-------

`Authorization`

A prepared & unsigned Authorization object.

Parameters
----------

### account

*   **Type:** `Account`

Account to use to prepare the Authorization object.

Accepts a [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.prepareAuthorization({
      account: privateKeyToAccount('0x...'), 
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
    }) 

### chainId (optional)

*   **Type:** `Address`
*   **Default:** `client.chain.id` or Network chain ID

The Chain ID to scope the Authorization to. If set to zero (`0`), then the Authorization will be valid on all chains.

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.prepareAuthorization({
      account: privateKeyToAccount('0x...'),
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      chainId: 1, 
    }) 

### contractAddress

*   **Type:** `Address`

The target Contract to designate onto the Account.

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.prepareAuthorization({
      account: privateKeyToAccount('0x...'),
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
    }) 

### executor (optional)

*   **Type:** `'self' | undefined`

Whether the EIP-7702 Transaction will be executed by the Account that signed the Authorization.

If not specified, it will be assumed that the EIP-7702 Transaction will be executed by another Account (ie. a relayer Account).

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.prepareAuthorization({
      account: privateKeyToAccount('0x...'),
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      executor: 'self', 
    }) 

### nonce (optional)

*   **Type:** `Address`
*   **Default:** Account's next available nonce.

The nonce to scope the Authorization to.

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.prepareAuthorization({
      account: privateKeyToAccount('0x...'),
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      nonce: 69, 
    })</content>
</page>

<page>
  <title>hashAuthorization</title>
  <url>https://viem.sh/docs/eip7702/hashAuthorization</url>
  <content>Calculates an Authorization hash in [EIP-7702 format](https://eips.ethereum.org/EIPS/eip-7702): `keccak256('0x05' || rlp([chain_id, address, nonce]))`.

Import
------

    import { hashAuthorization } from 'viem/utils'

Usage
-----

    import { hashAuthorization } from 'viem/utils'
     
    hashAuthorization({
      contractAddress: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
      chainId: 1,
      nonce: 0,
    })
    // 0xd428ed36e6098e46b40a4cb99b83b930b0ca1f054f40b5996589eda33c295663

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The hashed Authorization.

Parameters
----------

### address

*   **Type:** `Address`

Address of the contract to set as code for the Authority.

    import { hashAuthorization } from 'viem/utils'
     
    hashAuthorization({
      contractAddress: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
      chainId: 1,
      nonce: 0,
    }) 

### chainId

*   **Type:** `number`

Chain ID to authorize.

    import { hashAuthorization } from 'viem/utils'
     
    hashAuthorization({
      contractAddress: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
      chainId: 1, 
      nonce: 0,
    }) 

### nonce

*   **Type:** `number`

Nonce of the Authority to authorize.

    import { hashAuthorization } from 'viem/utils'
     
    hashAuthorization({
      contractAddress: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
      chainId: 1,
      nonce: 0, 
    }) 

### to

*   **Type:** `"hex" | "bytes"`
*   **Default:** `"hex"`

Output format.

    import { hashAuthorization } from 'viem/utils'
     
    hashAuthorization({
      contractAddress: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
      chainId: 1,
      nonce: 0, 
      to: 'bytes', 
    })</content>
</page>

<page>
  <title>recoverAuthorizationAddress</title>
  <url>https://viem.sh/docs/eip7702/recoverAuthorizationAddress</url>
  <content>Recovers the original signing address from a signed Authorization object.

Import
------

    import { recoverAuthorizationAddress } from 'viem/utils'

Usage
-----

    import { privateKeyToAccount } from 'viem/accounts'
    import { recoverAuthorizationAddress } from 'viem/utils'
    import { walletClient } from './client'
     
    const eoa = privateKeyToAccount('0x...')
     
    const authorization = await walletClient.signAuthorization({
      account: eoa,
      authorization: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
    })
     
    const address = await recoverAuthorizationAddress({ 
      authorization, 
    }) 

Returns
-------

`Address`

The address that signed the Authorization object.

Parameters
----------

### authorization

*   **Type:** `Authorization | SignedAuthorization`

The Authorization object that was signed.

    const authorization = await walletClient.signAuthorization({
      authorization: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
    })
    const address = await recoverAuthorizationAddress({
      authorization, 
    }) 

### signature

*   **Type:** `Hex | ByteArray | Signature | SignedAuthorization`

The signature that was generated by signing the Authorization object with the address's private key.

    const signature = await walletClient.signAuthorization({
      contractAddress: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
      chainId: 1,
      nonce: 0,
    })
     
    const address = await recoverAuthorizationAddress({
      authorization: {
        contractAddress: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        chainId: 1,
        nonce: 0,
      },
      signature, 
    })</content>
</page>

<page>
  <title>privateKeyToAccount</title>
  <url>https://viem.sh/docs/accounts/local/privateKeyToAccount</url>
  <content>A Private Key Account is an interface that has the ability to sign transactions and messages with a given private key.

Import
------

    import { privateKeyToAccount } from 'viem/accounts'

Usage
-----

To initialize a Private Key Account, you will need to pass a private key to `privateKeyToAccount`:

    import { createWalletClient, http } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const account = privateKeyToAccount('0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80') 
     
    const client = createWalletClient({
      account,
      chain: mainnet,
      transport: http()
    })

> Note: the above is a valid private key, but it is not a "real" private key. Please do not use it for anything other than testing.

### Generating Private Keys

You can generate a random private key using the `generatePrivateKey` function:

    import { generatePrivateKey } from 'viem/accounts'
     
    const privateKey = generatePrivateKey()

Parameters
----------

### privateKey

*   **Type:** `Hex`

The private key to use for the Account.</content>
</page>

<page>
  <title>signAuthorization</title>
  <url>https://viem.sh/docs/eip7702/signAuthorization</url>
  <content>[Skip to content](https://viem.sh/docs/eip7702/signAuthorization#vocs-content)

Signs an [EIP-7702 Authorization](https://eips.ethereum.org/EIPS/eip-7702). The signed Authorization can be used in Transaction APIs like [`sendTransaction`](https://viem.sh/docs/actions/wallet/sendTransaction#authorizationlist-optional) and [`writeContract`](https://viem.sh/docs/contract/writeContract#authorizationlist-optional) to delegate an authorized Contract onto an Account.

Usage
-----

A Contract can be authorized by supplying a `contractAddress`. By default, it will be signed over the Account's next available Nonce and the current Chain ID. You can also [explicitly set the `nonce` and `chainId`](https://viem.sh/docs/eip7702/signAuthorization#scoping).

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const eoa = privateKeyToAccount('0x...')
     
    const authorization = await walletClient.signAuthorization({ 
      account: eoa, 
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
    }) 
    {   chainId: 1,   contractAddress: "0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2",   nonce: 1,   r: "0xf507fb8fa33ffd05a7f26c980bbb8271aa113affc8f192feba87abe26549bda1",   s: "0x1b2687608968ecb67230bbf7944199560fa2b3cffe9cc2b1c024e1c8f86a9e08",   yParity: 0, } const hash = await walletClient.sendTransaction({
      authorizationList: [authorization],
      data: '0xdeadbeef',
      to: eoa.address,
    })

### Explicit Scoping

We can explicitly sign over a provided `nonce` and/or `chainId` by supplying them as parameters:

    import { walletClient } from './client'
     
    const eoa = privateKeyToAccount('0x...')
     
    const authorization = await walletClient.signAuthorization({
      account: eoa,
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      chainId: 10, 
      nonce: 420, 
    })
    {   chainId: 10,   contractAddress: "0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2",   nonce: 420,   r: "0xf507fb8fa33ffd05a7f26c980bbb8271aa113affc8f192feba87abe26549bda1",   s: "0x1b2687608968ecb67230bbf7944199560fa2b3cffe9cc2b1c024e1c8f86a9e08",   yParity: 0, } const hash = await walletClient.sendTransaction({
      authorizationList: [authorization],
      data: '0xdeadbeef',
      to: eoa.address,
    })

Returns
-------

`SignedAuthorization`

A signed Authorization object.

Parameters
----------

### account

*   **Type:** `Account`

Account to use for delegation.

Accepts a [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.signAuthorization({
      account: privateKeyToAccount('0x...'), 
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
    }) 

### chainId (optional)

*   **Type:** `Address`
*   **Default:** `client.chain.id` or Network chain ID

The Chain ID to scope the Authorization to.

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.signAuthorization({
      account: privateKeyToAccount('0x...'),
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      chainId: 1, 
    }) 

### contractAddress

*   **Type:** `Address`

The target Contract to delegate to the Account.

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.signAuthorization({
      account: privateKeyToAccount('0x...'),
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
    }) 

### executor (optional)

*   **Type:** `'self' | undefined`

Whether the EIP-7702 Transaction will be executed by the Account that signed the Authorization.

If not specified, it will be assumed that the EIP-7702 Transaction will be executed by another Account (ie. a relayer Account).

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.signAuthorization({
      account: privateKeyToAccount('0x...'),
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      executor: 'self', 
    }) 

### nonce (optional)

*   **Type:** `Address`
*   **Default:** Account's next available nonce.

The nonce to scope the Authorization to.

    import { privateKeyToAccount } from 'viem/accounts'
    import { walletClient } from './client'
     
    const authorization = await walletClient.signAuthorization({
      account: privateKeyToAccount('0x...'),
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      nonce: 69, 
    })</content>
</page>

<page>
  <title>JSON-RPC Account</title>
  <url>https://viem.sh/docs/accounts/jsonRpc</url>
  <content>A JSON-RPC Account is an Account whose signing keys are stored on the external Wallet. It **defers** signing of transactions & messages to the target Wallet over JSON-RPC. An example of such Wallet could be a Browser Extension Wallet, or Mobile Wallet over WalletConnect.

Usage
-----

A JSON-RPC Account can just be initialized as an [Address](https://viem.sh/docs/glossary/types#address) string. In the usage below, we are extracting the address from a Browser Extension Wallet (e.g. MetaMask) with the `window.ethereum` Provider via `eth_requestAccounts`:

    import 'viem/window'
    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const [address] = await window.ethereum.request({ 
      method: 'eth_requestAccounts' 
    })
     
    const client = createWalletClient({
      account: address, 
      chain: mainnet,
      transport: custom(window.ethereum!)
    })</content>
</page>

<page>
  <title>Types</title>
  <url>https://viem.sh/docs/glossary/types#transport</url>
  <content>`Abi`
-----

Type matching the [Contract ABI Specification](https://docs.soliditylang.org/en/latest/abi-spec.html#json)

Re-exported from [ABIType](https://abitype.dev/api/types#abi).

`AbiError`
----------

ABI [Error](https://docs.soliditylang.org/en/latest/abi-spec#errors) type.

Re-exported from [ABIType](https://abitype.dev/api/types#abierror).

`AbiEvent`
----------

ABI [Event](https://docs.soliditylang.org/en/latest/abi-spec#events) type.

Re-exported from [ABIType](https://abitype.dev/api/types#abievent).

`AbiFunction`
-------------

ABI [Function](https://docs.soliditylang.org/en/latest/abi-spec#argument-encoding) type.

Re-exported from [ABIType](https://abitype.dev/api/types#abifunction).

`AbiParameter`
--------------

`inputs` and `outputs` item for ABI functions, events, and errors.

Re-exported from [ABIType](https://abitype.dev/api/types#abiparameter).

`AbiParameterToPrimitiveTypes`
------------------------------

Converts `AbiParameter` to corresponding TypeScript primitive type.

[See more](https://abitype.dev/api/utilities#abiparametertoprimitivetype)

`AbiParametersToPrimitiveTypes`
-------------------------------

Converts array of `AbiParameter` to corresponding TypeScript primitive types.

[See more](https://abitype.dev/api/utilities#abiparameterstoprimitivetypes)

`AccessList`
------------

An access list.

`Address`
---------

An address.

Re-exported from [ABIType](https://abitype.dev/api/types#address).

`Block`
-------

A type for a [Block](https://viem.sh/docs/glossary/terms#block).

[See Type](https://github.com/wevm/viem/blob/main/src/types/block.ts)

`Chain`
-------

A type for a [Chain](https://viem.sh/docs/glossary/terms#chain).

[See Type](https://github.com/wevm/viem/blob/main/src/types/chain.ts)

`CompactSignature`
------------------

A type for [EIP-2098](https://eips.ethereum.org/EIPS/eip-2098) compact signatures.

[See Type](https://github.com/wevm/viem/blob/main/src/types/misc.ts)

`FeeHistory`
------------

A type for fee history.

[See Type](https://github.com/wevm/viem/blob/main/src/types/fee.ts)

`FeeValues`
-----------

A type for fee values.

[See Type](https://github.com/wevm/viem/blob/main/src/types/fee.ts)

`Filter`
--------

A type for a [Filter](https://viem.sh/docs/glossary/terms#filter).

[See Type](https://github.com/wevm/viem/blob/main/src/types/filter.ts)

`Hash`
------

Type for a hashed value – a "0x"-prefixed string: `"0x${string}"`

`Hex`
-----

Type for a hex value – a "0x"-prefixed string: `"0x${string}"`

`Log`
-----

A type for [Event Logs](https://viem.sh/docs/glossary/terms#event-log).

[See Type](https://github.com/wevm/viem/blob/main/src/types/log.ts)

`Signature`
-----------

A type for a structured signature.

[See Type](https://github.com/wevm/viem/blob/main/src/types/misc.ts)

`Transaction`
-------------

A type for [Transactions](https://viem.sh/docs/glossary/terms#transaction).

[See Type](https://github.com/wevm/viem/blob/main/src/types/transaction.ts)

`TransactionReceipt`
--------------------

A type for [Transaction Receipts](https://viem.sh/docs/glossary/terms#transaction-receipt).

[See Type](https://github.com/wevm/viem/blob/main/src/types/transaction.ts)

`Transport`
-----------

A type for [Transports](https://viem.sh/docs/glossary/terms#transports).

[See Type](https://github.com/wevm/viem/blob/main/src/clients/transports/createTransport.ts)

`WalletPermission`
------------------

A type for wallet (JSON-RPC Account) permissions.

[See Type](https://github.com/wevm/viem/blob/main/src/types/eip1193.ts)

`TransactionSerializedEIP1559`
------------------------------

EIP-1559 transaction hex value – a "0x02"-prefixed string: `"0x02${string}"`

`TransactionSerializedEIP2930`
------------------------------

EIP-2930 transaction hex value – a "0x01"-prefixed string: `"0x01${string}"`

`TransactionSerializedLegacy`
-----------------------------

Legacy transaction hex value – a "0x"-prefixed string: `"0x${string}"`

`TransactionType`
-----------------

All types of transactions. `"eip1559" | "eip2930" | "eip4844" | "eip7702" | "legacy"`

`TransactionRequest`
--------------------

A type for all transaction requests.

[See Type](https://github.com/wevm/viem/blob/main/src/types/transaction.ts).

`StateOverride`
---------------

A type defining state overrides for `eth_call` method. [See more](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-eth#eth-call)</content>
</page>

<page>
  <title>verifyAuthorization</title>
  <url>https://viem.sh/docs/eip7702/verifyAuthorization</url>
  <content>Verifies that an Authorization object was signed by the provided address.

Import
------

    import { verifyAuthorization } from 'viem/utils'

Usage
-----

    import { privateKeyToAccount } from 'viem/accounts'
    import { verifyAuthorization } from 'viem/utils'
    import { walletClient } from './client'
     
    const eoa = privateKeyToAccount('0x...')
     
    const authorization = await walletClient.signAuthorization({
      account: eoa,
      authorization: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
    })
     
    const valid = await verifyAuthorization({ 
      address: eoa.address, 
      authorization, 
    }) 

Returns
-------

`boolean`

Whether the signature is valid for the provided Authorization object.

Parameters
----------

### address

*   **Type:** `Address`

The address that signed the Authorization object.

    const valid = await verifyAuthorization({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48', 
      authorization,
    }) 

### authorization

*   **Type:** `Authorization | SignedAuthorization`

The Authorization object to be verified.

    const authorization = await walletClient.signAuthorization({
      authorization: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
    })
     
    const valid = await verifyAuthorization({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      authorization, 
    }) 

### signature

*   **Type:** `Hex | ByteArray | Signature | SignedAuthorization`

The signature that was generated by signing the Authorization object with the address's private key.

    const signature = await walletClient.signAuthorization({
      authorization: {
        address: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        chainId: 1,
        nonce: 0,
      }
    })
     
    const valid = await verifyAuthorization({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      authorization: {
        address: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        chainId: 1,
        nonce: 0,
      },
      signature, 
    })</content>
</page>

<page>
  <title>Contract Instances</title>
  <url>https://viem.sh/docs/contract/getContract</url>
  <content>A Contract Instance is a type-safe interface for performing contract-related actions with a specific ABI and address, created by the `getContract` function.

Import
------

    import { getContract } from 'viem'

Usage
-----

You can create a Contract Instance with the `getContract` function by passing in a [ABI](https://viem.sh/docs/glossary/types#abi), address, and [Public](https://viem.sh/docs/clients/public) and/or [Wallet Client](https://viem.sh/docs/clients/wallet). Once created, you can call contract methods, fetch for events, listen to events, etc.

    import { getContract } from 'viem'
    import { wagmiAbi } from './abi'
    import { publicClient, walletClient } from './client'
     
    // 1. Create contract instance
    const contract = getContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      // 1a. Insert a single client
      client: publicClient,
      // 1b. Or public and/or wallet clients
      client: { public: publicClient, wallet: walletClient }
    })
     
    // 2. Call contract methods, fetch events, listen to events, etc.
    const result = await contract.read.totalSupply()
    const logs = await contract.getEvents.Transfer()
    const unwatch = contract.watchEvent.Transfer(
      { from: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e' },
      { onLogs(logs) { console.log(logs) } }
    )

Using Contract Instances can make it easier to work with contracts if you don't want to pass the `abi` and `address` properties every time you perform contract actions, e.g. [`readContract`](https://viem.sh/docs/contract/readContract), [`writeContract`](https://viem.sh/docs/contract/writeContract), [`estimateContractGas`](https://viem.sh/docs/contract/estimateContractGas), etc. Switch between the tabs below to see the difference between standalone Contract Actions and Contract Instance Actions:

    import { getContract } from 'viem'
    import { wagmiAbi } from './abi'
    import { publicClient, walletClient } from './client'
     
    const contract = getContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      client: {
        public: publicClient,
        wallet: walletClient,
      }
    })
     
    const balance = await contract.read.balanceOf([
      '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
    ])
    const hash = await contract.write.mint([69420])
    const logs = await contract.getEvents.Transfer()
    const unwatch = contract.watchEvent.Transfer(
      {
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      },
      { onLogs: logs => console.log(logs) }
    )

Return Value
------------

Contract instance object. Type is inferred.

Depending on if you create a contract instance with a Public Client, Wallet Client, or both, the methods available on the contract instance will vary.

#### With Public Client

If you pass in a [`publicClient`](https://viem.sh/docs/clients/public), the following methods are available:

*   [`createEventFilter`](https://viem.sh/docs/contract/createContractEventFilter)
*   [`estimateGas`](https://viem.sh/docs/contract/estimateContractGas)
*   [`getEvents`](https://viem.sh/docs/contract/getContractEvents)
*   [`read`](https://viem.sh/docs/contract/readContract)
*   [`simulate`](https://viem.sh/docs/contract/simulateContract)
*   [`watchEvent`](https://viem.sh/docs/contract/watchContractEvent)

#### With Wallet Client

If you pass in a [`walletClient`](https://viem.sh/docs/clients/wallet), the following methods are available:

*   [`estimateGas`](https://viem.sh/docs/contract/estimateContractGas)
*   [`write`](https://viem.sh/docs/contract/writeContract)

#### Calling methods

If you are using [TypeScript](https://viem.sh/docs/typescript) with viem, your editor will be able to provide autocomplete suggestions for the methods available on the contract instance, as well as the arguments and other options for each method.

In general, contract instance methods follow the following format:

    // function
    contract.(estimateGas|read|simulate|write).(functionName)(args, options)
     
    // event
    contract.(createEventFilter|getEvents|watchEvent).(eventName)(args, options)

If the contract function/event you are using does not accept arguments (e.g. function has no inputs, event has no indexed inputs), then you can omit the `args` parameter so `options` is the first and only parameter.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const contract = getContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      client: publicClient
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const contract = getContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      client: publicClient
    })

### client

*   **Type:** [`Client | { public: Client; wallet: Client }`](https://viem.sh/docs/clients/public)

The Client used for performing [contract actions](https://viem.sh/docs/contract/getContract#return-value).

    const contract = getContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      client: publicClient, 
    })

You can also pass in multiple clients (ie. a Wallet Client and a Public Client):

    const contract = getContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      client: { 
        public: publicClient, 
        wallet: walletClient 
      }, 
    })</content>
</page>

<page>
  <title>mnemonicToAccount</title>
  <url>https://viem.sh/docs/accounts/local/mnemonicToAccount</url>
  <content>A Mnemonic Account is a [Hierarchical Deterministic (HD) Account](https://viem.sh/docs/accounts/local/hdKeyToAccount) that is derived from a [BIP-39 mnemonic phrase](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) and an optional HD path.

It has the ability to sign transactions and messages with the private key derived from the HD Node.

Import
------

    import { mnemonicToAccount } from 'viem/accounts'

Usage
-----

To initialize a Mnemonic Account, you will need to pass a mnemonic phrase to `mnemonicToAccount`:

    import { createWalletClient, http } from 'viem'
    import { mnemonicToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const account = mnemonicToAccount('legal winner thank year wave sausage worth useful legal winner thank yellow') 
     
    const client = createWalletClient({
      account,
      chain: mainnet,
      transport: http()
    })

> Note: the above is a valid mnemonic, but it is not a "real" mnemonic. Please do not use it for anything other than testing.

### Generating Mnemonics

You can generate a random BIP-39 mnemonic using the `generateMnemonic` function with a wordlist:

    import { english, generateMnemonic } from 'viem/accounts'
     
    const mnemonic = generateMnemonic(english)

Available wordlists:

*   `czech`
*   `english`
*   `french`
*   `italian`
*   `japanese`
*   `korean`
*   `portuguese`
*   `simplifiedChinese`
*   `spanish`
*   `traditionalChinese`

Parameters
----------

### mnemonic

*   **Type:** `string`

The BIP-39 mnemonic phrase.

    const account = mnemonicToAccount(
      'legal winner thank year wave sausage worth useful legal winner thank yellow'
    )

### options.accountIndex

*   **Type:** `number`
*   **Default:** `0`

The account index to use in the path (`"m/44'/60'/${accountIndex}'/0/0"`) to derive a private key.

    const account = mnemonicToAccount(
      'legal winner thank year wave sausage worth useful legal winner thank yellow',
      {
        accountIndex: 1
      }
    )

### options.addressIndex

*   **Type:** `number`
*   **Default:** `0`

The address index to use in the path (`"m/44'/60'/0'/0/${addressIndex}"`) to derive a private key.

    const account = mnemonicToAccount(
      'legal winner thank year wave sausage worth useful legal winner thank yellow',
      {
        accountIndex: 1,
        addressIndex: 6
      }
    )

### options.changeIndex

*   **Type:** `number`
*   **Default:** `0`

The change index to use in the path (`"m/44'/60'/0'/${changeIndex}/0"`) to derive a private key.

    const account = mnemonicToAccount(
      'legal winner thank year wave sausage worth useful legal winner thank yellow',
      {
        accountIndex: 1,
        addressIndex: 6,
        changeIndex: 2
      }
    )

### options.path

*   **Type:** `"m/44'/60'/${string}"`

The HD path to use to derive a private key.

    const account = mnemonicToAccount(
      'legal winner thank year wave sausage worth useful legal winner thank yellow',
      {
        path: "m/44'/60'/5'/0/2"
      }
    )</content>
</page>

<page>
  <title>requestAddresses</title>
  <url>https://viem.sh/docs/actions/wallet/requestAddresses</url>
  <content>[Skip to content](https://viem.sh/docs/actions/wallet/requestAddresses#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Requests a list of accounts managed by a wallet.

`requestAddresses` sends a request to the wallet, asking for permission to access the user's accounts. After the user accepts the request, it will return a list of accounts (addresses).

This API can be useful for dapps that need to access the user's accounts in order to execute transactions or interact with smart contracts.

Usage
-----

    import { walletClient } from './client'
     
    const accounts = await walletClient.requestAddresses() 
    // ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC']

Returns
-------

[`Address[]`](https://viem.sh/docs/glossary/types#address)

JSON-RPC Methods
----------------

[`eth_requestAccounts`](https://eips.ethereum.org/EIPS/eip-1102)</content>
</page>

<page>
  <title>hdKeyToAccount</title>
  <url>https://viem.sh/docs/accounts/local/hdKeyToAccount</url>
  <content>A [Hierarchical Deterministic (HD)](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#abstract) Account is derived from a [HD Key](https://github.com/paulmillr/scure-bip32#usage) and an optional HD path.

It has the ability to sign transactions and messages with the private key derived from the HD Node.

Import
------

    import { HDKey, hdKeyToAccount } from 'viem/accounts'

> Note: viem [re-exports `HDKey`](https://github.com/paulmillr/scure-bip32#usage) from `@scure/bip32`.

Usage
-----

To initialize a HD Account, you will need to pass a [`HDKey` instance](https://github.com/paulmillr/scure-bip32#usage) to `hdKeyToAccount`.

The `HDKey` instance comes with a few static methods to derive a HD Key:

*   `fromMasterSeed`
*   `fromExtendedKey`
*   `fromJSON`

    import { createWalletClient, http } from 'viem'
    import { HDKey, hdKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const hdKey = HDKey.fromMasterSeed(...) 
    const hdKey = HDKey.fromExtendedKey(...)
    const hdKey = HDKey.fromJSON({ xpriv: ... })
     
    const account = hdKeyToAccount(hdKey) 
     
    const client = createWalletClient({
      account,
      chain: mainnet,
      transport: http(),
    })

Parameters
----------

### hdKey

*   **Type:** `string`

The BIP-39 mnemonic phrase.

    const hdKey = HDKey.fromMasterSeed(...)
     
    const account = hdKeyToAccount(
      hdKey, 
    )

### options.accountIndex

*   **Type:** `number`
*   **Default:** `0`

The account index to use in the path (`"m/44'/60'/${accountIndex}'/0/0"`) to derive a private key.

    const hdKey = HDKey.fromMasterSeed(...)
     
    const account = hdKeyToAccount(
      hdKey,
      {
        accountIndex: 1
      }
    )

### options.addressIndex

*   **Type:** `number`
*   **Default:** `0`

The address index to use in the path (`"m/44'/60'/0'/0/${addressIndex}"`) to derive a private key.

    const hdKey = HDKey.fromMasterSeed(...)
     
    const account = hdKeyToAccount(
      hdKey,
      {
        accountIndex: 1,
        addressIndex: 6
      }
    )

### options.changeIndex

*   **Type:** `number`
*   **Default:** `0`

The change index to use in the path (`"m/44'/60'/0'/${changeIndex}/0"`) to derive a private key.

    const hdKey = HDKey.fromMasterSeed(...)
     
    const account = hdKeyToAccount(
      hdKey,
      {
        accountIndex: 1,
        addressIndex: 6,
        changeIndex: 2
      }
    )

### options.path

*   **Type:** `"m/44'/60'/${string}"`

The HD path to use to derive a private key.

    const hdKey = HDKey.fromMasterSeed(...)
     
    const account = hdKeyToAccount(
      hdKey,
      {
        path: "m/44'/60'/5'/0/2"
      }
    )</content>
</page>

<page>
  <title>sendTransaction</title>
  <url>https://viem.sh/docs/actions/wallet/sendTransaction</url>
  <content>Creates, signs, and sends a new transaction to the network.

Usage
-----

    import { account, walletClient } from './config'
     
    const hash = await walletClient.sendTransaction({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
    // '0x...'

### Account Hoisting

If you do not wish to pass an `account` to every `sendTransaction`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient } from './config'
     
    const hash = await walletClient.sendTransaction({ 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
    // '0x...'

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### account

*   **Type:** `Account | Address | null`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc). If set to `null`, it is assumed that the transport will handle filling the sender of the transaction.

    const hash = await walletClient.sendTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### to

*   **Type:** `0x${string}`

The transaction recipient or contract address.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: 1000000000000000000n,
      nonce: 69
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const hash = await walletClient.sendTransaction({
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### authorizationList (optional)

*   **Type:** `AuthorizationList`

Signed EIP-7702 Authorization list.

    const authorization = await walletClient.signAuthorization({ 
      account,
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
    }) 
     
    const hash = await walletClient.sendTransaction({
      account,
      authorizationList: [authorization], 
      data: '0xdeadbeef',
      to: account.address,
    })

### blobs (optional)

*   **Type:** `Hex[]`

Blobs for [Blob Transactions](https://viem.sh/docs/guides/blob-transactions).

    import * as cKzg from 'c-kzg'
    import { toBlobs, setupKzg, stringToHex } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const hash = await walletClient.sendTransaction({
      account,
      blobs: toBlobs({ data: stringToHex('blobby blob!') }), 
      kzg,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

The chain is also used to infer its request type (e.g. the Celo chain has a `gatewayFee` that you can pass through to `sendTransaction`).

    import { optimism } from 'viem/chains'
     
    const hash = await walletClient.sendTransaction({
      chain: optimism, 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const hash = await walletClient.sendTransaction({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const hash = await walletClient.sendTransaction({
      account,
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### kzg (optional)

*   **Type:** `KZG`

KZG implementation for [Blob Transactions](https://viem.sh/docs/guides/blob-transactions).

See [`setupKzg`](https://viem.sh/docs/utilities/setupKzg) for more information.

    import * as cKzg from 'c-kzg'
    import { toBlobs, setupKzg, stringToHex } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const hash = await walletClient.sendTransaction({
      account,
      blobs: toBlobs({ data: stringToHex('blobby blob!') }), 
      kzg, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await walletClient.sendTransaction({
      account,
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await walletClient.sendTransaction({
      account,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
      nonce: 69
    })

Tips
----

*   For dapps: When using this action, it is assumed that the user has connected to their wallet (e.g. given permission for the dapp to access their accounts via [`requestAddresses`](https://viem.sh/docs/actions/wallet/requestAddresses)). You can also check if the user has granted access to their accounts via [`getAddresses`](https://viem.sh/docs/actions/wallet/getAddresses)

Live Example
------------

Check out the usage of `sendTransaction` in the live [Sending Transactions Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/transactions_sending-transactions) below.

JSON-RPC Methods
----------------

*   JSON-RPC Accounts:
    *   [`eth_sendTransaction`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_sendtransaction)
*   Local Accounts:
    *   [`eth_sendRawTransaction`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_sendrawtransaction)</content>
</page>

<page>
  <title>createAccessList</title>
  <url>https://viem.sh/docs/actions/public/createAccessList</url>
  <content>Creates an [EIP-2930](https://eips.ethereum.org/EIPS/eip-2930) access list based on a transaction request.

Usage
-----

    import { account, publicClient } from './config'
     
    const result = await publicClient.createAccessList({ 
      data: '0xdeadbeef',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

Returns
-------

`{ accessList: AccessList, gasUsed: bigint }`

The access list and gas used.

Parameters
----------

### account (optional)

*   **Type:** `Account | Address`

The Account to create an access list for.

    import { parseEther } from 'viem'
     
    const result = await publicClient.createAccessList({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      data: '0xdeadbeef',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### blockNumber (optional)

*   **Type:** `number`

Block number to create an access list for.

    import { parseEther } from 'viem'
     
    const result = await publicClient.createAccessList({
      blockNumber: 15121123n, 
      data: '0xdeadbeef',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Block tag to create an access list for.

    import { parseEther } from 'viem'
     
    const result = await publicClient.createAccessList({
      blockTag: 'safe', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xdeadbeef',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### data (optional)

*   **Type:** `0x${string}`

Contract function selector with encoded arguments.

    import { parseEther } from 'viem'
     
    const result = await publicClient.createAccessList({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xdeadbeef', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    import { parseEther, parseGwei } from 'viem'
     
    const result = await publicClient.createAccessList({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xdeadbeef',
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    import { parseEther, parseGwei } from 'viem'
     
    const result = await publicClient.createAccessList({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xdeadbeef',
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    import { parseEther, parseGwei } from 'viem'
     
    const result = await publicClient.createAccessList({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xdeadbeef',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### to (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Transaction recipient.

    import { parseEther } from 'viem'
     
    const result = await publicClient.createAccessList({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xdeadbeef',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    import { parseEther } from 'viem'
     
    const result = await publicClient.createAccessList({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xdeadbeef',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>getBalance</title>
  <url>https://viem.sh/docs/actions/public/getBalance</url>
  <content>Returns the balance of an address in wei.

Usage
-----

    import { publicClient } from './client'
     
    const balance = await publicClient.getBalance({ 
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
    })
    > 10000000000000000000000n (wei)

Returns
-------

`bigint`

The balance of the address in wei.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The address of the account.

    const balance = await publicClient.getBalance({
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e', 
    })

### blockNumber (optional)

*   **Type:** `bigint`

The balance of the account at a block number.

    const balance = await publicClient.getBalance({
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
      blockNumber: 69420n
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`

The balance of the account at a block tag.

    const balance = await publicClient.getBalance({
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
      blockTag: 'safe'
    })

Tips
----

*   You can convert the balance to ether units with [`formatEther`](https://viem.sh/docs/utilities/formatEther).

    import { formatEther } from 'viem'
     
    const balance = await publicClient.getBalance({
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
      blockTag: 'safe'
    })
    const balanceAsEther = formatEther(balance) 
    // "6.942"

JSON-RPC Method
---------------

[`eth_getBalance`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getbalance)</content>
</page>

<page>
  <title>getTransactionCount</title>
  <url>https://viem.sh/docs/actions/public/getTransactionCount</url>
  <content>Returns the number of [Transactions](https://viem.sh/docs/glossary/terms#transaction) an Account has broadcast / sent.

Usage
-----

    import { publicClient } from './client'
     
    const transactionCount = await publicClient.getTransactionCount({  
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
    })
    > 420

Returns
-------

`number`

The number of transactions an account has sent.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The address of the account.

    const transactionCount = await publicClient.getTransactionCount({
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e', 
    })

### blockNumber (optional)

*   **Type:** `bigint`

Get the count at a block number.

    const transactionCount = await publicClient.getTransactionCount({
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
      blockNumber: 69420n
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`

Get the count at a block tag.

    const transactionCount = await publicClient.getTransactionCount({
      address: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
      blockTag: 'safe'
    })

Notes
-----

*   The transaction count of an account can also be used as a nonce.

JSON-RPC Method
---------------

[`eth_getTransactionCount`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_gettransactioncount)</content>
</page>

<page>
  <title>getBlockNumber</title>
  <url>https://viem.sh/docs/actions/public/getBlockNumber</url>
  <content>[Skip to content](https://viem.sh/docs/actions/public/getBlockNumber#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the number of the most recent block seen.

Usage
-----

    import { publicClient } from './client'
     
    const blockNumber = await publicClient.getBlockNumber() 
    Output: 69420n

Returns
-------

`bigint`

The number of the block.

Parameters
----------

### cacheTime (optional)

*   **Type:** `number`
*   **Default:** [Client's `cacheTime`](https://viem.sh/docs/clients/public#cachetime-optional)

Time (in ms) that cached block number will remain in memory.

    const block = await publicClient.getBlockNumber({
      cacheTime: 4_000
    })

By default, block numbers are cached for the period of the [Client's `cacheTime`](https://viem.sh/docs/clients/public#cacheTime-optional).

*   Setting a value of above zero will make block number remain in the cache for that period.
*   Setting a value of `0` will disable the cache, and always retrieve a fresh block number.

Example
-------

Check out the usage of `getBlockNumber` in the live [Fetching Blocks Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/blocks_fetching-blocks) below.

JSON-RPC Method
---------------

[`eth_blockNumber`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_blocknumber)</content>
</page>

<page>
  <title>getBlock</title>
  <url>https://viem.sh/docs/actions/public/getBlock</url>
  <content>Returns information about a block at a block number, hash or tag.

Usage
-----

    import { publicClient } from './client'
     
    const block = await publicClient.getBlock() 
    Output: {  baseFeePerGas: 10789405161n,  difficulty: 11569232145203128n,  extraData: '0x75732d656173742d38',  ... }

Returns
-------

[`Block`](https://viem.sh/docs/glossary/types#block)

Information about the block.

Parameters
----------

### blockHash (optional)

*   **Type:** [`Hash`](https://viem.sh/docs/glossary/types#hash)

Information at a given block hash.

    const block = await publicClient.getBlock({
      blockHash: '0x89644bbd5c8d682a2e9611170e6c1f02573d866d286f006cbf517eec7254ec2d'
    })

### blockNumber (optional)

*   **Type:** `bigint`

Information at a given block number.

    const block = await publicClient.getBlock({
      blockNumber: 42069n
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Information at a given block tag.

    const block = await publicClient.getBlock({
      blockTag: 'safe'
    })

### includeTransactions (optional)

*   **Type:** `boolean`

Whether or not to include transactions (as a structured array of `Transaction` objects).

    const block = await publicClient.getBlock({
      includeTransactions: true
    })

Example
-------

Check out the usage of `getBlock` in the live [Fetching Blocks Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/blocks_fetching-blocks) below.

JSON-RPC Method
---------------

*   Calls [`eth_getBlockByNumber`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getblockbynumber) for `blockNumber` & `blockTag`.
*   Calls [`eth_getBlockByHash`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getblockbyhash) for `blockHash`.</content>
</page>

<page>
  <title>watchBlockNumber</title>
  <url>https://viem.sh/docs/actions/public/watchBlockNumber</url>
  <content>Watches and returns incoming block numbers.

Usage
-----

Pass through your Public Client, along with a listener.

    import { publicClient } from './client'
     
    const unwatch = publicClient.watchBlockNumber( 
      { onBlockNumber: blockNumber => console.log(blockNumber) }
    )
    > 69420n > 69421n > 69422n

Listener
--------

`(blockNumber: bigint) => void`

The block number.

Returns
-------

`UnwatchFn`

A function that can be invoked to stop watching for new block numbers.

Parameters
----------

### emitMissed (optional)

*   **Type:** `boolean`
*   **Default:** `false`

Whether or not to emit missed block numbers to the callback.

Missed block numbers may occur in instances where internet connection is lost, or the block time is lesser than the [polling interval](https://viem.sh/docs/clients/public#pollinginterval-optional) of the client.

    const unwatch = publicClient.watchBlockNumber(
      { 
        emitMissed: true, 
        onBlockNumber: blockNumber => console.log(blockNumber),
      }
    )

### emitOnBegin (optional)

*   **Type:** `boolean`
*   **Default:** `false`

Whether or not to emit the latest block number to the callback when the subscription opens.

    const unwatch = publicClient.watchBlockNumber(
      { 
        emitOnBegin: true, 
        onBlockNumber: blockNumber => console.log(blockNumber),
      }
    )

### poll (optional)

*   **Type:** `boolean`
*   **Default:** `false` for WebSocket Transports, `true` for non-WebSocket Transports

Whether or not to use a polling mechanism to check for new block numbers instead of a WebSocket subscription.

This option is only configurable for Clients with a [WebSocket Transport](https://viem.sh/docs/clients/transports/websocket).

    import { createPublicClient, webSocket } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const publicClient = createPublicClient({
      chain: mainnet,
      transport: webSocket()
    })
     
    const unwatch = publicClient.watchBlockNumber(
      { 
        onBlockNumber: blockNumber => console.log(blockNumber),
        poll: true, 
      }
    )

### pollingInterval (optional)

*   **Type:** `number`

Polling frequency (in ms). Defaults to Client's `pollingInterval` config.

    const unwatch = publicClient.watchBlockNumber(
      { 
        onBlockNumber: blockNumber => console.log(blockNumber),
        pollingInterval: 12_000, 
      }
    )

Example
-------

Check out the usage of `watchBlockNumber` in the live [Watch Block Numbers Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/blocks_watching-blocks) below.

JSON-RPC Methods
----------------

*   When `poll: true`, calls [`eth_blockNumber`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_blocknumber) on a polling interval.
*   When `poll: false` & WebSocket Transport, uses a WebSocket subscription via [`eth_subscribe`](https://docs.alchemy.com/reference/eth-subscribe-polygon) and the `"newHeads"` event.</content>
</page>

<page>
  <title>getBlockTransactionCount</title>
  <url>https://viem.sh/docs/actions/public/getBlockTransactionCount</url>
  <content>Returns the number of Transactions at a block number, hash or tag.

Usage
-----

    import { publicClient } from './client'
     
    const count = await publicClient.getBlockTransactionCount() 
    Output: 23

Returns
-------

`number`

The block transaction count.

Parameters
----------

### blockHash (optional)

*   **Type:** [`Hash`](https://viem.sh/docs/glossary/types#hash)

Count at a given block hash.

    const count = await publicClient.getBlockTransactionCount({
      blockHash: '0x89644bbd5c8d682a2e9611170e6c1f02573d866d286f006cbf517eec7254ec2d'
    })

### blockNumber (optional)

*   **Type:** `bigint`

Count at a given block number.

    const block = await publicClient.getBlockTransactionCount({
      blockNumber: 42069n
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Count at a given block tag.

    const block = await publicClient.getBlockTransactionCount({
      blockTag: 'safe'
    })

JSON-RPC Method
---------------

*   Calls [`eth_getBlockTransactionCountByNumber`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getblocktransactioncountbynumber) for `blockNumber` & `blockTag`.
*   Calls [`eth_getBlockTransactionCountByHash`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getblocktransactioncountbyhash) for `blockHash`.</content>
</page>

<page>
  <title>watchBlocks</title>
  <url>https://viem.sh/docs/actions/public/watchBlocks</url>
  <content>Watches and returns information for incoming blocks.

Usage
-----

Pass through your Public Client, along with a listener.

    import { publicClient } from './client'
     
    const unwatch = publicClient.watchBlocks( 
      { onBlock: block => console.log(block) }
    )
    > {  baseFeePerGas: 10789405161n,  difficulty: 11569232145203128n,  extraData: '0x75732d656173742d38',  ... } > {  baseFeePerGas: 12394051511n,  difficulty: 11512315412421123n,  extraData: '0x5123ab1512dd14aa',  ... }

Returns
-------

`UnwatchFn`

A function that can be invoked to stop watching for new blocks.

Parameters
----------

### onBlock

*   **Type:** `(block: Block) => void`

The block information.

    const unwatch = publicClient.watchBlocks(
      { onBlock: block => console.log(block) } 
    )

### onError (optional)

*   **Type:** `(error: Error) => void`

Error thrown from getting a block.

    const unwatch = publicClient.watchBlocks(
      { 
        onBlock: block => console.log(block),
        onError: error => console.log(error) 
      }
    )

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Watch for new blocks on a given tag.

    const unwatch = publicClient.watchBlocks(
      { 
        blockTag: 'safe',
        onBlock: block => console.log(block), 
      }
    )

### emitMissed (optional)

*   **Type:** `boolean`
*   **Default:** `false`

Whether or not to emit missed blocks to the callback.

Missed blocks may occur in instances where internet connection is lost, or the block time is lesser than the [polling interval](https://viem.sh/docs/clients/public#pollinginterval-optional) of the client.

    const unwatch = publicClient.watchBlocks(
      { 
        emitMissed: true, 
        onBlock: block => console.log(block),
      }
    )

### emitOnBegin (optional)

*   **Type:** `boolean`
*   **Default:** `false`

Whether or not to emit the block to the callback when the subscription opens.

    const unwatch = publicClient.watchBlocks(
      { 
        emitOnBegin: true, 
        onBlock: block => console.log(block),
      }
    )

### includeTransactions (optional)

*   **Type:** `boolean`

Whether or not to include transactions (as a structured array of `Transaction` objects).

    const unwatch = publicClient.watchBlocks(
      { 
        includeTransactions: true,  
        onBlock: block => console.log(block),
      }
    )

### poll (optional)

*   **Type:** `boolean`
*   **Default:** `false` for WebSocket Clients, `true` for non-WebSocket Clients

Whether or not to use a polling mechanism to check for new blocks instead of a WebSocket subscription.

This option is only configurable for Clients with a [WebSocket Transport](https://viem.sh/docs/clients/transports/websocket).

    import { createPublicClient, webSocket } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const publicClient = createPublicClient({
      chain: mainnet,
      transport: webSocket()
    })
     
    const unwatch = publicClient.watchBlocks(
      { 
        onBlock: block => console.log(block),
        poll: true, 
      }
    )

### pollingInterval (optional)

*   **Type:** `number`

Polling frequency (in ms). Defaults to the Client's `pollingInterval` config.

    const unwatch = publicClient.watchBlocks(
      { 
        onBlock: block => console.log(block),
        pollingInterval: 1_000, 
      }
    )

Example
-------

Check out the usage of `watchBlocks` in the live [Watch Blocks Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/blocks_watching-blocks) below.

JSON-RPC Methods
----------------

*   When `poll: true`, calls [`eth_getBlockByNumber`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getBlockByNumber) on a polling interval.
*   When `poll: false` & WebSocket Transport, uses a WebSocket subscription via [`eth_subscribe`](https://docs.alchemy.com/reference/eth-subscribe-polygon) and the `"newHeads"` event.</content>
</page>

<page>
  <title>simulateBlocks</title>
  <url>https://viem.sh/docs/actions/public/simulateBlocks</url>
  <content>[Skip to content](https://viem.sh/docs/actions/public/simulateBlocks#vocs-content)

Simulates a set of calls on block(s) with optional block and state overrides. Internally uses the [`eth_simulateV1` JSON-RPC method](https://github.com/ethereum/execution-apis/pull/484).

Usage
-----

    import { parseEther } from 'viem'
    import { client } from './config'
     
    const result = await client.simulateBlocks({
      blocks: [{
        blockOverrides: {
          number: 69420n,
        },
        calls: [
          {
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
            to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
            value: parseEther('2'),
          },
          {
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
            value: parseEther('1'),
          },
        ],
        stateOverrides: [{
          address: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
          balance: parseEther('10'),
        }],
      }]
    })

### Contract Calls

The `calls` property also accepts **Contract Calls**, and can be used via the `abi`, `functionName`, and `args` properties.

    import { parseAbi, parseEther } from 'viem'
    import { client } from './config'
     
    const abi = parseAbi([
      'function approve(address, uint256) returns (bool)',
      'function transferFrom(address, address, uint256) returns (bool)',
    ])
     
    const result = await client.simulateBlocks({ 
      blocks: [{
        calls: [
          {
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
            value: parseEther('1')
          },
          {
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
            to: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
            abi,
            functionName: 'approve',
            args: [
              '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
              100n
            ],
          },
          {
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
            to: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
            abi,
            functionName: 'transferFrom',
            args: [
              '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
              '0x0000000000000000000000000000000000000000',
              100n
            ],
          },
        ],
      }]
    })

Return Value
------------

`SimulateBlocksReturnType`

Simulation results.

Parameters
----------

### blocks

Blocks to simulate.

### blocks.calls

*   **Type:** `TransactionRequest[]`

Calls to simulate. Each call can consist of transaction request properties.

    const result = await client.simulateBlocks({
      blocks: [{
        blockOverrides: {
          number: 69420n,
        },
        calls: [ 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            data: '0xdeadbeef', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
          }, 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
            value: parseEther('1'), 
          }, 
        ], 
        stateOverrides: [{
          address: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
          balance: parseEther('10'),
        }],
      }]
    })

### blocks.blockOverrides

*   **Type:** `BlockOverrides`

Values to override on the block.

    const result = await client.simulateBlocks({
      blocks: [{
        blockOverrides: { 
          number: 69420n, 
        }, 
        calls: [ 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            data: '0xdeadbeef', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
          }, 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
            value: parseEther('1'), 
          }, 
        ], 
        stateOverrides: [{
          address: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
          balance: parseEther('10'),
        }],
      }]
    })

### blocks.stateOverrides

*   **Type:** `StateOverride`

State overrides.

    const result = await client.simulateBlocks({
      blocks: [{
        blockOverrides: {
          number: 69420n,
        },
        calls: [ 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            data: '0xdeadbeef', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
          }, 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
            value: parseEther('1'), 
          }, 
        ], 
        stateOverrides: [{ 
          address: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
          balance: parseEther('10'), 
        }], 
      }]
    })

### returnFullTransactions

*   **Type:** `boolean`

Whether to return the full transactions.

    const result = await client.simulateBlocks({
      blocks: [{
        blockOverrides: {
          number: 69420n,
        },
        calls: [ 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            data: '0xdeadbeef', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
          }, 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
            value: parseEther('1'), 
          }, 
        ], 
        stateOverrides: [{
          address: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
          balance: parseEther('10'),
        }],
      }],
      returnFullTransactions: true, 
    })

### traceTransfers

*   **Type:** `boolean`

Whether to trace transfers.

    const result = await client.simulateBlocks({
      blocks: [{
        blockOverrides: {
          number: 69420n,
        },
        calls: [ 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            data: '0xdeadbeef', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
          }, 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
            value: parseEther('1'), 
          }, 
        ], 
        stateOverrides: [{
          address: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
          balance: parseEther('10'),
        }],
      }],
      traceTransfers: true, 
    })

### validation

*   **Type:** `boolean`

Whether to enable validation mode.

    const result = await client.simulateBlocks({
      blocks: [{
        blockOverrides: {
          number: 69420n,
        },
        calls: [ 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            data: '0xdeadbeef', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
          }, 
          { 
            from: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
            to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
            value: parseEther('1'), 
          }, 
        ], 
        stateOverrides: [{
          address: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
          balance: parseEther('10'),
        }],
      }],
      validation: true, 
    })</content>
</page>

<page>
  <title>getChainId</title>
  <url>https://viem.sh/docs/actions/public/getChainId</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/public/introduction)

Access List

[createAccessList](https://viem.sh/docs/actions/public/createAccessList)

Account

[getBalance](https://viem.sh/docs/actions/public/getBalance)[getTransactionCount](https://viem.sh/docs/actions/public/getTransactionCount)

Block

[getBlock](https://viem.sh/docs/actions/public/getBlock)[getBlockNumber](https://viem.sh/docs/actions/public/getBlockNumber)[getBlockTransactionCount](https://viem.sh/docs/actions/public/getBlockTransactionCount)[simulateBlocks](https://viem.sh/docs/actions/public/simulateBlocks)[watchBlockNumber](https://viem.sh/docs/actions/public/watchBlockNumber)[watchBlocks](https://viem.sh/docs/actions/public/watchBlocks)

Calls

[call](https://viem.sh/docs/actions/public/call)[simulateCalls](https://viem.sh/docs/actions/public/simulateCalls)

Chain

[getChainId](https://viem.sh/docs/actions/public/getChainId)

EIP-712

[getEip712Domain](https://viem.sh/docs/actions/public/getEip712Domain)

Fee

[estimateFeesPerGas](https://viem.sh/docs/actions/public/estimateFeesPerGas)[estimateGas](https://viem.sh/docs/actions/public/estimateGas)[estimateMaxPriorityFeePerGas](https://viem.sh/docs/actions/public/estimateMaxPriorityFeePerGas)[getBlobBaseFee](https://viem.sh/docs/actions/public/getBlobBaseFee)[getFeeHistory](https://viem.sh/docs/actions/public/getFeeHistory)[getGasPrice](https://viem.sh/docs/actions/public/getGasPrice)

Filters & Logs

[createBlockFilter](https://viem.sh/docs/actions/public/createBlockFilter)[createEventFilter](https://viem.sh/docs/actions/public/createEventFilter)[createPendingTransactionFilter](https://viem.sh/docs/actions/public/createPendingTransactionFilter)[getFilterChanges](https://viem.sh/docs/actions/public/getFilterChanges)[getFilterLogs](https://viem.sh/docs/actions/public/getFilterLogs)[getLogs](https://viem.sh/docs/actions/public/getLogs)[watchEvent](https://viem.sh/docs/actions/public/watchEvent)[uninstallFilter](https://viem.sh/docs/actions/public/uninstallFilter)

Proof

[getProof](https://viem.sh/docs/actions/public/getProof)

Signature

[verifyMessage](https://viem.sh/docs/actions/public/verifyMessage)[verifyTypedData](https://viem.sh/docs/actions/public/verifyTypedData)

Transaction

[prepareTransactionRequest](https://viem.sh/docs/actions/wallet/prepareTransactionRequest)[getTransaction](https://viem.sh/docs/actions/public/getTransaction)[getTransactionConfirmations](https://viem.sh/docs/actions/public/getTransactionConfirmations)[getTransactionReceipt](https://viem.sh/docs/actions/public/getTransactionReceipt)[sendRawTransaction](https://viem.sh/docs/actions/wallet/sendRawTransaction)[waitForTransactionReceipt](https://viem.sh/docs/actions/public/waitForTransactionReceipt)[watchPendingTransactions](https://viem.sh/docs/actions/public/watchPendingTransactions)

Wallet Actions

Chevron Right

Test Actions

Chevron Right

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>getEip712Domain</title>
  <url>https://viem.sh/docs/actions/public/getEip712Domain</url>
  <content>Reads the EIP-712 domain from a contract, based on the [ERC-5267 specification](https://eips.ethereum.org/EIPS/eip-5267).

Usage
-----

    import { publicClient } from './client'
     
    const { domain, extensions, fields } = await publicClient.getEip712Domain({ 
      address: '0x57ba3ec8df619d4d243ce439551cce713bb17411',
    })

### Counterfactual Call

It is possible to read the EIP-712 domain on a contract that **has not been deployed** by providing deployment factory (`factory` + `factoryData`) parameters:

    import { factory, publicClient } from './config'
     
    const { domain, extensions, fields } = await publicClient.getEip712Domain({ 
      address: '0x57ba3ec8df619d4d243ce439551cce713bb17411',
      factory: factory.address,
      factoryData: encodeFunctionData({
        abi: factory.abi,
        functionName: 'createAccount',
        args: ['0x0000000000000000000000000000000000000000', 0n]
      }),
    })

Returns
-------

`GetEip712DomainReturnType`

The EIP-712 domain (`domain`) for the contract, with `fields` and `extensions`, as per [ERC-5267](https://eips.ethereum.org/EIPS/eip-5267).

Parameters
----------

### address

*   **Type:** `string`

The address of the contract to read the EIP-712 domain from.

    const result = await publicClient.getEip712Domain({ 
      address: '0x57ba3ec8df619d4d243ce439551cce713bb17411', 
    })

### factory (optional)

*   **Type:**

Contract deployment factory address (ie. Create2 factory, Smart Account factory, etc).

    const result = await publicClient.getEip712Domain({ 
      address: '0x57ba3ec8df619d4d243ce439551cce713bb17411',
      factory: '0xE8Df82fA4E10e6A12a9Dab552bceA2acd26De9bb', 
      factoryData: '0xdeadbeef',
    })

### factoryData (optional)

*   **Type:**

Calldata to execute on the factory to deploy the contract.

    const result = await publicClient.getEip712Domain({ 
      address: '0x57ba3ec8df619d4d243ce439551cce713bb17411',
      factory: '0xE8Df82fA4E10e6A12a9Dab552bceA2acd26De9bb',
      factoryData: '0xdeadbeef', 
    })</content>
</page>

<page>
  <title>estimateFeesPerGas</title>
  <url>https://viem.sh/docs/actions/public/estimateFeesPerGas</url>
  <content>Returns an estimate for the fees per gas (in wei) for a transaction to be likely included in the next block.

If [`chain.fees.estimateFeesPerGas`](https://viem.sh/docs/actions/public/estimateFeesPerGas) is set on the [Client Chain](https://viem.sh/docs/clients/public#chain-optional) or [override Chain](https://viem.sh/docs/actions/public/estimateFeesPerGas#chain-optional), it will use the returned value.

Otherwise, for EIP-1559 Transactions, viem will estimate the fees using a combination of the block's base fee per gas (to derive `maxFeePerGas`) + the [`estimateMaxPriorityFeePerGas` Action](https://viem.sh/docs/actions/public/estimateMaxPriorityFeePerGas) (to derive `maxPriorityFeePerGas`). For Legacy Transactions, viem will estimate the fee based on the gas price (via the [`getGasPrice` Action](https://viem.sh/docs/actions/public/getGasPrice)).

Usage
-----

    import { publicClient } from './client'
     
    const {
      maxFeePerGas,
      maxPriorityFeePerGas
    } = await publicClient.estimateFeesPerGas()
    {   maxFeePerGas: 15_000_000_000n,   maxPriorityFeePerGas: 1_000_000_000n, } const { gasPrice } = await publicClient.estimateFeesPerGas({
      type: 'legacy'
    })
    { gasPrice: 15_000_000_000n } 

Returns
-------

[`FeeValues`](https://viem.sh/docs/glossary/types#feevalues)

An estimate (in wei) for the fees per gas.

Parameters
----------

### chain (optional)

*   **Type:** [Chain](https://viem.sh/docs/glossary/types#chain)
*   **Default:** [`client.chain`](https://viem.sh/docs/clients/public#chain-optional)

Optional Chain override. Used to infer the fees per gas from [`chain.fees.estimateFeesPerGas`](https://viem.sh/docs/actions/public/estimateFeesPerGas).

    import { optimism } from 'viem/chains'
     
    const { maxFeePerGas, maxPriorityFeePerGas } = 
      await publicClient.estimateFeesPerGas({
        chain: optimism 
      })

### type (optional)

*   **Type:** `"legacy" | "eip1559"`
*   **Default:** `"eip1559"`

    const { gasPrice } = await publicClient.estimateFeesPerGas({
      type: 'legacy'
    })</content>
</page>

<page>
  <title>call</title>
  <url>https://viem.sh/docs/actions/public/call</url>
  <content>Executes a new message call immediately without submitting a transaction to the network.

Usage
-----

    import { account, publicClient } from './config'
     
    const data = await publicClient.call({ 
      account,
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### Deployless Calls

It is possible to call a function on a contract that has not been deployed yet. For instance, we may want to call a function on an [ERC-4337 Smart Account](https://eips.ethereum.org/EIPS/eip-4337) contract which has not been deployed.

Viem offers two ways of performing a Deployless Call, via:

*   [Bytecode](https://viem.sh/docs/actions/public/call#bytecode)
*   a [Deploy Factory](https://viem.sh/docs/actions/public/call#deploy-factory): "temporarily deploys" a contract with a provided [Deploy Factory](https://docs.alchemy.com/docs/create2-an-alternative-to-deriving-contract-addresses#create2-contract-factory), and calls the function on the deployed contract.

#### Bytecode

The example below demonstrates how we can utilize a Deployless Call **via Bytecode** to call the `name` function on the [Wagmi Example ERC721 contract](https://etherscan.io/address/0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2#code) which has not been deployed:

    import { encodeFunctionData, parseAbi } from 'viem'
    import { publicClient } from './config'
     
    const data = await publicClient.call({
      // Bytecode of the contract. Accessible here: https://etherscan.io/address/0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2#code
      code: '0x...',
      // Function to call on the contract.
      data: encodeFunctionData({
        abi: parseAbi(['function name() view returns (string)']),
        functionName: 'name'
      }),
    })

#### Deploy Factory

The example below demonstrates how we can utilize a Deployless Call **via a [Deploy Factory](https://docs.alchemy.com/docs/create2-an-alternative-to-deriving-contract-addresses#create2-contract-factory)** to call the `entryPoint` function on an [ERC-4337 Smart Account](https://eips.ethereum.org/EIPS/eip-4337) which has not been deployed:

    import { encodeFunctionData, parseAbi } from 'viem'
    import { owner, publicClient } from './config'
     
    const data = await publicClient.call({
      // Address of the contract deployer (e.g. Smart Account Factory).
      factory: '0xE8Df82fA4E10e6A12a9Dab552bceA2acd26De9bb',
     
      // Function to execute on the factory to deploy the contract.
      factoryData: encodeFunctionData({
        abi: parseAbi(['function createAccount(address owner, uint256 salt)']),
        functionName: 'createAccount',
        args: [owner, 0n],
      }),
     
      // Function to call on the contract (e.g. Smart Account contract).
      data: encodeFunctionData({
        abi: parseAbi(['function entryPoint() view returns (address)']),
        functionName: 'entryPoint'
      }),
     
      // Address of the contract.
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

Returns
-------

`0x${string}`

The call data.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to call from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### data

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### to

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address or recipient.

    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### blockNumber (optional)

*   **Type:** `number`

The block number to perform the call against.

    const data = await publicClient.call({
      blockNumber: 15121123n, 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

The block tag to perform the call against.

    const data = await publicClient.call({
      blockTag: 'safe', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### code (optional)

*   **Type:**

Bytecode to perform the call against.

    const data = await publicClient.call({
      code: '0x...', 
      data: '0xdeadbeef',
    })

### factory (optional)

*   **Type:**

Contract deployment factory address (ie. Create2 factory, Smart Account factory, etc).

    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      factory: '0x0000000000ffe8b47b3e2130213b802212439497', 
      factoryData: '0xdeadbeef',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### factoryData (optional)

*   **Type:**

Calldata to execute on the factory to deploy the contract.

    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      factory: '0x0000000000ffe8b47b3e2130213b802212439497',
      factoryData: '0xdeadbeef', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### gas (optional)

*   **Type:** `bigint`

The gas provided for transaction execution.

    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      gas: 1_000_000n, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    import { parseGwei } from 'viem'
     
    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction).

    import { parseGwei } from 'viem'
     
    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      maxFeePerGas: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction).

    import { parseGwei } from 'viem'
     
    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### nonce (optional)

*   **Type:** `bigint`

Unique number identifying this transaction.

    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      nonce: 420, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### stateOverride (optional)

*   **Type:** [`StateOverride`](https://viem.sh/docs/glossary/types#stateoverride)

The state override set is an optional address-to-state mapping, where each entry specifies some state to be ephemerally overridden prior to executing the call.

    const data = await publicClient.call({
      account,
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      stateOverride: [ 
        { 
          address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
          balance: parseEther('1'), 
          stateDiff: [ 
            { 
              slot: '0x3ea2f1d0abf3fc66cf29eebb70cbd4e7fe762ef8a09bcc06c8edf641230afec0', 
              value: '0x00000000000000000000000000000000000000000000000000000000000001a4', 
            }, 
          ], 
        } 
      ], 
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    import { parseEther } from 'viem'
     
    const data = await publicClient.call({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
    })

JSON-RPC Methods
----------------

[`eth_call`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_call)</content>
</page>

<page>
  <title>simulateCalls</title>
  <url>https://viem.sh/docs/actions/public/simulateCalls</url>
  <content>Simulates a set of calls for a block, and optionally provides asset changes. Internally uses the [`eth_simulateV1` JSON-RPC method](https://github.com/ethereum/execution-apis/pull/484).

Usage
-----

    import { parseEther } from 'viem'
    import { client } from './config'
     
    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [
        {
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'),
        },
        {
          to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
          value: parseEther('1'),
        },
      ],
    })
     
    console.log(results)
    [   {     gasUsed: 21000n,     logs: [],     status: "success",   },   {     gasUsed: 21000n,     logs: [],     status: "success",   }, ]

### Contract Calls

The `calls` property also accepts **Contract Calls**, and can be used via the `abi`, `functionName`, and `args` properties.

    import { parseAbi, parseEther } from 'viem'
    import { client } from './config'
     
    const abi = parseAbi([
      'function mint()',
      'function transfer(address, uint256) returns (bool)',
    ])
     
    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [
        {
          to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
          value: parseEther('1')
        },
        {
          to: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi,
          functionName: 'mint',
        },
        {
          to: '0x95aD61b0a150d79219dCF64E1E6Cc01f0B64C4cE',
          abi,
          functionName: 'transfer',
          args: [
            '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
            100n
          ],
        },
      ],
    })
     
    console.log(results)
    [   {     gasUsed: 21000n,     logs: [],     result: undefined,     status: "success",   },   {     gasUsed: 78394n,     logs: [...],     result: undefined,     status: "success",   },   {     gasUsed: 51859n,     logs: [...],     result: true,     status: "success",   }, ]

### Asset Changes

Providing the `traceAssetChanges` parameter (with an `account`) will return asset balance changes for the calls.

    import { parseAbi, parseEther } from 'viem'
    import { client } from './config'
     
    const abi = parseAbi([
      'function mint()',
      'function transfer(address, uint256) returns (bool)',
    ])
     
    const { assetChanges, results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [
        {
          to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
          value: parseEther('1.5')
        },
        {
          to: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi,
          functionName: 'mint',
        },
        {
          to: '0x95aD61b0a150d79219dCF64E1E6Cc01f0B64C4cE',
          abi,
          functionName: 'transfer',
          args: [
            '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
            100n
          ],
        },
      ],
      traceAssetChanges: true, 
    })
     
    console.log(assetChanges)
    [   {     token: {       address: "0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee",       decimals: 18,       symbol: "ETH",     },     value: {       diff: -1500000000000000000n,       post: 9850000000000000000000n,       pre: 10000000000000000000000n,     },   }   {     token: {       address: "0xfba3912ca04dd458c843e2ee08967fc04f3579c2",       decimals: 1,       symbol: "WAGMI",     },     value: {       diff: 1n,       post: 1n,       pre: 0n,     },   },   {     token: {       address: "0x95ad61b0a150d79219dcf64e1e6cc01f0b64c4ce",       decimals: 18,       symbol: "SHIB",     },     value: {       diff: -1000000000000000000n,       post: 410429569258816445970930282571360n,       pre: 410429569258817445970930282571360n,     },   } ]

### Reading Contracts

It is also worth noting that `simulateCalls` also supports "reading" contracts.

    import { parseAbi } from 'viem'
    import { client } from './config'
     
    const abi = parseAbi([
      'function totalSupply() returns (uint256)',
      'function ownerOf(uint256) returns (address)',
    ])
     
    const { results } = await client.simulateCalls({
      calls: [
        {
          to: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi,
          functionName: 'totalSupply',
        },
        {
          to: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi,
          functionName: 'ownerOf',
          args: [69420n],
        },
        {
          to: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
          abi,
          functionName: 'ownerOf',
          args: [13371337n],
        },
      ],
    })
     
    console.log(results)
    [   {     result: 424122n,     status: "success",   },   {     result: "0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b",     status: "success",   },   {     error: [ContractFunctionExecutionError: token has no owner],     status: "failure",   }, ]

Return Value
------------

`SimulateCallsReturnType`

Simulation results.

Parameters
----------

### calls

*   **Type:** `Calls`

Calls to simulate.

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D', 
          value: parseEther('2'), 
        }, 
        { 
          to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
          value: parseEther('1'), 
        }, 
      ], 
    })

### calls.data

*   **Type:** `Hex`

Calldata to broadcast (typically a contract function selector with encoded arguments, or contract deployment bytecode).

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [ 
        { 
          data: '0xdeadbeef', 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D', 
          value: parseEther('2'), 
        },  
      ], 
    })

### calls.to

*   **Type:** `Address`

The recipient address.

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D', 
          value: parseEther('2'),
        },  
      ], 
    })

### calls.value

*   **Type:** `Address`

Value to send with the call.

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'), 
        },  
      ], 
    })

### account (optional)

*   **Type:** `Account | Address`

The account to simulate the calls from.

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'),
        },  
      ], 
    })

### blockNumber (optional)

*   **Type:** `bigint`

The block number to simulate the calls at.

    const { results } = await client.simulateCalls({
      blockNumber: 17030000n, 
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'),
        },  
      ], 
    })

### blockTag (optional)

*   **Type:** `BlockTag`

The block tag to simulate the calls at.

    const { results } = await client.simulateCalls({
      blockTag: 'pending', 
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'),
        },  
      ], 
    })

### stateOverrides (optional)

*   **Type:** `StateOverride`

The state overrides to simulate the calls with.

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'),
        },  
      ], 
      stateOverrides: [{ 
        address: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929', 
        balance: parseEther('10000'), 
      }], 
    })

### traceAssetChanges (optional)

*   **Type:** `boolean`

Whether to trace asset changes.

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'),
        },  
      ], 
      traceAssetChanges: true, 
    })

### traceTransfers (optional)

*   **Type:** `boolean`

Whether to trace transfers.

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'),
        },  
      ], 
      traceTransfers: true, 
    })

### validation (optional)

*   **Type:** `boolean`

Whether to enable validation mode.

    const { results } = await client.simulateCalls({
      account: '0x5a0b54d5dc17e482fe8b0bdca5320161b95fb929',
      calls: [ 
        { 
          to: '0xcb98643b8786950F0461f3B0edf99D88F274574D',
          value: parseEther('2'),
        },  
      ], 
      validation: true, 
    })</content>
</page>

<page>
  <title>getBlobBaseFee</title>
  <url>https://viem.sh/docs/actions/public/getBlobBaseFee</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/public/introduction)

Access List

[createAccessList](https://viem.sh/docs/actions/public/createAccessList)

Account

[getBalance](https://viem.sh/docs/actions/public/getBalance)[getTransactionCount](https://viem.sh/docs/actions/public/getTransactionCount)

Block

[getBlock](https://viem.sh/docs/actions/public/getBlock)[getBlockNumber](https://viem.sh/docs/actions/public/getBlockNumber)[getBlockTransactionCount](https://viem.sh/docs/actions/public/getBlockTransactionCount)[simulateBlocks](https://viem.sh/docs/actions/public/simulateBlocks)[watchBlockNumber](https://viem.sh/docs/actions/public/watchBlockNumber)[watchBlocks](https://viem.sh/docs/actions/public/watchBlocks)

Calls

[call](https://viem.sh/docs/actions/public/call)[simulateCalls](https://viem.sh/docs/actions/public/simulateCalls)

Chain

[getChainId](https://viem.sh/docs/actions/public/getChainId)

EIP-712

[getEip712Domain](https://viem.sh/docs/actions/public/getEip712Domain)

Fee

[estimateFeesPerGas](https://viem.sh/docs/actions/public/estimateFeesPerGas)[estimateGas](https://viem.sh/docs/actions/public/estimateGas)[estimateMaxPriorityFeePerGas](https://viem.sh/docs/actions/public/estimateMaxPriorityFeePerGas)[getBlobBaseFee](https://viem.sh/docs/actions/public/getBlobBaseFee)[getFeeHistory](https://viem.sh/docs/actions/public/getFeeHistory)[getGasPrice](https://viem.sh/docs/actions/public/getGasPrice)

Filters & Logs

[createBlockFilter](https://viem.sh/docs/actions/public/createBlockFilter)[createEventFilter](https://viem.sh/docs/actions/public/createEventFilter)[createPendingTransactionFilter](https://viem.sh/docs/actions/public/createPendingTransactionFilter)[getFilterChanges](https://viem.sh/docs/actions/public/getFilterChanges)[getFilterLogs](https://viem.sh/docs/actions/public/getFilterLogs)[getLogs](https://viem.sh/docs/actions/public/getLogs)[watchEvent](https://viem.sh/docs/actions/public/watchEvent)[uninstallFilter](https://viem.sh/docs/actions/public/uninstallFilter)

Proof

[getProof](https://viem.sh/docs/actions/public/getProof)

Signature

[verifyMessage](https://viem.sh/docs/actions/public/verifyMessage)[verifyTypedData](https://viem.sh/docs/actions/public/verifyTypedData)

Transaction

[prepareTransactionRequest](https://viem.sh/docs/actions/wallet/prepareTransactionRequest)[getTransaction](https://viem.sh/docs/actions/public/getTransaction)[getTransactionConfirmations](https://viem.sh/docs/actions/public/getTransactionConfirmations)[getTransactionReceipt](https://viem.sh/docs/actions/public/getTransactionReceipt)[sendRawTransaction](https://viem.sh/docs/actions/wallet/sendRawTransaction)[waitForTransactionReceipt](https://viem.sh/docs/actions/public/waitForTransactionReceipt)[watchPendingTransactions](https://viem.sh/docs/actions/public/watchPendingTransactions)

Wallet Actions

Chevron Right

Test Actions

Chevron Right

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>estimateMaxPriorityFeePerGas</title>
  <url>https://viem.sh/docs/actions/public/estimateMaxPriorityFeePerGas</url>
  <content>Returns an estimate for the max priority fee per gas (in wei) for a transaction to be likely included in the next block.

If [`chain.fees.defaultPriorityFee`](https://viem.sh/docs/chains/fees#feesdefaultpriorityfee) is set on the [Client Chain](https://viem.sh/docs/clients/public#chain-optional) or [override Chain](https://viem.sh/docs/actions/public/estimateMaxPriorityFeePerGas#chain-optional), it will use that value.

Otherwise, the Action will either call [`eth_maxPriorityFeePerGas`](https://github.com/ethereum/execution-apis/blob/fe8e13c288c592ec154ce25c534e26cb7ce0530d/src/eth/fee_market.yaml#L9-L16) (if supported) or manually calculate the max priority fee per gas based on the current block base fee per gas + gas price.

Usage
-----

    import { publicClient } from './client'
     
    const maxPriorityFeePerGas = await publicClient.estimateMaxPriorityFeePerGas()
    Output: 1_000_000_000n

Returns
-------

`bigint`

An estimate (in wei) for the max priority fee per gas.

Parameters
----------

### chain (optional)

*   **Type:** [Chain](https://viem.sh/docs/glossary/types#chain)
*   **Default:** [`client.chain`](https://viem.sh/docs/clients/public#chain-optional)

Optional Chain override. Used to infer the default `maxPriorityFeePerGas` from [`chain.fees.defaultPriorityFee`](https://viem.sh/docs/chains/fees#feesdefaultpriorityfee).

    import { optimism } from 'viem/chains'
     
    const maxPriorityFeePerGas = 
      await publicClient.estimateMaxPriorityFeePerGas({
        chain: optimism 
      })</content>
</page>

<page>
  <title>estimateGas</title>
  <url>https://viem.sh/docs/actions/public/estimateGas</url>
  <content>Estimates the gas necessary to complete a transaction without submitting it to the network.

Usage
-----

    import { account, publicClient } from './config'
     
    const gas = await publicClient.estimateGas({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

Returns
-------

`bigint`

The gas estimate (in gas).

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate gas from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    import { parseEther } from 'viem'
     
    const gas = await publicClient.estimateGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### data (optional)

*   **Type:** `0x${string}`

Contract code or a hashed method call with encoded args which can be generated using [encodeFunctionData](https://viem.sh/docs/contract/encodeFunctionData).

    import { parseEther } from 'viem'
     
    const gas = await publicClient.estimateGas({
      data: '0x...', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    import { parseEther, parseGwei } from 'viem'
     
    const gas = await publicClient.estimateGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    import { parseEther, parseGwei } from 'viem'
     
    const gas = await publicClient.estimateGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    import { parseEther, parseGwei } from 'viem'
     
    const gas = await publicClient.estimateGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### to (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Transaction recipient.

    import { parseEther } from 'viem'
     
    const gas = await publicClient.estimateGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1')
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    import { parseEther } from 'viem'
     
    const gas = await publicClient.estimateGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### blockNumber (optional)

*   **Type:** `number`

The block number to perform the gas estimate against.

    import { parseEther } from 'viem'
     
    const gas = await publicClient.estimateGas({
      blockNumber: 15121123n, 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

The block tag to perform the gas estimate against.

    import { parseEther } from 'viem'
     
    const gas = await publicClient.estimateGas({
      blockTag: 'safe', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### stateOverride (optional)

*   **Type:** [`StateOverride`](https://viem.sh/docs/glossary/types#stateoverride)

The state override set is an optional address-to-state mapping, where each entry specifies some state to be ephemerally overridden prior to executing the call.

    const data = await publicClient.estimateGas({
      account,
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      stateOverride: [ 
        { 
          address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
          balance: parseEther('1'), 
          stateDiff: [ 
            { 
              slot: '0x3ea2f1d0abf3fc66cf29eebb70cbd4e7fe762ef8a09bcc06c8edf641230afec0', 
              value: '0x00000000000000000000000000000000000000000000000000000000000001a4', 
            }, 
          ], 
        } 
      ], 
    })

JSON-RPC Methods
----------------

[`eth_estimateGas`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_estimategas)</content>
</page>

<page>
  <title>getGasPrice</title>
  <url>https://viem.sh/docs/actions/public/getGasPrice</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/public/introduction)

Access List

[createAccessList](https://viem.sh/docs/actions/public/createAccessList)

Account

[getBalance](https://viem.sh/docs/actions/public/getBalance)[getTransactionCount](https://viem.sh/docs/actions/public/getTransactionCount)

Block

[getBlock](https://viem.sh/docs/actions/public/getBlock)[getBlockNumber](https://viem.sh/docs/actions/public/getBlockNumber)[getBlockTransactionCount](https://viem.sh/docs/actions/public/getBlockTransactionCount)[simulateBlocks](https://viem.sh/docs/actions/public/simulateBlocks)[watchBlockNumber](https://viem.sh/docs/actions/public/watchBlockNumber)[watchBlocks](https://viem.sh/docs/actions/public/watchBlocks)

Calls

[call](https://viem.sh/docs/actions/public/call)[simulateCalls](https://viem.sh/docs/actions/public/simulateCalls)

Chain

[getChainId](https://viem.sh/docs/actions/public/getChainId)

EIP-712

[getEip712Domain](https://viem.sh/docs/actions/public/getEip712Domain)

Fee

[estimateFeesPerGas](https://viem.sh/docs/actions/public/estimateFeesPerGas)[estimateGas](https://viem.sh/docs/actions/public/estimateGas)[estimateMaxPriorityFeePerGas](https://viem.sh/docs/actions/public/estimateMaxPriorityFeePerGas)[getBlobBaseFee](https://viem.sh/docs/actions/public/getBlobBaseFee)[getFeeHistory](https://viem.sh/docs/actions/public/getFeeHistory)[getGasPrice](https://viem.sh/docs/actions/public/getGasPrice)

Filters & Logs

[createBlockFilter](https://viem.sh/docs/actions/public/createBlockFilter)[createEventFilter](https://viem.sh/docs/actions/public/createEventFilter)[createPendingTransactionFilter](https://viem.sh/docs/actions/public/createPendingTransactionFilter)[getFilterChanges](https://viem.sh/docs/actions/public/getFilterChanges)[getFilterLogs](https://viem.sh/docs/actions/public/getFilterLogs)[getLogs](https://viem.sh/docs/actions/public/getLogs)[watchEvent](https://viem.sh/docs/actions/public/watchEvent)[uninstallFilter](https://viem.sh/docs/actions/public/uninstallFilter)

Proof

[getProof](https://viem.sh/docs/actions/public/getProof)

Signature

[verifyMessage](https://viem.sh/docs/actions/public/verifyMessage)[verifyTypedData](https://viem.sh/docs/actions/public/verifyTypedData)

Transaction

[prepareTransactionRequest](https://viem.sh/docs/actions/wallet/prepareTransactionRequest)[getTransaction](https://viem.sh/docs/actions/public/getTransaction)[getTransactionConfirmations](https://viem.sh/docs/actions/public/getTransactionConfirmations)[getTransactionReceipt](https://viem.sh/docs/actions/public/getTransactionReceipt)[sendRawTransaction](https://viem.sh/docs/actions/wallet/sendRawTransaction)[waitForTransactionReceipt](https://viem.sh/docs/actions/public/waitForTransactionReceipt)[watchPendingTransactions](https://viem.sh/docs/actions/public/watchPendingTransactions)

Wallet Actions

Chevron Right

Test Actions

Chevron Right

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>createBlockFilter</title>
  <url>https://viem.sh/docs/actions/public/createBlockFilter</url>
  <content>    import { publicClient } from './client'
     
    const filter = await publicClient.createBlockFilter() 
    { id: "0x345a6572337856574a76364e457a4366", type: 'block' }</content>
</page>

<page>
  <title>getFeeHistory</title>
  <url>https://viem.sh/docs/actions/public/getFeeHistory</url>
  <content>Returns a collection of historical gas information.

Usage
-----

    import { publicClient } from './client'
     
    const feeHistory = await publicClient.getFeeHistory({ 
      blockCount: 4,
      rewardPercentiles: [25, 75]
    })

Returns
-------

[`FeeHistory`](https://viem.sh/docs/glossary/types#feehistory)

The fee history.

Parameters
----------

### blockCount

*   **Type:** `number`

Number of blocks in the requested range. Between 1 and 1024 blocks can be requested in a single query. Less than requested may be returned if not all blocks are available.

    const feeHistory = await publicClient.getFeeHistory({
      blockCount: 4, 
      rewardPercentiles: [25, 75]
    })

### rewardPercentiles

*   **Type:** `number[]`

A monotonically increasing list of percentile values to sample from each block's effective priority fees per gas in ascending order, weighted by gas used.

    const feeHistory = await publicClient.getFeeHistory({
      blockCount: 4,
      rewardPercentiles: [25, 75] 
    })

### blockNumber (optional)

*   **Type:** `number`

Highest number block of the requested range.

    const feeHistory = await publicClient.getFeeHistory({
      blockCount: 4,
      blockNumber: 1551231n, 
      rewardPercentiles: [25, 75]
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Highest number block of the requested range.

    const feeHistory = await publicClient.getFeeHistory({
      blockCount: 4,
      blockTag: 'safe', 
      rewardPercentiles: [25, 75]
    })

JSON-RPC Method
---------------

*   Calls [`eth_feeHistory`](https://docs.alchemy.com/reference/eth-feehistory).</content>
</page>

<page>
  <title>createPendingTransactionFilter</title>
  <url>https://viem.sh/docs/actions/public/createPendingTransactionFilter</url>
  <content>[Skip to content](https://viem.sh/docs/actions/public/createPendingTransactionFilter#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

An Action for creating a new pending transaction filter.

Creates a Filter to listen for new pending transaction hashes that can be used with [`getFilterChanges`](https://viem.sh/docs/actions/public/getFilterChanges).

Usage
-----

File

example.ts

    import { publicClient } from './client'
     
    const filter = await publicClient.createPendingTransactionFilter() 
    Output: { id: "0x345a6572337856574a76364e457a4366", type: 'transaction' }

Returns
-------

[`Filter`](https://viem.sh/docs/glossary/types#filter)

JSON-RPC Methods
----------------

[`eth_newPendingTransactionFilter`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_newpendingtransactionfilter)</content>
</page>

<page>
  <title>getFilterLogs</title>
  <url>https://viem.sh/docs/actions/public/getFilterLogs</url>
  <content>    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
     
    const filter = await publicClient.createEventFilter({ 
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed, address indexed, uint256)'),
    })
    const logs = await publicClient.getFilterLogs({ filter })
    [{ ... }, { ... }, { ... }]</content>
</page>

<page>
  <title>getFilterChanges</title>
  <url>https://viem.sh/docs/actions/public/getFilterChanges</url>
  <content>Returns a list of logs or hashes based on a [Filter](https://viem.sh/docs/glossary/terms#filter) since the last time it was called.

A Filter can be created from the following actions:

*   [`createBlockFilter`](https://viem.sh/docs/actions/public/createBlockFilter)
*   [`createContractEventFilter`](https://viem.sh/docs/contract/createContractEventFilter)
*   [`createEventFilter`](https://viem.sh/docs/actions/public/createEventFilter)
*   [`createPendingTransactionFilter`](https://viem.sh/docs/actions/public/createPendingTransactionFilter)

Usage
-----

### Blocks

    import { publicClient } from './client'
     
    const filter = await publicClient.createBlockFilter() 
    const hashes = await publicClient.getFilterChanges({ filter })
    Output: ["0x10d86dc08ac2f18f00ef0daf7998dcc8673cbcf1f1501eeb2fac1afd2f851128", ...]

### Contract Events

    import { publicClient } from './client'
     
    const filter = await publicClient.createContractEventFilter({ 
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      abi: wagmiAbi,
      eventName: 'Transfer'
    })
    const logs = await publicClient.getFilterChanges({ filter })
    Output: [{ ... }, { ... }, { ... }]

### Raw Events

    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
     
    const filter = await publicClient.createEventFilter({ 
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed, address indexed, uint256)'),
    })
    const logs = await publicClient.getFilterChanges({ filter })
    Output: [{ ... }, { ... }, { ... }]

### Transactions

    import { publicClient } from './client'
     
    const filter = await publicClient.createPendingTransactionFilter() 
    const hashes = await publicClient.getFilterChanges({ filter })
    Output: ["0x89b3aa1c01ca4da5d15eca9fab459d062db5c0c9b76609acb0741901f01f6d19", ...]

Returns
-------

[`Log[]`](https://viem.sh/docs/glossary/types#log)

If the filter was created with `createContractEventFilter` or `createEventFilter`, it returns a list of logs.

**OR**

`"0x${string}"[]`

If the filter was created with `createPendingTransactionFilter`, it returns a list of transaction hashes.

**OR**

`"0x${string}"[]`

If the filter was created with `createBlockFilter`, it returns a list of block hashes.

Parameters
----------

### filter

*   **Type:** [`Filter`](https://viem.sh/docs/glossary/types#filter)

A created filter.

    const filter = await publicClient.createPendingTransactionFilter()
    const logs = await publicClient.getFilterChanges({
      filter, 
    })

JSON-RPC Method
---------------

*   Calls [`eth_getFilterChanges`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getfilterchanges).</content>
</page>

<page>
  <title>uninstallFilter</title>
  <url>https://viem.sh/docs/actions/public/uninstallFilter</url>
  <content>[Skip to content](https://viem.sh/docs/actions/public/uninstallFilter#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Destroys a [`Filter`](https://viem.sh/docs/glossary/types#filter) that was created from one of the following Actions:

*   [`createBlockFilter`](https://viem.sh/docs/actions/public/createBlockFilter)
*   [`createEventFilter`](https://viem.sh/docs/actions/public/createEventFilter)
*   [`createPendingTransactionFilter`](https://viem.sh/docs/actions/public/createPendingTransactionFilter)

Usage
-----

File

example.ts

    import { publicClient } from './client'
     
    const filter = await publicClient.createPendingTransactionFilter()
    const uninstalled = await publicClient.uninstallFilter({ filter }) 
    // true

Returns
-------

`boolean`

A boolean indicating if the Filter was successfully uninstalled.

Parameters
----------

### filter

*   **Type:** [`Filter`](https://viem.sh/docs/glossary/terms#filter)

A created filter.

    const filter = await publicClient.createPendingTransactionFilter()
    const uninstalled = await publicClient.uninstallFilter({
      filter, 
    })

JSON-RPC Method
---------------

[`eth_uninstallFilter`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_uninstallFilter)</content>
</page>

<page>
  <title>getLogs</title>
  <url>https://viem.sh/docs/actions/public/getLogs</url>
  <content>Returns a list of **event** logs matching the provided parameters.

Usage
-----

By default, `getLogs` returns all events. In practice, you must use scoping to filter for specific events.

    import { publicClient } from './client'
     
    const logs = await publicClient.getLogs()  
    Output: [{ ... }, { ... }, { ... }]

Scoping
-------

You can also scope to a set of given attributes.

    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
     
    const logs = await publicClient.getLogs({  
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256)'),
      args: {
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      },
      fromBlock: 16330000n,
      toBlock: 16330050n
    })

By default, `event` accepts the [`AbiEvent`](https://viem.sh/docs/glossary/types#abievent) type:

    import { publicClient } from './client'
     
    const logs = await publicClient.getLogs(publicClient, {
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: { 
        name: 'Transfer', 
        inputs: [
          { type: 'address', indexed: true, name: 'from' },
          { type: 'address', indexed: true, name: 'to' },
          { type: 'uint256', indexed: false, name: 'value' }
        ] 
      },
      args: {
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      },
      fromBlock: 16330000n,
      toBlock: 16330050n
    })

### Address

Logs can be scoped to an **address**:

    import { publicClient } from './client'
     
    const logs = await publicClient.getLogs({
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2'
    })

### Event

Logs can be scoped to an **event**.

The `event` argument takes in an event in ABI format – we have a [`parseAbiItem` utility](https://viem.sh/docs/abi/parseAbiItem) that you can use to convert from a human-readable event signature → ABI.

    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
     
    const logs = await publicClient.getLogs({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'), 
    })

### Arguments

Logs can be scoped to given **_indexed_ arguments**:

    import { parseAbiItem } from 'viem'
     
    const logs = await publicClient.getLogs({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      }
    })

Only indexed arguments in `event` are candidates for `args`.

An argument can also be an array to indicate that other values can exist in the position:

    import { parseAbiItem } from 'viem'
     
    const logs = await publicClient.getLogs({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      args: { 
        // '0xd8da...' OR '0xa5cc...' OR '0xa152...'
        from: [
          '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
          '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac',
          '0xa152f8bb749c55e9943a3a0a3111d18ee2b3f94e',
        ],
      }
    })

### Block Range

Logs can be scoped to a **block range**:

    import { parseAbiItem } from 'viem'
     
    const logs = await publicClient.getLogs({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      fromBlock: 16330000n, 
      toBlock: 16330050n
    })

### Multiple Events

Logs can be scoped to **multiple events**:

    import { parseAbi } from 'viem'
     
    const logs = await publicClient.getLogs({
      events: parseAbi([ 
        'event Approval(address indexed owner, address indexed sender, uint256 value)',
        'event Transfer(address indexed from, address indexed to, uint256 value)',
      ]),
    })

Note: Logs scoped to multiple events cannot be also scoped with [indexed arguments](https://viem.sh/docs/actions/public/getLogs#arguments) (`args`).

### Strict Mode

By default, `getLogs` will include logs that [do not conform](https://viem.sh/docs/glossary/terms#non-conforming-log) to the indexed & non-indexed arguments on the `event`. viem will not return a value for arguments that do not conform to the ABI, thus, some arguments on `args` may be undefined.

    import { parseAbiItem } from 'viem' 
     
    const logs = await publicClient.getLogs({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)')
    })
     
    logs[0].args
     

You can turn on `strict` mode to only return logs that conform to the indexed & non-indexed arguments on the `event`, meaning that `args` will always be defined. The trade-off is that non-conforming logs will be filtered out.

    import { parseAbiItem } from 'viem' 
     
    const logs = await publicClient.getLogs({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      strict: true
    })
     
    logs[0].args
     

Returns
-------

[`Log[]`](https://viem.sh/docs/glossary/types#log)

A list of event logs.

Parameters
----------

### address

*   **Type:** [`Address | Address[]`](https://viem.sh/docs/glossary/types#address)

A contract address or a list of contract addresses. Only logs originating from the contract(s) will be included in the result.

    const logs = await publicClient.getLogs({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
    })

### event

*   **Type:** [`AbiEvent`](https://viem.sh/docs/glossary/types#abievent)

The event in ABI format.

A [`parseAbiItem` utility](https://viem.sh/docs/abi/parseAbiItem) is exported from viem that converts from a human-readable event signature → ABI.

    import { parseAbiItem } from 'viem'
     
    const logs = await publicClient.getLogs({
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'), 
    })

### args

*   **Type:** Inferred.

A list of _indexed_ event arguments.

    import { parseAbiItem } from 'viem'
     
    const logs = await publicClient.getLogs({
      event: parseAbiItem('event Transfer(address indexed from, address indexed to, uint256 value)'),
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      },
    })

### fromBlock

*   **Type:** `bigint | 'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`

Block to start including logs from. Mutually exclusive with `blockHash`.

    const filter = await publicClient.createEventFilter({
      fromBlock: 69420n
    })

### toBlock

*   **Type:** `bigint | 'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`

Block to stop including logs from. Mutually exclusive with `blockHash`.

    const filter = await publicClient.createEventFilter({
      toBlock: 70120n
    })

### blockHash

*   **Type:** `'0x${string}'`

Block hash to include logs from. Mutually exclusive with `fromBlock`/`toBlock`.

    const logs = await publicClient.getLogs({
      blockHash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d'
    })

Live Example
------------

Check out the usage of `getLogs` in the live [Event Logs Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/logs_event-logs) below.

JSON-RPC Method
---------------

[`eth_getLogs`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getlogs)</content>
</page>

<page>
  <title>getProof</title>
  <url>https://viem.sh/docs/actions/public/getProof</url>
  <content>Returns the account and storage values of the specified account including the Merkle-proof.

Usage
-----

    import { publicClient } from './client'
     
    const proof = await publicClient.getProof({ 
      address: '0x4200000000000000000000000000000000000016',
      storageKeys: [
        '0x4a932049252365b3eedbc5190e18949f2ec11f39d3bef2d259764799a1b27d99',
      ],
    })

Returns
-------

`Proof`

Proof data.

Parameters
----------

### address

*   **Type:** `bigint`

Account address.

    const proof = await publicClient.getProof({
      address: '0x4200000000000000000000000000000000000016', 
      storageKeys: [
        '0x4a932049252365b3eedbc5190e18949f2ec11f39d3bef2d259764799a1b27d99',
      ],
      blockNumber: 42069n
    })

### storageKeys

*   **Type:** `Hash[]`

Array of storage-keys that should be proofed and included.

    const proof = await publicClient.getProof({
      address: '0x4200000000000000000000000000000000000016',
      storageKeys: [ 
        '0x4a932049252365b3eedbc5190e18949f2ec11f39d3bef2d259764799a1b27d99',
      ],
      blockNumber: 42069n
    })

### blockNumber (optional)

*   **Type:** `bigint`

Proof at a given block number.

    const proof = await publicClient.getProof({
      address: '0x4200000000000000000000000000000000000016',
      storageKeys: [
        '0x4a932049252365b3eedbc5190e18949f2ec11f39d3bef2d259764799a1b27d99',
      ],
      blockNumber: 42069n
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Proof at a given block tag.

    const proof = await publicClient.getProof({
      address: '0x4200000000000000000000000000000000000016',
      storageKeys: [
        '0x4a932049252365b3eedbc5190e18949f2ec11f39d3bef2d259764799a1b27d99',
      ],
      blockTag: 'latest'
    })

JSON-RPC Method
---------------

*   Calls [`eth_getProof`](https://eips.ethereum.org/EIPS/eip-1186).</content>
</page>

<page>
  <title>verifyMessage</title>
  <url>https://viem.sh/docs/actions/public/verifyMessage</url>
  <content>Verify that a message was signed by the provided address.

Usage
-----

    import { account, walletClient, publicClient } from './client'
     
    const signature = await walletClient.signMessage({
      account,
      message: 'hello world',
    })
    
    const valid = await publicClient.verifyMessage({
      address: account.address,
      message: 'hello world',
      signature,
    })
    true

Returns
-------

`boolean`

Whether the signed message is valid for the given address.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The Ethereum address that signed the original message.

    const valid = await publicClient.verifyMessage({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      message: 'hello world',
      signature:
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })

### message

*   **Type:** `string`

The message to be verified.

By default, viem verifies the UTF-8 representation of the message.

    const valid = await publicClient.verifyMessage({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      message: 'hello world', 
      signature:
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })

To verify the data representation of the message, you can use the `raw` attribute.

    const valid = await publicClient.verifyMessage({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      message: { raw: '0x68656c6c6f20776f726c64' }, 
      signature:
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })

### signature

*   **Type:** `Hex | ByteArray | Signature`

The signature that was generated by signing the message with the address's signer.

    const valid = await publicClient.verifyMessage({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      message: 'hello world',
      signature: 
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c', 
    })

### blockNumber (optional)

*   **Type:** `bigint`

Only used when verifying a message that was signed by a Smart Contract Account. The block number to check if the contract was already deployed.

    const valid = await publicClient.verifyMessage({
      blockNumber: 42069n, 
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      message: 'hello world',
      signature:
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Only used when verifying a message that was signed by a Smart Contract Account. The block tag to check if the contract was already deployed.

    const valid = await publicClient.verifyMessage({
      blockTag: 'safe', 
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      message: 'hello world',
      signature:
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })

JSON-RPC Method
---------------

[`eth_call`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_call) to a deployless [universal signature validator contract](https://eips.ethereum.org/EIPS/eip-6492).</content>
</page>

<page>
  <title>getTransaction</title>
  <url>https://viem.sh/docs/actions/public/getTransaction</url>
  <content>Returns information about a [Transaction](https://viem.sh/docs/glossary/terms#transaction) given a hash or block identifier.

Usage
-----

    import { publicClient } from './client'
     
    const transaction = await publicClient.getTransaction({ 
      hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d'
    })
    {  blockHash: '0xaf1dadb8a98f1282e8f7b42cc3da8847bfa2cf4e227b8220403ae642e1173088',  blockNumber: 15132008n,  from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',  ... }

Returns
-------

[`Transaction`](https://viem.sh/docs/glossary/types#transaction)

The transaction information.

Parameters
----------

### hash (optional)

*   **Type:** `'0x${string}'`

Get information about a transaction given a transaction hash.

    const transaction = await publicClient.getTransaction({
      hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d'
    })

### blockHash (optional)

*   **Type:** `'0x${string}'`

Get information about a transaction given a block hash (and index).

    const transaction = await publicClient.getTransaction({
      blockHash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d', 
      index: 0
    })

### blockNumber (optional)

*   **Type:** `'0x${string}'`

Get information about a transaction given a block number (and index).

    const transaction = await publicClient.getTransaction({
      blockNumber: 69420n, 
      index: 0
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`

Get information about a transaction given a block tag (and index).

    const transaction = await publicClient.getTransaction({
      blockTag: 'safe', 
      index: 0
    })

### index (optional)

*   **Type:** `number`

An index to be used with a block identifier (number, hash or tag).

    const transaction = await publicClient.getTransaction({
      blockTag: 'safe',
      index: 0
    })

Example
-------

Check out the usage of `getTransaction` in the live [Fetching Transactions Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/transactions_fetching-transactions) below.

JSON-RPC Method
---------------

[`eth_getTransactionByHash`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getTransactionByHash)</content>
</page>

<page>
  <title>getTransactionConfirmations</title>
  <url>https://viem.sh/docs/actions/public/getTransactionConfirmations</url>
  <content>Returns the number of blocks passed (confirmations) since the transaction was processed on a block.

Usage
-----

    import { publicClient } from './client'
     
    const transactionReceipt = await publicClient.getTransactionReceipt({ hash: '...' })
    const confirmations = await publicClient.getTransactionConfirmations({  
      transactionReceipt
    })
    // 15n

You can also fetch confirmations by Transaction hash:

    import { publicClient } from './client'
     
    const confirmations = await publicClient.getTransactionConfirmations({  
      hash: '0x...'
    })
    15n

Returns
-------

`bigint`

The number of blocks passed since the transaction was processed. If confirmations is `0`, then the Transaction has not been confirmed & processed yet.

Parameters
----------

### transactionReceipt

*   **Type:** [`TransactionReceipt`](https://viem.sh/docs/glossary/types#transactionreceipt)

The transaction receipt.

    const balance = await publicClient.getTransactionConfirmations({
      transactionReceipt: { ... }, 
    })

### hash

*   **Type:** [`Hash`](https://viem.sh/docs/glossary/types#hash)

The hash of the transaction.

    const balance = await publicClient.getTransactionConfirmations({
      hash: '0x...'
    })

Example
-------

Check out the usage of `getTransactionConfirmations` in the live [Fetching Transactions Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/transactions_fetching-transactions) below.

JSON-RPC Method
---------------

[`eth_getTransactionConfirmations`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getTransactionConfirmations)</content>
</page>

<page>
  <title>sendRawTransaction</title>
  <url>https://viem.sh/docs/actions/wallet/sendRawTransaction</url>
  <content>Sends a **signed** transaction to the network. Can be used with both [Public Clients](https://viem.sh/docs/clients/public) and [Wallet Clients](https://viem.sh/docs/clients/wallet)

Usage
-----

    import { account, walletClient } from './config'
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
     
    const serializedTransaction = await walletClient.signTransaction(request)
     
    const hash = await walletClient.sendRawTransaction({ serializedTransaction }) 

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### serializedTransaction

*   **Type:** `Hex`

The signed serialized transaction.

    const signature = await walletClient.sendRawTransaction({
      serializedTransaction: '0x02f850018203118080825208808080c080a04012522854168b27e5dc3d5839bab5e6b39e1a0ffd343901ce1622e3d64b48f1a04e00902ae0502c4728cbf12156290df99c3ed7de85b1dbfe20b5c36931733a33'
    })</content>
</page>

<page>
  <title>prepareTransactionRequest</title>
  <url>https://viem.sh/docs/actions/wallet/prepareTransactionRequest</url>
  <content>Prepares a transaction request for signing by populating a nonce, gas limit, fee values, and a transaction type.

Usage
-----

    import { account, walletClient } from './config'
     
    const request = await walletClient.prepareTransactionRequest({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
    {   account: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',   to: '0x70997970C51812dc3A010C7d01b50e0d17dc79C8',   maxFeePerGas: 150000000000n,   maxPriorityFeePerGas: 1000000000n,   nonce: 69,   type: 'eip1559',   value: 1000000000000000000n }  
    const serializedTransaction = await walletClient.signTransaction(request)
    const hash = await walletClient.sendRawTransaction({ serializedTransaction })

### Account Hoisting

If you do not wish to pass an `account` to every `prepareTransactionRequest`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient } from './config'
     
    const request = await walletClient.prepareTransactionRequest({ 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
    {   account: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',   to: '0x70997970C51812dc3A010C7d01b50e0d17dc79C8',   maxFeePerGas: 150000000000n,   maxPriorityFeePerGas: 1000000000n,   nonce: 69,   type: 'eip1559',   value: 1000000000000000000n }  
    const serializedTransaction = await walletClient.signTransaction(request)
    const hash = await walletClient.sendRawTransaction({ serializedTransaction })

Returns
-------

[`TransactionRequest`](https://viem.sh/docs/glossary/types#transactionrequest)

The transaction request.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const request = await walletClient.prepareTransactionRequest({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### to

*   **Type:** `0x${string}`

The transaction recipient or contract address.

    const request = await walletClient.prepareTransactionRequest({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: 1000000000000000000n,
      nonce: 69
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const request = await walletClient.prepareTransactionRequest({
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### authorizationList (optional)

*   **Type:** `AuthorizationList`

Signed EIP-7702 Authorization list.

    const authorization = await walletClient.signAuthorization({ 
      account,
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
    }) 
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      authorizationList: [authorization], 
      data: '0xdeadbeef',
      to: account.address,
    })

### blobs (optional)

*   **Type:** `Hex[]`

Blobs for [Blob Transactions](https://viem.sh/docs/guides/blob-transactions).

    import * as cKzg from 'c-kzg'
    import { toBlobs, setupKzg, stringToHex } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      blobs: toBlobs({ data: stringToHex('blobby blob!') }), 
      kzg,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

The chain is also used to infer its request type (e.g. the Celo chain has a `gatewayFee` that you can pass through to `prepareTransactionRequest`).

    import { optimism } from 'viem/chains'
     
    const request = await walletClient.prepareTransactionRequest({
      chain: optimism, 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const request = await walletClient.prepareTransactionRequest({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    import { parseEther, parseGwei } from 'viem'
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### kzg (optional)

*   **Type:** `KZG`

KZG implementation for [Blob Transactions](https://viem.sh/docs/guides/blob-transactions).

See [`setupKzg`](https://viem.sh/docs/utilities/setupKzg) for more information.

    import * as cKzg from 'c-kzg'
    import { toBlobs, setupKzg, stringToHex } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      blobs: toBlobs({ data: stringToHex('blobby blob!') }), 
      kzg, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    import { parseEther, parseGwei } from 'viem'
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    import { parseEther, parseGwei } from 'viem'
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const request = await walletClient.prepareTransactionRequest({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### nonceManager (optional)

*   **Type:** `NonceManager | undefined`

Nonce Manager to consume and increment the Account nonce for the transaction request.

    const request = await walletClient.prepareTransactionRequest({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonceManager: account.nonceManager 
    })

### parameters (optional)

*   **Type:** `("fees" | "gas" | "nonce" | "type")[]`
*   **Default:** `["fees", "gas", "nonce", "type"]`

Parameters to prepare.

For instance, if `["gas", "nonce"]` is provided, then only the `gas` and `nonce` parameters will be prepared.

    const request = await walletClient.prepareTransactionRequest({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    import { parseEther } from 'viem'
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
      nonce: 69
    })</content>
</page>

<page>
  <title>verifyTypedData</title>
  <url>https://viem.sh/docs/actions/public/verifyTypedData</url>
  <content>Verify that typed data was signed by the provided address.

Usage
-----

    import { account, walletClient, publicClient } from './client'
    import { domain, types } from './data'
     
    const message = {
      from: {
        name: 'Cow',
        wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
      },
      to: {
        name: 'Bob',
        wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
      },
      contents: 'Hello, Bob!',
    }
     
    const signature = await walletClient.signTypedData({
      account,
      domain,
      types,
      primaryType: 'Mail',
      message,
    })
    
    const valid = await publicClient.verifyTypedData({
      address: account.address,
      domain,
      types,
      primaryType: 'Mail',
      message,
      signature,
    })
    // true

Returns
-------

`boolean`

Whether the signed message is valid for the given address.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The Ethereum address that signed the original message.

    const valid = await publicClient.verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### domain

**Type:** `TypedDataDomain`

The typed data domain.

    const valid = await publicClient.verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### types

The type definitions for the typed data.

    const valid = await publicClient.verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: { 
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### primaryType

**Type:** Inferred `string`.

The primary type to extract from `types` and use in `value`.

    const valid = await publicClient.verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [ 
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### message

**Type:** Inferred from `types` & `primaryType`.

    const valid = await publicClient.verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: { 
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### signature

*   **Type:** `Hex | ByteArray | Signature`

The signature of the typed data.

    const valid = await publicClient.verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...', 
    })

### blockNumber (optional)

*   **Type:** `bigint`

Only used when verifying a typed data that was signed by a Smart Contract Account. The block number to check if the contract was already deployed.

    const valid = await publicClient.verifyTypedData({
      blockNumber: 42069n, 
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Only used when verifying a typed data that was signed by a Smart Contract Account. The block tag to check if the contract was already deployed.

    const valid = await publicClient.verifyTypedData({
      blockNumber: 42069n, 
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

JSON-RPC Method
---------------

[`eth_call`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_call) to a deployless [universal signature validator contract](https://eips.ethereum.org/EIPS/eip-6492).</content>
</page>

<page>
  <title>getTransactionReceipt</title>
  <url>https://viem.sh/docs/actions/public/getTransactionReceipt</url>
  <content>Returns the [Transaction Receipt](https://viem.sh/docs/glossary/terms#transaction-receipt) given a [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Usage
-----

    import { publicClient } from './client'
     
    const transaction = await publicClient.getTransactionReceipt({ 
      hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d'
    })
    {  blockHash: '0xaf1dadb8a98f1282e8f7b42cc3da8847bfa2cf4e227b8220403ae642e1173088',  blockNumber: 15132008n,  from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',  ...  status: 'success', }

Returns
-------

[`TransactionReceipt`](https://viem.sh/docs/glossary/types#transactionreceipt)

The transaction receipt.

Parameters
----------

### hash

*   **Type:** `'0x${string}'`

A transaction hash.

    const transaction = await publicClient.getTransactionReceipt({
      hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d'
    })

Example
-------

Check out the usage of `getTransactionReceipt` in the live [Fetching Transactions Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/transactions_fetching-transactions) below.

JSON-RPC Method
---------------

[`eth_getTransactionReceipt`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getTransactionReceipt)</content>
</page>

<page>
  <title>waitForTransactionReceipt</title>
  <url>https://viem.sh/docs/actions/public/waitForTransactionReceipt</url>
  <content>Waits for the [Transaction](https://viem.sh/docs/glossary/terms#transaction) to be included on a [Block](https://viem.sh/docs/glossary/terms#block) (one confirmation), and then returns the [Transaction Receipt](https://viem.sh/docs/glossary/terms#transaction-receipt).

The `waitForTransactionReceipt` action additionally supports Replacement detection (e.g. sped up Transactions).

Usage
-----

    import { publicClient } from './client'
     
    const transaction = await publicClient.waitForTransactionReceipt( 
      { hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d' }
    )
    {  blockHash: '0xaf1dadb8a98f1282e8f7b42cc3da8847bfa2cf4e227b8220403ae642e1173088',  blockNumber: 15132008n,  from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',  ...  status: 'success', }

Returns
-------

[`TransactionReceipt`](https://viem.sh/docs/glossary/types#transactionreceipt)

The transaction receipt.

Parameters
----------

### confirmations (optional)

*   **Type:** `number`
*   **Default:** `1`

The number of confirmations (blocks that have passed) to wait before resolving.

    const transaction = await publicClient.waitForTransactionReceipt(
      { 
        confirmations: 5, 
        hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d' 
      }
    )

### onReplaced (optional)

*   **Type:** `({ reason: 'replaced' | 'repriced' | 'cancelled', replacedTransaction: Transaction, transaction: Transaction, transactionReceipt: TransactionReceipt }) => void`

Optional callback to emit if the transaction has been replaced.

    const transaction = await publicClient.waitForTransactionReceipt(
      { 
        hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d',
        onReplaced: replacement => console.log(replacement) 
      }
    )

### pollingInterval (optional)

*   **Type:** `number`

Polling frequency (in ms). Defaults to the Client's `pollingInterval` config.

    const transaction = await publicClient.waitForTransactionReceipt(
      { 
        hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d',
        pollingInterval: 12_000, 
      }
    )

### retryCount (optional)

*   **Type:** `number`
*   **Default:** `6`

Number of times to retry if the transaction or block is not found.

    const transaction = await publicClient.waitForTransactionReceipt(
      { 
        hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d',
        retryCount: 3, 
      }
    )

### retryDelay (optional)

*   **Type:** `number | (({ count: number; error: Error }) => number)`
*   **Default:** `({ count }) => ~~(1 << count) * 200` (exponential backoff)

Time to wait (in ms) between retries.

    const transaction = await publicClient.waitForTransactionReceipt(
      { 
        hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d',
        retryDelay: 10_000, 
      }
    )

### timeout (optional)

*   **Type:** `number`
*   **Default:** `180_000`

Optional timeout (in milliseconds) to wait before stopping polling.

    const transaction = await publicClient.waitForTransactionReceipt(
      { 
        hash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d',
        timeout: 60_000, 
      }
    )

### Notes

*   Transactions can be replaced when a user modifies their transaction in their wallet (to speed up or cancel). Transactions are replaced when they are sent from the same nonce.
*   There are 3 types of Transaction Replacement reasons:
    *   `repriced`: The gas price has been modified (ie. different `maxFeePerGas`)
    *   `cancelled`: The Transaction has been cancelled (ie. `value === 0n`)
    *   `replaced`: The Transaction has been replaced (ie. different `value` or `data`)

Live Example
------------

Check out the usage of `waitForTransactionReceipt` in the live [Sending Transactions Example](https://stackblitz.com/github/wevm/viem/tree/main/examples/transactions_sending-transactions) below.

JSON-RPC Methods
----------------

*   Polls [`eth_getTransactionReceipt`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getTransactionReceipt) on each block until it has been processed.
*   If a Transaction has been replaced:
    *   Calls [`eth_getBlockByNumber`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getblockbynumber) and extracts the transactions
    *   Checks if one of the Transactions is a replacement
    *   If so, calls [`eth_getTransactionReceipt`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getTransactionReceipt).</content>
</page>

<page>
  <title>watchPendingTransactions</title>
  <url>https://viem.sh/docs/actions/public/watchPendingTransactions</url>
  <content>Watches and returns pending transaction hashes.

This Action will batch up all the pending transactions found within the [`pollingInterval`](https://viem.sh/docs/actions/public/watchPendingTransactions#pollinginterval-optional), and invoke them via [`onTransactions`](https://viem.sh/docs/actions/public/watchPendingTransactions#ontransactions).

Usage
-----

    import { publicClient } from './client'
     
    const unwatch = publicClient.watchPendingTransactions( 
      { onTransactions: hashes => console.log(hashes) }
    )
    > ['0x...', '0x...', '0x...'] > ['0x...', '0x...'] > ['0x...', '0x...', '0x...', ...]

Returns
-------

`UnwatchFn`

A function that can be invoked to stop watching for new pending transaction hashes.

Parameters
----------

### onTransactions

*   **Type:** `(hashes: '0x${string}'[]) => void`

The new pending transaction hashes.

    const unwatch = publicClient.watchPendingTransactions(
      { onTransactions: hashes => console.log(hashes) } 
    )

### batch (optional)

*   **Type:** `boolean`
*   **Default:** `true`

Whether or not to batch the transaction hashes between polling intervals.

    const unwatch = publicClient.watchPendingTransactions(
      { 
        batch: false, 
        onTransactions: hashes => console.log(hashes),
      }
    )

### onError (optional)

*   **Type:** `(error: Error) => void`

Error thrown from listening for new pending transactions.

    const unwatch = publicClient.watchPendingTransactions(
      { 
        onError: error => console.log(error), 
        onTransactions: hashes => console.log(hashes),
      }
    )

### poll (optional)

*   **Type:** `boolean`
*   **Default:** `false` for WebSocket Clients, `true` for non-WebSocket Clients

Whether or not to use a polling mechanism to check for new pending transactions instead of a WebSocket subscription.

This option is only configurable for Clients with a [WebSocket Transport](https://viem.sh/docs/clients/transports/websocket).

    import { createPublicClient, webSocket } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const publicClient = createPublicClient({
      chain: mainnet,
      transport: webSocket()
    })
     
    const unwatch = publicClient.watchPendingTransactions(
      { 
        onTransactions: transactions => console.log(transactions),
        poll: true, 
      }
    )

### pollingInterval (optional)

*   **Type:** `number`

Polling frequency (in ms). Defaults to the Client's `pollingInterval` config.

    const unwatch = publicClient.watchPendingTransactions(
      { 
        pollingInterval: 1_000, 
        onTransactions: hashes => console.log(hashes),
      }
    )

JSON-RPC Methods
----------------

*   When `poll: true`
    *   Calls [`eth_newPendingTransactionFilter`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_newpendingtransactionfilter) to initialize the filter.
    *   Calls [`eth_getFilterChanges`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getFilterChanges) on a polling interval.
*   When `poll: false` & WebSocket Transport, uses a WebSocket subscription via [`eth_subscribe`](https://docs.alchemy.com/reference/eth-subscribe-polygon) and the `"newPendingTransactions"` event.</content>
</page>

<page>
  <title>Fees</title>
  <url>https://viem.sh/docs/chains/fees</url>
  <content>You can modify how fees are derived by using the `fees` property on the Chain.

Usage
-----

    import { defineChain } from 'viem'
     
    export const example = defineChain({
      /* ... */
      fees: { 
        baseFeeMultiplier: 1.2, 
        defaultPriorityFee: parseGwei('0.01'), 
      } 
    })

API
---

### `fees.baseFeeMultiplier`

*   **Type**: `number`
*   **Default**: `1.2`

The fee multiplier to use to account for fee fluctuations. Used in the [`estimateFeesPerGas` Action](https://viem.sh/docs/actions/public/estimateFeesPerGas) against the latest block's base fee per gas to derive a final `maxFeePerGas` (EIP-1193), or gas price to derive a final `gasPrice` (Legacy).

**Parameters**

*   `block`: The latest block.
*   `client`: The Client instance.
*   `request`: The transaction request (if exists).

    import { defineChain } from 'viem'
     
    const example = defineChain({ 
      /* ... */
      fees: { 
        baseFeeMultiplier: 1.2,
        // or
        async baseFeeMultiplier({ block, request }) {
          // some async work
          return // ...
        },
      },
    })

### `fees.defaultPriorityFee`

*   **Type**: `number | ((args: FeesFnParameters) => Promise<bigint> | bigint)`

The default `maxPriorityFeePerGas` to use when a priority fee is not defined upon sending a transaction.

Also overrides the return value in the [`estimateMaxPriorityFeePerGas` Action](https://viem.sh/docs/actions/public/estimateMaxPriorityFeePerGas) and `maxPriorityFeePerGas` value in [`estimateFeesPerGas`](https://viem.sh/docs/actions/public/estimateFeesPerGas).

**Parameters**

*   `block`: The latest block.
*   `client`: The Client instance.
*   `request`: The transaction request (if exists).

    import { defineChain } from 'viem'
     
    const example = defineChain({
      /* ... */
      fees: { 
        defaultPriorityFee: parseGwei('0.01'),
        // or
        async defaultPriorityFee({ block, request }) {
          // some async work
          return // ...
        },
      },
    })

### `fees.estimateFeesPerGas`

*   **Type**: `(args: FeesFnParameters) => Promise<EstimateFeesPerGasResponse>`

Allows customization of fee per gas values (ie. `maxFeePerGas`, `maxPriorityFeePerGas`, `gasPrice`).

Also overrides the return value in [`estimateFeesPerGas`](https://viem.sh/docs/actions/public/estimateFeesPerGas).

**Parameters**

*   `block`: The latest block.
*   `client`: The Client instance.
*   `multiply`: A function to apply the `baseFeeMultiplier` to the provided value.
*   `request`: The transaction request (if exists).
*   `type`: The transaction type (ie. `legacy` or `eip1559`).

    import { defineChain } from 'viem'
     
    const example = defineChain({
      /* ... */
      fees: { 
        async estimateFeesPerGas({ client, multiply, type }) {
          const gasPrice = // ...
          const baseFeePerGas = // ...
          const maxPriorityFeePerGas = // ...
     
          if (type === 'legacy') return { gasPrice: multiply(gasPrice) }
          return {
            maxFeePerGas: multiply(baseFeePerGas) + maxPriorityFeePerGas,
            maxPriorityFeePerGas
          },
        },
      },
    })</content>
</page>

<page>
  <title>Serializers</title>
  <url>https://viem.sh/docs/chains/serializers</url>
  <content>Usage
-----

    import { defineChain, serializeTransaction } from 'viem'
     
    const example = defineChain({
      /* ... */
      serializers: {
        transaction(transaction, signature) {
          return serializeTransaction(transaction, signature)
        },
      },
    })

API
---

### `serializers.transaction`

*   **Type**: `(transaction: Transaction, signature?: Signature) => "0x${string}"`

You can modify how Transactions are serialized by using the `serializers.transaction` property on the Chain.

**Parameters**

*   `transaction`: The transaction to serialize.
*   `signature`: The transaction signature (if exists).

    import { defineChain, serializeTransaction } from 'viem'
     
    const example = defineChain({
      /* ... */
      serializers: { 
        transaction(transaction, signature) {
          return serializeTransaction(transaction, signature)
        },
      },
    })</content>
</page>

<page>
  <title>Getting Started with OP Stack</title>
  <url>https://viem.sh/op-stack</url>
  <content>Viem provides first-class support for chains implemented on the [OP Stack](https://docs.optimism.io/stack/getting-started).

The OP Stack is a set of modular open-source software that enable developers to build fast, secure, and scalable Layer 2 Ethereum protocols & applications. [Read more.](https://docs.optimism.io/stack/getting-started)

Quick Start
-----------

### 1\. Set up your Client & Transport

Firstly, set up your [Client](https://viem.sh/docs/clients/intro) with a desired [Transport](https://viem.sh/docs/clients/intro) & [OP Stack Chain](https://viem.sh/op-stack/chains).

    import { createPublicClient, http } from 'viem'
    import { base } from 'viem/chains'
     
    const client = createPublicClient({ 
      chain: base, 
      transport: http(), 
    }) 

### 2\. Extend Client with the OP Stack

Now that you have a Client set up, you can extend it with OP Stack Actions! [Read more.](https://viem.sh/op-stack/client)

    import { createPublicClient, http } from 'viem'
    import { base } from 'viem/chains'
    import { publicActionsL2 } from 'viem/op-stack'
     
    const client = createPublicClient({
      chain: base,
      transport: http(),
    }).extend(publicActionsL2()) 

### 3\. Consume OP Stack Actions

Now that you have an OP Stack Client set up, you can now interact with the OP Stack and consume [Actions](https://viem.sh/op-stack/actions/estimateL1Gas)!

    import { createPublicClient, http, parseEther } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createPublicClient({
      chain: mainnet,
      transport: http(),
    }).extend(publicActionsL2()) 
     
    const l1Gas = await client.estimateL1Gas({ 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>Celo</title>
  <url>https://viem.sh/docs/chains/celo</url>
  <content>Viem provides first-class support for chains implemented on [Celo](https://celo.org/).

Chains
------

The following Viem chains are implemented on Celo:

    import {
      celo, 
      celoAlfajores, 
    } from 'viem/chains'

### Configuration

Viem exports Celo's chain [formatters](https://viem.sh/docs/chains/formatters) & [serializers](https://viem.sh/docs/chains/serializers) via `chainConfig`. This is useful if you need to define another chain which is implemented on Celo.

    import { defineChain } from 'viem'
    import { chainConfig } from 'viem/celo'
     
    export const celoExample = defineChain({
      ...chainConfig,
      name: 'Celo Example',
      // ...
    })

Utilities
---------

### `parseTransaction`

Parses a serialized RLP-encoded transaction. Supports signed & unsigned CIP-64, EIP-1559, EIP-2930 and Legacy Transactions.

Celo-flavored version of [Viem's `parseTransaction`](https://viem.sh/docs/utilities/parseTransaction).

#### Parameters

*   `serializedTransaction` (`Hex`): The serialized transaction.

    import { parseTransaction } from 'viem/celo'
     
    const transaction = parseTransaction('0x7cf84682a4ec80847735940084773594008094765de816845861e75a25fca122bb6898b8b1282a808094f39fd6e51aad88f6f4ce6ab8827279cfffb92266880de0b6b3a764000080c0')

### `serializeTransaction`

Serializes a transaction object. Supports CIP-64, EIP-1559, EIP-2930, and Legacy transactions.

Celo-flavored version of [Viem's `serializeTransaction`](https://viem.sh/docs/utilities/serializeTransaction).

#### Parameters

*   `transaction` (`TransactionSerializable`): The transaction object to serialize.
*   `signature` (`Signature`): Optional signature to include.

    import { serializeTransaction } from 'viem/celo'
     
    const serialized = serializeTransaction({
      chainId: 42220,
      gas: 21001n,
      feeCurrency: "0x2F25deB3848C207fc8E0c34035B3Ba7fC157602B" // whitelisted adapter for USDC
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69,
      to: '0x1234512345123451234512345123451234512345',
      value: parseEther('0.01'),
    })</content>
</page>

<page>
  <title>Formatters</title>
  <url>https://viem.sh/docs/chains/formatters</url>
  <content>You can modify how Blocks & Transactions are formatted by using the `formatters` property on the Chain.

This is useful for chains that have a different Block or Transaction structure than Mainnet (e.g. Celo & OP Stack chains).

Usage
-----

    import { 
      defineBlock,
      defineChain,
      defineTransaction, 
      defineTransactionReceipt, 
      defineTransactionRequest 
    } from 'viem' 
     
    export const example = defineChain({
      /* ... */
      formatters: { 
        block: defineBlock(/* ... */),
        transaction: defineTransaction(/* ... */),
        transactionReceipt: defineTransactionReceipt(/* ... */),
        transactionRequest: defineTransactionRequest(/* ... */),
      } 
    })

API
---

### `formatters.block`

You can modify how Blocks are formatted by using the `formatters.block` property on the Chain.

You can either pass in the Block overrides, or the whole Block itself to the `format` function of `defineBlock`. You can also exclude certain properties with `exclude`.

    import { defineBlock, defineChain, hexToBigInt } from 'viem'
     
    type RpcBlockOverrides = { 
      secondaryFee: `0x${string}`
    }
    type BlockOverrides = {
      secondaryFee: bigint
    }
     
    const example = defineChain({
      /* ... */
      formatters: { 
        block: defineBlock({
          exclude: ['difficulty'],
          format(args: RpcBlockOverrides): BlockOverrides {
            return {
              secondaryFee: hexToBigInt(args.secondaryFee)
            }
          },
        }),
      },
    })
     
    const block = await client.getBlock() 
    //    ^? { ..., difficulty: never, secondaryFee: bigint, ... }

### `formatters.transaction`

You can modify how Transactions are formatted by using the `formatters.transaction` property on the Chain.

You can either pass in the Transaction overrides, or the whole Transaction itself to the `format` function of `defineTransaction`. You can also exclude certain properties with `exclude`.

    import { defineTransaction, defineChain, hexToBigInt } from 'viem'
     
    type RpcTransactionOverrides = { 
      mint: `0x${string}`
    }
    type TransactionOverrides = {
      mint: bigint
    }
     
    const example = defineChain({
      /* ... */
      formatters: { 
        transaction: defineTransaction({
          exclude: ['gasPrice'],
          format(args: RpcTransactionOverrides): TransactionOverrides {
            return {
              mint: hexToBigInt(args.mint)
            }
          },
        }),
      },
    })
     
    const transaction = await client.getTransaction({ hash: '0x...' }) 
    //    ^? { ..., gasPrice: never, mint: bigint, ... }

### `formatters.transactionReceipt`

You can modify how Transaction Receipts are formatted by using the `formatters.transactionReceipt` property on the Chain.

You can either pass in the Transaction Receipt overrides, or the whole Transaction Receipt itself to the `format` function of `defineTransactionReceipt`. You can also exclude certain properties with `exclude`.

    import { defineTransactionReceipt, defineChain, hexToBigInt } from 'viem'
     
    type RpcTransactionReceiptOverrides = { 
      l1Fee: `0x${string}`
    }
    type TransactionReceiptOverrides = {
      l1Fee: bigint
    }
     
    const example = defineChain({
      /* ... */
      formatters: { 
        transactionReceipt: defineTransactionReceipt({
          exclude: ['effectiveGasPrice'],
          format(args: RpcTransactionReceiptOverrides): 
            TransactionReceiptOverrides {
            return {
              l1Fee: hexToBigInt(args.l1Fee)
            }
          },
        }),
      },
    })
     
    const receipt = await client.getTransactionReceipt({ hash: '0x...' }) 
    //    ^? { ..., effectiveGasPrice: never, l1Fee: bigint, ... }

### `formatters.transactionRequest`

You can modify how Transaction Requests are formatted by using the `formatters.transactionRequest` property on the Chain.

You can either pass in the Transaction Request overrides, or the whole Transaction Request itself to the `format` function of `defineTransactionRequest`. You can also exclude certain properties with `exclude`.

    import { defineTransactionRequest, defineChain, hexToBigInt } from 'viem'
     
    type RpcTransactionRequestOverrides = { 
      secondaryFee: `0x${string}`
    }
    type TransactionRequestOverrides = {
      secondaryFee: bigint
    }
     
    const example = defineChain({
      /* ... */
      formatters: { 
        transactionRequest: defineTransactionRequest({
          exclude: ['effectiveGasPrice'],
          format(args: TransactionRequestOverrides): 
            RpcTransactionRequestOverrides {
            return {
              secondaryFee: numberToHex(args.secondaryFee)
            }
          },
        }),
      },
    })
     
    const receipt = await client.getTransactionReceipt({ hash: '0x...' }) 
    //    ^? { ..., effectiveGasPrice: never, l1Fee: bigint, ... }</content>
</page>

<page>
  <title>Getting Started with ZKsync</title>
  <url>https://viem.sh/zksync</url>
  <content>Viem provides first-class support for the [ZKsync](https://zksync.io/) chain.

ZKsync is a Layer-2 protocol that scales Ethereum with cutting-edge ZK tech.

Quick Start
-----------

### 1\. Set up your Client & Transport

Firstly, set up your [Client](https://viem.sh/docs/clients/intro) with a desired [Transport](https://viem.sh/docs/clients/intro) & [ZKsync Chain](https://viem.sh/zksync/chains) and extend it with ZKsync EIP712 actions.

    import { createWalletClient, custom } from 'viem'
    import { zksync } from 'viem/chains'
    import { eip712WalletActions } from 'viem/zksync'
     
    const walletClient = createWalletClient({ 
      chain: zksync, 
      transport: custom(window.ethereum!), 
    }).extend(eip712WalletActions()) 

### 2\. Use Actions

Now that you have a Client set up, you can [send a transaction](https://viem.sh/zksync/actions/sendTransaction) on ZKsync using a [paymaster](https://docs.zksync.io/build/developer-reference/account-abstraction.html#paymasters)!

    const hash = await walletClient.sendTransaction({
      account: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      paymaster: '0xFD9aE5ebB0F6656f4b77a0E99dCbc5138d54b0BA',
      paymasterInput: '0x123abc...'
    })

...and even write to contracts:

    const hash = await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: parseAbi(['function mint(uint32 tokenId) nonpayable']),
      functionName: 'mint',
      args: [69420],
    })</content>
</page>

<page>
  <title>getCode</title>
  <url>https://viem.sh/docs/contract/getCode</url>
  <content>[Skip to content](https://viem.sh/docs/contract/getCode#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Retrieves the bytecode at an address.

Usage
-----

    import { publicClient } from './client'
     
    const bytecode = await publicClient.getCode({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
    })

Return Value
------------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The contract's bytecode.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const bytecode = await publicClient.getCode({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
    })

### blockNumber (optional)

*   **Type:** `number`

The block number to perform the bytecode read against.

    const bytecode = await publicClient.getCode({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      blockNumber: 15121123n, 
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

The block tag to perform the bytecode read against.

    const bytecode = await publicClient.getCode({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      blockTag: 'safe', 
    })

JSON-RPC Method
---------------

[`eth_getCode`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getcode)</content>
</page>

<page>
  <title>getContractEvents</title>
  <url>https://viem.sh/docs/contract/getContractEvents</url>
  <content>Returns a list of contract **event logs** matching the provided parameters.

Usage
-----

By default, `getContractEvents` returns all matched events on the ABI. In practice, you must use scoping to filter for specific events.

    import { publicClient } from './client'
    import { erc20Abi } from './abi'
     
    // Fetch event logs for every event on every ERC-20 contract. 
    const logs = await publicClient.getContractEvents({ 
      abi: erc20Abi 
    })
    // [{ ... }, { ... }, { ... }]

Scoping
-------

You can also scope to a set of given attributes.

    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
    import { erc20Abi } from './abi'
     
    const usdcContractAddress = '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48'
     
    const logs = await publicClient.getContractEvents({ 
      address: usdcContractAddress,
      abi: erc20Abi,
      eventName: 'Transfer',
      args: {
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      },
      fromBlock: 16330000n,
      toBlock: 16330050n
    })

### Address

Logs can be scoped to an **address**:

    import { publicClient } from './client'
    import { erc20Abi } from './abi'
     
    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      address: '0xfba3912ca04dd458c843e2ee08967fc04f3579c2', 
    })

### Event

Logs can be scoped to an **event**.

    import { parseAbiItem } from 'viem'
    import { publicClient } from './client'
    import { erc20Abi } from './abi'
     
    const logs = await publicClient.getContractEvents({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      abi: erc20Abi,
      eventName: 'Transfer', 
    })

### Arguments

Logs can be scoped to given **_indexed_ arguments**:

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      eventName: 'Transfer',
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      }
    })

Only indexed arguments in `event` are candidates for `args`.

An argument can also be an array to indicate that other values can exist in the position:

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      eventName: 'Transfer',
      args: { 
        // '0xd8da...' OR '0xa5cc...' OR '0xa152...'
        from: [
          '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
          '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac',
          '0xa152f8bb749c55e9943a3a0a3111d18ee2b3f94e',
        ],
      }
    })

### Block Range

Logs can be scoped to a **block range**:

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      eventName: 'Transfer',
      fromBlock: 16330000n, 
      toBlock: 16330050n
    })

### Strict Mode

By default, `getContractEvents` will include logs that [do not conform](https://viem.sh/docs/glossary/terms#non-conforming-log) to the indexed & non-indexed arguments on the `event`. viem will not return a value for arguments that do not conform to the ABI, thus, some arguments on `args` may be undefined.

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      eventName: 'Transfer',
    })
     
    logs[0].args 
    //      ^? { address?: Address, to?: Address, value?: bigint } 

You can turn on `strict` mode to only return logs that conform to the indexed & non-indexed arguments on the `event`, meaning that `args` will always be defined. The trade-off is that non-conforming logs will be filtered out.

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      eventName: 'Transfer',
      strict: true
    })
     
    logs[0].args 
    //      ^? { address: Address, to: Address, value: bigint } 

Returns
-------

[`Log[]`](https://viem.sh/docs/glossary/types#log)

A list of event logs.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi, 
    })

### address

*   **Type:** [`Address | Address[]`](https://viem.sh/docs/glossary/types#address)

A contract address or a list of contract addresses. Only logs originating from the contract(s) will be included in the result.

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
    })

### eventName

*   **Type:** `string`

An event name on the `abi`.

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      eventName: 'Transfer'
    })

### args

*   **Type:** Inferred.

A list of _indexed_ event arguments.

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      eventName: 'Transfer',
      args: { 
        from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
        to: '0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac'
      },
    })

### fromBlock

*   **Type:** `bigint | 'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`

Block to start including logs from. Mutually exclusive with `blockHash`.

    const filter = await publicClient.getContractEvents({
      abi: erc20Abi,
      fromBlock: 69420n
    })

### toBlock

*   **Type:** `bigint | 'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`

Block to stop including logs from. Mutually exclusive with `blockHash`.

    const filter = await publicClient.getContractEvents({
      abi: erc20Abi,
      toBlock: 70120n
    })

### blockHash

*   **Type:** `'0x${string}'`

Block hash to include logs from. Mutually exclusive with `fromBlock`/`toBlock`.

    const logs = await publicClient.getContractEvents({
      abi: erc20Abi,
      blockHash: '0x4ca7ee652d57678f26e887c149ab0735f41de37bcad58c9f6d3ed5824f15b74d'
    })

JSON-RPC Method
---------------

[`eth_getLogs`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getLogs)</content>
</page>

<page>
  <title>decodeErrorResult</title>
  <url>https://viem.sh/docs/contract/decodeErrorResult</url>
  <content>    import { decodeErrorResult } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const value = decodeErrorResult({
      abi: wagmiAbi,
      data: '0xb758934b000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000b68656c6c6f20776f726c64000000000000000000000000000000000000000000'
    })
    // { errorName: 'InvalidTokenError', args: ['sold out'] }</content>
</page>

<page>
  <title>decodeDeployData</title>
  <url>https://viem.sh/docs/contract/decodeDeployData</url>
  <content>    import { decodeDeployData } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const { args } = decodeDeployData({
      abi: wagmiAbi,
      bytecode: '0x6080604052348015600f57600080fd5b50603f80601d6000396000f3fe6080604052600080fdfea2646970667358221220116554d4ba29ee08da9e97dc54ff9a2a65d67a648140d616fc225a25ff08c86364736f6c63430008070033',
      data: '0x6080604052348015600f57600080fd5b50603f80601d6000396000f3fe6080604052600080fdfea2646970667358221220116554d4ba29ee08da9e97dc54ff9a2a65d67a648140d616fc225a25ff08c86364736f6c634300080700330000000000000000000000000000000000000000000000000000000000010f2c'
    })
    // { args: [69420n], bytecode: '0x6080604...' }</content>
</page>

<page>
  <title>Terms</title>
  <url>https://viem.sh/docs/glossary/terms#non-conforming-log</url>
  <content>Block
-----

A block is a bundled unit of information that include an ordered list of transactions and consensus-related information. Blocks are proposed by proof-of-stake validators, at which point they are shared across the entire peer-to-peer network, where they can easily be independently verified by all other nodes. Consensus rules govern what contents of a block are considered valid, and any invalid blocks are disregarded by the network. The ordering of these blocks and the transactions therein create a deterministic chain of events with the end representing the current state of the network.

Chain
-----

A Chain refers to a specific blockchain network or protocol that maintains a decentralized, distributed ledger of transactions and other data. Each Chain has its own rules, consensus mechanism, and native cryptocurrency (if any).

Examples of Chains include: Ethereum Mainnet, Polygon, Optimism, Avalanche, Binance Smart Chain, etc.

EIP-1559 Transaction
--------------------

EIP-1559 is an Ethereum Improvement Proposal that was implemented in August 2021 as part of the London hard fork. It introduced a new transaction format for Ethereum transactions, which is referred to as an EIP-1559 transaction (aka "transaction type 2").

When a user creates an EIP-1559 transaction, they specify the maximum fee they are willing to pay (`maxFeePerGas`) as well as a tip (`maxPriorityFeePerGas`) to incentivize the miner. The actual fee paid by the user is then determined by the network based on the current demand for block space and the priority of the transaction.

Event Log
---------

An Event Log is a record of an event emitted by a smart contract. Events are a type of function in a smart contract that can be triggered by specific actions or conditions, and they can be used to notify dapps of changes on the network.

[See more](https://ethereum.org/en/developers/docs/smart-contracts/anatomy/#events-and-logs)

Filter
------

In Ethereum, a filter is a mechanism used to query the Ethereum blockchain for specific events or information.

There are three types of filters in Ethereum:

1.  Block filters - these filters allow users to monitor the blockchain for new blocks that have been added.
    
2.  Pending Transaction filters - these filters allow users to monitor the blockchain for new pending transactions in the mempool.
    
3.  Event filters - these filters allow users to monitor the blockchain for specific events emitted by smart contracts, such as a token transfer.
    

When a filter is created, it returns a filter ID, which can be used to retrieve the results of the filter at a later time. Users can then periodically poll the filter for new events or changes that match the filter criteria.

Human-Readable ABI
------------------

Human-Readable ABIs compress JSON ABIs into signatures that are nicer to read and less verbose to write. For more info, check out the [ABIType](https://abitype.dev/api/human) docs.

Legacy Transaction
------------------

A Legacy Transaction in Ethereum refers to a transaction that was created using an older version of Ethereum's transaction format, known as "transaction type 0". This transaction format was used prior to the introduction of the EIP-1559 upgrade, which was implemented in August 2021.

Non-conforming Log
------------------

A non-conforming log is a log where its `topics` & `data` do not match the **indexed** & **non-indexed** arguments on the `event`. `topics` correspond to **indexed** arguments, while `data` corresponds to **non-indexed** arguments.

For example, here is an event definition that has 3 indexed arguments & 1 non-indexed arguments:

    event Transfer(
      bool indexed foo, 
      uint256 baz, 
      string indexed bar, 
      boolean indexed barry
    )

A conforming log for the above signature would be:

    const log = {
      ...
      data: '0x
        00...23c346 // ✅ non-indexed argument (baz)
      ',
      topics: [
        '0xdd...23b3ef', // event signature
        '0x00...000001', // ✅ indexed argument (foo)
        '0xae...e1cc58', // ✅ indexed argument (bar)
        '0x00...000000', // ✅ indexed argument (barry)
      ],
      ...
    }

A non-conforming log for the above signature would be:

    const log = {
      ...
      data: '0x
        00...23c346 // ✅ non-indexed argument (baz)
        00...ae0000 // ❌ indexed argument (bar)
        00...000001 // ❌ indexed argument (barry)
      ',
      topics: [
        '0xdd...23b3ef', // event signature
        '0x00...b92266', // ✅ indexed argument (foo)
      ],
      ...
    }

A non-conforming log can arise when another contract could be using the same event signature, but with a different number of indexed & non-indexed arguments. For example, the definition for the above log would be:

    event Transfer(
      bool indexed foo, 
      uint256 baz, 
      string bar, 
      boolean barry
    )

Transaction
-----------

A transaction is a message sent by an Account requesting to perform an action on the Ethereum blockchain. Transactions can be used to transfer Ether between accounts, execute smart contract code, deploy smart contracts, etc.

Transaction Receipt
-------------------

A Transaction Receipt is a record of the result of a specific transaction on the Ethereum blockchain. When a transaction is submitted to the Ethereum network, it is processed by miners and included in a block. Once the block is added to the blockchain, a transaction receipt is generated and stored on the blockchain.

A transaction receipt contains information about the transaction, including:

*   The transaction hash: a unique identifier for the transaction.
*   The block number and block hash: the block in which the transaction was included.
*   The gas used: the amount of gas consumed by the transaction.
*   The status of the transaction: "success" if the transaction was executed, otherwise "reverted" if the transaction reverted.
*   The logs generated by the transaction: any log events generated by the smart contract during the transaction execution.

Transport
---------

A Transport is the intermediary layer that is responsible for executing outgoing requests (ie. RPC requests) in viem.</content>
</page>

<page>
  <title>getAddresses</title>
  <url>https://viem.sh/docs/actions/wallet/getAddresses</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/wallet/introduction)

Account

[getAddresses](https://viem.sh/docs/actions/wallet/getAddresses)[requestAddresses](https://viem.sh/docs/actions/wallet/requestAddresses)

Assets

[watchAsset](https://viem.sh/docs/actions/wallet/watchAsset)

Chain

[addChain](https://viem.sh/docs/actions/wallet/addChain)[switchChain](https://viem.sh/docs/actions/wallet/switchChain)

Data

[signMessage](https://viem.sh/docs/actions/wallet/signMessage)[signTypedData](https://viem.sh/docs/actions/wallet/signTypedData)

Permissions

[getPermissions](https://viem.sh/docs/actions/wallet/getPermissions)[requestPermissions](https://viem.sh/docs/actions/wallet/requestPermissions)

Transaction

[prepareTransactionRequest](https://viem.sh/docs/actions/wallet/prepareTransactionRequest)[sendRawTransaction](https://viem.sh/docs/actions/wallet/sendRawTransaction)[sendTransaction](https://viem.sh/docs/actions/wallet/sendTransaction)[signTransaction](https://viem.sh/docs/actions/wallet/signTransaction)

Test Actions

Chevron Right

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>getStorageAt</title>
  <url>https://viem.sh/docs/contract/getStorageAt</url>
  <content>[Skip to content](https://viem.sh/docs/contract/getStorageAt#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the value from a storage slot at a given address.

Usage
-----

    import { toHex } from 'viem'
    import { wagmiAbi } from './abi'
    import { publicClient } from './client'
     
    const data = await publicClient.getStorageAt({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      slot: toHex(0)
    })

Return Value
------------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The value of the storage slot.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const data = await publicClient.getStorageAt({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      slot: toHex(0)
    })

### slot

*   **Type**: [`Hex`](https://viem.sh/docs/glossary/types#hex)

The storage position (as a hex encoded value).

    const data = await publicClient.getStorageAt({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      slot: toHex(0) 
    })

### blockNumber (optional)

*   **Type:** `number`

The block number to perform the storage slot read against.

    const bytecode = await publicClient.getStorageAt({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      slot: toHex(0),
      blockNumber: 15121123n, 
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

The block tag to perform the storage slot read against.

    const bytecode = await publicClient.getStorageAt({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      slot: toHex(0),
      blockTag: 'safe', 
    })

JSON-RPC Method
---------------

[`eth_getStorageAt`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_getstorageat)</content>
</page>

<page>
  <title>parseEventLogs</title>
  <url>https://viem.sh/docs/contract/parseEventLogs</url>
  <content>Extracts & decodes logs matching the provided `abi` (and optional `eventName`) from a set of opaque logs.

Useful for decoding logs on Transaction Receipts.

Install
-------

    import { parseEventLogs } from 'viem'

Usage
-----

    import { parseEventLogs } from 'viem'
    import { erc20Abi } from './abi'
    import { client } from './client'
     
    const receipt = await getTransactionReceipt(client, {
      hash: '0xec23b2ba4bc59ba61554507c1b1bc91649e6586eb2dd00c728e8ed0db8bb37ea',
    })
     
    const logs = parseEventLogs({ 
      abi: erc20Abi, 
      logs: receipt.logs,
    })
    // [
    //   { args: { ... }, eventName: 'Transfer', logIndex: 3 ... },  
    //   { args: { ... }, eventName: 'Approval', logIndex: 5 ... },
    //   ...
    // ]

### Scoping to Event Name(s)

You can scope the logs to a specific event name by providing the `eventName` argument:

    import { parseEventLogs } from 'viem'
    import { erc20Abi } from './abi'
    import { client } from './client'
     
    const receipt = await getTransactionReceipt(client, {
      hash: '0xec23b2ba4bc59ba61554507c1b1bc91649e6586eb2dd00c728e8ed0db8bb37ea',
    })
     
    const logs = parseEventLogs({ 
      abi: erc20Abi, 
      eventName: 'Transfer', 
      logs: receipt.logs,
    })
    // [
    //   { args: { ... }, eventName: 'Transfer', logIndex: 3, ... },  
    //   { args: { ... }, eventName: 'Transfer', logIndex: 7, ... },
    //   ...
    // ]

You can also pass an array to scope multiple event names:

    import { parseEventLogs } from 'viem'
    import { erc20Abi } from './abi'
    import { client } from './client'
     
    const receipt = await getTransactionReceipt(client, {
      hash: '0xec23b2ba4bc59ba61554507c1b1bc91649e6586eb2dd00c728e8ed0db8bb37ea',
    })
     
    const logs = parseEventLogs({ 
      abi: erc20Abi, 
      eventName: ['Transfer', 'Approval'], 
      logs: receipt.logs,
    })
    // [
    //   { args: { ... }, eventName: 'Transfer', logIndex: 3, ... },  
    //   { args: { ... }, eventName: 'Approval', logIndex: 5, ... },  
    //   { args: { ... }, eventName: 'Transfer', logIndex: 7, ... },
    //   ...
    // ]

### Scoping to Arguments

You can scope the logs to arguments by providing the `args` argument:

    import { parseEventLogs } from 'viem'
    import { erc20Abi } from './abi'
    import { client } from './client'
     
    const receipt = await getTransactionReceipt(client, {
      hash: '0xec23b2ba4bc59ba61554507c1b1bc91649e6586eb2dd00c728e8ed0db8bb37ea',
    })
     
    const logs = parseEventLogs({ 
      abi: erc20Abi, 
      args: { 
        from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      }, 
      logs: receipt.logs,
    })
    // [
    //   { args: { from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', ... }, eventName: '...', logIndex: 3, ... },  
    //   { args: { from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', ... }, eventName: '...', logIndex: 7, ... },
    //   ...
    // ]

You can also pass an array to scope multiple values of an argument:

    import { parseEventLogs } from 'viem'
    import { erc20Abi } from './abi'
    import { client } from './client'
     
    const receipt = await getTransactionReceipt(client, {
      hash: '0xec23b2ba4bc59ba61554507c1b1bc91649e6586eb2dd00c728e8ed0db8bb37ea',
    })
     
    const logs = parseEventLogs({ 
      abi: erc20Abi, 
      args: { 
        from: [ 
          '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
          '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', 
        ], 
      }, 
      logs: receipt.logs,
    })
    // [
    //   { args: { from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', ... }, eventName: '...', logIndex: 3, ... },  
    //   { args: { from: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045', ... }, eventName: '...', logIndex: 7, ... },
    //   ...
    // ]

### Partial Decode

By default, if the `topics` and `data` does not conform to the ABI (a mismatch between the number of indexed/non-indexed arguments), `parseEventLogs` will not return return the decoded log.

For example, the following will not return the nonconforming log as there is a mismatch in non-`indexed` arguments & `data` length.

    parseEventLogs({
      abi: parseAbi(['event Transfer(address indexed, address, uint256)']),
      logs: [{
        // `data` should be 64 bytes, but is only 32 bytes. 
        data: '0x0000000000000000000000000000000000000000000000000000000000000001', 
        topics: [
          '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
          '0x000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266',
        ]
        // ...
      }]
    })
    // []

It is possible for `parseEventLogs` to try and partially decode the Log, this can be done by setting the `strict` argument to `false`:

    parseEventLogs({
      abi: parseAbi(['event Transfer(address indexed, address, uint256)']),
      logs: [{
        data: '0x0000000000000000000000000000000000000000000000000000000000000001',
        topics: [
          '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
          '0x000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266',
        ]
        // ...
      }]
      strict: false
    })
    /**
     * [
     *  {
     *    eventName: 'Transfer',
     *    args: ['0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'],
     *    blockNumber: 42069420n,
     *    logIndex: 69,
     *    ...
     *  }
     * ]
     */

Return Value
------------

`Log[]`

Decoded logs.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const topics = parseEventLogs({
      abi: wagmiAbi, 
      logs: [{
        blockNumber: 69420n,
        data: '0x0000000000000000000000000000000000000000000000000000000000000001',
        logIndex: 1,
        topics: [
          '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
          '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
          '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
        ]
        // ...
      }]
    })

### logs

*   **Type:** `Log[]`

An array of logs to parse.

    const topics = parseEventLogs({
      abi: wagmiAbi,
      logs: [{ 
        blockNumber: 69420n, 
        data: '0x0000000000000000000000000000000000000000000000000000000000000001', 
        logIndex: 1, 
        topics: [ 
          '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0',  
          '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
          '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
        ] 
        // ... 
      }] 
    })

### args (optional)

*   **Type:** `{ [property: string]: string | string[] | null }`

Arguments to scope the logs to.

    const topics = parseEventLogs({
      abi: wagmiAbi,
      args: { 
        from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      }, 
      logs: [{
        blockNumber: 69420n,
        data: '0x0000000000000000000000000000000000000000000000000000000000000001',
        logIndex: 1,
        topics: [
          '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
          '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
          '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
        ]
        // ...
      }]
    })

### eventName (optional)

*   **Type:** `string`

An event name from the ABI.

    const topics = parseEventLogs({
      abi: wagmiAbi,
      eventName: 'Transfer', 
      logs: [{
        blockNumber: 69420n,
        data: '0x0000000000000000000000000000000000000000000000000000000000000001',
        logIndex: 1,
        topics: [
          '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
          '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
          '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
        ]
        // ...
      }]
    })

### strict (optional)

*   **Type:** `boolean`
*   **Default:** `true`

If `true`, `parseEventLogs` will not return [nonconforming logs](https://viem.sh/docs/contract/parseEventLogs#partial-decode). If `false`, `parseEventLogs` will try and [partially decode](https://viem.sh/docs/contract/parseEventLogs#partial-decode) nonconforming logs.

    const topics = parseEventLogs({
      abi: wagmiAbi,
      eventName: 'Transfer',
      logs: [{
        blockNumber: 69420n,
        data: '0x0000000000000000000000000000000000000000000000000000000000000001',
        logIndex: 1,
        topics: [
          '0x406dade31f7ae4b5dbc276258c28dde5ae6d5c2773c5745802c493a2360e55e0', 
          '0x00000000000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
          '0x0000000000000000000000000000000070997970c51812dc3a010c7d01b50e0d17dc79c8'
        ]
        // ...
      }],
      strict: false
    })</content>
</page>

<page>
  <title>switchChain</title>
  <url>https://viem.sh/docs/actions/wallet/switchChain</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/wallet/introduction)

Account

[getAddresses](https://viem.sh/docs/actions/wallet/getAddresses)[requestAddresses](https://viem.sh/docs/actions/wallet/requestAddresses)

Assets

[watchAsset](https://viem.sh/docs/actions/wallet/watchAsset)

Chain

[addChain](https://viem.sh/docs/actions/wallet/addChain)[switchChain](https://viem.sh/docs/actions/wallet/switchChain)

Data

[signMessage](https://viem.sh/docs/actions/wallet/signMessage)[signTypedData](https://viem.sh/docs/actions/wallet/signTypedData)

Permissions

[getPermissions](https://viem.sh/docs/actions/wallet/getPermissions)[requestPermissions](https://viem.sh/docs/actions/wallet/requestPermissions)

Transaction

[prepareTransactionRequest](https://viem.sh/docs/actions/wallet/prepareTransactionRequest)[sendRawTransaction](https://viem.sh/docs/actions/wallet/sendRawTransaction)[sendTransaction](https://viem.sh/docs/actions/wallet/sendTransaction)[signTransaction](https://viem.sh/docs/actions/wallet/signTransaction)

Test Actions

Chevron Right

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>addChain</title>
  <url>https://viem.sh/docs/actions/wallet/addChain</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/wallet/introduction)

Account

[getAddresses](https://viem.sh/docs/actions/wallet/getAddresses)[requestAddresses](https://viem.sh/docs/actions/wallet/requestAddresses)

Assets

[watchAsset](https://viem.sh/docs/actions/wallet/watchAsset)

Chain

[addChain](https://viem.sh/docs/actions/wallet/addChain)[switchChain](https://viem.sh/docs/actions/wallet/switchChain)

Data

[signMessage](https://viem.sh/docs/actions/wallet/signMessage)[signTypedData](https://viem.sh/docs/actions/wallet/signTypedData)

Permissions

[getPermissions](https://viem.sh/docs/actions/wallet/getPermissions)[requestPermissions](https://viem.sh/docs/actions/wallet/requestPermissions)

Transaction

[prepareTransactionRequest](https://viem.sh/docs/actions/wallet/prepareTransactionRequest)[sendRawTransaction](https://viem.sh/docs/actions/wallet/sendRawTransaction)[sendTransaction](https://viem.sh/docs/actions/wallet/sendTransaction)[signTransaction](https://viem.sh/docs/actions/wallet/signTransaction)

Test Actions

Chevron Right

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>watchAsset</title>
  <url>https://viem.sh/docs/actions/wallet/watchAsset</url>
  <content>Requests that the user tracks the token in their wallet. Returns a boolean indicating if the token was successfully added.

Usage
-----

    import { walletClient } from './client'
     
    const success = await walletClient.watchAsset({ 
      type: 'ERC20',
      options: {
        address: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
        decimals: 18,
        symbol: 'WETH',
      },
    })

Returns
-------

`boolean`

Boolean indicating if the token was successfully added.

Parameters
----------

### type

*   **Type:** `string`

Token type.

    import { createWalletClient, custom } from 'viem'
    import { mainnet } from 'viem/chains'
     
    export const walletClient = createWalletClient({
      chain: mainnet,
      transport: custom(window.ethereum!),
    })
    // ---cut--
    const success = await walletClient.watchAsset({
      type: 'ERC20', 
      options: {
        address: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
        decimals: 18,
        symbol: 'WETH',
      },
    });

### options.address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The address of the token contract.

    const success = await walletClient.watchAsset({
      type: 'ERC20',
      options: {
        address: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
        decimals: 18,
        symbol: 'WETH',
      },
    });

### options.decimals

*   **Type:** `number`

The number of token decimals.

    const success = await walletClient.watchAsset({
      type: 'ERC20',
      options: {
        address: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
        decimals: 18, 
        symbol: 'WETH',
      },
    });

### options.symbol

*   **Type:** `string`

A ticker symbol or shorthand, up to 11 characters.

    const success = await walletClient.watchAsset({
      type: 'ERC20',
      options: {
        address: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
        decimals: 18,
        symbol: 'WETH', 
      }
    })

### options.image

*   **Type:** `string`

A string url of the token logo.

    const success = await walletClient.watchAsset({
      type: 'ERC20',
      options: {
        address: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
        decimals: 18,
        symbol: 'WETH',
        image: 'https://weth.com/icon.png', 
      }
    })

JSON-RPC Methods
----------------

[`wallet_watchAsset`](https://eips.ethereum.org/EIPS/eip-747)</content>
</page>

<page>
  <title>getPermissions</title>
  <url>https://viem.sh/docs/actions/wallet/getPermissions</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/wallet/introduction)

Account

[getAddresses](https://viem.sh/docs/actions/wallet/getAddresses)[requestAddresses](https://viem.sh/docs/actions/wallet/requestAddresses)

Assets

[watchAsset](https://viem.sh/docs/actions/wallet/watchAsset)

Chain

[addChain](https://viem.sh/docs/actions/wallet/addChain)[switchChain](https://viem.sh/docs/actions/wallet/switchChain)

Data

[signMessage](https://viem.sh/docs/actions/wallet/signMessage)[signTypedData](https://viem.sh/docs/actions/wallet/signTypedData)

Permissions

[getPermissions](https://viem.sh/docs/actions/wallet/getPermissions)[requestPermissions](https://viem.sh/docs/actions/wallet/requestPermissions)

Transaction

[prepareTransactionRequest](https://viem.sh/docs/actions/wallet/prepareTransactionRequest)[sendRawTransaction](https://viem.sh/docs/actions/wallet/sendRawTransaction)[sendTransaction](https://viem.sh/docs/actions/wallet/sendTransaction)[signTransaction](https://viem.sh/docs/actions/wallet/signTransaction)

Test Actions

Chevron Right

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>requestPermissions</title>
  <url>https://viem.sh/docs/actions/wallet/requestPermissions</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/wallet/introduction)

Account

[getAddresses](https://viem.sh/docs/actions/wallet/getAddresses)[requestAddresses](https://viem.sh/docs/actions/wallet/requestAddresses)

Assets

[watchAsset](https://viem.sh/docs/actions/wallet/watchAsset)

Chain

[addChain](https://viem.sh/docs/actions/wallet/addChain)[switchChain](https://viem.sh/docs/actions/wallet/switchChain)

Data

[signMessage](https://viem.sh/docs/actions/wallet/signMessage)[signTypedData](https://viem.sh/docs/actions/wallet/signTypedData)

Permissions

[getPermissions](https://viem.sh/docs/actions/wallet/getPermissions)[requestPermissions](https://viem.sh/docs/actions/wallet/requestPermissions)

Transaction

[prepareTransactionRequest](https://viem.sh/docs/actions/wallet/prepareTransactionRequest)[sendRawTransaction](https://viem.sh/docs/actions/wallet/sendRawTransaction)[sendTransaction](https://viem.sh/docs/actions/wallet/sendTransaction)[signTransaction](https://viem.sh/docs/actions/wallet/signTransaction)

Test Actions

Chevron Right

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>decodeFunctionData</title>
  <url>https://viem.sh/docs/contract/decodeFunctionData</url>
  <content>Decodes ABI encoded data (4 byte selector & arguments) into a function name and arguments.

The opposite of [`encodeFunctionData`](https://viem.sh/docs/contract/encodeFunctionData).

Install
-------

    import { decodeFunctionData } from 'viem'

Usage
-----

Below is a very basic example of how to decode a function to calldata.

    import { decodeFunctionData } from 'viem'
    import { wagmiAbi } from './abi.ts'
     
    const { functionName } = decodeFunctionData({
      abi: wagmiAbi,
      data: '0x18160ddd'
    })
    // { functionName: 'totalSupply' }

### Extracting Arguments

If your calldata includes argument(s) after the 4byte function signature, you can extract them with the `args` return value.

    import { decodeFunctionData } from 'viem'
    import { wagmiAbi } from './abi'
     
    
    const { functionName, args } = decodeFunctionData({
      abi: wagmiAbi,
      data: '0x70a08231000000000000000000000000fba3912ca04dd458c843e2ee08967fc04f3579c2'
    })
    // { functionName: 'balanceOf', args: ["0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2"] }

Return Value
------------

    {
      functionName: string;
      args: unknown[] | undefined;
    }

Decoded ABI function data.

### functionName

*   **Type**: `string`

The decoded function name.

### args

*   **Type**: `unknown[] | undefined`

The decoded function arguments.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const { functionName } = decodeFunctionData({
      abi: wagmiAbi, 
      data: '0x18160ddd'
    })

### data

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The encoded calldata.

    const { functionName } = decodeFunctionData({
      abi: wagmiAbi,
      data: '0x18160ddd'
    })</content>
</page>

<page>
  <title>signMessage</title>
  <url>https://viem.sh/docs/actions/wallet/signMessage</url>
  <content>    import { account, walletClient } from './config'
     
    const signature_1 = await walletClient.signMessage({ 
      account,
      message: 'hello world',
    })
    Output: "0xa461f509887bd19e312c0c58467ce8ff8e300d3c1a90b608a760c5b80318eaf15fe57c96f9175d6cd4daad4663763baa7e78836e067d0163e9a2ccf2ff753f5b1b" const signature_2 = await walletClient.signMessage({
      account,
      // Hex data representation of message.
      message: { raw: '0x68656c6c6f20776f726c64' },
    })
    Output: "0xa461f509887bd19e312c0c58467ce8ff8e300d3c1a90b608a760c5b80318eaf15fe57c96f9175d6cd4daad4663763baa7e78836e067d0163e9a2ccf2ff753f5b1b"</content>
</page>

<page>
  <title>impersonateAccount</title>
  <url>https://viem.sh/docs/actions/test/impersonateAccount</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/impersonateAccount#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Impersonate an account or contract address. This lets you send transactions from that account even if you don't have access to its private key.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.impersonateAccount({ 
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'
    })

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The address of the target account.

    await testClient.impersonateAccount({
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
    })</content>
</page>

<page>
  <title>setBalance</title>
  <url>https://viem.sh/docs/actions/test/setBalance</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setBalance#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Modifies the balance of an account.

Usage
-----

    import { parseEther } from 'viem'
    import { testClient } from './client'
     
    await testClient.setBalance({ 
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: parseEther('1')
    })

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The address of the target account.

    await testClient.setBalance({
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
      value: parseEther('1')
    })

### value (optional)

*   **Type:** `bigint`

The value (in wei) to set.

    await testClient.setBalance({
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: 1000000000000000000n
    })</content>
</page>

<page>
  <title>setCode</title>
  <url>https://viem.sh/docs/actions/test/setCode</url>
  <content>Modifies the bytecode stored at an account's address.

Usage
-----

    import { testClient } from './client'
     
    await testClient.setCode({ 
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79',
      bytecode: '0x60806040526000600355600019600955600c80546001600160a01b031916737a250d5630b4cf539739df...'
    })

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The account address.

    await testClient.setCode({
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79', 
      bytecode: '0x60806040526000600355600019600955600c80546001600160a01b031916737a250d5630b4cf539739df...'
    })

### bytecode

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The stored bytecode.

    await testClient.setCode({
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79',
      bytecode: '0x60806040526000600355600019600955600c80546001600160a01b031916737a250d5630b4cf539739df...'
    })</content>
</page>

<page>
  <title>signTransaction</title>
  <url>https://viem.sh/docs/actions/wallet/signTransaction</url>
  <content>Signs a transaction.

Usage
-----

    import { account, walletClient } from './config'
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
     
    const signature = await walletClient.signTransaction(request) 
    // 0x02f850018203118080825208808080c080a04012522854168b27e5dc3d5839bab5e6b39e1a0ffd343901ce1622e3d64b48f1a04e00902ae0502c4728cbf12156290df99c3ed7de85b1dbfe20b5c36931733a33
     
    const hash = await walletClient.sendRawTransaction(signature)

### Account Hoisting

If you do not wish to pass an `account` to every `prepareTransactionRequest`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient } from './config'
     
    const request = await walletClient.prepareTransactionRequest({
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
     
    const signature = await walletClient.signTransaction(request) 
    // 0x02f850018203118080825208808080c080a04012522854168b27e5dc3d5839bab5e6b39e1a0ffd343901ce1622e3d64b48f1a04e00902ae0502c4728cbf12156290df99c3ed7de85b1dbfe20b5c36931733a33
     
    const hash = await walletClient.sendRawTransaction(signature)

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The signed serialized transaction.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const signature = await walletClient.signTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### to

*   **Type:** `0x${string}`

The transaction recipient or contract address.

    const signature = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: 1000000000000000000n,
      nonce: 69
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const signature = await walletClient.signTransaction({
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### authorizationList (optional)

*   **Type:** `AuthorizationList`

Signed EIP-7702 Authorization list.

    const authorization = await walletClient.signAuthorization({ 
      account,
      contractAddress: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
    }) 
     
    const signature = await walletClient.signTransaction({
      account,
      authorizationList: [authorization], 
      data: '0xdeadbeef',
      to: account.address,
    })

### blobs (optional)

*   **Type:** `Hex[]`

Blobs for [Blob Transactions](https://viem.sh/docs/guides/blob-transactions).

    import * as cKzg from 'c-kzg'
    import { toBlobs, setupKzg, stringToHex } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const hash = await walletClient.signTransaction({
      account,
      blobs: toBlobs({ data: stringToHex('blobby blob!') }), 
      kzg,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

The chain is also used to infer its request type (e.g. the Celo chain has a `gatewayFee` that you can pass through to `signTransaction`).

    import { optimism } from 'viem/chains'
     
    const signature = await walletClient.signTransaction({
      chain: optimism, 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const signature = await walletClient.signTransaction({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const signature = await walletClient.signTransaction({
      account,
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### kzg (optional)

*   **Type:** `KZG`

KZG implementation for [Blob Transactions](https://viem.sh/docs/guides/blob-transactions).

See [`setupKzg`](https://viem.sh/docs/utilities/setupKzg) for more information.

    import * as cKzg from 'c-kzg'
    import { toBlobs, setupKzg, stringToHex } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const signature = await walletClient.signTransaction({
      account,
      blobs: toBlobs({ data: stringToHex('blobby blob!') }), 
      kzg, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const signature = await walletClient.signTransaction({
      account,
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const signature = await walletClient.signTransaction({
      account,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const signature = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    const signature = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
      nonce: 69
    })</content>
</page>

<page>
  <title>setNonce</title>
  <url>https://viem.sh/docs/actions/test/setNonce</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setNonce#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Modifies (overrides) the nonce of an account.

Usage
-----

    import { testClient } from './client'
     
    await testClient.setNonce({ 
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      nonce: 420
    })

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The address of the target account.

    await testClient.setNonce({
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
      nonce: 420
    })

### nonce (optional)

*   **Type:** `number`

The nonce.

    await testClient.setNonce({
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      nonce: 420
    })</content>
</page>

<page>
  <title>setStorageAt</title>
  <url>https://viem.sh/docs/actions/test/setStorageAt</url>
  <content>Writes to a slot of an account's storage.

Usage
-----

    import { testClient } from './client'
     
    await testClient.setStorageAt({ 
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79',
      index: 2,
      value: '0x0000000000000000000000000000000000000000000000000000000000000069'
    })

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The account address.

    await testClient.setStorageAt({
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79', 
      index: 2,
      value: '0x0000000000000000000000000000000000000000000000000000000000000069'
    })

### index

*   **Type:** `number | Hash`

The storage slot (index). Can either be a number or hash value.

    await testClient.setStorageAt({
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79',
      index: '0xa6eef7e35abe7026729641147f7915573c7e97b47efa546f5f6e3230263bcb49', 
      value: '0x0000000000000000000000000000000000000000000000000000000000000069'
    })

### value

*   **Type:** `number`

The value to store as a 32 byte hex string.

    await testClient.setStorageAt({
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79',
      index: 2,
      value: '0x0000000000000000000000000000000000000000000000000000000000000069'
    })</content>
</page>

<page>
  <title>stopImpersonatingAccount</title>
  <url>https://viem.sh/docs/actions/test/stopImpersonatingAccount</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/stopImpersonatingAccount#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Stop impersonating an account after having previously used [`impersonateAccount`](https://viem.sh/docs/actions/test/impersonateAccount).

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.stopImpersonatingAccount({ 
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'
    })

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The address of the target account.

    await testClient.stopImpersonatingAccount({
      address: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 
    })</content>
</page>

<page>
  <title>getAutomine</title>
  <url>https://viem.sh/docs/actions/test/getAutomine</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

Test Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/test/introduction)

Account

[impersonateAccount](https://viem.sh/docs/actions/test/impersonateAccount)[setBalance](https://viem.sh/docs/actions/test/setBalance)[setCode](https://viem.sh/docs/actions/test/setCode)[setNonce](https://viem.sh/docs/actions/test/setNonce)[setStorageAt](https://viem.sh/docs/actions/test/setStorageAt)[stopImpersonatingAccount](https://viem.sh/docs/actions/test/stopImpersonatingAccount)

Block

[getAutomine](https://viem.sh/docs/actions/test/getAutomine)[increaseTime](https://viem.sh/docs/actions/test/increaseTime)[mine](https://viem.sh/docs/actions/test/mine)[removeBlockTimestampInterval](https://viem.sh/docs/actions/test/removeBlockTimestampInterval)[setAutomine](https://viem.sh/docs/actions/test/setAutomine)[setIntervalMining](https://viem.sh/docs/actions/test/setIntervalMining)[setBlockTimestampInterval](https://viem.sh/docs/actions/test/setBlockTimestampInterval)[setBlockGasLimit](https://viem.sh/docs/actions/test/setBlockGasLimit)[setNextBlockBaseFeePerGas](https://viem.sh/docs/actions/test/setNextBlockBaseFeePerGas)[setNextBlockTimestamp](https://viem.sh/docs/actions/test/setNextBlockTimestamp)

Node

[setCoinbase](https://viem.sh/docs/actions/test/setCoinbase)[setMinGasPrice](https://viem.sh/docs/actions/test/setMinGasPrice)

Settings

[reset](https://viem.sh/docs/actions/test/reset)[setLoggingEnabled](https://viem.sh/docs/actions/test/setLoggingEnabled)[setRpcUrl](https://viem.sh/docs/actions/test/setRpcUrl)

State

[dumpState](https://viem.sh/docs/actions/test/dumpState)[loadState](https://viem.sh/docs/actions/test/loadState)[revert](https://viem.sh/docs/actions/test/revert)[snapshot](https://viem.sh/docs/actions/test/snapshot)

Transaction

[dropTransaction](https://viem.sh/docs/actions/test/dropTransaction)[getTxpoolContent](https://viem.sh/docs/actions/test/getTxpoolContent)[getTxpoolStatus](https://viem.sh/docs/actions/test/getTxpoolStatus)[inspectTxpool](https://viem.sh/docs/actions/test/inspectTxpool)[sendUnsignedTransaction](https://viem.sh/docs/actions/test/sendUnsignedTransaction)

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>increaseTime</title>
  <url>https://viem.sh/docs/actions/test/increaseTime</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/increaseTime#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Jump forward in time by the given amount of time, in seconds.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.increaseTime({ 
      seconds: 420,
    })

Parameters
----------

### seconds

*   **Type:** `number`

The amount of seconds to jump forward in time.

    await testClient.increaseTime({
      seconds: 20, 
    })</content>
</page>

<page>
  <title>mine</title>
  <url>https://viem.sh/docs/actions/test/mine</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/mine#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Mine a specified number of blocks.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.mine({ 
      blocks: 1,
    })

Parameters
----------

### blocks

*   **Type:** `number`

Number of blocks to mine.

    await testClient.mine({
      blocks: 1, 
    })

### interval (optional)

*   **Type:** `number`
*   **Default:** `1`

Interval between each block in seconds.

    await testClient.mine({
      blocks: 10,
      interval: 4
    })</content>
</page>

<page>
  <title>removeBlockTimestampInterval</title>
  <url>https://viem.sh/docs/actions/test/removeBlockTimestampInterval</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/removeBlockTimestampInterval#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Removes [`setBlockTimestampInterval`](https://viem.sh/docs/actions/test/setBlockTimestampInterval) if it exists.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.removeBlockTimestampInterval()</content>
</page>

<page>
  <title>setIntervalMining</title>
  <url>https://viem.sh/docs/actions/test/setIntervalMining</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setIntervalMining#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Sets the automatic mining interval (in seconds) of blocks. Setting the interval to `0` will disable automatic mining.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.setIntervalMining({ 
      interval: 5
    })

Parameters
----------

### interval

*   **Type:** `number`

The mining interval (in seconds). Setting the interval to `0` will disable automatic mining.

    await testClient.setIntervalMining({
      interval: 5
    })</content>
</page>

<page>
  <title>setAutomine</title>
  <url>https://viem.sh/docs/actions/test/setAutomine</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setAutomine#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Enables or disables the automatic mining of new blocks with each new transaction submitted to the network.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.setAutomine(true) 

Parameters
----------

### enabled

*   **Type:** `boolean`

    await testClient.setAutomine(false)</content>
</page>

<page>
  <title>setBlockGasLimit</title>
  <url>https://viem.sh/docs/actions/test/setBlockGasLimit</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setBlockGasLimit#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Sets the block's gas limit.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.setBlockGasLimit({ 
      gasLimit: 420_000n
    })

Parameters
----------

### gasLimit

*   **Type:** `bigint`

The gas limit.

    await testClient.setBlockGasLimit({
      gasLimit: 420_000n
    })</content>
</page>

<page>
  <title>setBlockTimestampInterval</title>
  <url>https://viem.sh/docs/actions/test/setBlockTimestampInterval</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setBlockTimestampInterval#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Similar to [`increaseTime`](https://viem.sh/docs/actions/test/increaseTime), but sets a block timestamp `interval`. The timestamp of future blocks will be computed as `lastBlock_timestamp` + `interval`.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.setBlockTimestampInterval({ 
      interval: 5
    })

Parameters
----------

### interval

*   **Type:** `number`

    await testClient.setBlockTimestampInterval({
      interval: 1
    })</content>
</page>

<page>
  <title>setNextBlockBaseFeePerGas</title>
  <url>https://viem.sh/docs/actions/test/setNextBlockBaseFeePerGas</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setNextBlockBaseFeePerGas#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Sets the next block's base fee per gas.

Usage
-----

File

example.ts

    import { parseGwei } from 'viem'
    import { testClient } from './client'
     
    await testClient.setNextBlockBaseFeePerGas({ 
      baseFeePerGas: parseGwei('20')
    })

Parameters
----------

### baseFeePerGas

*   **Type:** `bigint`

Base fee per gas.

    await testClient.setNextBlockBaseFeePerGas({
      baseFeePerGas: parseGwei('30') 
    })</content>
</page>

<page>
  <title>setNextBlockTimestamp</title>
  <url>https://viem.sh/docs/actions/test/setNextBlockTimestamp</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setNextBlockTimestamp#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Sets the next block's timestamp.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.setNextBlockTimestamp({ 
      timestamp: 1671744314n
    })

Parameters
----------

### timestamp

*   **Type:** `bigint`

    await testClient.setNextBlockTimestamp({
      timestamp: 1671744314n
    })

Notes
-----

*   The next Block `timestamp` cannot be lesser than the current Block `timestamp`.</content>
</page>

<page>
  <title>setCoinbase</title>
  <url>https://viem.sh/docs/actions/test/setCoinbase</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setCoinbase#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Sets the coinbase address to be used in new blocks.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.setCoinbase({ 
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79',
    })

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The coinbase address.

    await testClient.setCoinbase({
      address: '0xe846c6fcf817734ca4527b28ccb4aea2b6663c79', 
    })</content>
</page>

<page>
  <title>reset</title>
  <url>https://viem.sh/docs/actions/test/reset</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/reset#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Resets the fork back to its original state.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.reset() 

Parameters
----------

### blockNumber (optional)

*   **Type:** `bigint`

Resets the fork to a given block number.

    await testClient.reset({
      blockNumber: 69420n, 
      jsonRpcUrl: 'https://1.rpc.thirdweb.com'
    })

### jsonRpcUrl (optional)

*   **Type:** `string`

Resets the fork with a given JSON RPC URL.

    await testClient.reset({
      blockNumber: 69420n,
      jsonRpcUrl: 'https://1.rpc.thirdweb.com'
    })</content>
</page>

<page>
  <title>setMinGasPrice</title>
  <url>https://viem.sh/docs/actions/test/setMinGasPrice</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/setMinGasPrice#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Change the minimum gas price accepted by the network (in wei).

> Note: `setMinGasPrice` can only be used on clients that do not have EIP-1559 enabled.

Usage
-----

File

example.ts

    import { parseGwei } from 'viem'
    import { testClient } from './client'
     
    await testClient.setMinGasPrice({ 
      gasPrice: parseGwei('20'),
    })

Parameters
----------

### gasPrice

*   **Type:** `bigint`

The gas price (in wei).

    await testClient.setMinGasPrice({
      gasPrice: parseGwei('20'), 
    })</content>
</page>

<page>
  <title>setLoggingEnabled</title>
  <url>https://viem.sh/docs/actions/test/setLoggingEnabled</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

Test Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/test/introduction)

Account

[impersonateAccount](https://viem.sh/docs/actions/test/impersonateAccount)[setBalance](https://viem.sh/docs/actions/test/setBalance)[setCode](https://viem.sh/docs/actions/test/setCode)[setNonce](https://viem.sh/docs/actions/test/setNonce)[setStorageAt](https://viem.sh/docs/actions/test/setStorageAt)[stopImpersonatingAccount](https://viem.sh/docs/actions/test/stopImpersonatingAccount)

Block

[getAutomine](https://viem.sh/docs/actions/test/getAutomine)[increaseTime](https://viem.sh/docs/actions/test/increaseTime)[mine](https://viem.sh/docs/actions/test/mine)[removeBlockTimestampInterval](https://viem.sh/docs/actions/test/removeBlockTimestampInterval)[setAutomine](https://viem.sh/docs/actions/test/setAutomine)[setIntervalMining](https://viem.sh/docs/actions/test/setIntervalMining)[setBlockTimestampInterval](https://viem.sh/docs/actions/test/setBlockTimestampInterval)[setBlockGasLimit](https://viem.sh/docs/actions/test/setBlockGasLimit)[setNextBlockBaseFeePerGas](https://viem.sh/docs/actions/test/setNextBlockBaseFeePerGas)[setNextBlockTimestamp](https://viem.sh/docs/actions/test/setNextBlockTimestamp)

Node

[setCoinbase](https://viem.sh/docs/actions/test/setCoinbase)[setMinGasPrice](https://viem.sh/docs/actions/test/setMinGasPrice)

Settings

[reset](https://viem.sh/docs/actions/test/reset)[setLoggingEnabled](https://viem.sh/docs/actions/test/setLoggingEnabled)[setRpcUrl](https://viem.sh/docs/actions/test/setRpcUrl)

State

[dumpState](https://viem.sh/docs/actions/test/dumpState)[loadState](https://viem.sh/docs/actions/test/loadState)[revert](https://viem.sh/docs/actions/test/revert)[snapshot](https://viem.sh/docs/actions/test/snapshot)

Transaction

[dropTransaction](https://viem.sh/docs/actions/test/dropTransaction)[getTxpoolContent](https://viem.sh/docs/actions/test/getTxpoolContent)[getTxpoolStatus](https://viem.sh/docs/actions/test/getTxpoolStatus)[inspectTxpool](https://viem.sh/docs/actions/test/inspectTxpool)[sendUnsignedTransaction](https://viem.sh/docs/actions/test/sendUnsignedTransaction)

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>dumpState</title>
  <url>https://viem.sh/docs/actions/test/dumpState</url>
  <content>    import { testClient } from './client'
     
    const state = await testClient.dumpState()
    // 0x1f8b08000000000000ffad934d8e1c310885ef52eb5e003660e636184c3651b7949948915a7df7b8934ded6bbcc23fe2f3e3c1f3f088c7effbd7e7f1f13ce00ff60c35939e4e016352131bb3658bd0f046682dcd98dfafef8f7bace3036ec7f49ffe2fde190817da82b0e9933abcd7713be291ffaf77fcf9f5f8e53ff6f6f97addde4cced6dd8b3b89e6d4d468a2a3d93e537480fd15713933f12a73ebc2b106ae561c59bae1d152784733c067f1dc49479d987295d9a2f7c8cc296e00e534797026d94ed312a9bc93b5192726d155a882999a42300ea48ce680109a80936141a2be0d8f7182f6cb4a0d4a6d96ac49d16b2834e1a5836dd0c242c0b5751ac8d9d1cb4a4d65b97620594ac2dc77a159cbb9ab349f096fedee76828ecb4cdb20d044679e1124c6c1633a4acda639d026f81ea96f15eab0963a76ca3d2f81b58705fbea3e4a59761b11f8769ce0046d5799d5ac5216a37b8e51523d96f81c839476fb54d53422393bda94af505fafbf9d0612379c040000</content>
</page>

<page>
  <title>setRpcUrl</title>
  <url>https://viem.sh/docs/actions/test/setRpcUrl</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

Test Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/test/introduction)

Account

[impersonateAccount](https://viem.sh/docs/actions/test/impersonateAccount)[setBalance](https://viem.sh/docs/actions/test/setBalance)[setCode](https://viem.sh/docs/actions/test/setCode)[setNonce](https://viem.sh/docs/actions/test/setNonce)[setStorageAt](https://viem.sh/docs/actions/test/setStorageAt)[stopImpersonatingAccount](https://viem.sh/docs/actions/test/stopImpersonatingAccount)

Block

[getAutomine](https://viem.sh/docs/actions/test/getAutomine)[increaseTime](https://viem.sh/docs/actions/test/increaseTime)[mine](https://viem.sh/docs/actions/test/mine)[removeBlockTimestampInterval](https://viem.sh/docs/actions/test/removeBlockTimestampInterval)[setAutomine](https://viem.sh/docs/actions/test/setAutomine)[setIntervalMining](https://viem.sh/docs/actions/test/setIntervalMining)[setBlockTimestampInterval](https://viem.sh/docs/actions/test/setBlockTimestampInterval)[setBlockGasLimit](https://viem.sh/docs/actions/test/setBlockGasLimit)[setNextBlockBaseFeePerGas](https://viem.sh/docs/actions/test/setNextBlockBaseFeePerGas)[setNextBlockTimestamp](https://viem.sh/docs/actions/test/setNextBlockTimestamp)

Node

[setCoinbase](https://viem.sh/docs/actions/test/setCoinbase)[setMinGasPrice](https://viem.sh/docs/actions/test/setMinGasPrice)

Settings

[reset](https://viem.sh/docs/actions/test/reset)[setLoggingEnabled](https://viem.sh/docs/actions/test/setLoggingEnabled)[setRpcUrl](https://viem.sh/docs/actions/test/setRpcUrl)

State

[dumpState](https://viem.sh/docs/actions/test/dumpState)[loadState](https://viem.sh/docs/actions/test/loadState)[revert](https://viem.sh/docs/actions/test/revert)[snapshot](https://viem.sh/docs/actions/test/snapshot)

Transaction

[dropTransaction](https://viem.sh/docs/actions/test/dropTransaction)[getTxpoolContent](https://viem.sh/docs/actions/test/getTxpoolContent)[getTxpoolStatus](https://viem.sh/docs/actions/test/getTxpoolStatus)[inspectTxpool](https://viem.sh/docs/actions/test/inspectTxpool)[sendUnsignedTransaction](https://viem.sh/docs/actions/test/sendUnsignedTransaction)

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>loadState</title>
  <url>https://viem.sh/docs/actions/test/loadState</url>
  <content>    import { testClient } from './client'
     
    await testClient.loadState({ state: '0x1f8b08000000000000ffad934d8e1c310885ef52eb5e003660e636184c3651b7949948915a7df7b8934ded6bbcc23fe2f3e3c1f3f088c7effbd7e7f1f13ce00ff60c35939e4e016352131bb3658bd0f046682dcd98dfafef8f7bace3036ec7f49ffe2fde190817da82b0e9933abcd7713be291ffaf77fcf9f5f8e53ff6f6f97addde4cced6dd8b3b89e6d4d468a2a3d93e537480fd15713933f12a73ebc2b106ae561c59bae1d152784733c067f1dc49479d987295d9a2f7c8cc296e00e534797026d94ed312a9bc93b5192726d155a882999a42300ea48ce680109a80936141a2be0d8f7182f6cb4a0d4a6d96ac49d16b2834e1a5836dd0c242c0b5751ac8d9d1cb4a4d65b97620594ac2dc77a159cbb9ab349f096fedee76828ecb4cdb20d044679e1124c6c1633a4acda639d026f81ea96f15eab0963a76ca3d2f81b58705fbea3e4a59761b11f8769ce0046d5799d5ac5216a37b8e51523d96f81c839476fb54d53422393bda94af505fafbf9d0612379c040000' })</content>
</page>

<page>
  <title>revert</title>
  <url>https://viem.sh/docs/actions/test/revert</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/revert#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Revert the state of the blockchain at the current block.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.revert({ 
      id: '0x...'
    })

Parameters
----------

### id

*   **Type:** `"0x${string}"`

The snapshot ID.

    await testClient.revert({
      id: '0x...'
    })</content>
</page>

<page>
  <title>snapshot</title>
  <url>https://viem.sh/docs/actions/test/snapshot</url>
  <content>Introduction

[Why Viem](https://viem.sh/docs/introduction)[Installation](https://viem.sh/docs/installation)[Getting Started](https://viem.sh/docs/getting-started)[Platform Compatibility](https://viem.sh/docs/compatibility)[FAQ](https://viem.sh/docs/faq)

Guides

[Migration Guide](https://viem.sh/docs/migration-guide)[Ethers v5 → viem](https://viem.sh/docs/ethers-migration)[TypeScript](https://viem.sh/docs/typescript)[Error Handling](https://viem.sh/docs/error-handling)

[EIP-7702](https://viem.sh/docs/eip7702)

Chevron Right

[Blob Transactions](https://viem.sh/docs/guides/blob-transactions)

Clients & Transports

[Introduction](https://viem.sh/docs/clients/intro)[Public Client](https://viem.sh/docs/clients/public)[Wallet Client](https://viem.sh/docs/clients/wallet)[Test Client](https://viem.sh/docs/clients/test)[Build your own Client](https://viem.sh/docs/clients/custom)

Transports

[HTTP](https://viem.sh/docs/clients/transports/http)[WebSocket](https://viem.sh/docs/clients/transports/websocket)[Custom (EIP-1193)](https://viem.sh/docs/clients/transports/custom)[IPC](https://viem.sh/docs/clients/transports/ipc)[Fallback](https://viem.sh/docs/clients/transports/fallback)

Public Actions

Chevron Right

Wallet Actions

Chevron Right

Test Actions

Chevron Right

[Introduction](https://viem.sh/docs/actions/test/introduction)

Account

[impersonateAccount](https://viem.sh/docs/actions/test/impersonateAccount)[setBalance](https://viem.sh/docs/actions/test/setBalance)[setCode](https://viem.sh/docs/actions/test/setCode)[setNonce](https://viem.sh/docs/actions/test/setNonce)[setStorageAt](https://viem.sh/docs/actions/test/setStorageAt)[stopImpersonatingAccount](https://viem.sh/docs/actions/test/stopImpersonatingAccount)

Block

[getAutomine](https://viem.sh/docs/actions/test/getAutomine)[increaseTime](https://viem.sh/docs/actions/test/increaseTime)[mine](https://viem.sh/docs/actions/test/mine)[removeBlockTimestampInterval](https://viem.sh/docs/actions/test/removeBlockTimestampInterval)[setAutomine](https://viem.sh/docs/actions/test/setAutomine)[setIntervalMining](https://viem.sh/docs/actions/test/setIntervalMining)[setBlockTimestampInterval](https://viem.sh/docs/actions/test/setBlockTimestampInterval)[setBlockGasLimit](https://viem.sh/docs/actions/test/setBlockGasLimit)[setNextBlockBaseFeePerGas](https://viem.sh/docs/actions/test/setNextBlockBaseFeePerGas)[setNextBlockTimestamp](https://viem.sh/docs/actions/test/setNextBlockTimestamp)

Node

[setCoinbase](https://viem.sh/docs/actions/test/setCoinbase)[setMinGasPrice](https://viem.sh/docs/actions/test/setMinGasPrice)

Settings

[reset](https://viem.sh/docs/actions/test/reset)[setLoggingEnabled](https://viem.sh/docs/actions/test/setLoggingEnabled)[setRpcUrl](https://viem.sh/docs/actions/test/setRpcUrl)

State

[dumpState](https://viem.sh/docs/actions/test/dumpState)[loadState](https://viem.sh/docs/actions/test/loadState)[revert](https://viem.sh/docs/actions/test/revert)[snapshot](https://viem.sh/docs/actions/test/snapshot)

Transaction

[dropTransaction](https://viem.sh/docs/actions/test/dropTransaction)[getTxpoolContent](https://viem.sh/docs/actions/test/getTxpoolContent)[getTxpoolStatus](https://viem.sh/docs/actions/test/getTxpoolStatus)[inspectTxpool](https://viem.sh/docs/actions/test/inspectTxpool)[sendUnsignedTransaction](https://viem.sh/docs/actions/test/sendUnsignedTransaction)

Accounts

Chevron Right

Chains

Chevron Right

Contract

Chevron Right

ENS

Chevron Right

SIWE

Chevron Right

ABI

Chevron Right

EIP-7702

Chevron Right

Utilities

Chevron Right

Glossary

Chevron Right</content>
</page>

<page>
  <title>dropTransaction</title>
  <url>https://viem.sh/docs/actions/test/dropTransaction</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/dropTransaction#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Remove a transaction from the mempool.

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    await testClient.dropTransaction({ 
      hash: '0xe58dceb6b20b03965bb678e27d141e151d7d4efc2334c2d6a49b9fac523f7364'
    })

Parameters
----------

### hash

*   **Type:** [`Hash`](https://viem.sh/docs/glossary/types#hash)

The hash of the transaction.

    await testClient.dropTransaction({
      hash: '0xe58dceb6b20b03965bb678e27d141e151d7d4efc2334c2d6a49b9fac523f7364', 
    })</content>
</page>

<page>
  <title>getTxpoolContent</title>
  <url>https://viem.sh/docs/actions/test/getTxpoolContent</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/getTxpoolContent#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the details of all transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only. [Read more](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool).

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    const content = await testClient.getTxpoolContent() 

Returns
-------

Transaction pool content. [See here](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool).</content>
</page>

<page>
  <title>getTxpoolStatus</title>
  <url>https://viem.sh/docs/actions/test/getTxpoolStatus</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/getTxpoolStatus#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns a summary of all the transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only. [Read more](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool).

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    const status = await testClient.getTxpoolStatus() 

Returns
-------

Transaction pool status. [See here](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool).</content>
</page>

<page>
  <title>inspectTxpool</title>
  <url>https://viem.sh/docs/actions/test/inspectTxpool</url>
  <content>[Skip to content](https://viem.sh/docs/actions/test/inspectTxpool#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns a summary of all the transactions currently pending for inclusion in the next block(s), as well as the ones that are being scheduled for future execution only. [Read more](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool).

Usage
-----

File

example.ts

    import { testClient } from './client'
     
    const data = await testClient.inspectTxpool() 

Returns
-------

Transaction pool inspection data. [See here](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool).</content>
</page>

<page>
  <title>signMessage (Local Account)</title>
  <url>https://viem.sh/docs/accounts/local/signMessage</url>
  <content>Calculates an Ethereum-specific signature in [EIP-191 format](https://eips.ethereum.org/EIPS/eip-191): `keccak256("\x19Ethereum Signed Message:\n" + len(message) + message))`.

With the calculated signature, you can:

*   use [`verifyMessage`](https://viem.sh/docs/utilities/verifyMessage) to verify the signature,
*   use [`recoverMessageAddress`](https://viem.sh/docs/utilities/recoverMessageAddress) to recover the signing address from a signature.

Usage
-----

    import { privateKeyToAccount } from 'viem/accounts'
     
    const account = privateKeyToAccount('0x...')
     
    const signature = await account.signMessage({
      // Hex data representation of message.
      message: { raw: '0x68656c6c6f20776f726c64' },
    })
    Output: "0xa461f509887bd19e312c0c58467ce8ff8e300d3c1a90b608a760c5b80318eaf15fe57c96f9175d6cd4daad4663763baa7e78836e067d0163e9a2ccf2ff753f5b1b"

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The signed message.

Parameters
----------

### message

*   **Type:** `string | { raw: Hex | ByteArray }`

Message to sign.

By default, viem signs the UTF-8 representation of the message.

    const signature = await account.signMessage({
      message: 'hello world', 
    })

To sign the data representation of the message, you can use the `raw` attribute.

    const signature = await account.signMessage({
      message: { raw: '0x68656c6c6f20776f726c64' }, 
    })</content>
</page>

<page>
  <title>createNonceManager</title>
  <url>https://viem.sh/docs/accounts/local/createNonceManager</url>
  <content>Creates a Nonce Manager for automatic nonce generation

Creates a new Nonce Manager instance to be used with a [Local Account](https://viem.sh/docs/accounts/local). The Nonce Manager is used to automatically manage & generate nonces for transactions.

Import
------

    import { createNonceManager } from 'viem/nonce'

Usage
-----

A Nonce Manager can be instantiated with the `createNonceManager` function with a provided `source`.

The example below demonstrates how to create a Nonce Manager with a JSON-RPC source (ie. uses `eth_getTransactionCount` as the source of truth).

    import { createNonceManager, jsonRpc } from 'viem/nonce'
     
    const nonceManager = createNonceManager({
      source: jsonRpc()
    })

### Integration with Local Accounts

A `nonceManager` can be passed as an option to [Local Accounts](https://viem.sh/docs/accounts/local) to automatically manage nonces for transactions.

    import { privateKeyToAccount, nonceManager } from 'viem/accounts'
    import { client } from './config'
     
    const account = privateKeyToAccount('0x...', { nonceManager }) 
     
    const hashes = await Promise.all([ 
      ↓ nonce = 0  client.sendTransaction({     account, 
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('0.1'), 
      }), 
      ↓ nonce = 1  client.sendTransaction({     account, 
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('0.2'), 
      }), 
    ]) 

Return Type
-----------

`NonceManager`

The Nonce Manager.

Parameters
----------

### source

*   **Type:** `NonceManagerSource`

The source of truth for the Nonce Manager.

Available sources:

*   `jsonRpc`

    import { createNonceManager, jsonRpc } from 'viem/nonce'
     
    const nonceManager = createNonceManager({
      source: jsonRpc() 
    })</content>
</page>

<page>
  <title>sendUnsignedTransaction</title>
  <url>https://viem.sh/docs/actions/test/sendUnsignedTransaction</url>
  <content>Executes a transaction regardless of the signature.

Usage
-----

    import { testClient } from './client'
     
    const hash = await testClient.sendUnsignedTransaction({ 
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
    // '0x...'

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The transaction hash.

Parameters
----------

### from

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The Transaction sender.

    const hash = await testClient.sendUnsignedTransaction({
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### to

*   **Type:** `number`

The transaction recipient or contract address.

    const hash = await testClient.sendUnsignedTransaction({
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const data = await testClient.sendUnsignedTransaction({
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const hash = await testClient.sendUnsignedTransaction({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const hash = await testClient.sendUnsignedTransaction({
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await testClient.sendUnsignedTransaction({
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await testClient.sendUnsignedTransaction({
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await testClient.sendUnsignedTransaction({
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### value (optional)

*   **Type:** `number`

Value in wei sent with this transaction.

    const hash = await testClient.sendUnsignedTransaction({
      from: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
      nonce: 69
    })</content>
</page>

<page>
  <title>toAccount</title>
  <url>https://viem.sh/docs/accounts/local/toAccount</url>
  <content>Creates an Account from a custom signing implementation

Import
------

    import { toAccount } from 'viem/accounts'

Usage
-----

    import { 
      signMessage, 
      signTransaction, 
      signTypedData, 
      privateKeyToAddress,
      toAccount 
    } from 'viem/accounts'
     
    const privateKey = '0x...'
     
    const account = toAccount({ 
      address: getAddress(privateKey),
     
      async signMessage({ message }) {
        return signMessage({ message, privateKey })
      },
     
      async signTransaction(transaction, { serializer }) {
        return signTransaction({ privateKey, transaction, serializer })
      },
     
      async signTypedData(typedData) {
        return signTypedData({ ...typedData, privateKey })
      },
    })

Parameters
----------

### address

*   **Type:** `Address`

The Address of the Account.

    const account = toAccount({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48', 
      async signMessage({ message }) {
        return signMessage({ message, privateKey })
      },
      async signTransaction(transaction, { serializer }) {
        return signTransaction({ privateKey, transaction, serializer })
      },
      async signTypedData(typedData) {
        return signTypedData({ ...typedData, privateKey })
      },
    })

### signMessage

Function to sign a message in [EIP-191 format](https://eips.ethereum.org/EIPS/eip-191).

    const account = toAccount({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
     
      async signMessage({ message }) { 
        return signMessage({ message, privateKey })
      },
      async signTransaction(transaction, { serializer }) {
        return signTransaction({ privateKey, transaction, serializer })
      },
      async signTypedData(typedData) {
        return signTypedData({ ...typedData, privateKey })
      },
    })

### signTransaction

Function to sign a transaction.

    const account = toAccount({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      async signMessage({ message }) {
        return signMessage({ message, privateKey })
      },
      async signTransaction(transaction, { serializer }) {  
        return signTransaction({ privateKey, transaction, serializer })
      },
      async signTypedData(typedData) {
        return signTypedData({ ...typedData, privateKey })
      },
    })

### signTypedData

Function to sign [EIP-712](https://eips.ethereum.org/EIPS/eip-712) typed data.

    const account = toAccount({
      address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
      async signMessage({ message }) {
        return signMessage({ message, privateKey })
      },
      async signTransaction(transaction, { serializer }) {
        return signTransaction({ privateKey, transaction, serializer })
      },
      async signTypedData(typedData) {  
        return signTypedData({ ...typedData, privateKey })
      },
    })</content>
</page>

<page>
  <title>Local Accounts (Private Key, Mnemonic, etc)</title>
  <url>https://viem.sh/docs/accounts/local</url>
  <content>A Local Account is an Account whose signing keys are stored on the consuming user's machine. It performs signing of transactions & messages with a private key **before** broadcasting the transaction or message over JSON-RPC.

There are three types of Local Accounts in viem:

*   [Private Key Account](https://viem.sh/docs/accounts/local/privateKeyToAccount)
*   [Mnemonic Account](https://viem.sh/docs/accounts/local/mnemonicToAccount)
*   [Hierarchical Deterministic (HD) Account](https://viem.sh/docs/accounts/local/hdKeyToAccount)

Instantiation
-------------

### 1\. Initialize a Wallet Client

Before we set up our Account and start consuming Wallet Actions, we will need to set up our Wallet Client with the [`http` Transport](https://viem.sh/docs/clients/transports/http):

    import { createWalletClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: http()
    })

### 2\. Set up your Local Account

Next, we will instantiate a Private Key Account using `privateKeyToAccount`:

    import { createWalletClient, http } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: http()
    })
     
    const account = privateKeyToAccount('0x...') 

### 3\. Consume [Wallet Actions](https://viem.sh/docs/actions/wallet/introduction)

Now you can use that Account within Wallet Actions that need a signature from the user:

    import { createWalletClient, http, parseEther } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const client = createWalletClient({
      chain: mainnet,
      transport: http()
    })
     
    const account = privateKeyToAccount('0x...')
     
    const hash = await client.sendTransaction({ 
      account,
      to: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: parseEther('0.001')
    })

### 4\. Optional: Hoist the Account

If you do not wish to pass an account around to every Action that requires an `account`, you can also hoist the account into the Wallet Client.

    import { createWalletClient, http, parseEther } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const account = privateKeyToAccount('0x...')
     
    const client = createWalletClient({ 
      account, 
      chain: mainnet,
      transport: http()
    })
     
    const hash = await client.sendTransaction({
      account, 
      to: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
      value: parseEther('0.001')
    })

### 5\. Optional: Extend with Public Actions

When using a Local Account, you may be finding yourself using a [Public Client](https://viem.sh/docs/clients/public) instantiated with the same parameters (`transport`, `chain`, etc) as your Wallet Client.

In this case, you can extend your Wallet Client with [Public Actions](https://viem.sh/docs/actions/public/introduction) to avoid having to handle multiple Clients.

    import { createWalletClient, http, publicActions } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
    import { mainnet } from 'viem/chains'
     
    const account = privateKeyToAccount('0x...')
     
    const client = createWalletClient({
      account,
      chain: mainnet,
      transport: http()
    }).extend(publicActions) 
     
    const { request } = await client.simulateContract({ ... }) // Public Action
    const hash = await client.writeContract(request) // Wallet Action</content>
</page>

<page>
  <title>signTransaction (Local Account)</title>
  <url>https://viem.sh/docs/accounts/local/signTransaction</url>
  <content>Signs a transaction with the Account's private key.

Usage
-----

    import { parseGwei } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
     
    const account = privateKeyToAccount('0x...')
     
    const signature = await account.signTransaction({
      chainId: 1,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('3'),
      gas: 21000n,
      nonce: 69,
      to: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    })
    Output: "0x02f850018203118080825208808080c080a04012522854168b27e5dc3d5839bab5e6b39e1a0ffd343901ce1622e3d64b48f1a04e00902ae0502c4728cbf12156290df99c3ed7de85b1dbfe20b5c36931733a33"

### Custom serializer

viem has a built-in serializer for **Legacy**, **EIP-2930** (`0x01`) and **EIP-1559** (`0x02`) transaction types. If you would like to serialize on another transaction type that viem does not support internally, you can pass a custom serializer.

    import { parseGwei } from 'viem'
    import { privateKeyToAccount } from 'viem/accounts'
     
    const account = privateKeyToAccount('0x...')
     
    const signature = await account.signTransaction({
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('3'),
      gas: 21000n,
      nonce: 69,
      to: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
    }, {
      serializer(transaction) { 
        const {
          chainId,
          nonce,
          // ...
        } = transaction
     
        return concatHex([
          '0x69',
          toRlp([
            toHex(chainId),
            nonce ? toHex(nonce) : '0x',
            // ...
          ]),
        ])
      }
    })

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#Hex)

The signed transaction.

Parameters
----------

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const signature = await account.signTransaction({
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      chainId: 1,
    })

### authorizationList (optional)

*   **Type:** `AuthorizationList`

Signed EIP-7702 Authorization list.

    const authorization = await account.signAuthorization({
      contractAddress: '0x...',
      chainId: 1,
      nonce: 1,
    })
     
    const signature = await account.signTransaction({
      authorizationList: [authorization], 
      chainId: 1,
    })

### blobs (optional)

*   **Type:** `Hex[]`

Blobs for [Blob Transactions](https://viem.sh/docs/guides/blob-transactions).

    import * as cKzg from 'c-kzg'
    import { toBlobs, setupKzg, stringToHex } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const hash = await account.signTransaction({
      blobs: toBlobs({ data: stringToHex('blobby blob!') }), 
      kzg,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### chainId (optional)

*   **Type:** `number`

The chain ID.

    const signature = await account.signTransaction({
      chainId: 1, 
    })

### data (optional)

*   **Type:** `0x${string}`

Transaction data.

    const signature = await account.signTransaction({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2'
    })

### gas (optional)

*   **Type:** `bigint`

The gas limit for the transaction.

    const signature = await account.signTransaction({
      gas: 69420n, 
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const signature = await account.signTransaction({
      gasPrice: parseGwei('20'), 
    })

### kzg (optional)

*   **Type:** `KZG`

KZG implementation for [Blob Transactions](https://viem.sh/docs/guides/blob-transactions).

See [`setupKzg`](https://viem.sh/docs/utilities/setupKzg) for more information.

    import * as cKzg from 'c-kzg'
    import { toBlobs, setupKzg, stringToHex } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const signature = await account.signTransaction({
      blobs: toBlobs({ data: stringToHex('blobby blob!') }), 
      kzg, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8'
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const signature = await account.signTransaction({
      chainId: 1,
      maxFeePerGas: parseGwei('20'), 
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const signature = await account.signTransaction({
      chainId: 1,
      maxPriorityFeePerGas: parseGwei('3'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const signature = await account.signTransaction({
      nonce: 69
    })

### to (optional)

*   **Type:** `Address`

The transaction recipient.

    const signature = await account.signTransaction({
      to: '0x...'
    })

### type (optional)

*   **Type:** `"legacy" | "eip2930" | "eip1559"`

The transaction type.

    const signature = await account.signTransaction({
      type: 'eip1559'
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    const signature = await account.signTransaction({
      value: parseEther('1'), 
    })</content>
</page>

<page>
  <title>formatEther</title>
  <url>https://viem.sh/docs/utilities/formatEther</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/formatEther#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Converts numerical wei to a string representation of ether.

Import
------

    import { formatEther } from 'viem'

Usage
-----

    import { formatEther } from 'viem'
     
    formatEther(1000000000000000000n) 
    // '1'

Returns
-------

`string`

Parameters
----------

### value

*   **Type:** `bigint`

The wei value.</content>
</page>

<page>
  <title>signTypedData (Local Account)</title>
  <url>https://viem.sh/docs/accounts/local/signTypedData</url>
  <content>Signs typed data with the Account's private key.

Signs typed data and calculates an Ethereum-specific signature in [https://eips.ethereum.org/EIPS/eip-712](https://eips.ethereum.org/EIPS/eip-712): `sign(keccak256("\x19\x01" ‖ domainSeparator ‖ hashStruct(message)))`

Usage
-----

    import { privateKeyToAccount } from 'viem/accounts'
    import { domain, types } from './data'
     
    const account = privateKeyToAccount('0x...')
     
    const signature = await account.signTypedData({
      domain,
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

Returns
-------

`0x${string}`

The signed data.

Parameters
----------

### domain

**Type:** `TypedDataDomain`

The typed data domain.

    const signature = await account.signTypedData({
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### types

The type definitions for the typed data.

    const signature = await account.signTypedData({
      domain,
      types: { 
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### primaryType

**Type:** Inferred `string`.

The primary type to extract from `types` and use in `value`.

    const signature = await account.signTypedData({
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [ 
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### message

**Type:** Inferred from `types` & `primaryType`.

    const signature = await account.signTypedData({
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: { 
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })</content>
</page>

<page>
  <title>Errors</title>
  <url>https://viem.sh/docs/glossary/errors</url>
  <content>All errors in viem extend the [`BaseError`](https://github.com/wevm/viem/blob/main/src/errors/base.ts).

ABI
---

### `AbiConstructorNotFoundError`

### `AbiConstructorParamsNotFoundError`

### `AbiDecodingDataSizeInvalidError`

### `AbiDecodingDataSizeTooSmallError`

### `AbiDecodingZeroDataError`

### `AbiEncodingArrayLengthMismatchError`

### `AbiEncodingBytesSizeMismatchError`

### `AbiEncodingLengthMismatchError`

### `AbiErrorInputsNotFoundError`

### `AbiErrorNotFoundError`

### `AbiErrorSignatureNotFoundError`

### `AbiEventNotFoundError`

### `AbiEventSignatureEmptyTopicsError`

### `AbiEventSignatureNotFoundError`

### `AbiFunctionNotFoundError`

### `AbiFunctionOutputsNotFoundError`

### `AbiFunctionSignatureNotFoundError`

### `BytesSizeMismatchError`

### `DecodeLogTopicsMismatch`

### `InvalidAbiDecodingTypeError`

### `InvalidAbiEncodingTypeError`

### `InvalidArrayError`

### `InvalidDefinitionTypeError`

### `UnsupportedPackedAbiType`

Account
-------

### `AccountNotFoundError`

When no account is provided to an action that requires an account.

Address
-------

### `InvalidAddressError`

When address is invalid.

Block
-----

### `BlockNotFoundError`

Chain
-----

### `ChainDoesNotSupportContract`

### `ChainMismatchError`

### `ChainNotFoundError`

### `ClientChainNotConfiguredError`

### `InvalidChainIdError`

Contract
--------

### `CallExecutionError`

### `ContractFunctionExecutionError`

### `ContractFunctionRevertedError`

### `ContractFunctionZeroDataError`

### `RawContractError`

Data
----

### `SizeExceedsPaddingSizeError`

Encoding
--------

### `DataLengthTooLongError`

### `DataLengthTooShortError`

### `IntegerOutOfRangeError`

### `InvalidBytesBooleanError`

### `InvalidHexBooleanError`

### `InvalidHexValueError`

### `OffsetOutOfBoundsError`

### `SizeOverflowError`

ENS
---

### `EnsAvatarInvalidMetadataError`

### `EnsAvatarInvalidNftUriError`

### `EnsAvatarUnsupportedNamespaceError`

### `EnsAvatarUriResolutionError`

Estimate Gas
------------

### `EstimateGasExecutionError`

Log
---

### `FilterTypeNotSupportedError`

Node
----

### `ExecutionRevertedError`

### `FeeCapTooHighError`

### `FeeCapTooLowError`

### `InsufficientFundsError`

### `IntrinsicGasTooHighError`

### `IntrinsicGasTooLowError`

### `NonceMaxValueError`

### `NonceTooHighError`

### `NonceTooLowError`

### `TipAboveFeeCapError`

### `TransactionTypeNotSupportedError`

### `UnknownNodeError`

Request
-------

### `HttpRequestError`

### `RpcRequestError`

### `TimeoutError`

### `WebSocketRequestError`

RPC
---

### `ChainDisconnectedError`

### `InternalRpcError`

### `InvalidInputRpcError`

### `InvalidParamsRpcError`

### `InvalidRequestRpcError`

### `JsonRpcVersionUnsupportedError`

### `LimitExceededRpcError`

### `MethodNotFoundRpcError`

### `MethodNotSupportedRpcError`

### `ParseRpcError`

### `ProviderDisconnectedError`

### `ProviderRpcError`

### `ResourceNotFoundRpcError`

### `ResourceUnavailableRpcError`

### `RpcError`

### `SwitchChainError`

### `TransactionRejectedRpcError`

### `UnauthorizedProviderError`

### `UnknownRpcError`

### `UnsupportedProviderMethodError`

### `UserRejectedRequestError`

SIWE
----

### CreateSiweMessageErrorType

### SiweInvalidMessageFieldErrorType

### VerifySiweMessageErrorType

Transaction
-----------

### `FeeConflictError`

### `InvalidLegacyVError`

### `InvalidSerializableTransactionError`

### `InvalidSerializedTransactionError`

### `InvalidSerializedTransactionTypeError`

### `InvalidStorageKeySizeError`

### `TransactionExecutionError`

### `TransactionNotFoundError`

### `TransactionReceiptNotFoundError`

### `WaitForTransactionReceiptTimeoutError`

Transport
---------

### `UrlRequiredError`</content>
</page>

<page>
  <title>Chains</title>
  <url>https://viem.sh/op-stack/chains</url>
  <content>The following Viem chains are implemented on the OP Stack:

    import {
      base, 
      baseGoerli, 
      baseSepolia, 
      fraxtal, 
      fraxtalTestnet, 
      ink, 
      inkSepolia, 
      optimism, 
      optimismGoerli, 
      optimismSepolia, 
      soneium, 
      soneiumMinato, 
      unichain, 
      unichainSepolia, 
      zircuit, 
      zircuitTestnet, 
      zora, 
      zoraSepolia, 
      zoraTestnet, 
    } from 'viem/chains'

Configuration
-------------

Viem exports OP Stack's chain [formatters](https://viem.sh/docs/chains/formatters) & [serializers](https://viem.sh/docs/chains/serializers) via `chainConfig`. This is useful if you need to define another chain which is implemented on the OP Stack.

    import { defineChain } from 'viem'
    import { chainConfig } from 'viem/op-stack'
     
    export const opStackExample = defineChain({
      ...chainConfig,
      name: 'OP Stack Example',
      // ...
    })</content>
</page>

<page>
  <title>setupKzg</title>
  <url>https://viem.sh/docs/utilities/setupKzg</url>
  <content>Sets up and defines a [EIP-4844](https://eips.ethereum.org/EIPS/eip-4844) compatible [KZG interface](https://notes.ethereum.org/@vbuterin/proto_danksharding_faq#How-%E2%80%9Ccomplicated%E2%80%9D-and-%E2%80%9Cnew%E2%80%9D-is-KZG). The KZG interface is used in the blob transaction signing process to generate KZG commitments & proofs.

`setupKzg` accepts a KZG interface that implements three functions:

*   `loadTrustedSetup`: A function to initialize the KZG trusted setup.
*   `blobToKzgCommitment`: A function that takes a blob and returns it's KZG commitment.
*   `computeBlobKzgProof`: A function that takes a blob and it's commitment, and returns the KZG proof.

A couple of KZG implementations we recommend are:

*   [c-kzg](https://github.com/ethereum/c-kzg-4844): Node.js bindings to c-kzg.
*   [kzg-wasm](https://github.com/ethereumjs/kzg-wasm): WebAssembly bindings to c-kzg.

Import
------

    import { setupKzg } from 'viem'

Usage
-----

    import * as cKzg from 'c-kzg'
    import { setupKzg } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath)

### Trusted Setups

As seen above, when you set up your KZG interface, you will need to provide a trusted setup file. You can either import a trusted setup via the [`viem/node` entrypoint](https://viem.sh/docs/utilities/setupKzg#viemnode-entrypoint) (if you're using an engine that supports Node.js' `node:fs` module), or you can directly import the trusted setup `.json` via the [`viem/trusted-setups` entrypoint](https://viem.sh/docs/utilities/setupKzg#viemtrusted-setups-entrypoint).

Viem exports the following trusted setups:

*   `mainnet.json`: For Ethereum Mainnet & it's Testnets (Sepolia, Goerli, etc).
*   `minimal.json`: For low-resource local dev testnets, and spec-testing.

The trusted setup files are retrieved from the Ethereum [consensus-specs repository](https://github.com/ethereum/consensus-specs/tree/dev/presets).

#### `viem/node` Entrypoint

Viem exports **paths to the trusted setup** via the `viem/node` entrypoint, designed to be used with `setupKzg`.

    import {
      mainnetTrustedSetupPath,
      minimalTrustedSetupPath,
    } from 'viem/node'

#### `viem/trusted-setups` Entrypoint

Alternatively, you can directly import the **contents of the trusted setup** file from the `viem/trusted-setups` entrypoint.

    import mainnetTrustedSetup from 'viem/trusted-setups/mainnet.json'
    import minimalTrustedSetup from 'viem/trusted-setups/minimal.json'

Returns
-------

`Kzg`

The KZG interface.

Parameters
----------

### kzg

*   **Type:** `Kzg & { loadTrustedSetup(path: string): void }`

The [EIP-4844](https://eips.ethereum.org/EIPS/eip-4844) compatible [KZG interface](https://notes.ethereum.org/@vbuterin/proto_danksharding_faq#How-%E2%80%9Ccomplicated%E2%80%9D-and-%E2%80%9Cnew%E2%80%9D-is-KZG).

    import * as cKzg from 'c-kzg'
    import { setupKzg } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(
      cKzg, 
      mainnetTrustedSetupPath
    )

### path

*   **Type:** `string`

The path to the trusted setup file.

    import * as cKzg from 'c-kzg'
    import { setupKzg } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(
      cKzg, 
      mainnetTrustedSetupPath 
    )</content>
</page>

<page>
  <title>Client</title>
  <url>https://viem.sh/op-stack/client</url>
  <content>To use the OP Stack functionality of Viem, you must extend your existing (or new) Viem Client with OP Stack Actions.

Usage
-----

### Layer 1 Extensions

    import { createPublicClient, createWalletClient, http } from 'viem'
    import { mainnet } from 'viem/chains'
    import { walletActionsL1 } from 'viem/op-stack'
     
    const walletClient = createWalletClient({
      chain: mainnet,
      transport: http(),
    }).extend(walletActionsL1()) 
     
    const hash = await walletClient.depositTransaction({/* ... */})

### Layer 2 Extensions

    import { createPublicClient, http } from 'viem'
    import { base } from 'viem/chains'
    import { publicActionsL2 } from 'viem/op-stack'
     
    const publicClient = createPublicClient({
      chain: base,
      transport: http(),
    }).extend(publicActionsL2()) 
     
    const l1Gas = await publicClient.estimateL1Gas({/* ... */})

Extensions
----------

### `walletActionsL1`

A suite of [Wallet Actions](https://viem.sh/op-stack/actions/estimateL1Gas) for suited for development with **Layer 1** chains that interact with **Layer 2 (OP Stack)** chains.

    import { walletActionsL1 } from 'viem/op-stack'

### `publicActionsL1`

A suite of [Public Actions](https://viem.sh/op-stack/actions/getTimeToProve) suited for development with **Layer 1** chains. These actions provide functionalities specific to public clients operating at the Layer 1 level, enabling them to interact seamlessly with Layer 2 protocols.

    import { publicActionsL1 } from 'viem/op-stack'

### `walletActionsL2`

A suite of [Wallet Actions](https://viem.sh/op-stack/actions/estimateL1Fee) suited for development with **Layer 2 (OP Stack)** chains. These actions are tailored for wallets operating on Layer 2, providing advanced features and integrations necessary for Layer 2 financial operations.

    import { walletActionsL2 } from 'viem/op-stack'

### `publicActionsL2`

A suite of [Public Actions](https://viem.sh/op-stack/actions/estimateL1Gas) for suited for development with **Layer 2 (OP Stack)** chains.

    import { publicActionsL2 } from 'viem/op-stack'</content>
</page>

<page>
  <title>verifyMessage</title>
  <url>https://viem.sh/docs/utilities/verifyMessage</url>
  <content>Verify that a message was signed by the provided address.

Usage
-----

    import { verifyMessage } from 'viem'
    import { account, walletClient } from './client'
     
    const signature = await walletClient.signMessage({
      account,
      message: 'hello world',
    })
     
    const valid = await verifyMessage({ 
      address: account.address,
      message: 'hello world',
      signature,
    })
    // true

Returns
-------

`boolean`

Whether the provided `address` generated the `signature`.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The Ethereum address that signed the original message.

    const valid = await verifyMessage({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      message: 'hello world',
      signature:
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })

### message

*   **Type:** `string`

The message to be verified.

By default, viem signs the UTF-8 representation of the message.

    const valid = await verifyMessage({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      message: 'hello world', 
      signature:
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })

To sign the data representation of the message, you can use the `raw` attribute.

    const valid = await verifyMessage({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      message: { raw: '0x68656c6c6f20776f726c64' }, 
      signature:
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })

### signature

*   **Type:** `Hex | ByteArray | Signature`

The signature that was generated by signing the message with the address's private key.

    const valid = await verifyMessage({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      message: 'hello world',
      signature: 
        '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c',
    })</content>
</page>

<page>
  <title>verifyTypedData</title>
  <url>https://viem.sh/docs/utilities/verifyTypedData</url>
  <content>Verify that typed data was signed by the provided address.

Usage
-----

    import { verifyTypedData } from 'viem'
    import { account, walletClient } from './client'
     
    const message = {
      from: {
        name: 'Cow',
        wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
      },
      to: {
        name: 'Bob',
        wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
      },
      contents: 'Hello, Bob!',
    } as const
     
    const signature = await walletClient.signTypedData({
      account,
      domain,
      types,
      primaryType: 'Mail',
      message,
    })
    
    const valid = await verifyTypedData({
      address: account.address,
      domain,
      types,
      primaryType: 'Mail',
      message,
      signature,
    })
    // true

Returns
-------

`boolean`

Whether the provided `address` generated the `signature`.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The Ethereum address that signed the original message.

    const valid = await verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### domain

**Type:** `TypedDataDomain`

The typed data domain.

    const valid = await verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### types

The type definitions for the typed data.

    const valid = await verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain,
      types: { 
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### primaryType

**Type:** Inferred `string`.

The primary type to extract from `types` and use in `value`.

    const valid = await verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [ 
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### message

**Type:** Inferred from `types` & `primaryType`.

    const valid = await verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: { 
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### signature

*   **Type:** `Hex | ByteArray | Signature`

The signature of the typed data.

    const valid = await verifyTypedData({
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...', 
    })

### blockNumber (optional)

*   **Type:** `bigint`

Only used when verifying a typed data that was signed by a Smart Contract Account. The block number to check if the contract was already deployed.

    const valid = await verifyTypedData({
      blockNumber: 42069n, 
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

### blockTag (optional)

*   **Type:** `'latest' | 'earliest' | 'pending' | 'safe' | 'finalized'`
*   **Default:** `'latest'`

Only used when verifying a typed data that was signed by a Smart Contract Account. The block tag to check if the contract was already deployed.

    const valid = await verifyTypedData({
      blockNumber: 42069n, 
      address: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...',
    })

JSON-RPC Method
---------------

[`eth_call`](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_call) to a deployless [universal signature validator contract](https://eips.ethereum.org/EIPS/eip-6492).</content>
</page>

<page>
  <title>Viem</title>
  <url>https://viem.sh/op-stack/guides/withdrawals</url>
  <content>This guide will demonstrate how to withdraw **1 Ether** from **[Optimism (OP Mainnet)](https://www.optimism.io/)** to **Mainnet**.

Overview
--------

Withdrawals on the OP Stack are a [two-step (plus one) process](https://blog.oplabs.co/two-step-withdrawals/). The process involves:

0.  **Initiating** the Withdrawal Transaction on the L2,

> _Wait one hour (max) for the L2 Output containing the transaction to be proposed._

1.  **Proving** the Withdrawal Transaction on the L1,

> _Wait the 7 day finalization period_

2.  **Finalizing** the Withdrawal Transaction on the L1.

> _Withdrawal complete!_

Here is a complete end-to-end overview of how to execute a withdrawal. Don't worry, we will break it down into [Steps](https://viem.sh/op-stack/guides/withdrawals#steps) below.

    import { getWithdrawals } from 'viem/op-stack'
    import { 
      account, 
      publicClientL1, 
      walletClientL1,
      publicClientL2, 
      walletClientL2 
    } from './config'
     
    // Build parameters to initiate the withdrawal transaction on the L1.
    const args = await publicClientL1.buildInitiateWithdrawal({
      to: account.address,
      value: parseEther('1')
    })
     
    // Execute the initiate withdrawal transaction on the L2.
    const hash = await walletClientL2.initiateWithdrawal(args)
     
    // Wait for the initiate withdrawal transaction receipt.
    const receipt = await publicClientL2.waitForTransactionReceipt({ hash })
     
    // Wait until the withdrawal is ready to prove.
    const { output, withdrawal } = await publicClientL1.waitToProve({
      receipt,
      targetChain: walletClientL2.chain
    })
     
    // Build parameters to prove the withdrawal on the L2.
    const proveArgs = await publicClientL2.buildProveWithdrawal({
      output,
      withdrawal,
    })
     
    // Prove the withdrawal on the L1.
    const proveHash = await walletClientL1.proveWithdrawal(proveArgs)
     
    // Wait until the prove withdrawal is processed.
    const proveReceipt = await publicClientL1.waitForTransactionReceipt({
      hash: proveHash
    })
     
    // Wait until the withdrawal is ready to finalize.
    await publicClientL1.waitToFinalize({
      targetChain: walletClientL2.chain,
      withdrawalHash: withdrawal.withdrawalHash,
    })
     
    // Finalize the withdrawal.
    const finalizeHash = await walletClientL1.finalizeWithdrawal({
      targetChain: walletClientL2.chain,
      withdrawal,
    })
     
    // Wait until the withdrawal is finalized.
    const finalizeReceipt = await publicClientL1.waitForTransactionReceipt({
      hash: finalizeHash
    })

Steps
-----

### 1\. Set up Viem Clients

First, we will set up our Viem Clients for the Mainnet and Optimism chains, including the necessary extensions for the OP Stack.

We will need the following clients:

*   `publicClientL1`/`walletClientL1`: Public & Wallet Client for **Mainnet**
*   `publicClientL2`/`walletClientL2`: Public & Wallet Client for **OP Mainnet**

We will place these in a `config.ts` file.

File

config.ts (JSON-RPC Account)

    // Import Viem modules.
    import { createPublicClient, createWalletClient, custom, http } from 'viem'
    import { mainnet, optimism } from 'viem/chains'
    import { publicActionsL1, walletActionsL1, walletActionsL2 } from 'viem/op-stack'
     
    // Retrieve Account from an EIP-1193 Provider. 
    export const [account] = await window.ethereum.request({ 
      method: 'eth_requestAccounts' 
    }) 
     
    export const publicClientL1 = createPublicClient({
      chain: mainnet,
      transport: http()
    }).extend(publicActionsL1())
     
    export const walletClientL1 = createWalletClient({
      account,
      chain: mainnet,
      transport: custom(window.ethereum)
    }).extend(walletActionsL1())
     
    export const publicClientL2 = createPublicClient({
      chain: optimism,
      transport: http()
    }).extend(publicActionsL2())
     
    export const walletClientL2 = createWalletClient({
      account,
      chain: optimism,
      transport: custom(window.ethereum)
    }).extend(walletActionsL2())

### 2\. Initiate Withdrawal

Next, we will initiate the withdrawal transaction on the L2 by building the parameters on the L1 (1), and then executing the transaction on the L2 (2). We also want to wait for the L2 transaction to be processed on a block (3) before we continue.

In the example below, we are initiating a withdrawal for **1 Ether** from the L2 (OP Mainnet) to the L1 (Mainnet).

    import { 
      account, 
      publicClientL1,
      publicClientL2, 
      walletClientL2 
    } from './config'
     
    // 1. Build parameters to initiate the withdrawal transaction on the L1.
    const args = await publicClientL1.buildInitiateWithdrawal({
      to: account.address,
      value: parseEther('1')
    })
     
    // 2. Execute the initiate withdrawal transaction on the L2.
    const hash = await walletClientL2.initiateWithdrawal(args)
     
    // 3. Wait for the initiate withdrawal transaction receipt.
    const receipt = await publicClientL2.waitForTransactionReceipt({ hash })

### 3\. Prove Withdrawal

After the initiate withdrawal transaction has been processed on a block on the L2, we will then need to prove that withdrawal on the L1.

Before a withdrawal transaction can be proved, the transaction needs to be included in an L2 Output proposal. Until then, we will need to wait for the withdrawal transaction to be ready to be proved (1). This usually takes a maximum of **one hour**.

Once the L2 output has been proposed, we will need to build the parameters for the prove withdrawal transaction on the L2 (2), and then execute the transaction on the L1 (3). We also want to wait for the L1 transaction to be processed on a block (4) before we continue.

    import { 
      account, 
      publicClientL1,
      publicClientL2, 
      walletClientL1,
      walletClientL2 
    } from './config'
     
    // (Shortcut) Get receipt from transaction created in Step 1.
    const receipt = 
      await publicClientL2.getTransactionReceipt({ hash: '0x...' })
     
    // 1. Wait until the withdrawal is ready to prove. 
    const { output, withdrawal } = await publicClientL1.waitToProve({ 
      receipt, 
      targetChain: walletClientL2.chain 
    }) 
     
    // 2. Build parameters to prove the withdrawal on the L2. 
    const args = await publicClientL2.buildProveWithdrawal({ 
      output, 
      withdrawal, 
    }) 
     
    // 3. Prove the withdrawal on the L1. 
    const hash = await walletClientL1.proveWithdrawal(args) 
     
    // 4. Wait until the prove withdrawal is processed. 
    const receipt = await publicClientL1.waitForTransactionReceipt({ 
      hash 
    }) 

### 4\. Finalize Withdrawal

When the withdrawal transaction has been proved, we will then need to finalize that withdrawal on the L1.

Before a withdrawal transaction can be finalized, we will need to wait the **finalization period** of **7 days** (1).

After the finalization period has elapsed, we can finalize the withdrawal (2).

Once the withdrawal has been successfully finalized (3), then the withdrawal is complete! 🥳

    import { getWithdrawals } from 'viem/op-stack'
    import { 
      account, 
      publicClientL1,
      publicClientL2, 
      walletClientL1,
      walletClientL2 
    } from './config'
     
    // (Shortcut) Get receipt from transaction created in Step 1.
    const receipt = 
      await publicClientL2.getTransactionReceipt({ hash: '0x...' })
     
    // (Shortcut) Get withdrawals from receipt in Step 3.
    const [withdrawal] = getWithdrawals(receipt)
     
    // 1. Wait until the withdrawal is ready to finalize.  
    await publicClientL1.waitToFinalize({ 
      targetChain: walletClientL2.chain, 
      withdrawalHash: withdrawal.withdrawalHash, 
    }) 
     
    // 2. Finalize the withdrawal. 
    const hash = await walletClientL1.finalizeWithdrawal({ 
      targetChain: walletClientL2.chain, 
      withdrawal, 
    }) 
     
    // 3. Wait until the withdrawal is finalized. 
    const receipt = await publicClientL1.waitForTransactionReceipt({ 
      hash 
    })</content>
</page>

<page>
  <title>buildProveWithdrawal</title>
  <url>https://viem.sh/op-stack/actions/buildProveWithdrawal</url>
  <content>    import { account, publicClientL2, walletClientL1 } from './config'
     
    const receipt = await getTransactionReceipt(publicClientL2, {
      hash: '0xbbdd0957a82a057a76b5f093de251635ac4ddc6e2d0c4aa7fbf82d73e4e11039',
    })
     
    const [withdrawal] = getWithdrawals(receipt)
    const output = await walletClientL1.getL2Output({
      l2BlockNumber: receipt.blockNumber,
      targetChain: publicClientL2.chain,
    })
     
    const args = await publicClientL2.buildProveWithdrawal({ 
      account, 
      output, 
      withdrawal, 
    }) 
     
    const hash = await walletClientL1.proveWithdrawal(args)</content>
</page>

<page>
  <title>buildDepositTransaction</title>
  <url>https://viem.sh/op-stack/actions/buildDepositTransaction</url>
  <content>[Skip to content](https://viem.sh/op-stack/actions/buildDepositTransaction#vocs-content)

Builds & prepares parameters for a [deposit transaction](https://github.com/ethereum-optimism/optimism/blob/develop/specs/deposits.md) to be initiated on an L1 and executed on the L2.

Usage
-----

    import { account, publicClientL2, walletClientL1 } from './config'
     
    const args = await publicClientL2.buildDepositTransaction({ 
      account, 
      mint: parseEther('1'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
    }) 
     
    const hash = await walletClientL1.depositTransaction(args)

### Account Hoisting

If you do not wish to pass an `account` to every `buildDepositTransaction`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { publicClientL2, walletClientL1 } from './config'
     
    const args = await publicClientL2.buildDepositTransaction({
      mint: parseEther('1')
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })
     
    const hash = await walletClientL1.depositTransaction(args)

Returns
-------

`DepositTransactionParameters`

The parameters required to execute a [deposit transaction](https://viem.sh/op-stack/actions/depositTransaction).

Parameters
----------

### account (optional)

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const args = await client.buildDepositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### data (optional)

*   **Type:** `Hex`

Contract deployment bytecode or encoded contract method & arguments.

    const args = await client.buildDepositTransaction({
      data: '0x...', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### gas (optional)

*   **Type:** `bigint`

Gas limit for transaction execution on the L2.

    const args = await client.buildDepositTransaction({
      gas: 21_000n, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### isCreation (optional)

*   **Type:** `boolean`

Whether or not this is a contract deployment transaction.

    const args = await client.buildDepositTransaction({
      data: '0x...',
      isCreation: true
    })

### mint (optional)

*   **Type:** `bigint`

Value in wei to mint (deposit) on the L2. Debited from the caller's L1 balance.

    const args = await client.buildDepositTransaction({
      mint: parseEther('1') 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
    })

### to (optional)

*   **Type:** `Address`

L2 Transaction recipient.

    const args = await client.buildDepositTransaction({
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',  
      value: parseEther('1')
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction on the L2. Debited from the caller's L2 balance.

    const args = await client.buildDepositTransaction({
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>Viem</title>
  <url>https://viem.sh/op-stack/guides/deposits</url>
  <content>This guide will demonstrate how to deposit (bridge) **1 Ether** from **Mainnet** to **[Optimism (OP Mainnet)](https://www.optimism.io/)**.

Overview
--------

Here is an end-to-end overview of how to execute a deposit transaction. We will break it down into [Steps](https://viem.sh/op-stack/guides/deposits#steps) below.

    import { getL2TransactionHashes } from 'viem/op-stack'
    import { account, publicClientL1, publicClientL2, walletClientL1 } from './config'
     
    // Build parameters for the transaction on the L2.
    const args = await publicClientL2.buildDepositTransaction({
      mint: parseEther('1'),
      to: account.address,
    })
     
    // Execute the deposit transaction on the L1.
    const hash = await walletClientL1.depositTransaction(args)
     
    // Wait for the L1 transaction to be processed.
    const receipt = await publicClientL1.waitForTransactionReceipt({ hash })
     
    // Get the L2 transaction hash from the L1 transaction receipt.
    const [l2Hash] = getL2TransactionHashes(receipt)
     
    // Wait for the L2 transaction to be processed.
    const l2Receipt = await publicClientL2.waitForTransactionReceipt({ 
      hash: l2Hash 
    })

Steps
-----

### 1\. Set up Viem Clients

First, we will set up our Viem Clients for the Mainnet and Optimism chains, including the necessary extensions for the OP Stack.

We will place these in a `config.ts` file.

File

config.ts (JSON-RPC Account)

    // Import Viem modules.
    import { createPublicClient, createWalletClient, custom, http } from 'viem'
    import { mainnet, optimism } from 'viem/chains'
    import { publicActionsL2, walletActionsL1 } from 'viem/op-stack'
     
    // Retrieve Account from an EIP-1193 Provider. 
    export const [account] = await window.ethereum.request({ 
      method: 'eth_requestAccounts' 
    }) 
     
    export const publicClientL1 = createPublicClient({
      chain: mainnet,
      transport: http()
    })
     
    export const walletClientL1 = createWalletClient({
      account,
      chain: mainnet,
      transport: custom(window.ethereum)
    }).extend(walletActionsL1())
     
    export const publicClientL2 = createPublicClient({
      chain: optimism,
      transport: http()
    }).extend(publicActionsL2())

### 2\. Build the Deposit Transaction

Next, we will build the deposit transaction on the Optimism (L2) chain using the Clients that we created in the previous step.

In the example below, we want to deposit **1 Ether** (via `mint`) onto the Optimism chain, to ourselves (`account.address`).

    // Import Viem Clients.
    import { publicClientL2 } from './config'
     
    // Build parameters for the transaction on the L2.
    const args = await publicClientL2.buildDepositTransaction({
      mint: parseEther('1'),
      to: account.address,
    })

### 3\. Execute the Deposit Transaction

After that, we will execute the deposit transaction on the Mainnet (L1) chain.

    // Import Viem Clients.
    import { account, publicClientL2, walletClientL1 } from './config'
     
    // Build parameters for the transaction on the L2.
    const args = await publicClientL2.buildDepositTransaction({
      mint: parseEther('1'),
      to: account.address,
    })
     
    // Execute the deposit transaction on the L1. 
    const hash = await walletClientL1.depositTransaction(args) 

### 4\. Wait for Transaction to be Processed

Once we have broadcast the transaction to the Mainnet (L1) chain, we need to wait for it to be processed on a block so we can extract the transaction receipt. We will need the transaction receipt to extract the transaction on the Optimism (L2) chain.

    // Import Viem Clients.
    import { 
      account, 
      publicClientL1, 
      publicClientL2,
      walletClientL1 
    } from './config'
     
    // Build parameters for the transaction on the L2.
    const args = await publicClientL2.buildDepositTransaction({
      mint: parseEther('1'),
      to: account.address,
    })
     
    // Execute the deposit transaction on the L1. 
    const hash = await walletClientL1.depositTransaction(args) 
     
    // Wait for the L1 transaction to be processed. 
    const receipt = await publicClientL1.waitForTransactionReceipt({ hash }) 

### 5\. Compute the L2 Transaction Hash

Once we have the transaction receipt from the Mainnet (L1) chain, we can extract the Optimism (L2) transaction hash from the logs in the transaction receipt.

    // Import Viem Clients.
    import { 
      account, 
      publicClientL1, 
      publicClientL2,
      walletClientL1 
    } from './config'
     
    // Build parameters for the transaction on the L2.
    const args = await publicClientL2.buildDepositTransaction({
      mint: parseEther('1'),
      to: account.address,
    })
     
    // Execute the deposit transaction on the L1. 
    const hash = await walletClientL1.depositTransaction(args) 
     
    // Wait for the L1 transaction to be processed. 
    const receipt = await publicClientL1.waitForTransactionReceipt({ hash }) 
     
    // Get the L2 transaction hash from the L1 transaction receipt. 
    const [l2Hash] = getL2TransactionHashes(receipt) 

### 6\. Wait for Transaction to be Processed

Now that we have the Optimism (L2) transaction hash, we can wait for the transaction to be processed on the Optimism (L2) chain.

Once the `waitForTransactionReceipt` call resolves, the transaction has been processed and you should now be credited with 1 Ether on the Optimism (L2) chain 🥳.

    // Import Viem Clients.
    import { 
      account, 
      publicClientL1, 
      publicClientL2,
      walletClientL1 
    } from './config'
     
    // Build parameters for the transaction on the L2.
    const args = await publicClientL2.buildDepositTransaction({
      mint: parseEther('1'),
      to: account.address,
    })
     
    // Execute the deposit transaction on the L1. 
    const hash = await walletClientL1.depositTransaction(args) 
     
    // Wait for the L1 transaction to be processed. 
    const receipt = await publicClientL1.waitForTransactionReceipt({ hash }) 
     
    // Get the L2 transaction hash from the L1 transaction receipt. 
    const [l2Hash] = getL2TransactionHashes(receipt) 
     
    // Wait for the L2 transaction to be processed. 
    const l2Receipt = await publicClientL2.waitForTransactionReceipt({  
      hash: l2Hash  
    }) 

Example
-------</content>
</page>

<page>
  <title>estimateInitiateWithdrawalGas</title>
  <url>https://viem.sh/op-stack/actions/estimateInitiateWithdrawalGas</url>
  <content>Estimates gas required to initiate a [withdrawal](https://github.com/ethereum-optimism/optimism/blob/develop/specs/deposits.md) on an L2 to the L1.

Usage
-----

    import { base } from 'viem/chains'
    import { account, publicClientL2 } from './config'
     
    const gas = await publicClientL2.estimateInitiateWithdrawalGas({
      account,
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
    })

Returns
-------

`bigint`

Estimated gas required to initiate the withdrawal.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.data (optional)

*   **Type:** `Hex`

Encoded contract method & arguments.

    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        data: '0x...', 
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
    })

### args.gas

*   **Type:** `bigint`

Gas limit for transaction execution on the L1.

    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n, 
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
    })

### args.to

*   **Type:** `Address`

L1 Transaction recipient.

    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',  
        value: parseEther('1')
      },
    })

### args.value (optional)

*   **Type:** `bigint`

Value in wei to withdrawal from the L2 to the L1. Debited from the caller's L2 balance.

    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1') 
      },
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The L2 chain. If there is a mismatch between the wallet's current chain & this chain, an error will be thrown.

    import { optimism } from 'viem/chains'
     
    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      chain: optimism, 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      maxFeePerGas: parseGwei('20'), 
      maxPriorityFeePerGas: parseGwei('2'),  
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const gas = await client.estimateInitiateWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      nonce: 69, 
    })</content>
</page>

<page>
  <title>estimateContractL1Fee</title>
  <url>https://viem.sh/op-stack/actions/estimateContractL1Fee</url>
  <content>Estimates the [L1 data fee](https://docs.optimism.io/stack/transactions/fees#l1-data-fee) to execute an L2 contract write.

Invokes the `getL1Fee` method on the [Gas Price Oracle](https://github.com/ethereum-optimism/optimism/blob/233ede59d16cb01bdd8e7ff662a153a4c3178bdd/packages/contracts/contracts/L2/predeploys/OVM_GasPriceOracle.sol) predeploy contract.

Usage
-----

    import { account, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const l1Fee = await publicClient.estimateContractL1Fee({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })

Returns
-------

`bigint`

The L1 data fee estimate (in wei).

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate fee from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'mint',
    })

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint', 
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0x1dfe7ca09e99d10835bf73044a23b73fc20623df',
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'], 
    })

### gasPriceOracleAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Address of the Gas Price Oracle predeploy contract.

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      gasPriceOracleAddress: '0x420000000000000000000000000000000000000F', 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei).

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      maxPriorityFeePerGas: parseGwei('2'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      nonce: 69, 
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    const fee = await publicClient.estimateContractL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>estimateContractTotalGas</title>
  <url>https://viem.sh/op-stack/actions/estimateContractTotalGas</url>
  <content>Estimates the total ([L1 data](https://docs.optimism.io/stack/transactions/fees#l1-data-fee) + L2) gas to execute an L2 contract write.

Invokes the `getL1GasUsed` method on the [Gas Price Oracle](https://github.com/ethereum-optimism/optimism/blob/233ede59d16cb01bdd8e7ff662a153a4c3178bdd/packages/contracts/contracts/L2/predeploys/OVM_GasPriceOracle.sol) predeploy contract.

Usage
-----

    import { account, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const gas = await publicClient.estimateContractTotalGas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })

Returns
-------

`bigint`

The total (L1 data + L2) gas estimate.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate gas from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'mint',
    })

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint', 
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0x1dfe7ca09e99d10835bf73044a23b73fc20623df',
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'], 
    })

### gasPriceOracleAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Address of the Gas Price Oracle predeploy contract.

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      gasPriceOracleAddress: '0x420000000000000000000000000000000000000F', 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei).

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      maxPriorityFeePerGas: parseGwei('2'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const { result } = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      nonce: 69, 
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    const gas = await publicClient.estimateContractTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>estimateContractTotalFee</title>
  <url>https://viem.sh/op-stack/actions/estimateContractTotalFee</url>
  <content>Estimates the total ([L1 data](https://docs.optimism.io/stack/transactions/fees#l1-data-fee) + L2) fee to execute an L2 contract write.

Invokes the `getL1Fee` method on the [Gas Price Oracle](https://github.com/ethereum-optimism/optimism/blob/233ede59d16cb01bdd8e7ff662a153a4c3178bdd/packages/contracts/contracts/L2/predeploys/OVM_GasPriceOracle.sol) predeploy contract.

Usage
-----

    import { account, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const fee = await publicClient.estimateContractTotalFee({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })

Returns
-------

`bigint`

The total (L1 + L2) fee estimate (in wei).

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate fee from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'mint',
    })

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint', 
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0x1dfe7ca09e99d10835bf73044a23b73fc20623df',
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'], 
    })

### gasPriceOracleAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Address of the Gas Price Oracle predeploy contract.

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      gasPriceOracleAddress: '0x420000000000000000000000000000000000000F', 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei).

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      maxPriorityFeePerGas: parseGwei('2'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      nonce: 69, 
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    const fee = await publicClient.estimateContractTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>estimateContractL1Gas</title>
  <url>https://viem.sh/op-stack/actions/estimateContractL1Gas</url>
  <content>Estimates the [L1 data gas](https://docs.optimism.io/stack/transactions/fees#l1-data-fee) to execute an L2 contract write.

Invokes the `getL1GasUsed` method on the [Gas Price Oracle](https://github.com/ethereum-optimism/optimism/blob/233ede59d16cb01bdd8e7ff662a153a4c3178bdd/packages/contracts/contracts/L2/predeploys/OVM_GasPriceOracle.sol) predeploy contract.

Usage
-----

    import { account, publicClient } from './config'
    import { wagmiAbi } from './abi'
     
    const l1Fee = await publicClient.estimateContractL1Gas({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      account,
    })

Returns
-------

`bigint`

The L1 data gas estimate.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate gas from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'mint',
    })

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint', 
    })

### args (optional)

*   **Type:** Inferred from ABI.

Arguments to pass to function call.

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      address: '0x1dfe7ca09e99d10835bf73044a23b73fc20623df',
      abi: wagmiAbi,
      functionName: 'balanceOf',
      args: ['0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC'], 
    })

### gasPriceOracleAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Address of the Gas Price Oracle predeploy contract.

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      gasPriceOracleAddress: '0x420000000000000000000000000000000000000F', 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei).

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      maxPriorityFeePerGas: parseGwei('2'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const { result } = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      nonce: 69, 
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    const gas = await publicClient.estimateContractL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>estimateL1Fee</title>
  <url>https://viem.sh/op-stack/actions/estimateL1Fee</url>
  <content>Estimates the [L1 data fee](https://docs.optimism.io/stack/transactions/fees#l1-data-fee) to execute an L2 transaction.

Invokes the `getL1Fee` method on the [Gas Price Oracle](https://github.com/ethereum-optimism/optimism/blob/233ede59d16cb01bdd8e7ff662a153a4c3178bdd/packages/contracts/contracts/L2/predeploys/OVM_GasPriceOracle.sol) predeploy contract.

Usage
-----

    import { account, publicClient } from './config'
     
    const fee = await publicClient.estimateL1Fee({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

Returns
-------

`bigint`

The L1 data fee (in wei).

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate fee from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const fee = await publicClient.estimateL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### data (optional)

*   **Type:** `0x${string}`

Contract code or a hashed method call with encoded args.

    const fee = await publicClient.estimateL1Fee({
      data: '0x...', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### gasPriceOracleAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Address of the Gas Price Oracle predeploy contract.

    const fee = await publicClient.estimateL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      gasPriceOracleAddress: '0x420000000000000000000000000000000000000F', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const fee = await publicClient.estimateL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei).

    const fee = await publicClient.estimateL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const fee = await publicClient.estimateL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### to (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Transaction recipient.

    const fee = await publicClient.estimateL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1')
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    const fee = await publicClient.estimateL1Fee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>estimateTotalFee</title>
  <url>https://viem.sh/op-stack/actions/estimateTotalFee</url>
  <content>Estimates the [L1 data fee](https://docs.optimism.io/stack/transactions/fees#l1-data-fee) + L2 fee to execute an L2 transaction.

It is the sum of [`estimateL1Fee`](https://viem.sh/op-stack/actions/estimateL1Fee) (L1 Gas) and [`estimateGas`](https://viem.sh/docs/actions/public/estimateGas) \* [`getGasPrice`](https://viem.sh/docs/actions/public/getGasPrice) (L2 Gas \* L2 Gas Price).

Usage
-----

    import { account, publicClient } from './config'
     
    const fee = await publicClient.estimateTotalFee({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

Returns
-------

`bigint`

The L1 fee (in wei).

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate fee from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const fee = await publicClient.estimateTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### data (optional)

*   **Type:** `0x${string}`

Contract code or a hashed method call with encoded args.

    const fee = await publicClient.estimateTotalFee({
      data: '0x...', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### gasPriceOracleAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Address of the Gas Price Oracle predeploy contract.

    const fee = await publicClient.estimateTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      gasPriceOracleAddress: '0x420000000000000000000000000000000000000F', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const fee = await publicClient.estimateTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei).

    const fee = await publicClient.estimateTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const fee = await publicClient.estimateTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### to (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Transaction recipient.

    const fee = await publicClient.estimateTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1')
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    const fee = await publicClient.estimateTotalFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>estimateL1Gas</title>
  <url>https://viem.sh/op-stack/actions/estimateL1Gas</url>
  <content>Estimates the amount of [L1 data gas](https://docs.optimism.io/stack/transactions/fees#l1-data-fee) required to execute an L2 transaction.

Invokes the `getL1GasUsed` method on the [Gas Price Oracle](https://github.com/ethereum-optimism/optimism/blob/233ede59d16cb01bdd8e7ff662a153a4c3178bdd/packages/contracts/contracts/L2/predeploys/OVM_GasPriceOracle.sol) predeploy contract.

Usage
-----

    import { account, publicClient } from './config'
     
    const gas = await publicClient.estimateL1Gas({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

Returns
-------

`bigint`

The L1 data gas estimate.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate gas from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const gas = await publicClient.estimateL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### data (optional)

*   **Type:** `0x${string}`

Contract code or a hashed method call with encoded args.

    const gas = await publicClient.estimateL1Gas({
      data: '0x...', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### gasPriceOracleAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Address of the Gas Price Oracle predeploy contract.

    const gas = await publicClient.estimateL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      gasPriceOracleAddress: '0x420000000000000000000000000000000000000F', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const gas = await publicClient.estimateL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei).

    const gas = await publicClient.estimateL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const fee = await publicClient.estimateL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### to (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Transaction recipient.

    const gas = await publicClient.estimateL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1')
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    const gas = await publicClient.estimateL1Gas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>estimateTotalGas</title>
  <url>https://viem.sh/op-stack/actions/estimateTotalGas</url>
  <content>Estimates the amount of [L1 data gas](https://docs.optimism.io/stack/transactions/fees#l1-data-fee) + L2 gas required to execute an L2 transaction.

It is the sum of [`estimateL1Gas`](https://viem.sh/op-stack/actions/estimateL1Gas) (L1 Gas) and [`estimateGas`](https://viem.sh/docs/actions/public/estimateGas) (L2 Gas).

Usage
-----

    import { account, publicClient } from './config'
     
    const gas = await publicClient.estimateTotalGas({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

Returns
-------

`bigint`

The total (L1 + L2) gas estimate.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to estimate gas from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const gas = await publicClient.estimateTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### data (optional)

*   **Type:** `0x${string}`

Contract code or a hashed method call with encoded args.

    const gas = await publicClient.estimateTotalGas({
      data: '0x...', 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### gasPriceOracleAddress (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Address of the Gas Price Oracle predeploy contract.

    const gas = await publicClient.estimateTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      gasPriceOracleAddress: '0x420000000000000000000000000000000000000F', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const gas = await publicClient.estimateTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),  
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei).

    const gas = await publicClient.estimateTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const fee = await publicClient.estimateTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### to (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

Transaction recipient.

    const gas = await publicClient.estimateTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1')
    })

### value (optional)

*   **Type:** `bigint`

Value (in wei) sent with this transaction.

    const gas = await publicClient.estimateTotalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>initiateWithdrawal</title>
  <url>https://viem.sh/op-stack/actions/initiateWithdrawal</url>
  <content>Initiates a [withdrawal](https://github.com/ethereum-optimism/optimism/blob/develop/specs/deposits.md) on an L2 to the L1.

Internally performs a contract write to the [`initiateWithdrawal` function](https://github.com/ethereum-optimism/optimism/blob/283f0aa2e3358ced30ff7cbd4028c0c0c3faa140/packages/contracts-bedrock/src/L2/L2ToL1MessagePasser.sol#L73) on the [Optimism L2ToL1MessagePasser predeploy contract](https://github.com/ethereum-optimism/optimism/blob/283f0aa2e3358ced30ff7cbd4028c0c0c3faa140/packages/contracts-bedrock/src/L2/L2ToL1MessagePasser.sol).

Usage
-----

    import { base } from 'viem/chains'
    import { account, walletClientL2 } from './config'
     
    const hash = await walletClientL2.initiateWithdrawal({
      account,
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
    })

### Building Parameters

The [`buildInitiateWithdrawal` Action](https://viem.sh/op-stack/actions/buildInitiateWithdrawal) builds & prepares the initiate withdrawal transaction parameters.

We can use the resulting `args` to initiate the withdrawal transaction on the L2.

    import { account, publicClientL1, walletClientL2 } from './config'
     
    const args = await publicClientL1.buildInitiateWithdrawal({ 
      account, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1'), 
    }) 
     
    const hash = await walletClientL2.initiateWithdrawal(args)

[See more on the `buildInitiateWithdrawal` Action.](https://viem.sh/op-stack/actions/buildInitiateWithdrawal)

### Account Hoisting

If you do not wish to pass an `account` to every `proveWithdrawal`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more.](https://viem.sh/docs/clients/wallet#account)

    import { account, publicClientL1, walletClientL2 } from './config'
     
    const args = await publicClientL1.buildInitiateWithdrawal({ 
      account, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1'), 
    }) 
     
    const hash = await walletClientL2.initiateWithdrawal(args)

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [L2 Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.data (optional)

*   **Type:** `Hex`

Encoded contract method & arguments.

    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        data: '0x...', 
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
    })

### args.gas

*   **Type:** `bigint`

Gas limit for transaction execution on the L1.

    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n, 
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
    })

### args.to

*   **Type:** `Address`

L1 Transaction recipient.

    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',  
        value: parseEther('1')
      },
    })

### args.value (optional)

*   **Type:** `bigint`

Value in wei to withdrawal from the L2 to the L1. Debited from the caller's L2 balance.

    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1') 
      },
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The L2 chain. If there is a mismatch between the wallet's current chain & this chain, an error will be thrown.

    import { optimism } from 'viem/chains'
     
    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      chain: optimism, 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      maxFeePerGas: parseGwei('20'), 
      maxPriorityFeePerGas: parseGwei('2'),  
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await client.initiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      nonce: 69, 
    })</content>
</page>

<page>
  <title>buildInitiateWithdrawal</title>
  <url>https://viem.sh/op-stack/actions/buildInitiateWithdrawal</url>
  <content>Builds & prepares parameters for a [withdrawal](https://community.optimism.io/docs/protocol/withdrawal-flow/#withdrawal-initiating-transaction) to be initiated on an L2.

Usage
-----

    import { account, publicClientL1, walletClientL2 } from './config'
     
    const args = await publicClientL1.buildInitiateWithdrawal({ 
      account, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1'), 
    }) 
     
    const hash = await walletClientL2.initiateWithdrawal(args)

### Account Hoisting

If you do not wish to pass an `account` to every `buildInitiateWithdrawal`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { publicClientL1, walletClientL2 } from './config'
     
    const args = await publicClientL1.buildInitiateWithdrawal({
      mint: parseEther('1')
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })
     
    const hash = await walletClientL2.initiateWithdrawal(args)

Returns
-------

`InitiateWithdrawalParameters`

The parameters required to initiate a [withdrawal](https://viem.sh/op-stack/actions/initiateWithdrawal).

Parameters
----------

### account (optional)

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const args = await client.buildInitiateWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### data (optional)

*   **Type:** `Hex`

Encoded contract method & arguments.

    const args = await client.buildInitiateWithdrawal({
      data: '0x...', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### gas (optional)

*   **Type:** `bigint`

Gas limit for transaction execution on the L1.

    const args = await client.buildInitiateWithdrawal({
      gas: 21_000n, 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1')
    })

### to (optional)

*   **Type:** `Address`

L1 recipient.

    const args = await client.buildInitiateWithdrawal({
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',  
      value: parseEther('1')
    })

### value (optional)

*   **Type:** `bigint`

Value in wei to withdrawal from the L2 to the L1. Debited from the caller's L2 balance.

    const args = await client.buildInitiateWithdrawal({
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: parseEther('1') 
    })</content>
</page>

<page>
  <title>estimateFinalizeWithdrawalGas</title>
  <url>https://viem.sh/op-stack/actions/estimateFinalizeWithdrawalGas</url>
  <content>Estimates gas required to finalize a withdrawal that occurred on an L2.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1 } from './config'
     
    const gas = await publicClientL1.estimateFinalizeWithdrawalGas({ 
      account: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e', 
      targetChain: optimism, 
      withdrawal: { ... }, 
    }) 

Returns
-------

`bigint`

The estimated gas.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The L1 chain. If there is a mismatch between the wallet's current chain & this chain, an error will be thrown.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      chain: mainnet, 
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### gas (optional)

*   **Type:** `bigint`

Gas limit for transaction execution on the L1.

    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n,  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### proofSubmitter (optional)

*   **Type:** `Address`

The address of the proof submitter to use when finalizing the withdrawal. No-op when the OptimismPortal contract version is less than v3.

If unspecified, the sending account is the proof submitter.

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      proofSubmitter: '0xD15F47c16BD277ff2dee6a0bD4e418165231CB69', 
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      maxFeePerGas: parseGwei('20'),  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      maxFeePerGas: parseGwei('20'), 
      maxPriorityFeePerGas: parseGwei('2'),  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      withdrawal: { /* ... */ },
      nonce: 69, 
      targetChain: optimism,
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the Optimism Portal contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
      targetChain: optimism,
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
    })

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain to execute the transaction on.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      withdrawal: { /* ... */ },
      targetChain: optimism, 
    })

### withdrawal

*   **Type:** `bigint`

The withdrawal.

    const hash = await client.estimateFinalizeWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n, 
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ }, 
      targetChain: optimism,
    })</content>
</page>

<page>
  <title>estimateDepositTransactionGas</title>
  <url>https://viem.sh/op-stack/actions/estimateDepositTransactionGas</url>
  <content>Estimates gas to initiate a [deposit transaction](https://github.com/ethereum-optimism/optimism/blob/develop/specs/deposits.md) on an L1, which executes a transaction on an L2.

Usage
-----

    import { base } from 'viem/chains'
    import { account, publicClientL1 } from './config'
     
    const gas = await publicClientL1.estimateDepositTransactionGas({
      account,
      request: {
        gas: 21_000n,
        mint: parseEther('1')
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      },
      targetChain: base,
    })

Returns
-------

`bigint`

Gas required to execute the transaction on the L1.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.data (optional)

*   **Type:** `Hex`

Contract deployment bytecode or encoded contract method & arguments.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        data: '0x...', 
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.gas

*   **Type:** `bigint`

Gas limit for transaction execution on the L2.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n, 
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.isCreation (optional)

*   **Type:** `boolean`

Whether or not this is a contract deployment transaction.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        data: '0x...',
        gas: 69_420n,
        isCreation: true
      },
      targetChain: base,
    })

### args.mint (optional)

*   **Type:** `bigint`

Value in wei to mint (deposit) on the L2. Debited from the caller's L1 balance.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        mint: parseEther('1') 
      },
      targetChain: base,
    })

### args.to (optional)

*   **Type:** `Address`

L2 Transaction recipient.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',  
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction on the L2. Debited from the caller's L2 balance.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1') 
      },
      targetChain: base,
    })

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain to execute the transaction on.

    import { mainnet } from 'viem/chains'
     
    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      chain: mainnet,
      targetChain: base, 
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The L1 chain. If there is a mismatch between the wallet's current chain & this chain, an error will be thrown.

    import { mainnet } from 'viem/chains'
     
    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      chain: mainnet, 
      targetChain: base,
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      maxFeePerGas: parseGwei('20'),  
      targetChain: base,
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      maxFeePerGas: parseGwei('20'), 
      maxPriorityFeePerGas: parseGwei('2'),  
      targetChain: base,
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      nonce: 69, 
      targetChain: base,
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the Optimism Portal contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const gas = await client.estimateDepositTransactionGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>getGames</title>
  <url>https://viem.sh/op-stack/actions/getGames</url>
  <content>Retrieves dispute games for an L2. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1 } from './config'
     
    const games = await publicClientL1.getGames({ 
      targetChain: optimism, 
    }) 

Returns
-------

`GetGamesReturnType`

Dispute games.

Parameters
----------

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const games = await publicClientL1.getGames({
      l2BlockNumber,
      targetChain: optimism, 
    })

### disputeGameFactoryAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.disputeGameFactory[chainId].address`

The address of the [`DisputeGameFactory` contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/dispute/DisputeGameFactory.sol). Defaults to the `DisputeGameFactory` contract specified on the `targetChain`.

If a `disputeGameFactoryAddress` is provided, the `targetChain` parameter becomes optional.

    const games = await publicClientL1.getGames({
      l2BlockNumber,
      disputeGameFactoryAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })

### l2BlockNumber (optional)

*   **Type:** `bigint`

The L2 block number.

    const games = await publicClientL1.getGames({ 
      l2BlockNumber: 69420n, 
      targetChain: optimism, 
    }) 

### limit (optional)

*   **Type:** `number`
*   **Default:** `100`

Limit of games to extract.

    const games = await publicClientL1.getGames({ 
      limit: 10, 
      targetChain: optimism, 
    }) 

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [`Portal` contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal2.sol). Defaults to the `Portal` contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const games = await publicClientL1.getGames({
      l2BlockNumber,
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>estimateProveWithdrawalGas</title>
  <url>https://viem.sh/op-stack/actions/estimateProveWithdrawalGas</url>
  <content>Estimates gas required to prove a withdrawal that occurred on an L2.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1 } from './config'
     
    const gas = await publicClientL1.estimateProveWithdrawalGas({ 
      account: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e', 
      l2OutputIndex: 4529n, 
      outputRootProof: { ... }, 
      targetChain: optimism, 
      withdrawalProof: [ ... ], 
      withdrawal: { ... }, 
    }) 

Returns
-------

`bigint`

The estimated gas.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The L1 chain. If there is a mismatch between the wallet's current chain & this chain, an error will be thrown.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      chain: mainnet, 
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### gas (optional)

*   **Type:** `bigint`

Gas limit for transaction execution on the L1.

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n,  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### l2OutputIndex

*   **Type:** `bigint`

The index of the L2 output. Typically derived from the [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal).

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n, 
      gas: 420_000n, 
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      maxFeePerGas: parseGwei('20'),  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      maxFeePerGas: parseGwei('20'), 
      maxPriorityFeePerGas: parseGwei('2'),  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      nonce: 69, 
      targetChain: optimism,
    })

### outputRootProof (optional)

*   **Type:** `bigint`

The proof of the L2 output. Typically derived from the [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal).

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n, 
      outputRootProof: { /* ... */ }, 
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the Optimism Portal contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
      targetChain: optimism,
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
    })

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain to execute the transaction on.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism, 
    })

### withdrawalProof

*   **Type:** `bigint`

The proof of the L2 withdrawal. Typically derived from the [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal).

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n, 
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ], 
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### withdrawal

*   **Type:** `bigint`

The withdrawal. Typically derived from the [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal).

    const hash = await client.estimateProveWithdrawalGas({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n, 
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ }, 
      targetChain: optimism,
    })</content>
</page>

<page>
  <title>getGame</title>
  <url>https://viem.sh/op-stack/actions/getGame</url>
  <content>Retrieves a valid dispute game on an L2 that occurred after a provided L2 block number. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1 } from './config'
     
    const game = await publicClientL1.getGame({ 
      l2BlockNumber: 69420n, 
      targetChain: optimism, 
    }) 

Returns
-------

`GetGameReturnType`

A valid dispute game.

Parameters
----------

### l2BlockNumber

*   **Type:** `bigint`

The L2 block number.

    const game = await publicClientL1.getGame({ 
      l2BlockNumber: 69420n, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const game = await publicClientL1.getGame({
      l2BlockNumber,
      targetChain: optimism, 
    })

### disputeGameFactoryAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.disputeGameFactory[chainId].address`

The address of the [`DisputeGameFactory` contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/dispute/DisputeGameFactory.sol). Defaults to the `DisputeGameFactory` contract specified on the `targetChain`.

If a `disputeGameFactoryAddress` is provided, the `targetChain` parameter becomes optional.

    const game = await publicClientL1.getGame({
      l2BlockNumber,
      disputeGameFactoryAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>getTimeToFinalize</title>
  <url>https://viem.sh/op-stack/actions/getTimeToFinalize</url>
  <content>Returns the time until the withdrawal transaction can be finalized. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1, publicClientL2 } from './config'
     
    const receipt = await publicClientL2.getTransactionReceipt({
      hash: '0x9a2f4283636ddeb9ac32382961b22c177c9e86dd3b283735c154f897b1a7ff4a',
    })
     
    const [message] = getWithdrawals(receipt)
     
    const { 
      period, 
      seconds, 
      timestamp, 
    } = await publicClientL1.getTimeToFinalize({ 
      withdrawalHash: message.withdrawalHash, 
      targetChain: optimism 
    }) 

Returns
-------

`{ period: number, seconds: number, timestamp: number }`

*   `period` in seconds of the finalization stage (max wait time).
*   `seconds` until the transaction can be finalized.
*   `timestamp` of when the transaction can be finalized.

Parameters
----------

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const { seconds } = await publicClientL1.getTimeToFinalize({
      withdrawalHash: '0x...', 
      targetChain: optimism, 
    })

### withdrawalHash

*   **Type:** `Hash`

The withdrawal hash.

    const { seconds, timestamp } = await publicClientL1.getTimeToFinalize({ 
      withdrawalHash: '0x...', 
      targetChain: optimism, 
    }) 

### l2OutputOracleAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.l2OutputOracle[chainId].address`

The address of the [L2 Output Oracle contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/L2OutputOracle.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `l2OutputOracleAddress` is provided, the `targetChain` parameter becomes optional.

    const { seconds } = await publicClientL1.getTimeToFinalize({
      withdrawalHash: '0x...',
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const { seconds } = await publicClientL1.getTimeToFinalize({
      withdrawalHash: '0x...',
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed',
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>getL2Output</title>
  <url>https://viem.sh/op-stack/actions/getL2Output</url>
  <content>Retrieves the first L2 output proposal that occurred after a provided block number. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1 } from './config'
     
    const output = await publicClientL1.getL2Output({ 
      l2BlockNumber: 69420n, 
      targetChain: optimism, 
    }) 

Returns
-------

`GetL2OutputReturnType`

The L2 output proposal.

Parameters
----------

### l2BlockNumber

*   **Type:** `bigint`

The L2 block number.

    const output = await publicClientL1.getL2Output({ 
      l2BlockNumber: 69420n, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const output = await publicClientL1.getL2Output({
      l2BlockNumber,
      targetChain: optimism, 
    })

### l2OutputOracleAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.l2OutputOracle[chainId].address`

The address of the [L2 Output Oracle contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/L2OutputOracle.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `l2OutputOracleAddress` is provided, the `targetChain` parameter becomes optional.

    const output = await publicClientL1.getL2Output({
      l2BlockNumber,
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>getTimeToProve</title>
  <url>https://viem.sh/op-stack/actions/getTimeToProve</url>
  <content>Gets time until the L2 withdrawal transaction is ready to be proved. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Internally calls [`getTimeToNextL2Output`](https://viem.sh/op-stack/actions/getTimeToNextL2Output).

Usage
-----

    import { account, publicClientL1, publicClientL2 } from './config'
     
    const receipt = await publicClientL2.getTransactionReceipt({
      hash: '0x7b5cedccfaf9abe6ce3d07982f57bcb9176313b019ff0fc602a0b70342fe3147'
    })
     
    const { 
      interval, 
      seconds, 
      timestamp
    } = await publicClientL1.getTimeToProve({ 
      receipt, 
      targetChain: publicClientL2.chain, 
    }) 

Returns
-------

`{ interval: number, seconds: number, timestamp: number }`

*   `interval` between L2 outputs – the max time to wait for transaction to be proved.
*   Estimated `seconds` until the transaction can be proved.
*   Estimated `timestamp` of when the transaction can be proved.

Parameters
----------

### receipt

*   **Type:** `TransactionReceipt`

The transaction receipt.

    const time = await publicClientL1.getTimeToProve({ 
      receipt, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const time = await publicClientL1.getTimeToProve({
      l2BlockNumber,
      targetChain: optimism, 
    })

### intervalBuffer (optional)

*   **Type:** `number`
*   **Default:** `1.1`

The buffer to account for discrepancies between non-deterministic time intervals.

    const time = await publicClientL1.getTimeToProve({ 
      intervalBuffer: 1.2, 
      l2BlockNumber,
      targetChain: optimism, 
    }) 

### l2OutputOracleAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.l2OutputOracle[chainId].address`

The address of the [L2 Output Oracle contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/L2OutputOracle.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `l2OutputOracleAddress` is provided, the `targetChain` parameter becomes optional.

    const time = await publicClientL1.getTimeToProve({
      l2BlockNumber,
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>getTimeToNextL2Output</title>
  <url>https://viem.sh/op-stack/actions/getTimeToNextL2Output</url>
  <content>Returns the time until the next L2 output (after a provided block number) is submitted. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1, publicClientL2 } from './config'
     
    const l2BlockNumber = publicClientL2.getBlockNumber()
     
    const { 
      interval, 
      seconds, 
      timestamp
    } = await publicClientL1.getTimeToNextL2Output({ 
      l2BlockNumber, 
      targetChain: publicClientL2.chain, 
    }) 

Returns
-------

`{ interval: number, seconds: number, timestamp: number }`

*   `interval` between L2 outputs – the max time to wait for transaction to be proved.
*   Estimated `seconds` until the next L2 Output is submitted.
*   Estimated `timestamp` of the next L2 Output.

Parameters
----------

### l2BlockNumber

*   **Type:** `bigint`

The latest L2 block number.

    const l2BlockNumber = publicClientL2.getBlockNumber() 
    const { seconds } = await publicClientL1.getTimeToNextL2Output({ 
      l2BlockNumber, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const { seconds } = await publicClientL1.getTimeToNextL2Output({
      l2BlockNumber,
      targetChain: optimism, 
    })

### intervalBuffer (optional)

*   **Type:** `number`
*   **Default:** `1.1`

The buffer to account for discrepancies between non-deterministic time intervals.

    const { seconds } = await publicClientL1.getTimeToNextL2Output({ 
      intervalBuffer: 1.2, 
      l2BlockNumber,
      targetChain: optimism, 
    }) 

### l2OutputOracleAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.l2OutputOracle[chainId].address`

The address of the [L2 Output Oracle contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/L2OutputOracle.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `l2OutputOracleAddress` is provided, the `targetChain` parameter becomes optional.

    const { seconds } = await publicClientL1.getTimeToNextL2Output({
      l2BlockNumber,
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>getTimeToNextGame</title>
  <url>https://viem.sh/op-stack/actions/getTimeToNextGame</url>
  <content>Returns the time until the next L2 dispute game (after the provided block number) is submitted. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1, publicClientL2 } from './config'
     
    const l2BlockNumber = publicClientL2.getBlockNumber()
     
    const { 
      interval, 
      seconds, 
      timestamp
    } = await publicClientL1.getTimeToNextGame({ 
      l2BlockNumber, 
      targetChain: publicClientL2.chain, 
    }) 

Returns
-------

`{ interval: number, seconds: number, timestamp: number }`

*   Estimated `interval` between dispute games – the max time to wait for transaction to be proved.
*   Estimated `seconds` until the next dispute game is submitted.
*   Estimated `timestamp` of the next dispute game.

Parameters
----------

### l2BlockNumber

*   **Type:** `bigint`

The latest L2 block number.

    const l2BlockNumber = publicClientL2.getBlockNumber() 
    const { seconds } = await publicClientL1.getTimeToNextGame({ 
      l2BlockNumber, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const { seconds } = await publicClientL1.getTimeToNextGame({
      l2BlockNumber,
      targetChain: optimism, 
    })

### disputeGameFactoryAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.disputeGameFactory[chainId].address`

The address of the [`DisputeGameFactory` contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/dispute/DisputeGameFactory.sol). Defaults to the `DisputeGameFactory` contract specified on the `targetChain`.

If a `disputeGameFactoryAddress` is provided, the `targetChain` parameter becomes optional.

    const { seconds } = await publicClientL1.getTimeToNextGame({
      l2BlockNumber,
      disputeGameFactoryAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })

### intervalBuffer (optional)

*   **Type:** `number`
*   **Default:** `1.1`

The buffer to account for discrepancies between non-deterministic time intervals.

    const { seconds } = await publicClientL1.getTimeToNextGame({ 
      intervalBuffer: 1.2, 
      l2BlockNumber,
      targetChain: optimism, 
    }) 

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [`Portal` contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal2.sol). Defaults to the `Portal` contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const { seconds } = await publicClientL1.getTimeToNextGame({
      l2BlockNumber,
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>getWithdrawalStatus</title>
  <url>https://viem.sh/op-stack/actions/getWithdrawalStatus</url>
  <content>Returns the current status of a withdrawal. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Usage
-----

    import { account, publicClientL1, publicClientL2 } from './config'
     
    const receipt = await publicClientL2.getTransactionReceipt({
      hash: '0x7b5cedccfaf9abe6ce3d07982f57bcb9176313b019ff0fc602a0b70342fe3147'
    })
     
    const status = await publicClientL1.getWithdrawalStatus({ 
      receipt, 
      targetChain: publicClientL2.chain, 
    }) 
    // "ready-to-prove" //

Returns
-------

`"waiting-to-prove" | "ready-to-prove" | "waiting-to-finalize" | "ready-to-finalize" | "finalized"`

Parameters
----------

### receipt

*   **Type:** `TransactionReceipt`

The transaction receipt.

    const status = await publicClientL1.getWithdrawalStatus({ 
      receipt, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const status = await publicClientL1.getWithdrawalStatus({
      receipt,
      targetChain: optimism, 
    })

### l2OutputOracleAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.l2OutputOracle[chainId].address`

The address of the [L2 Output Oracle contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/L2OutputOracle.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `l2OutputOracleAddress` is provided, the `targetChain` parameter becomes optional.

    const status = await publicClientL1.getWithdrawalStatus({
      receipt,
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const status = await publicClientL1.getWithdrawalStatus({
      receipt,
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed',
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>waitForNextL2Output</title>
  <url>https://viem.sh/op-stack/actions/waitForNextL2Output</url>
  <content>Waits for the next L2 output (after the provided block number) to be submitted. Used within the [waitToProve](https://viem.sh/op-stack/actions/waitToProve) Action.

Internally calls [`getTimeToNextL2Output`](https://viem.sh/op-stack/actions/getTimeToNextL2Output) and waits the returned `seconds`.

Usage
-----

    import { account, publicClientL1, publicClientL2 } from './config'
     
    const l2BlockNumber = await publicClientL2.getBlockNumber()
    const output = await publicClientL1.waitForNextL2Output({ 
      l2BlockNumber, 
      targetChain: publicClientL2.chain, 
    }) 

Returns
-------

`WaitForNextL2OutputReturnType`

The L2 output proposal.

Parameters
----------

### l2BlockNumber

*   **Type:** `bigint`

The L2 block number.

    const output = await publicClientL1.waitForNextL2Output({ 
      l2BlockNumber: 69420n, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const output = await publicClientL1.waitForNextL2Output({
      l2BlockNumber,
      targetChain: optimism, 
    })

### intervalBuffer (optional)

*   **Type:** `number`
*   **Default:** `1.1`

The buffer to account for discrepancies between non-deterministic time intervals.

    const output = await publicClientL1.waitForNextL2Output({
      intervalBuffer: 1.2, 
      l2BlockNumber,
      targetChain: optimism, 
    }) 

### l2OutputOracleAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.l2OutputOracle[chainId].address`

The address of the [L2 Output Oracle contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/L2OutputOracle.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `l2OutputOracleAddress` is provided, the `targetChain` parameter becomes optional.

    const output = await publicClientL1.waitForNextL2Output({
      l2BlockNumber,
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>waitForNextGame</title>
  <url>https://viem.sh/op-stack/actions/waitForNextGame</url>
  <content>Waits for the next dispute game (after the provided block number) to be submitted. Used within the [waitToProve](https://viem.sh/op-stack/actions/waitToProve) Action.

Internally calls [`getTimeToNextGame`](https://viem.sh/op-stack/actions/getTimeToNextGame) and waits the returned `seconds`.

Usage
-----

    import { account, publicClientL1, publicClientL2 } from './config'
     
    const l2BlockNumber = await publicClientL2.getBlockNumber()
    const game = await publicClientL1.waitForNextGame({ 
      l2BlockNumber, 
      targetChain: publicClientL2.chain, 
    }) 

Returns
-------

`waitForNextGameReturnType`

The dispute game.

Parameters
----------

### l2BlockNumber

*   **Type:** `bigint`

The L2 block number.

    const game = await publicClientL1.waitForNextGame({ 
      l2BlockNumber: 69420n, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const game = await publicClientL1.waitForNextGame({
      l2BlockNumber,
      targetChain: optimism, 
    })

### disputeGameFactoryAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.disputeGameFactory[chainId].address`

The address of the [`DisputeGameFactory` contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/dispute/DisputeGameFactory.sol). Defaults to the `DisputeGameFactory` contract specified on the `targetChain`.

If a `disputeGameFactoryAddress` is provided, the `targetChain` parameter becomes optional.

    const game = await publicClientL1.waitForNextGame({
      l2BlockNumber,
      disputeGameFactoryAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })

### intervalBuffer (optional)

*   **Type:** `number`
*   **Default:** `1.1`

The buffer to account for discrepancies between non-deterministic time intervals.

    const game = await publicClientL1.waitForNextGame({
      intervalBuffer: 1.2, 
      l2BlockNumber,
      targetChain: optimism, 
    }) 

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [`Portal` contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal2.sol). Defaults to the `Portal` contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const game = await publicClientL1.waitForNextGame({
      l2BlockNumber,
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>waitToProve</title>
  <url>https://viem.sh/op-stack/actions/waitToProve</url>
  <content>Waits until the L2 withdrawal transaction is ready to be proved. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Internally calls [`getTimeToNextL2Output`](https://viem.sh/op-stack/actions/getTimeToNextL2Output) and waits the returned `seconds`.

Usage
-----

    import { account, publicClientL1, publicClientL2 } from './config'
     
    const receipt = await publicClientL2.getTransactionReceipt({
      hash: '0x7b5cedccfaf9abe6ce3d07982f57bcb9176313b019ff0fc602a0b70342fe3147'
    })
    const output = await publicClientL1.waitToProve({ 
      receipt, 
      targetChain: publicClientL2.chain, 
    }) 

Returns
-------

`WaitToProveReturnType`

The L2 output and the withdrawal message.

Parameters
----------

### receipt

*   **Type:** `TransactionReceipt`

The transaction receipt.

    const output = await publicClientL1.waitToProve({ 
      receipt, 
      targetChain: optimism, 
    }) 

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const output = await publicClientL1.waitToProve({
      l2BlockNumber,
      targetChain: optimism, 
    })

### l2OutputOracleAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.l2OutputOracle[chainId].address`

The address of the [L2 Output Oracle contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/L2OutputOracle.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `l2OutputOracleAddress` is provided, the `targetChain` parameter becomes optional.

    const output = await publicClientL1.waitToProve({
      l2BlockNumber,
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>waitToFinalize</title>
  <url>https://viem.sh/op-stack/actions/waitToFinalize</url>
  <content>Waits until the withdrawal transaction can be finalized. Used for the [Withdrawal](https://viem.sh/op-stack/guides/withdrawals) flow.

Internally calls [`getTimeToFinalize`](https://viem.sh/op-stack/actions/getTimeToFinalize) and waits the returned `seconds`.

Usage
-----

    import { optimism } from 'viem/chains'
    import { account, publicClientL1, publicClientL2 } from './config'
     
    const receipt = await publicClientL2.getTransactionReceipt({
      hash: '0x9a2f4283636ddeb9ac32382961b22c177c9e86dd3b283735c154f897b1a7ff4a',
    })
     
    const [message] = getWithdrawals(receipt)
     
    await publicClientL1.waitToFinalize({ 
      withdrawalHash: message.withdrawalHash, 
      targetChain: optimism 
    }) 

Parameters
----------

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain.

    const { seconds } = await publicClientL1.waitToFinalize({
      withdrawalHash: '0x...', 
      targetChain: optimism, 
    })

### withdrawalHash

*   **Type:** `Hash`

The withdrawal hash.

    const { seconds, timestamp } = await publicClientL1.waitToFinalize({ 
      withdrawalHash: '0x...', 
      targetChain: optimism, 
    }) 

### l2OutputOracleAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.l2OutputOracle[chainId].address`

The address of the [L2 Output Oracle contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/L2OutputOracle.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `l2OutputOracleAddress` is provided, the `targetChain` parameter becomes optional.

    const { seconds } = await publicClientL1.waitToFinalize({
      withdrawalHash: '0x...',
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the L2 Output Oracle contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const { seconds } = await publicClientL1.waitToFinalize({
      withdrawalHash: '0x...',
      l2OutputOracleAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed',
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>depositTransaction</title>
  <url>https://viem.sh/op-stack/actions/depositTransaction</url>
  <content>Initiates a [deposit transaction](https://github.com/ethereum-optimism/optimism/blob/develop/specs/deposits.md) on an L1, which executes a transaction on an L2.

Internally performs a contract write to the [`depositTransaction` function](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol#L378) on the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol).

Usage
-----

    import { base } from 'viem/chains'
    import { account, walletClientL1 } from './config'
     
    const hash = await walletClientL1.depositTransaction({
      account,
      request: {
        gas: 21_000n,
        mint: parseEther('1')
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      },
      targetChain: base,
    })

### Building Parameters

The [`buildDepositTransaction` Action](https://viem.sh/op-stack/actions/buildDepositTransaction) builds & prepares the deposit transaction parameters (ie. `gas`, `targetChain`, etc).

We can use the resulting `args` to initiate the deposit transaction on the L1.

    import { account, publicClientL2, walletClientL1 } from './config'
     
    // Build parameters for the transaction on the L2.
    const args = await publicClientL2.buildDepositTransaction({
      account,
      mint: parseEther('1')
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })
     
    // Execute the deposit transaction on the L1.
    const hash = await walletClientL1.depositTransaction(args)

[See more on the `buildDepositTransaction` Action.](https://viem.sh/op-stack/actions/buildDepositTransaction)

### Account Hoisting

If you do not wish to pass an `account` to every `depositTransaction`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more.](https://viem.sh/docs/clients/wallet#account)

    import { publicClientL2, walletClientL1 } from './config'
     
    // Prepare parameters for the deposit transaction on the L2.
    const args = await publicClientL2.buildDepositTransaction({
      mint: parseEther('1')
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })
     
    // Initiate the deposit transaction on the L1.
    const hash = await walletClientL1.depositTransaction(args)

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [L1 Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.data (optional)

*   **Type:** `Hex`

Contract deployment bytecode or encoded contract method & arguments.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        data: '0x...', 
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.gas

*   **Type:** `bigint`

Gas limit for transaction execution on the L2.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n, 
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.isCreation (optional)

*   **Type:** `boolean`

Whether or not this is a contract deployment transaction.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        data: '0x...',
        gas: 69_420n,
        isCreation: true
      },
      targetChain: base,
    })

### args.mint (optional)

*   **Type:** `bigint`

Value in wei to mint (deposit) on the L2. Debited from the caller's L1 balance.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        mint: parseEther('1') 
      },
      targetChain: base,
    })

### args.to (optional)

*   **Type:** `Address`

L2 Transaction recipient.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',  
        value: parseEther('1')
      },
      targetChain: base,
    })

### args.value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction on the L2. Debited from the caller's L2 balance.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1') 
      },
      targetChain: base,
    })

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain to execute the transaction on.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      chain: mainnet,
      targetChain: base, 
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The L1 chain. If there is a mismatch between the wallet's current chain & this chain, an error will be thrown.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      chain: mainnet, 
      targetChain: base,
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      maxFeePerGas: parseGwei('20'),  
      targetChain: base,
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      maxFeePerGas: parseGwei('20'), 
      maxPriorityFeePerGas: parseGwei('2'),  
      targetChain: base,
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      nonce: 69, 
      targetChain: base,
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the Optimism Portal contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const hash = await client.depositTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      request: {
        gas: 21_000n,
        to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
        value: parseEther('1')
      },
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
    })</content>
</page>

<page>
  <title>finalizeWithdrawal</title>
  <url>https://viem.sh/op-stack/actions/finalizeWithdrawal</url>
  <content>Finalizes a withdrawal that occurred on an L2. Used in the Withdrawal flow.

Internally performs a contract write to the [`finalizeWithdrawalTransaction` function](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal2.sol#L383) on the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal2.sol).

If the proof submitter is specified and the OptimismPortal contract version is v3 or greater, the [`finalizeWithdrawalTransactionExternalProof` function](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal2.sol#L390) function will be used to finalize the withdrawal with the provided address as the proof submitter.

Usage
-----

    import { account, publicClientL2, walletClientL1 } from './config'
     
    const receipt = await getTransactionReceipt(publicClientL2, {
      hash: '0xbbdd0957a82a057a76b5f093de251635ac4ddc6e2d0c4aa7fbf82d73e4e11039',
    })
     
    const [withdrawal] = getWithdrawals(receipt)
     
    const hash = await walletClientL1.finalizeWithdrawal({ 
      account, 
      targetChain: publicClientL2.chain, 
      withdrawal, 
    }) 

### Account Hoisting

If you do not wish to pass an `account` to every `finalizeWithdrawal`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more.](https://viem.sh/docs/clients/wallet#account)

    import { account, publicClientL2, walletClientL1 } from './config'
     
    const receipt = await getTransactionReceipt(publicClientL2, {
      hash: '0xbbdd0957a82a057a76b5f093de251635ac4ddc6e2d0c4aa7fbf82d73e4e11039',
    })
     
    const [withdrawal] = getWithdrawals(receipt)
     
    const hash = await walletClientL1.finalizeWithdrawal({ 
      account, 
      targetChain: publicClientL2.chain, 
      withdrawal, 
    }) 

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The finalize withdrawal [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The L1 chain. If there is a mismatch between the wallet's current chain & this chain, an error will be thrown.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      chain: mainnet, 
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### gas (optional)

*   **Type:** `bigint`

Gas limit for transaction execution on the L1.

`null` to skip gas estimation & defer calculation to signer.

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      gas: 420_000n,  
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### proofSubmitter (optional)

*   **Type:** `Address`

The address of the proof submitter to use when finalizing the withdrawal. No-op when the OptimismPortal contract version is less than v3.

If unspecified, the sending account is the proof submitter.

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      proofSubmitter: '0xD15F47c16BD277ff2dee6a0bD4e418165231CB69', 
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'),  
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      maxFeePerGas: parseGwei('20'), 
      maxPriorityFeePerGas: parseGwei('2'),  
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      withdrawal: { /* ... */ },
      nonce: 69, 
      targetChain: optimism,
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the Optimism Portal contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
      targetChain: optimism,
      withdrawal: { /* ... */ },
    })

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain to execute the transaction on.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      withdrawal: { /* ... */ },
      targetChain: optimism, 
    })

### withdrawal

*   **Type:** `bigint`

The withdrawal.

    const hash = await client.finalizeWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      gas: 420_000n, 
      withdrawal: { /* ... */ }, 
      targetChain: optimism,
    })</content>
</page>

<page>
  <title>extractWithdrawalMessageLogs</title>
  <url>https://viem.sh/op-stack/utilities/extractWithdrawalMessageLogs</url>
  <content>Extracts [`MessagePassed` logs](https://github.com/ethereum-optimism/optimism/blob/9f73402cb4341f7cfa83bf79769c8dddd9b014c0/packages/contracts-bedrock/src/L2/L2ToL1MessagePasser.sol#L29-L45) from a withdrawal initialization from an opaque array of logs.

Import
------

    import { extractWithdrawalMessageLogs } from 'viem'

Usage
-----

    import { extractWithdrawalMessageLogs } from 'viem'
     
    const receipt = await client.getTransactionReceipt({
      hash: '0xc9c0361bc3da9cd3560e48b469d0d6aac0e633e4897895edfd26a287f7c578ec',
    })
     
    const logs = extractWithdrawalMessageLogs(receipt)
    // [
    //   { args: { ... }, blockHash: '0x...', eventName: 'MessagePassed'  },
    //   { args: { ... }, blockHash: '0x...', eventName: 'MessagePassed'  },
    //   { args: { ... }, blockHash: '0x...', eventName: 'MessagePassed'  },
    // ]

Returns
-------

`Log[]`

The `MessagePassed` logs.

Parameters
----------

### logs

*   **Type:** `Log[]`

An array of opaque logs.

    const logs = extractWithdrawalMessageLogs({ 
      logs: receipt.logs 
    })</content>
</page>

<page>
  <title>extractTransactionDepositedLogs</title>
  <url>https://viem.sh/op-stack/utilities/extractTransactionDepositedLogs</url>
  <content>Extracts `TransactionDeposited` logs from an opaque array of logs.

Import
------

    import { extractTransactionDepositedLogs } from 'viem'

Usage
-----

    import { extractTransactionDepositedLogs } from 'viem'
     
    const receipt = await client.getTransactionReceipt({
      hash: '0xc9c0361bc3da9cd3560e48b469d0d6aac0e633e4897895edfd26a287f7c578ec',
    })
     
    const logs = extractTransactionDepositedLogs(receipt)
    // [
    //   { args: { ... }, blockHash: '0x...', eventName: 'TransactionDeposited'  },
    //   { args: { ... }, blockHash: '0x...', eventName: 'TransactionDeposited'  },
    //   { args: { ... }, blockHash: '0x...', eventName: 'TransactionDeposited'  },
    // ]

Returns
-------

`Log[]`

The `TransactionDeposited` logs.

Parameters
----------

### logs

*   **Type:** `Log[]`

An array of opaque logs.

    const logs = extractTransactionDepositedLogs({ 
      logs: receipt.logs 
    })</content>
</page>

<page>
  <title>getL2TransactionHash</title>
  <url>https://viem.sh/op-stack/utilities/getL2TransactionHash</url>
  <content>Computes the L2 transaction hash from an L1 `TransactionDeposited` log.

Import
------

    import { getL2TransactionHash } from 'viem'

Usage
-----

    import { extractTransactionDepositedLogs, getL2TransactionHash } from 'viem'
     
    const receipt = await client.getTransactionReceipt({
      hash: '0xa08acae48f12243bccd7153c88d892673d5578cce4ee9988c0332e8bba47436b',
    })
     
    const [log] = extractTransactionDepositedLogs(receipt)
     
    const l2Hash = getL2TransactionHash({ log }) 

Returns
-------

`Hex`

The L2 transaction hash.

Parameters
----------

### log

*   **Type:** `Log`

An L1 `TransactionDeposited` log.

    const l2Hash = getL2TransactionHash({ 
      log: { 
        args: { 
          from: '0x1a1E021A302C237453D3D45c7B82B19cEEB7E2e6', 
          opaqueData: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000045000000000000520800', 
          to: '0x1a1E021A302C237453D3D45c7B82B19cEEB7E2e6', 
          version: 0n, 
        }, 
        blockHash: '0x634c52556471c589f42db9131467e0c9484f5c73049e32d1a74e2a4ce0f91d57', 
        eventName: 'TransactionDeposited', 
        logIndex: 109, 
      } 
    })</content>
</page>

<page>
  <title>getL2TransactionHashes</title>
  <url>https://viem.sh/op-stack/utilities/getL2TransactionHashes</url>
  <content>Computes the L2 transaction hashes from an array of L1 `TransactionDeposited` logs.

Useful for extracting L2 hashes from an **L1 Transaction Receipt**.

Import
------

    import { getL2TransactionHashes } from 'viem'

Usage
-----

    import { extractTransactionDepositedLogs, getL2TransactionHashes } from 'viem'
     
    const receipt = await client.getTransactionReceipt({
      hash: '0xa08acae48f12243bccd7153c88d892673d5578cce4ee9988c0332e8bba47436b',
    })
     
    const l2Hashes = getL2TransactionHashes(receipt) 

Returns
-------

`Hex`

The L2 transaction hash.

Parameters
----------

### logs

*   **Type:** `Log[]`

An array of L1 logs.

    const l2Hashes = getL2TransactionHash({ 
      logs: receipt.logs 
    })</content>
</page>

<page>
  <title>proveWithdrawal</title>
  <url>https://viem.sh/op-stack/actions/proveWithdrawal</url>
  <content>Proves a withdrawal that occurred on an L2. Used in the Withdrawal flow.

Internally performs a contract write to the [`proveWithdrawalTransaction` function](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol#L197) on the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol).

Usage
-----

    import { account, publicClientL1, publicClientL2, walletClientL1 } from './config'
     
    const receipt = await getTransactionReceipt(publicClientL2, {
      hash: '0xbbdd0957a82a057a76b5f093de251635ac4ddc6e2d0c4aa7fbf82d73e4e11039',
    })
     
    const [withdrawal] = getWithdrawals(receipt)
    const output = await publicClientL1.getL2Output({
      l2BlockNumber: receipt.blockNumber,
      targetChain: publicClientL2.chain,
    })
     
    const args = await publicClientL2.buildProveWithdrawal({
      account,
      output,
      withdrawal,
    })
     
    const hash = await walletClientL1.proveWithdrawal(args) 

### Building Parameters

The [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal) builds & prepares the prove withdrawal transaction parameters.

We can use the resulting `args` to prove the withdrawal transaction on the L1.

    import { account, publicClientL2, walletClientL1 } from './config'
     
    const receipt = await getTransactionReceipt(publicClientL2, {
      hash: '0xbbdd0957a82a057a76b5f093de251635ac4ddc6e2d0c4aa7fbf82d73e4e11039',
    })
     
    const [withdrawal] = getWithdrawals(receipt)
    const output = await walletClientL1.getL2Output({
      l2BlockNumber: receipt.blockNumber,
      targetChain: publicClientL2.chain,
    })
     
    const args = await publicClientL2.buildProveWithdrawal({ 
      account, 
      output, 
      withdrawal, 
    }) 
     
    const hash = await walletClientL1.proveWithdrawal(args)

[See more on the `buildProveWithdrawal` Action.](https://viem.sh/op-stack/actions/buildProveWithdrawal)

### Account Hoisting

If you do not wish to pass an `account` to every `proveWithdrawal`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more.](https://viem.sh/docs/clients/wallet#account)

    import { account, publicClientL2, walletClientL1 } from './config'
     
    const receipt = await getTransactionReceipt(publicClientL2, {
      hash: '0xbbdd0957a82a057a76b5f093de251635ac4ddc6e2d0c4aa7fbf82d73e4e11039',
    })
     
    const [withdrawal] = getWithdrawals(receipt)
    const output = await walletClientL1.getL2Output({
      l2BlockNumber: receipt.blockNumber,
      targetChain: publicClientL2.chain,
    })
     
    const args = await publicClientL2.buildProveWithdrawal({
      output,
      withdrawal,
    })
     
    const hash = await walletClientL1.proveWithdrawal(args)

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The prove withdrawal [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The L1 chain. If there is a mismatch between the wallet's current chain & this chain, an error will be thrown.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      chain: mainnet, 
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### gas (optional)

*   **Type:** `bigint`

Gas limit for transaction execution on the L1.

`null` to skip gas estimation & defer calculation to signer.

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n,  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### l2OutputIndex

*   **Type:** `bigint`

The index of the L2 output. Typically derived from the [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal).

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n, 
      gas: 420_000n, 
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`.

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      maxFeePerGas: parseGwei('20'),  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      maxFeePerGas: parseGwei('20'), 
      maxPriorityFeePerGas: parseGwei('2'),  
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      nonce: 69, 
      targetChain: optimism,
    })

### outputRootProof (optional)

*   **Type:** `bigint`

The proof of the L2 output. Typically derived from the [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal).

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n, 
      outputRootProof: { /* ... */ }, 
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### portalAddress (optional)

*   **Type:** `Address`
*   **Default:** `targetChain.contracts.portal[chainId].address`

The address of the [Optimism Portal contract](https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/L1/OptimismPortal.sol). Defaults to the Optimism Portal contract specified on the `targetChain`.

If a `portalAddress` is provided, the `targetChain` parameter becomes optional.

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      portalAddress: '0xbEb5Fc579115071764c7423A4f12eDde41f106Ed'
      targetChain: optimism,
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
    })

### targetChain

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)

The L2 chain to execute the transaction on.

    import { mainnet } from 'viem/chains'
     
    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ },
      targetChain: optimism, 
    })

### withdrawalProof

*   **Type:** `bigint`

The proof of the L2 withdrawal. Typically derived from the [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal).

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n, 
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ], 
      withdrawal: { /* ... */ },
      targetChain: optimism,
    })

### withdrawal

*   **Type:** `bigint`

The withdrawal. Typically derived from the [`buildProveWithdrawal` Action](https://viem.sh/op-stack/actions/buildProveWithdrawal).

    const hash = await client.proveWithdrawal({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      l2OutputIndex: 4529n,
      gas: 420_000n, 
      outputRootProof: { /* ... */ },
      withdrawalProof: [ /* ... */ ],
      withdrawal: { /* ... */ }, 
      targetChain: optimism,
    })</content>
</page>

<page>
  <title>getWithdrawals</title>
  <url>https://viem.sh/op-stack/utilities/getWithdrawals</url>
  <content>Gets withdrawal messages emitted from the [`MessagePassed` log](https://github.com/ethereum-optimism/optimism/blob/9f73402cb4341f7cfa83bf79769c8dddd9b014c0/packages/contracts-bedrock/src/L2/L2ToL1MessagePasser.sol#L29-L45) from a withdrawal initialization.

Import
------

    import { getWithdrawals } from 'viem'

Usage
-----

    import { extractTransactionDepositedLogs, getWithdrawals } from 'viem'
     
    const receipt = await client.getTransactionReceipt({
      hash: '0xa08acae48f12243bccd7153c88d892673d5578cce4ee9988c0332e8bba47436b',
    })
     
    const withdrawals = getWithdrawals(receipt) 

Returns
-------

`Hex`

The L2 transaction hash.

Parameters
----------

### logs

*   **Type:** `Log[]`

An array of L2 logs.

    const withdrawals = getWithdrawals({ 
      logs: receipt.logs 
    })</content>
</page>

<page>
  <title>getSourceHash</title>
  <url>https://viem.sh/op-stack/utilities/getSourceHash</url>
  <content>Computes the [source hash](https://github.com/ethereum-optimism/optimism/blob/develop/specs/deposits.md#source-hash-computation) of a deposit transaction.

Import
------

    import { getSourceHash } from 'viem'

Usage
-----

    import { getSourceHash } from 'viem'
     
    // User Deposit
    const sourceHash = getSourceHash({
      domain: 'userDeposit',
      l1BlockHash:
        '0x9ba3933dc6ce43c145349770a39c30f9b647f17668f004bd2e05c80a2e7262f7',
      l1LogIndex: 196,
    })
     
    // L1 attributes deposited
    const sourceHash = getSourceHash({
      domain: 'l1InfoDeposit',
      l1BlockHash:
        '0x9ba3933dc6ce43c145349770a39c30f9b647f17668f004bd2e05c80a2e7262f7',
      sequenceNumber: 1,
    })

Returns
-------

`Hex`

The source hash of the deposit transaction.

Parameters
----------

### domain

*   **Type:** `"userDeposit" | "l1InfoDeposit"`

The domain of the deposit transaction.

    const sourceHash = getSourceHash({
      domain: 'userDeposit', 
      l1BlockHash:
        '0x9ba3933dc6ce43c145349770a39c30f9b647f17668f004bd2e05c80a2e7262f7',
      l1LogIndex: 196,
    })

### l1BlockHash

*   **Type:** `Hex`

The hash of the L1 block the deposit transaction was included in.

    const sourceHash = getSourceHash({
      domain: 'userDeposit',
      l1BlockHash:
        '0x9ba3933dc6ce43c145349770a39c30f9b647f17668f004bd2e05c80a2e7262f7', 
      l1LogIndex: 196,
    })

### l1LogIndex

*   **Type:** `number`

The index of the L1 log. **Only required for `"userDeposit"` domain.**

    const sourceHash = getSourceHash({
      domain: 'userDeposit',
      l1BlockHash:
        '0x9ba3933dc6ce43c145349770a39c30f9b647f17668f004bd2e05c80a2e7262f7',
      l1LogIndex: 196, 
    })

### sequenceNumber

*   **Type:** `number`

The sequence number (difference between L2 block number and first L2 epoch block number). **Only required for `"l1InfoDeposit"` domain.**

    const sourceHash = getSourceHash({
      domain: 'l1InfoDeposit',
      l1BlockHash:
        '0x9ba3933dc6ce43c145349770a39c30f9b647f17668f004bd2e05c80a2e7262f7',
      sequenceNumber: 1, 
    })</content>
</page>

<page>
  <title>getWithdrawalHashStorageSlot</title>
  <url>https://viem.sh/op-stack/utilities/getWithdrawalHashStorageSlot</url>
  <content>Computes the withdrawal hash storage slot to be used when proving a withdrawal.

Import
------

    import { getWithdrawalHashStorageSlot } from 'viem'

Usage
-----

    import { getWithdrawalHashStorageSlot } from 'viem'
     
    const slot = getWithdrawalHashStorageSlot({ 
      withdrawalHash: '0xB1C3824DEF40047847145E069BF467AA67E906611B9F5EF31515338DB0AABFA2'
    }) 

Returns
-------

`Hex`

The storage slot.

Parameters
----------

### withdrawalHash

*   **Type:** `Hash`

Hash emitted from the L2 withdrawal `MessagePassed` event.

    const slot = getWithdrawalHashStorageSlot({ 
      withdrawalHash: '0xB1C3824DEF40047847145E069BF467AA67E906611B9F5EF31515338DB0AABFA2'
    })</content>
</page>

<page>
  <title>parseTransaction (OP Stack)</title>
  <url>https://viem.sh/op-stack/utilities/parseTransaction</url>
  <content>Parses a serialized RLP-encoded transaction. Supports signed & unsigned Deposit, EIP-1559, EIP-2930 and Legacy Transactions.

Import
------

    import { parseTransaction } from 'viem'

Usage
-----

    import { parseTransaction } from 'viem'
     
    const transaction = parseTransaction('0x02ef0182031184773594008477359400809470997970c51812dc3a010c7d01b50e0d17dc79c8880de0b6b3a764000080c0')

### Deposit Transactions

The `parseTransaction` module from `viem/op-stack` also supports parsing deposit transactions (`0x7e`\-prefixed):

    import { parseTransaction } from 'viem'
     
    const transaction = parseTransaction('0x7ef83ca018040f35752170c3339ddcd850f185c9cc46bdef4d6e1f2ab323f4d3d710431994977f82a600a1414e583f7f13623f1ac5d58b1c0b808080808080')

Returns
-------

`TransactionSerializable`

The parsed transaction object.

Parameters
----------

### serializedTransaction

*   **Type:** `Hex`

The serialized transaction.</content>
</page>

<page>
  <title>opaqueDataToDepositData</title>
  <url>https://viem.sh/op-stack/utilities/opaqueDataToDepositData</url>
  <content>Converts an opaque data into a structured deposit data object. This includes extracting and converting the `mint`, `value`, `gas`, `isCreation` flag, and `data` from a hex string.

Import
------

    import { opaqueDataToDepositData } from "viem";

Usage
-----

    import { opaqueDataToDepositData } from "viem";
     
    const opaqueData =
      "0x00000000000000000000000000000000000000000000000000470DE4DF82000000000000000000000000000000000000000000000000000000470DE4DF82000000000000000186A00001";
     
    const depositData = opaqueDataToDepositData(opaqueData);
    // {
    //   mint: 20000000000000000n,
    //   value: 20000000000000000n,
    //   gas: 100000n,
    //   isCreation: false,
    //   data: '0x01',
    // }

Returns
-------

`OpaqueDataToDepositDataReturnType`

An object containing the parsed deposit data.

Parameters
----------

### opaqueData

*   **Type:** `Hex`

The opaque hex-encoded data.

Errors
------

`OpaqueDataToDepositDataErrorType`

An error type that includes potential slice, size, and generic errors encountered during the parsing process.</content>
</page>

<page>
  <title>serializeTransaction (OP Stack)</title>
  <url>https://viem.sh/op-stack/utilities/serializeTransaction</url>
  <content>Serializes a transaction object, with support for OP Stack transactions. Supports Deposit, EIP-1559, EIP-2930, and Legacy transactions.

Import
------

    import { serializeTransaction } from 'viem/op-stack'

Usage
-----

    import { serializeTransaction } from 'viem/op-stack'
     
    const serialized = serializeTransaction({
      chainId: 1,
      gas: 21001n,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69,
      to: "0x1234512345123451234512345123451234512345",
      value: parseEther('0.01'),
    })

### Deposit Transactions

The `serializeTransaction` module from `viem/op-stack` also supports serializing deposit transactions:

    import { parseEther } from 'viem'
    import { serializeTransaction } from 'viem/op-stack'
     
    const serialized = serializeTransaction({
      from: '0x977f82a600a1414e583f7f13623f1ac5d58b1c0b',
      gas: 21000n,
      mint: parseEther('1'),
      sourceHash: '0x18040f35752170c3339ddcd850f185c9cc46bdef4d6e1f2ab323f4d3d7104319',
      value: parseEther('1'),
      type: 'deposit'
    })

Returns
-------

Returns a template `Hex` value based on transaction type:

*   `deposit`: [TransactionSerializedDeposit](https://viem.sh/docs/glossary/types#TransactionSerializedDeposit)
*   `eip1559`: [TransactionSerializedEIP1559](https://viem.sh/docs/glossary/types#TransactionSerializedEIP1559)
*   `eip2930`: [TransactionSerializedEIP2930](https://viem.sh/docs/glossary/types#TransactionSerializedEIP2930)
*   `legacy`: [TransactionSerializedLegacy](https://viem.sh/docs/glossary/types#TransactionSerializedLegacy)

Parameters
----------

### transaction

*   **Type:** `TransactionSerializable`

The transaction object to serialize.

    const serialized = serializeTransaction({
      chainId: 1,
      gas: 21001n,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69,
      to: '0x1234512345123451234512345123451234512345',
      value: parseEther('0.01'),
    })

### signature

*   **Type:** `Hex`

Optional signature to include. **Ignored for deposit transactions.**

    const serialized = serializeTransaction({
      chainId: 1,
      gas: 21001n,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69,
      to: '0x1234512345123451234512345123451234512345',
      value: parseEther('0.01'),
    }, { 
      r: '0x123451234512345123451234512345123451234512345123451234512345',
      s: '0x123451234512345123451234512345123451234512345123451234512345',
      yParity: 1
    })</content>
</page>

<page>
  <title>parseTransaction</title>
  <url>https://viem.sh/docs/utilities/parseTransaction</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/parseTransaction#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Parses a serialized RLP-encoded transaction. Supports signed & unsigned EIP-1559, EIP-2930 and Legacy Transactions.

Import
------

    import { parseTransaction } from 'viem'

Usage
-----

    import { parseTransaction } from 'viem'
     
    const transaction = parseTransaction('0x02ef0182031184773594008477359400809470997970c51812dc3a010c7d01b50e0d17dc79c8880de0b6b3a764000080c0')

Returns
-------

`TransactionSerializable`

The parsed transaction object.

Parameters
----------

### serializedTransaction

*   **Type:** `Hex`

The serialized transaction.</content>
</page>

<page>
  <title>serializeTransaction</title>
  <url>https://viem.sh/docs/utilities/serializeTransaction</url>
  <content>Serializes a transaction object. Supports EIP-1559, EIP-2930, and Legacy transactions.

Import
------

    import { serializeTransaction } from 'viem'

Usage
-----

    import { serializeTransaction } from 'viem'
     
    const serialized = serializeTransaction({
      chainId: 1,
      gas: 21001n,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69,
      to: "0x1234512345123451234512345123451234512345",
      value: parseEther('0.01'),
    })

Returns
-------

Returns a template `Hex` value based on transaction type:

*   `eip1559`: [TransactionSerializedEIP1559](https://viem.sh/docs/glossary/types#TransactionSerializedEIP1559)
*   `eip2930`: [TransactionSerializedEIP2930](https://viem.sh/docs/glossary/types#TransactionSerializedEIP2930)
*   `eip4844`: [TransactionSerializedEIP4844](https://viem.sh/docs/glossary/types#TransactionSerializedEIP4844)
*   `eip7702`: [TransactionSerializedEIP7702](https://viem.sh/docs/glossary/types#TransactionSerializedEIP7702)
*   `legacy`: [TransactionSerializedLegacy](https://viem.sh/docs/glossary/types#TransactionSerializedLegacy)

Parameters
----------

### transaction

*   **Type:** `TransactionSerializable`

The transaction object to serialize.

    const serialized = serializeTransaction({
      chainId: 1,
      gas: 21001n,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69,
      to: '0x1234512345123451234512345123451234512345',
      value: parseEther('0.01'),
    })

### signature

*   **Type:** `Hex`

Optional signature to include.

    const serialized = serializeTransaction({
      chainId: 1,
      gas: 21001n,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'),
      nonce: 69,
      to: '0x1234512345123451234512345123451234512345',
      value: parseEther('0.01'),
    }, { 
      r: '0x123451234512345123451234512345123451234512345123451234512345',
      s: '0x123451234512345123451234512345123451234512345123451234512345',
      yParity: 1
    })</content>
</page>

<page>
  <title>Chains</title>
  <url>https://viem.sh/zksync/chains</url>
  <content>[Skip to content](https://viem.sh/zksync/chains#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

The following ZKsync chains are supported in Viem:

    import {
      zksync, 
      zksyncSepoliaTestnet, 
    } from 'viem/chains'

Configuration
-------------

Viem exports ZKsync's chain [formatters](https://viem.sh/docs/chains/formatters) & [serializers](https://viem.sh/docs/chains/serializers) via `chainConfig`. This is useful if you need to define another chain which is implemented on ZKsync.

    import { defineChain } from 'viem'
    import { chainConfig } from 'viem/zksync'
     
    export const zkStackExample = defineChain({
      ...chainConfig,
      name: 'ZKsync Example',
      // ...
    })</content>
</page>

<page>
  <title>Client</title>
  <url>https://viem.sh/zksync/client</url>
  <content>To use the ZKsync functionality of Viem, you must extend your existing (or new) Viem Client with ZKsync Actions.

Usage
-----

    import { createPublicClient, createWalletClient, custom, http } from 'viem'
    import { zksync } from 'viem/chains'
    import { eip712WalletActions } from 'viem/zksync'
     
    const walletClient = createWalletClient({
      chain: zksync,
      transport: custom(window.ethereum!),
    }).extend(eip712WalletActions()) 
     
    const publicClient = createPublicClient({
      chain: zksync,
      transport: http()
    })

Extensions
----------

### `eip712WalletActions`

A suite of [Wallet Actions](https://viem.sh/zksync/actions/sendTransaction) for suited for development with ZKsync chains.

    import { eip712WalletActions } from 'viem/zksync'

#### Sending transactions using paymaster

[Read more](https://viem.sh/actions/sendTransaction)

    const hash = await walletClient.sendTransaction({
      account: '0xA0Cf798816D4b9b9866b5330EEa46a18382f251e',
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      paymaster: '0xFD9aE5ebB0F6656f4b77a0E99dCbc5138d54b0BA',
      paymasterInput: '0x123abc...'
    })

#### Calling contracts

[Read more](https://viem.sh/vercel/path0/site/pages/docs/contract/writeContract)

    import { simulateContract } from 'viem/contract'
     
    const { request } = await publicClient.simulateContract(walletClient, {
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: parseAbi(['function mint(uint32 tokenId) nonpayable']),
      functionName: 'mint',
      args: [69420],
    });
    const hash = await walletClient.writeContract(request)

### `publicActionsL1`

A suite of [Public Actions](https://viem.sh/zksync/actions/getL1Allowance) suited for development with **Layer 1** chains. These actions provide functionalities specific to public clients operating at the Layer 1 level, enabling them to interact seamlessly with Layer 2 protocols.

    import { publicActionsL1 } from 'viem/zksync'</content>
</page>

<page>
  <title>toMultisigSmartAccount (ZKsync)</title>
  <url>https://viem.sh/zksync/accounts/toMultisigSmartAccount</url>
  <content>Creates a multi-signature [ZKsync Smart Account](https://docs.zksync.io/build/developer-reference/account-abstraction/building-smart-accounts) from a Contract Address and the Private Key of the owner.

Usage
-----

    import { toMultisigSmartAccount } from 'viem/zksync'
     
    const account = toMultisigSmartAccount({
      address: '0xf39Fd6e51aad8F6F4ce6aB8827279cffFb92266', 
      privateKeys: ['0x...', '0x...']
    })

Parameters
----------

### address

*   **Type:** `Hex`

Address of the deployed Account's Contract implementation.

    const account = toMultisigSmartAccount({
      address: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', 
      privateKeys: ['0x...', '0x...']
    })

### privateKeys

*   **Type:** `Hex[]`

Private Keys of the owners.

    const account = toMultisigSmartAccount({
      address: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', 
      privateKeys: ['0x...', '0x...'] 
    })</content>
</page>

<page>
  <title>toSinglesigSmartAccount (ZKsync)</title>
  <url>https://viem.sh/zksync/accounts/toSinglesigSmartAccount</url>
  <content>Creates a single-signature [ZKsync Smart Account](https://docs.zksync.io/build/developer-reference/account-abstraction/building-smart-accounts) from a Contract Address and the Private Key of the owner.

Usage
-----

    import { toSinglesigSmartAccount } from 'viem/zksync'
     
    const account = toSinglesigSmartAccount({
      address: '0xf39Fd6e51aad8F6F4ce6aB8827279cffFb92266', 
      privateKey: '0x...'
    })

Parameters
----------

### address

*   **Type:** `Hex`

Address of the deployed Account's Contract implementation.

    const account = toSinglesigSmartAccount({
      address: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', 
      privateKey: '0x...'
    })

### privateKey

*   **Type:** `Hex`

Private Key of the owner.

    const account = toSinglesigSmartAccount({
      address: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', 
      privateKey: '0x...'
    })</content>
</page>

<page>
  <title>toSmartAccount (ZKsync)</title>
  <url>https://viem.sh/zksync/accounts/toSmartAccount</url>
  <content>Creates a [ZKsync Smart Account](https://docs.zksync.io/build/developer-reference/account-abstraction/building-smart-accounts) from a Contract Address and a custom sign function.

Usage
-----

    import { toSmartAccount } from 'viem/zksync'
     
    const account = toSmartAccount({
      address: '0xf39Fd6e51aad8F6F4ce6aB8827279cffFb92266', 
      async sign({ hash }) {
        // ... signing logic
        return '0x...'
      }
    })

Parameters
----------

### address

*   **Type:** `Hex`

Address of the deployed Account's Contract implementation.

    const account = toSmartAccount({
      address: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', 
      async sign({ hash }) {
        // ...
      }
    })

### sign

*   **Type:** `({ hash: Hex }) => Hex`

Custom sign function for the Smart Account.

    const account = toSmartAccount({
      address: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266', 
      async sign({ hash }) { 
        // ... 
      } 
    })</content>
</page>

<page>
  <title>deployContract</title>
  <url>https://viem.sh/zksync/actions/deployContract</url>
  <content>Deploys a contract to the network, given bytecode & constructor arguments by using EIP712 transaction.

Usage
-----

    import { wagmiAbi } from './abi'
    import { account, walletClient } from './config'
     
    const hash = await walletClient.deployContract({
      abi,
      account,
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
    })

### Deploying with Constructor Args

    import { deployContract } from 'viem'
    import { wagmiAbi } from './abi'
    import { account, walletClient } from './config'
     
    const hash = await walletClient.deployContract({
      abi,
      account,
      args: [69420],
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
    })

### Deploying with Factory Deps

    import { deployContract } from 'viem'
    import { wagmiAbi } from './abi'
    import { account, walletClient } from './config'
     
    const hash = await walletClient.deployContract({
      abi,
      account,
      args: [69420],
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      factoryDeps: [
        '0x702040405260405161083e38038061083e833981016040819123456...', 
        '0x102030405260405161083e38038061083e833981016040819112233...'
      ]
    })

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    const hash = await walletClient.deployContract({
      abi: wagmiAbi, 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
    })

### account

*   **Type:** `Account | Address`

The Account to deploy the contract from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await walletClient.deployContract({
      abi: wagmiAbi, 
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
    })

### bytecode

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The contract's bytecode.

    const hash = await walletClient.deployContract({
      abi: wagmiAbi,
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...', 
    })

### args

*   **Type:** Inferred from ABI.

Constructor arguments to call upon deployment.

    const hash = await walletClient.deployContract({
      abi: wagmiAbi,
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      args: [69] 
    })

### deploymentType (optional)

*   **Type:** `'create' | 'create2' | 'createAccount' | 'create2Account'`

Specifies the type of contract deployment. Defaults to 'create'.

    const hash = await walletClient.deployContract({
      abi: wagmiAbi,
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      args: [69],
      deploymentType: 'create2'
    })

### salt (optional)

*   **Type:** [`Hash`](https://viem.sh/docs/glossary/types#hash)

Specifies a unique identifier for the contract deployment.

    const hash = await walletClient.deployContract({
      abi: wagmiAbi,
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      args: [69],
      salt: '0x201050...'
    })

### gasPerPubdata (optional)

*   **Type:** `bigint`

The amount of gas for publishing one byte of data on Ethereum.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      gasPerPubdata: 50000, 
      nonce: 69,
      value: 1000000000000000000n
    })

### paymaster (optional)

*   **Type:** `Account | Address`

Address of the paymaster account that will pay the fees. The `paymasterInput` field is required with this one.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69,
      value: 1000000000000000000n
    })

### paymasterInput (optional)

*   **Type:** `0x${string}`

Input data to the paymaster. The `paymaster` field is required with this one.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69,
      value: 1000000000000000000n
    })</content>
</page>

<page>
  <title>signTransaction</title>
  <url>https://viem.sh/zksync/actions/signTransaction</url>
  <content>Signs a transaction, with EIP712 transaction support.

Usage
-----

    import { account, walletClient } from './config'
     
    const request = await walletClient.prepareTransactionRequest({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
     
    const signature = await walletClient.signTransaction(request) 
    // 0x02f850018203118080825208808080c080a04012522854168b27e5dc3d5839bab5e6b39e1a0ffd343901ce1622e3d64b48f1a04e00902ae0502c4728cbf12156290df99c3ed7de85b1dbfe20b5c36931733a33
     
    const hash = await walletClient.sendRawTransaction(signature)

### Account Hoisting

If you do not wish to pass an `account` to every `prepareTransactionRequest`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient } from './config' 
     
    const request = await walletClient.prepareTransactionRequest({
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
     
    const signature = await walletClient.signTransaction(request) 
    // 0x02f850018203118080825208808080c080a04012522854168b27e5dc3d5839bab5e6b39e1a0ffd343901ce1622e3d64b48f1a04e00902ae0502c4728cbf12156290df99c3ed7de85b1dbfe20b5c36931733a33
     
    const hash = await client.sendRawTransaction(signature)

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The signed serialized transaction.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const signature = await walletClient.signTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### to

*   **Type:** `0x${string}`

The transaction recipient or contract address.

    const signature = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: 1000000000000000000n,
      nonce: 69
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const signature = await walletClient.signTransaction({
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

The chain is also used to infer its request type (e.g. the Celo chain has a `gatewayFee` that you can pass through to `signTransaction`).

    import { zksync } from 'viem/chains'
     
    const signature = await walletClient.signTransaction({
      chain: zksync, 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const signature = await walletClient.signTransaction({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const signature = await walletClient.signTransaction({
      account,
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1') 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const signature = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    const signature = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
      nonce: 69
    })

### gasPerPubdata (optional)

*   **Type:** `bigint`

The amount of gas for publishing one byte of data on Ethereum.

    const hash = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      gasPerPubdata: 50000, 
      nonce: 69
    })

### factoryDeps (optional)

*   **Type:** `[0x${string}]`

Contains bytecode of the deployed contract.

    const hash = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      factoryDeps: ['0xcde...'], 
      nonce: 69
    })

### paymaster (optional)

*   **Type:** `Account | Address`

Address of the paymaster account that will pay the fees. The `paymasterInput` field is required with this one.

    const hash = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69
    })

### paymasterInput (optional)

*   **Type:** `0x${string}`

Input data to the paymaster. The `paymaster` field is required with this one.

    const hash = await walletClient.signTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69
    })</content>
</page>

<page>
  <title>sendTransaction</title>
  <url>https://viem.sh/zksync/actions/sendTransaction</url>
  <content>Creates, signs, and sends a new transaction to the network, with EIP712 transaction support.

Usage
-----

    import { account, walletClient } from './config'
     
    const hash = await walletClient.sendTransaction({ 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
    // '0x...'

### Account Hoisting

If you do not wish to pass an `account` to every `sendTransaction`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient } from './config'
     
    const hash = await walletClient.sendTransaction({ 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
    // '0x...'

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await walletClient.sendTransaction({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### to

*   **Type:** `0x${string}`

The transaction recipient or contract address.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: 1000000000000000000n,
      nonce: 69
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const hash = await walletClient.sendTransaction({
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

The chain is also used to infer its request type (e.g. the Celo chain has a `gatewayFee` that you can pass through to `sendTransaction`).

    import { zksync } from 'viem/chains'
     
    const hash = await walletClient.sendTransaction({
      chain: zksync, 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const hash = await walletClient.sendTransaction({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const hash = await walletClient.sendTransaction({
      account,
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
      nonce: 69
    })

### gasPerPubdata (optional)

*   **Type:** `bigint`

The amount of gas for publishing one byte of data on Ethereum.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      gasPerPubdata: 50000, 
      nonce: 69,
      value: 1000000000000000000n
    })

### factoryDeps (optional)

*   **Type:** `[0x${string}]`

Contains bytecode of the deployed contract.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      factoryDeps: ['0xcde...'], 
      nonce: 69,
      value: 1000000000000000000n
    })

### paymaster (optional)

*   **Type:** `Account | Address`

Address of the paymaster account that will pay the fees. The `paymasterInput` field is required with this one.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69,
      value: 1000000000000000000n
    })

### paymasterInput (optional)

*   **Type:** `0x${string}`

Input data to the paymaster. The `paymaster` field is required with this one.

    const hash = await walletClient.sendTransaction({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69,
      value: 1000000000000000000n
    })</content>
</page>

<page>
  <title>getAllBalances</title>
  <url>https://viem.sh/zksync/actions/getAllBalances</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getAllBalances#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns all known balances for a given account.

Usage
-----

    import { client, account } from './config'
     
    const balances = await client.getAllBalances({
      account
    });

Returns
-------

`GetAllBalancesReturnType`

Array of all known balances for an address.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account used for check.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const balances = await client.getAllBalances({
      account: "0x36615Cf349d7F6344891B1e7CA7C72883F5dc049"
    });</content>
</page>

<page>
  <title>getBlockDetails</title>
  <url>https://viem.sh/zksync/actions/getBlockDetails</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getBlockDetails#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns additional ZKsync-specific information about the L2 block.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const blockDetails = await client.getBlockDetails({
      number: 1
    });

Returns
-------

`BaseBlockDetails`

Structure that represent ZKsync-specific information about L2 block.

Parameters
----------

### number

Block Number

*   **Type** `number`

    const blockDetails = await client.getBlockDetails({
      number: 1
    });</content>
</page>

<page>
  <title>estimateFee</title>
  <url>https://viem.sh/zksync/actions/estimateFee</url>
  <content>Returns an estimated Fee for requested transaction.

Usage
-----

    import { client } from './config'
     
    const fee = await client.estimateFee({
      account: '0x636A122e48079f750d44d13E5b39804227E1467e',
      to: "0xa61464658AfeAf65CccaaFD3a512b69A83B77618",
      value: 0n
    });

Returns
-------

`Fee`

The fee values.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const fee = await walletClient.estimateFee({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### to

*   **Type:** `0x${string}`

The transaction recipient or contract address.

    const fee = await walletClient.estimateFee({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: 1000000000000000000n,
      nonce: 69
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const fee = await walletClient.estimateFee({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const fee = await walletClient.estimateFee({
      account,
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const fee = await walletClient.estimateFee({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    const fee = await walletClient.estimateFee({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
      nonce: 69
    })

### gasPerPubdata (optional)

*   **Type:** `bigint`

The amount of gas for publishing one byte of data on Ethereum.

    const fee = await walletClient.estimateFee({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      gasPerPubdata: 50000, 
      nonce: 69,
      value: 1000000000000000000n
    })

### factoryDeps (optional)

*   **Type:** `[0x${string}]`

Contains bytecode of the deployed contract.

    const fee = await walletClient.estimateFee({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      factoryDeps: ['0xcde...'], 
      nonce: 69,
      value: 1000000000000000000n
    })

### paymaster (optional)

*   **Type:** `Account | Address`

Address of the paymaster account that will pay the fees. The `paymasterInput` field is required with this one.

    const fee = await walletClient.estimateFee({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69,
      value: 1000000000000000000n
    })

### paymasterInput (optional)

*   **Type:** `0x${string}`

Input data to the paymaster. The `paymaster` field is required with this one.

    const fee = await walletClient.estimateFee({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69,
      value: 1000000000000000000n
    })</content>
</page>

<page>
  <title>writeContract</title>
  <url>https://viem.sh/zksync/actions/writeContract</url>
  <content>Executes a write function on a contract, with EIP712 transaction support.

Usage
-----

    import { account, walletClient } from './config'
     
    const hash = await walletClient.writeContract({ 
      account,
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
    })
    // '0x...'

### Account Hoisting

If you do not wish to pass an `account` to every `sendTransaction`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient } from './config'
     
    const hash = await walletClient.writeContract({ 
      account,
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
    })
    // '0x...'

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### address

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420]
    })

### abi

*   **Type:** [`Abi`](https://viem.sh/docs/glossary/types#abi)

The contract's ABI.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi, 
      functionName: 'mint',
      args: [69420]
    })

### functionName

*   **Type:** `string`

A function to extract from the ABI.

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint', 
      args: [69420]
    })

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2', 
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420]
    })

### accessList (optional)

*   **Type:** [`AccessList`](https://viem.sh/docs/glossary/types#accesslist)

The access list.

    const hash = await walletClient.writeContract({
      accessList: [ 
        {
          address: '0x1',
          storageKeys: ['0x1'],
        },
      ],
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420]
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

    import { zksync } from 'viem/chains'
     
    const hash = await walletClient.writeContract({
      chain: zksync, 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420]
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const hash = await walletClient.writeContract({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420]
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const hash = await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      gasPrice: parseGwei('20'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      nonce: 69
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    const hash = await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      value: parseEther('1'), 
    })

### gasPerPubdata (optional)

*   **Type:** `bigint`

The amount of gas for publishing one byte of data on Ethereum.

    const hash = await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      gasPerPubdata: 50000, 
    })

### factoryDeps (optional)

*   **Type:** `[0x${string}]`

Contains bytecode of the deployed contract.

    const hash = await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      factoryDeps: ['0xcde...'], 
    })

### paymaster (optional)

*   **Type:** `Account | Address`

Address of the paymaster account that will pay the fees. The `paymasterInput` field is required with this one.

    const hash = await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
    })

### paymasterInput (optional)

*   **Type:** `0x${string}`

Input data to the paymaster. The `paymaster` field is required with this one.

    const hash = await walletClient.writeContract({
      address: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2',
      abi: wagmiAbi,
      functionName: 'mint',
      args: [69420],
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
    })</content>
</page>

<page>
  <title>getBaseTokenL1Address</title>
  <url>https://viem.sh/zksync/actions/getBaseTokenL1Address</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getBaseTokenL1Address#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the address of the base L1 token.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const address = await client.getBaseTokenL1Address();

Returns
-------

`Address`

Base Token L1 address.</content>
</page>

<page>
  <title>getBridgehubContractAddress</title>
  <url>https://viem.sh/zksync/actions/getBridgehubContractAddress</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getBridgehubContractAddress#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the Bridgehub smart contract address.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const address = await client.getBridgehubContractAddress();

Returns
-------

`Address`

Bridgehub smart contract address.</content>
</page>

<page>
  <title>getDefaultBridgeAddresses</title>
  <url>https://viem.sh/zksync/actions/getDefaultBridgeAddress</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getDefaultBridgeAddress#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the addresses of the default ZKsync Era bridge contracts on both L1 and L2.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const addresses = await client.getDefaultBridgeAddresses();

Returns
-------

`GetDefaultBridgeAddressesReturnType`

Addresses of the default ZKsync Era bridge contracts on both L1 and L2.</content>
</page>

<page>
  <title>estimateGasL1ToL2</title>
  <url>https://viem.sh/zksync/actions/estimateGasL1ToL2</url>
  <content>Returns an estimated gas for L1 to L2 execution

Usage
-----

    import { client } from './config'
     
    const gas = await client.estimateGasL1ToL2({
      account: '0x636A122e48079f750d44d13E5b39804227E1467e',
      to: '0xa61464658AfeAf65CccaaFD3a512b69A83B77618',
      value: 0n
    });

Returns
-------

`bigint`

The estimated gas value.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const gas = await walletClient.estimateGasL1ToL2({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### to

*   **Type:** `0x${string}`

The transaction recipient or contract address.

    const gas = await walletClient.estimateGasL1ToL2({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
      value: 1000000000000000000n,
      nonce: 69
    })

### data (optional)

*   **Type:** `0x${string}`

A contract hashed method call with encoded args.

    const gas = await walletClient.estimateGasL1ToL2({
      data: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2', 
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const gas = await walletClient.estimateGasL1ToL2({
      account,
      gasPrice: parseGwei('20'), 
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const gas = await walletClient.estimateGasL1ToL2({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n,
      nonce: 69
    })

### value (optional)

*   **Type:** `bigint`

Value in wei sent with this transaction.

    const gas = await walletClient.estimateGasL1ToL2({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: parseEther('1'), 
      nonce: 69
    })

### gasPerPubdata (optional)

*   **Type:** `bigint`

The amount of gas for publishing one byte of data on Ethereum.

    const gas = await walletClient.estimateGasL1ToL2({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      gasPerPubdata: 50000, 
      nonce: 69,
      value: 1000000000000000000n
    })

### factoryDeps (optional)

*   **Type:** `[0x${string}]`

Contains bytecode of the deployed contract.

    const gas = await walletClient.estimateGasL1ToL2({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      factoryDeps: ['0xcde...'], 
      nonce: 69,
      value: 1000000000000000000n
    })

### paymaster (optional)

*   **Type:** `Account | Address`

Address of the paymaster account that will pay the gas. The `paymasterInput` field is required with this one.

    const gas = await walletClient.estimateGasL1ToL2({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69,
      value: 1000000000000000000n
    })

### paymasterInput (optional)

*   **Type:** `0x${string}`

Input data to the paymaster. The `paymaster` field is required with this one.

    const gas = await walletClient.estimateGasL1ToL2({
      account,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
      nonce: 69,
      value: 1000000000000000000n
    })</content>
</page>

<page>
  <title>getL1BatchBlockRange</title>
  <url>https://viem.sh/zksync/actions/getL1BatchBlockRange</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getL1BatchBlockRange#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the range of blocks contained within a batch given by batch number.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const batchBlockRange = await client.getL1BatchBlockRange({
      number: 1
    });

Returns
-------

`GetL1BatchBlockRangeReturnType`

Array of two elements representing the range of blocks within a batch.

Parameters
----------

### number

L1 Batch Number

*   **Type** `number`

    const batchBlockRange = await client.getL1BatchBlockRange({
      number: 1
    });</content>
</page>

<page>
  <title>getL1BatchDetails</title>
  <url>https://viem.sh/zksync/actions/getL1BatchDetails</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getL1BatchDetails#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns data pertaining to a given batch.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const batchDetails = await client.getL1BatchDetails({
      number: 1
    });

Returns
-------

`GetL1BatchDetailsReturnType`

Batch details.

Parameters
----------

### number

L1 Batch Number

*   **Type** `number`

    const batchDetails = await client.getL1BatchDetails({
      number: 1
    });</content>
</page>

<page>
  <title>getL1TokenAddress</title>
  <url>https://viem.sh/zksync/actions/getL1TokenAddress</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getL1TokenAddress#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the L1 token address equivalent for a L2 token address as they are not equal.

Usage
-----

    import { client } from './config'
     
    const address = await client.getL1TokenAddress({
      token: '0x3e7676937A7E96CFB7616f255b9AD9FF47363D4b'
    })

Returns
-------

`Address`

Returns the L1 token address equivalent for a L2 token address.

Parameters
----------

### token

*   **Type:** `Address`

The address of the token on L2.

    const address = await client.getL1TokenAddress({
        token: '0x3e7676937A7E96CFB7616f255b9AD9FF47363D4b'
    })</content>
</page>

<page>
  <title>getL2TokenAddress</title>
  <url>https://viem.sh/zksync/actions/getL2TokenAddress</url>
  <content>Returns the L2 token address equivalent for a L1 token address as they are not equal.

Usage
-----

    import { client } from './config'
     
    const address = await client.getL2TokenAddress({
        token: '0x5C221E77624690fff6dd741493D735a17716c26B'
    })

Returns
-------

`Address`

Returns the L2 token address equivalent for a L1 token address.

Parameters
----------

### token

*   **Type:** `Address`

The address of the token on L1.

    const address = await client.getL2TokenAddress({
        token: '0x5C221E77624690fff6dd741493D735a17716c26B'
    })

### bridgeAddress (optional)

*   **Type:** `Address`

The address of custom bridge, which will be used to get l2 token address.

    const address = await client.getL2TokenAddress({
        token: '0x5C221E77624690fff6dd741493D735a17716c26B',
        bridgeAddress: '0xf8c919286126ccf2e8abc362a15158a461429c82'
    })</content>
</page>

<page>
  <title>getL1ChainId</title>
  <url>https://viem.sh/zksync/actions/getL1ChainId</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getL1ChainId#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the Chain Id of underlying L1 network.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const chainId = await client.getL1ChainId();

Returns
-------

`Hex`

L1 Chain ID.</content>
</page>

<page>
  <title>getL1BatchNumber</title>
  <url>https://viem.sh/zksync/actions/getL1BatchNumber</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getL1BatchNumber#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the latest L1 batch number.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const latestNumber = await client.getL1BatchNumber();

Returns
-------

`Hex`

Latest L1 batch number.</content>
</page>

<page>
  <title>getLogProof</title>
  <url>https://viem.sh/zksync/actions/getLogProof</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getLogProof#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the proof for the corresponding L2 to L1 log.

Usage
-----

    import { client } from './config'
     
    const proof = await client.getLogProof({
      txHash: '0x...',
      index: 1
    });

Returns
-------

`GetLogProofReturnType`

Proof of the corresponding L2 to L1 log

Parameters
----------

### txHash

Hash of the L2 transaction the L2 to L1 log was produced within.

    const proof = await client.getLogProof({
      txHash: '0x...', 
      index: 1
    });

### index (optional)

The index of the L2 to L1 log in the transaction.

    const proof = await client.getLogProof({
      txHash: '0x...', 
      index: 1
    });</content>
</page>

<page>
  <title>getTestnetPaymasterAddress</title>
  <url>https://viem.sh/zksync/actions/getTestnetPaymasterAddress</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getTestnetPaymasterAddress#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the address of a Paymaster on a Testnet.

Usage
-----

File

example.ts

    import { client } from './config'
    const address = await client.getTestnetPaymasterAddress();

Returns
-------

`Address | null`

Testnet paymaster address if available, or `null`.</content>
</page>

<page>
  <title>getMainContractAddress</title>
  <url>https://viem.sh/zksync/actions/getMainContractAddress</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getMainContractAddress#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns the address of a Main ZKsync Contract.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const address = await client.getMainContractAddress();

Returns
-------

`Address`

Main ZKsync Era smart contract address.</content>
</page>

<page>
  <title>getTransactionDetails</title>
  <url>https://viem.sh/zksync/actions/getTransactionDetails</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getTransactionDetails#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns data from a specific transaction given by the transaction hash.

Usage
-----

File

example.ts

    import { client } from './config'
     
    const details = await client.getTransactionDetails({
      txHash: '0x...'
    });

Returns
-------

`TransactionDetails`

Data from a specific transaction given by the transaction hash.

Parameters
----------

`GetTransactionDetailsParameters`

### hash

Transaction hash

    const details = await client.getTransactionDetails({
      txHash: '0x...'
    });</content>
</page>

<page>
  <title>getL1Allowance</title>
  <url>https://viem.sh/zksync/actions/getL1Allowance</url>
  <content>Determines the amount of approved tokens for a specific L1 bridge.

Usage
-----

    import { account, publicClient } from './config'
     
    const allowance = await publicClient.getL1Allowance({
      account
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
      bridgeAddress: '0x84DbCC0B82124bee38e3Ce9a92CdE2f943bab60D',
    })

Returns
-------

`bigint`

Returns the amount of approved tokens.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account used for check.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const allowance = await publicClient.getL1Allowance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      blockTag: 'latest',
      bridgeAddress: '0x84DbCC0B82124bee38e3Ce9a92CdE2f943bab60D',
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
    })

### blockTag (optional)

*   **Type:** `BlockTag | undefined`

In which block an allowance should be checked on. The latest processed one is the default option.

    const allowance = await publicClient.getL1Allowance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      blockTag: 'latest', 
      bridgeAddress: '0x84DbCC0B82124bee38e3Ce9a92CdE2f943bab60D',
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
    })

### bridgeAddress

*   **Type:** `Address`

The address of the bridge contract to be used.

    const allowance = await publicClient.getL1Allowance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      blockTag: 'latest', 
      bridgeAddress: '0x84DbCC0B82124bee38e3Ce9a92CdE2f943bab60D', 
      token: '0x5C221E77624690fff6dd741493D735a17716c26B', 
    })

### token

*   **Type:** `Address`

The Ethereum address of the token.

    const allowance = await publicClient.getL1Allowance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      blockTag: 'latest',
      bridgeAddress: '0x84DbCC0B82124bee38e3Ce9a92CdE2f943bab60D',
      token: '0x5C221E77624690fff6dd741493D735a17716c26B', 
    })</content>
</page>

<page>
  <title>getRawBlockTransaction</title>
  <url>https://viem.sh/zksync/actions/getRawBlockTransactions</url>
  <content>[Skip to content](https://viem.sh/zksync/actions/getRawBlockTransactions#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Returns data of transactions in a block.

Usage
-----

File

example.ts

    import { client } from './config'
     
     
    const rawTx = await client.getRawBlockTransaction({
      number: 1
    });

Returns
-------

`RawBlockTransactions`

Data of transactions in a block.

Parameters
----------

### number

Block number.

    const rawTx = await client.getRawBlockTransaction({
      number: 1
    });</content>
</page>

<page>
  <title>getL1Balance</title>
  <url>https://viem.sh/zksync/actions/getL1Balance</url>
  <content>Returns the amount of the token held by the account on the L1 network.

Usage
-----

File

example.ts (token balance)

    import { account, publicClient } from './config'
     
    const balance = await publicClient.getL1Balance({
      account
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
    })

Returns
-------

`bigint`

Returns the amount of the tokens.

Parameters
----------

### account (optional)

*   **Type:** `Account | Address`

The Account used for check.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const balance = await publicClient.getL1Balance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      blockTag: 'latest',
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
    })

### blockTag (optional)

*   **Type:** `BlockTag | undefined`

In which block an balance should be checked on. The latest processed one is the default option.

    const balance = await publicClient.getL1Balance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      blockTag: 'latest', 
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
    })

### token (optional)

*   **Type:** `Address`

The address of the token. Defaults to ETH if not provided.

    const balance = await publicClient.getL1Balance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      blockTag: 'latest',
      token: '0x5C221E77624690fff6dd741493D735a17716c26B', 
    })</content>
</page>

<page>
  <title>isWithdrawalFinalized</title>
  <url>https://viem.sh/zksync/actions/isWithdrawalFinalized</url>
  <content>Returns whether the withdrawal transaction is finalized on the L1 network.

Usage
-----

    import { client, zksyncClient } from './config'
     
    const hash = await client.isWithdrawalFinalized({
      client: zksyncClient,
      hash: '0x…',
    })

Returns
-------

`boolean`

Whether the withdrawal transaction is finalized on the L1 network.

Parameters
----------

### client

*   **Type:** `Client`

The L2 client for fetching data from L2 chain.

    const hash = await client.isWithdrawalFinalized({
      client: zksyncClient, 
      hash: '0x…',
    })

### hash

*   **Type:** `Hex`

Hash of the L2 transaction where the withdrawal was initiated.

    const hash = await client.isWithdrawalFinalized({
      client: zksyncClient,
      hash: '0x…',  
    })

### index (optional)

*   **Type:** `number`
*   **Default:** `0`

In case there were multiple withdrawals in one transaction, you may pass an index of the withdrawal you want to finalize.

    const hash = await client.isWithdrawalFinalized({
      client: zksyncClient,
      hash: '0x…',
      index: 0n, 
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `client.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

    import { zksync } from 'viem/chains'
     
    const hash = await client.isWithdrawalFinalized({
      chain: zksync, 
      client: zksyncClient,
      hash: '0x…',
    })</content>
</page>

<page>
  <title>getL1TokenBalance</title>
  <url>https://viem.sh/zksync/actions/getL1TokenBalance</url>
  <content>Retrieve the token balance held by the contract on L1.

Usage
-----

    import { account, publicClient } from './config'
     
    const balance = await publicClient.getL1TokenBalance({
      account
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
    })

Returns
-------

`bigint`

Returns the amount of the tokens.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account used for check.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const balance = await publicClient.getL1TokenBalance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      blockTag: 'latest',
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
    })

### blockTag (optional)

*   **Type:** `BlockTag | undefined`

In which block an balance should be checked on. The latest processed one is the default option.

    const balance = await publicClient.getL1TokenBalance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266'
      blockTag: 'latest', 
      token: '0x5C221E77624690fff6dd741493D735a17716c26B',
    })

### token

*   **Type:** `Address`

The address of the token.

    const balance = await publicClient.getL1TokenBalance({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266',
      blockTag: 'latest',
      token: '0x5C221E77624690fff6dd741493D735a17716c26B', 
    })</content>
</page>

<page>
  <title>withdraw</title>
  <url>https://viem.sh/zksync/actions/withdraw</url>
  <content>Initiates the withdrawal process which withdraws ETH or any ERC20 token from the associated account on L2 network to the target account on L1 network.

Usage
-----

    import { account, walletClient } from './config'
    import { legacyEthAddress } from 'viem/zksync'
     
    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
    })

### Account Hoisting

If you do not wish to pass an `account` to every `withdraw`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient } from './config'
    import { legacyEthAddress } from 'viem/zksync'
     
    const hash = await walletClient.withdraw({ 
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,  
    })
    // '0x...'

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### account

*   **Type:** `Account | Address`

The Account to send the transaction from.

Accepts a [JSON-RPC Account](https://viem.sh/docs/clients/wallet#json-rpc-accounts) or [Local Account (Private Key, etc)](https://viem.sh/docs/clients/wallet#local-accounts-private-key-mnemonic-etc).

    const hash = await walletClient.withdraw({
      account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', 
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
    })

### amount

*   **Type:** `bigint`

The amount of the token to withdraw.

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n, 
      token: legacyEthAddress,
    })

### token

*   **Type:** `Address`

The address of the token on L2.

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress, 
    })

### bridgeAddress (optional)

*   **Type:** `Address`

The address of the bridge contract to be used. By default, uses shared bridge.

    const address = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      bridgeAddress: '0xf8c919286126ccf2e8abc362a15158a461429c82'
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

The chain is also used to infer its request type.

    import { zksync } from 'viem/chains'
     
    const hash = await walletClient.withdraw({
      chain: zksync, 
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
    })

### gasPerPubdata (optional)

*   **Type:** `bigint`

The amount of gas for publishing one byte of data on Ethereum.

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      gasPerPubdata: 50000, 
    })

### gasPrice (optional)

*   **Type:** `bigint`

The price (in wei) to pay per gas. Only applies to [Legacy Transactions](https://viem.sh/docs/glossary/terms#legacy-transaction).

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      gasPrice: parseGwei('20'), 
    })

### maxFeePerGas (optional)

*   **Type:** `bigint`

Total fee per gas (in wei), inclusive of `maxPriorityFeePerGas`. Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      maxFeePerGas: parseGwei('20'),  
    })

### maxPriorityFeePerGas (optional)

*   **Type:** `bigint`

Max priority fee per gas (in wei). Only applies to [EIP-1559 Transactions](https://viem.sh/docs/glossary/terms#eip-1559-transaction)

    const hash = await walletClient.withdraw({
      account, 
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      maxFeePerGas: parseGwei('20'),
      maxPriorityFeePerGas: parseGwei('2'), 
    })

### nonce (optional)

*   **Type:** `number`

Unique number identifying this transaction.

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      nonce: 69
    })

### paymaster (optional)

*   **Type:** `Account | Address`

Address of the paymaster account that will pay the fees. The `paymasterInput` field is required with this one.

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
    })

### paymasterInput (optional)

*   **Type:** `0x${string}`

Input data to the paymaster. The `paymaster` field is required with this one.

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      paymaster: '0x4B5DF730c2e6b28E17013A1485E5d9BC41Efe021', 
      paymasterInput: '0x8c5a...'
    })

### to (optional)

*   **Type:** `Address`

The address of the recipient on L1. Defaults to the sender address.

    const hash = await walletClient.withdraw({
      account,
      amount: 1_000_000_000_000_000_000n,
      token: legacyEthAddress,
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', 
    })</content>
</page>

<page>
  <title>requestExecute</title>
  <url>https://viem.sh/zksync/actions/requestExecute</url>
  <content>Requests execution of a L2 transaction from L1.

Usage
-----

    import { account, walletClient, zksyncClient } from './config'
     
    const hash = await walletClient.requestExecute({
      account,
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(),
      calldata: '0x',
      l2Value: 7_000_000_000n,
      l2GasLimit: 900_000n
    })

### Account Hoisting

If you do not wish to pass an `account` to every `requestExecute`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient, zksyncClient } from './config'
     
    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(),
      calldata: '0x',
      l2Value: 7_000_000_000n,
      l2GasLimit: 900_000n
    })

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### client

*   **Type:** `Client`

The L2 client for fetching data from L2 chain.

    const hash = await walletClient.requestExecute({
      client: zksyncClient, 
      contractAddress: await zksyncClient.getBridgehubContractAddress(),
      calldata: '0x',
      l2Value: 7_000_000_000n,
      l2GasLimit: 900_000n
    })

### contractAddress

*   **Type:** `Address`

The L2 contract to be called.

    const hash = await walletClient.requestExecute({
      client: zksyncClient, 
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x',
      l2Value: 7_000_000_000n,
      l2GasLimit: 900_000n
    })

### calldata

*   **Type:** `Hex`

The input of the L2 transaction.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x', 
      l2Value: 7_000_000_000n,
      l2GasLimit: 900_000n
    })

### l2Value (optional)

*   **Type:** `bigint`

The `msg.value` of L2 transaction.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x', 
      l2Value: 7_000_000_000n, 
      l2GasLimit: 900_000n
    })

### l2GasLimit (optional)

*   **Type:** `bigint`

Maximum amount of L2 gas that transaction can consume during execution on L2.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x', 
      l2Value: 7_000_000_000n, 
      l2GasLimit: 900_000n
    })

### mintValue (optional)

*   **Type:** `bigint`

The amount of base token that needs to be minted on non-ETH-based L2.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x', 
      l2Value: 7_000_000_000n, 
      l2GasLimit: 900_000n,
      mintValue: 100_000n
    })

### factoryDeps (optional)

*   **Type:** `Hex[]`

An array of L2 bytecodes that will be marked as known on L2.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x', 
      l2Value: 7_000_000_000n, 
      l2GasLimit: 900_000n,
      factoryDeps: ['0x...'] 
    })

### operatorTip (optional)

*   **Type:** `bigint`

The tip the operator will receive on top of the base cost of the transaction. Currently, ZKsync node do not consider this tip.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x', 
      l2Value: 7_000_000_000n, 
      l2GasLimit: 900_000n,
      operatorTip: 100_000n
    })

### gasPerPubdataByte (optional)

*   **Type:** `bigint`

The L2 gas price for each published L1 calldata byte.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x', 
      l2Value: 7_000_000_000n, 
      l2GasLimit: 900_000n,
      gasPerPubdataByte: 250_000_000_000n
    })

### refundRecipient (optional)

*   **Type:** `Address`
*   **Default:** `walletClient.account`

The address on L2 that will receive the refund for the transaction. If the transaction fails, it will also be the address to receive `l2Value`.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(), 
      calldata: '0x', 
      l2Value: 7_000_000_000n, 
      l2GasLimit: 900_000n,
      refundRecipient: '0x...'
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

    import { zksync } from 'viem/chains'
     
    const hash = await walletClient.requestExecute({
      chain: zksync, 
      client: zksyncClient,
      contractAddress: await zksyncClient.getBridgehubContractAddress(),
      calldata: '0x',
      l2Value: 7_000_000_000n,
      l2GasLimit: 900_000n
    })</content>
</page>

<page>
  <title>finalizeWithdrawal</title>
  <url>https://viem.sh/zksync/actions/finalizeWithdrawal</url>
  <content>Proves the inclusion of the `L2->L1` withdrawal message.

Usage
-----

    import { account, walletClient, zksyncClient } from './config'
     
    const hash = await walletClient.finalizeWithdrawal({
      account,
      client: zksyncClient,
      hash: '0x…',
    })

### Account Hoisting

If you do not wish to pass an `account` to every `finalizeWithdrawal`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient, zksyncClient } from './config'
     
    const hash = await walletClient.finalizeWithdrawal({
      client: zksyncClient,
      hash: '0x…',
    })

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### client

*   **Type:** `Client`

The L2 client for fetching data from L2 chain.

    const hash = await walletClient.finalizeWithdrawal({
      client: zksyncClient, 
      hash: '0x…',
    })

### hash

*   **Type:** `Hex`

Hash of the L2 transaction where the withdrawal was initiated.

    const hash = await walletClient.finalizeWithdrawal({
      client: zksyncClient,
      hash: '0x…',  
    })

### index (optional)

*   **Type:** `number`
*   **Default:** `0`

In case there were multiple withdrawals in one transaction, you may pass an index of the withdrawal you want to finalize.

    const hash = await walletClient.finalizeWithdrawal({
      client: zksyncClient,
      hash: '0x…',
      index: 0n, 
    })

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

    import { zksync } from 'viem/chains'
     
    const hash = await walletClient.finalizeWithdrawal({
      chain: zksync, 
      client: zksyncClient,
      hash: '0x…',
    })</content>
</page>

<page>
  <title>getApprovalBasedPaymasterInput</title>
  <url>https://viem.sh/zksync/utilities/paymaster/getApprovalBasedPaymasterInput</url>
  <content>Returns encoded formatted approval-based paymaster params.

Import
------

    import { getApprovalBasedPaymasterInput } from 'viem/zksync'

Usage
-----

    import { getApprovalBasedPaymasterInput } from 'viem/zksync'
     
    const data = getApprovalBasedPaymasterInput({
      innerInput: '0x',
      minAllowance: 1n,
      token: "0x65C899B5fb8Eb9ae4da51D67E1fc417c7CB7e964",
    })

Returns
-------

`EncodeFunctionDataReturnType`

The `Hex` value of the provided approval-based paymaster inputs.

Parameters
----------

### token

*   **Type:** `Address`

The token address.

    const data = getApprovalBasedPaymasterInput({
      innerInput: '0x',
      minAllowance: 1n,
      token: "0x65C899B5fb8Eb9ae4da51D67E1fc417c7CB7e964", 
    })

### minAllowance

*   **Type:** `bigint`

Minimum allowance (in wei) of token that can be sent towards the paymaster.

    const data = getApprovalBasedPaymasterInput({
      innerInput: new Uint8Array(),
      minAllowance: 1n, 
      token: "0x65C899B5fb8Eb9ae4da51D67E1fc417c7CB7e964",
    })

### innerInput

*   **Type:** `Hex | ByteArray`

Additional payload that can be sent to the paymaster to implement any logic .

    const data = getApprovalBasedPaymasterInput({
      innerInput: "0x0005040302010", 
      minAllowance: 1n, 
      token: "0x65C899B5fb8Eb9ae4da51D67E1fc417c7CB7e964",
    })</content>
</page>

<page>
  <title>getGeneralPaymasterInput</title>
  <url>https://viem.sh/zksync/utilities/paymaster/getGeneralPaymasterInput</url>
  <content>Returns encoded formatted general-based paymaster params.

Import
------

    import { getGeneralPaymasterInput } from 'viem/zksync'

Usage
-----

    import { getGeneralPaymasterInput } from 'viem/zksync'
     
    const data = getGeneralPaymasterInput({
      innerInput: '0x',
    })

Returns
-------

`EncodeFunctionDataReturnType`

The `Hex` value of the provided general-based paymaster inputs.

Parameters
----------

### innerInput

Additional payload that can be sent to the paymaster to implement any logic

*   **Type:** `Hex` or `ByteArray`

    const data = getGeneralPaymasterInput({
          innerInput: new Uint8Array([0, 1, 2, 3, 4, 5]), 
        })

    const data = getGeneralPaymasterInput({
          innerInput: "0x0005040302010", 
        })</content>
</page>

<page>
  <title>getL2HashFromPriorityOp</title>
  <url>https://viem.sh/zksync/utilities/bridge/getL2HashFromPriorityOp</url>
  <content>Returns the hash of the L2 priority operation from a given L1 transaction receipt.

Import
------

    import { getL2HashFromPriorityOp } from 'viem/zksync'

Usage
-----

    import { client, zksyncClient } from './config'
    import { getL2HashFromPriorityOp } from 'viem/zksync'
     
    const receipt = await client.waitForTransactionReceipt({
      hash: '0x...'
    })
    const l2Hash = getL2HashFromPriorityOp(
      receipt,
      await zksyncClient.getMainContractAddress()
    )

Returns
-------

`Hash`

The hash of the L2 priority operation.

Parameters
----------

### receipt

*   **Type:** [`TransactionReceipt`](https://viem.sh/docs/glossary/types#transactionreceipt)

The L1 transaction receipt.

    const l2Hash = getL2HashFromPriorityOp(
      receipt, 
      '0x14b947814912c71bdbc3275c143a065d2ecafaba'
    )

### zksync

*   **Type:** `Address`

The address of the ZKsync Era main contract.

    const l2Hash = getL2HashFromPriorityOp(
      receipt, 
      '0x14b947814912c71bdbc3275c143a065d2ecafaba'
    )</content>
</page>

<page>
  <title>parseEip712Transaction</title>
  <url>https://viem.sh/zksync/utilities/parseEip712Transaction</url>
  <content>Parses a serialized EIP712 transaction.

Import
------

    import { parseEip712Transaction } from 'viem/zksync'

Usage
-----

    import { parseEip712Transaction } from 'viem/zksync'
     
    const serializedTransaction =
        '0x71f87f8080808094a61464658afeaf65cccaafd3a512b69a83b77618830f42408001a073a20167b8d23b610b058c05368174495adf7da3a4ed4a57eb6dbdeb1fafc24aa02f87530d663a0d061f69bb564d2c6fb46ae5ae776bbd4bd2a2a4478b9cd1b42a82010e9436615cf349d7f6344891b1e7ca7c72883f5dc04982c350c080c0'
    const transaction = parseEip712Transaction(serializedTransaction)

Returns
-------

`ZksyncTransactionSerializableEIP712`

The ZKsync EIP712 transaction.

Parameters
----------

### tx

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The serialized EIP712 transaction.

    const serializedTransaction =
        '0x71f87f8080808094a61464658afeaf65cccaafd3a512b69a83b77618830f42408001a073a20167b8d23b610b058c05368174495adf7da3a4ed4a57eb6dbdeb1fafc24aa02f87530d663a0d061f69bb564d2c6fb46ae5ae776bbd4bd2a2a4478b9cd1b42a82010e9436615cf349d7f6344891b1e7ca7c72883f5dc04982c350c080c0'
    const transaction = parseEip712Transaction(serializedTransaction)</content>
</page>

<page>
  <title>deposit</title>
  <url>https://viem.sh/zksync/actions/deposit</url>
  <content>Transfers the specified token from the associated account on the L1 network to the target account on the L2 network. The token can be either ETH or any ERC20 token. For ERC20 tokens, enough approved tokens must be associated with the specified L1 bridge (default one or the one defined in `bridgeAddress`). In this case, depending on is the chain ETH-based or not `approveToken` or `approveBaseToken` can be enabled to perform token approval. If there are already enough approved tokens for the L1 bridge, token approval will be skipped.

Usage
-----

    import { account, walletClient, zksyncClient } from './config'
    import { legacyEthAddress } from 'viem/zksync'
     
    // deposit ETH
    const hash = await walletClient.deposit({
      account,
      client: zksyncClient,
      token: legacyEthAddress,
      amount: 7_000_000_000n,
      to: account.address,
      refundRecipient: account.address,
    })
     
    // deposit ERC20
    const txHash = await walletClient.deposit({
        account,
        client: zksyncClient,
        token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
        amount: 20n,
        to: account.address,
        approveToken: true,
        refundRecipient: account.address,
    })

### Account Hoisting

If you do not wish to pass an `account` to every `deposit`, you can also hoist the Account on the Wallet Client (see `config.ts`).

[Learn more](https://viem.sh/docs/clients/wallet#account).

    import { walletClient, zksyncClient } from './config'
    import { legacyEthAddress } from 'viem/zksync'
     
    // deposit ETH
    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: legacyEthAddress,
      amount: 7_000_000_000n,
      to: walletClient.account.address,
      refundRecipient: walletClient.account.address,
    })
     
    // deposit ERC20
    const txHash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: true,
      refundRecipient: walletClient.account.address,
    })

Returns
-------

[`Hash`](https://viem.sh/docs/glossary/types#hash)

The [Transaction](https://viem.sh/docs/glossary/terms#transaction) hash.

Parameters
----------

### client

*   **Type:** `Client`

The L2 client for fetching data from L2 chain.

    const hash = await walletClient.deposit({
      client: zksyncClient, 
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: true,
      refundRecipient: walletClient.account.address,
    })

### token

*   **Type:** `Address`

The address of the token to deposit.

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55', 
      amount: 20n,
      to: walletClient.account.address,  
      approveToken: true,
      refundRecipient: walletClient.account.address,
    })

### amount

*   **Type:** `bigint`

The amount of the token to deposit.

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n, 
      to: walletClient.account.address,
      approveToken: true,
      refundRecipient: walletClient.account.address,
    })

### to (optional)

*   **Type:** `Address`
*   **Default:** `walletClient.account`

The address that will receive the deposited tokens on L2.

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address, 
      approveToken: true,
      refundRecipient: walletClient.account.address,
    })

### operatorTip (optional)

*   **Type:** `bigint`

The tip the operator will receive on top of the base cost of the transaction. Currently, ZKsync node do not consider this tip.

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      operatorTip: 100_000n, 
      approveToken: true,
      refundRecipient: walletClient.account.address,
    })

### l2GasLimit (optional)

*   **Type:** `bigint`

Maximum amount of L2 gas that transaction can consume during execution on L2.

    const hash = await walletClient.requestExecute({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      l2GasLimit: 900_000n, 
      approveToken: true,
      refundRecipient: walletClient.account.address,
    })

### gasPerPubdataByte (optional)

*   **Type:** `bigint`

The L2 gas price for each published L1 calldata byte.

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: true,
      refundRecipient: walletClient.account.address,
      gasPerPubdataByte: 250_000_000_000n
    })

### refundRecipient (optional)

*   **Type:** `Address`
*   **Default:** `walletClient.account`

The address on L2 that will receive the refund for the transaction. If the transaction fails, it will also be the address to receive `amount`.

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: true,
      refundRecipient: walletClient.account.address, 
    })

### bridgeAddress (optional)

*   **Type:** `Address`
*   **Default:** ZKsync L1 shared bridge

The address of the bridge contract to be used.

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: true,
      refundRecipient: walletClient.account.address, 
      bridgeAddress: '0xFC073319977e314F251EAE6ae6bE76B0B3BAeeCF'
    })

### customBridgeData (optional)

*   **Type:** `Hex`

Additional data that can be sent to a bridge.

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: true,
      refundRecipient: walletClient.account.address,
      bridgeAddress: '0xFC073319977e314F251EAE6ae6bE76B0B3BAeeCF', 
      customBridgeData: '0x...' //,
    })

### approveToken (optional)

*   **Type:** `boolean | TransactionRequest`

Whether token approval should be performed under the hood. Set this flag to true (or provide transaction overrides) if the bridge does not have sufficient allowance. The approval transaction is executed only if the bridge lacks sufficient allowance; otherwise, it is skipped.

::: code-group

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: true, //,
      refundRecipient: walletClient.account.address,
      bridgeAddress: '0xFC073319977e314F251EAE6ae6bE76B0B3BAeeCF',
    })

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: { 
        maxFeePerGas: 200_000_000_000n //,
      },
      refundRecipient: walletClient.account.address,
      bridgeAddress: '0xFC073319977e314F251EAE6ae6bE76B0B3BAeeCF',
    })

:::

### approveBaseToken (optional)

*   **Type:** `boolean | TransactionRequest`

Whether base token approval should be performed under the hood. Set this flag to true (or provide transaction overrides) if the bridge does not have sufficient allowance. The approval transaction is executed only if the bridge lacks sufficient allowance; otherwise, it is skipped.

::: code-group

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveBaseToken: true, //,
      refundRecipient: walletClient.account.address,
      bridgeAddress: '0xFC073319977e314F251EAE6ae6bE76B0B3BAeeCF',
    })

    const hash = await walletClient.deposit({
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveBaseToken: { 
        maxFeePerGas: 200_000_000_000n //,
      },
      refundRecipient: walletClient.account.address,
      bridgeAddress: '0xFC073319977e314F251EAE6ae6bE76B0B3BAeeCF',
    })

:::

### chain (optional)

*   **Type:** [`Chain`](https://viem.sh/docs/glossary/types#chain)
*   **Default:** `walletClient.chain`

The target chain. If there is a mismatch between the wallet's current chain & the target chain, an error will be thrown.

    import { zksync } from 'viem/chains'
     
    const hash = await walletClient.deposit({
      chain: zksync, 
      client: zksyncClient,
      token: '0x70a0F165d6f8054d0d0CF8dFd4DD2005f0AF6B55',
      amount: 20n,
      to: walletClient.account.address,
      approveToken: true,
      refundRecipient: walletClient.account.address,
    })</content>
</page>

<page>
  <title>recoverMessageAddress</title>
  <url>https://viem.sh/docs/utilities/recoverMessageAddress</url>
  <content>Recovers the original signing address from a message & signature.

Useful for obtaining the address of a message that was signed with [`signMessage`](https://viem.sh/docs/actions/wallet/signMessage).

Usage
-----

    import { recoverMessageAddress } from 'viem';
    import { account, walletClient } from './config'
     
    const signature = await walletClient.signMessage({
      account,
      message: 'hello world',
    })
     
    const address = await recoverMessageAddress({ 
      message: 'hello world',
      signature,
    })

Returns
-------

[`Address`](https://viem.sh/docs/glossary/types#address)

The signing address.

Parameters
----------

### message

*   **Type:** `string | { raw: Hex | ByteArray }`

The message that was signed.

By default, viem verifies the UTF-8 representation of the message.

    const address = await recoverMessageAddress({ 
      message: 'hello world', 
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })

To verify the data representation of the message, you can use the `raw` attribute.

    const address = await recoverMessageAddress({ 
      message: { raw: '0x68656c6c6f20776f726c64' }, 
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })

### signature

*   **Type:** `Hex | ByteArray | Signature`

The signature of the message.

    const address = await recoverMessageAddress({ 
      message: 'hello world',
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })</content>
</page>

<page>
  <title>getAddress</title>
  <url>https://viem.sh/docs/utilities/getAddress</url>
  <content>**Warning**

EIP-1191 checksum addresses are generally not backwards compatible with the wider Ethereum ecosystem, meaning it will break when validated against an application/tool that relies on EIP-55 checksum encoding (checksum without chainId).

It is highly recommended to not use this feature unless you know what you are doing.

See more: [https://github.com/ethereum/EIPs/issues/1121](https://github.com/ethereum/EIPs/issues/1121)</content>
</page>

<page>
  <title>getContractAddress</title>
  <url>https://viem.sh/docs/utilities/getContractAddress</url>
  <content>Retrieves the contract address generated by the [`CREATE`](https://ethereum.stackexchange.com/a/68945) or [`CREATE2`](https://eips.ethereum.org/EIPS/eip-1014) opcode – invoked after deploying a contract to the network.

Import
------

    import { getContractAddress } from 'viem'

Usage
-----

    import { getContractAddress } from 'viem'
     
    getContractAddress({ 
      from: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b',
      nonce: 69420n
    })
    // '0xDf2e056f7062790dF95A472f691670717Ae7b1B6'

Returns
-------

[`Address`](https://viem.sh/docs/glossary/types#address)

The contract address.

Parameters
----------

### from (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The address the contract was deployed from.

    getContractAddress({
      from: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b', 
      nonce: 69420n
    })

### nonce (optional)

*   **Type:** [`Address`](https://viem.sh/docs/glossary/types#address)

The nonce of the transaction which deployed the contract.

    getContractAddress({
      from: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b',
      nonce: 69420n
    })

### opcode (optional)

*   **Type:** `"CREATE" | "CREATE2"`
*   **Default:** `"CREATE"`

The opcode to invoke the contract deployment. Defaults to `"CREATE"`.

[Learn more about `CREATE2`](https://eips.ethereum.org/EIPS/eip-1014).

    getContractAddress({
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      from: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b',
      opcode: 'CREATE2', 
      salt: toBytes('wagmi'),
    })

### bytecode (optional)

*   **Type:** `ByteArray` | [`Hex`](https://viem.sh/docs/glossary/types#hex)
*   **Only applicable for `opcode: 'CREATE2'` deployments**

The to-be-deployed contract’s bytecode

    getContractAddress({
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...', 
      from: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b',
      opcode: 'CREATE2',
      salt: toBytes('wagmi'),
    })

### bytecodeHash (optional)

*   **Type:** `ByteArray` | [`Hex`](https://viem.sh/docs/glossary/types#hex)
*   **Only applicable for `opcode: 'CREATE2'` deployments**

A hash of the to-be-deployed contract’s bytecode

    getContractAddress({
      bytecodeHash: '0xe34f199b19b2b4f47f68442619d555527d244f78a3297ea89325f843f87b8b54', 
      from: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b',
      opcode: 'CREATE2',
      salt: toBytes('wagmi'),
    })

### salt (optional)

*   **Type:** `ByteArray` | [`Hex`](https://viem.sh/docs/glossary/types#hex)
*   **Only applicable for `opcode: 'CREATE2'` deployments**

An arbitrary value provided by the sender.

    getContractAddress({
      bytecode: '0x608060405260405161083e38038061083e833981016040819052610...',
      from: '0xc961145a54C96E3aE9bAA048c4F4D6b04C13916b',
      opcode: 'CREATE2',
      salt: toBytes('wagmi'), 
    })</content>
</page>

<page>
  <title>isAddressEqual</title>
  <url>https://viem.sh/docs/utilities/isAddressEqual</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/isAddressEqual#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Checks if the given addresses (checksummed) are equal.

Import
------

    import { isAddressEqual } from 'viem'

Usage
-----

    import { isAddressEqual } from 'viem'
     
    isAddressEqual('0xa5cc3c03994db5b0d9a5eEdD10Cabab0813678ac', '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC') 
    // true

Returns
-------

`boolean`

Whether or not the addresses are equal.</content>
</page>

<page>
  <title>isAddress</title>
  <url>https://viem.sh/docs/utilities/isAddress</url>
  <content>Checks if the address is valid. By default, it also verifies whether the address is in checksum format.

Import
------

    import { isAddress } from 'viem'

Usage
-----

    import { isAddress } from 'viem'
     
    isAddress('0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC') 
    // true

Returns
-------

`boolean`

Whether or not the address is valid.

Parameters
----------

### address

*   **Type:** `string`

An Ethereum address.

### options.strict (optional)

*   **Type:** `boolean`
*   **Default:** `true`

Enables strict mode. If enabled, it also verifies whether the address is in checksum format.

    isAddress('0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac', { strict: false })
    // true
     
    isAddress('0xa5cc3c03994db5b0d9a5eedd10cabab0813678ac', { strict: true })
    // false
     
    isAddress('lol', { strict: false })
    // false</content>
</page>

<page>
  <title>blobsToProofs</title>
  <url>https://viem.sh/docs/utilities/blobsToProofs</url>
  <content>Compute the proofs for a list of blobs and their commitments.

Import
------

    import { blobsToProofs } from 'viem'

Usage
-----

    import { blobsToCommitments, blobsToProofs, toBlobs } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x...' })
    const commitments = blobsToCommitments({ blobs, kzg })
    const proofs = blobsToProofs({ blobs, commitments, kzg }) 

Returns
-------

`Hex[] | ByteArray[]`

Proofs from the input blobs and commitments.

Parameters
----------

### blobs

*   **Type:** `Hex[] | ByteArray[]`

Blobs to transform into proofs.

    import { blobsToCommitments, blobsToProofs, toBlobs } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x...' }) 
    const commitments = blobsToCommitments({ blobs, kzg })
     
    const proofs = blobsToProofs({ 
      blobs, 
      commitments, 
      kzg 
    })

### commitments

*   **Type:** `Hex[] | ByteArray[]`

Commitments corresponding to the input blobs.

    import { blobsToCommitments, blobsToProofs, toBlobs } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x...' })
    const commitments = blobsToCommitments({ blobs, kzg }) 
     
    const proofs = blobsToProofs({ 
      blobs,
      commitments,  
      kzg 
    })

### kzg

*   **Type:** `KZG`

KZG implementation. See [`setupKzg`](https://viem.sh/docs/utilities/setupKzg) for more information.

    import * as cKzg from 'c-kzg'
    import { blobsToProofs, setupKzg } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const blobs = toBlobs({ data: '0x...' })
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
    const commitments = blobsToCommitments({ blobs, kzg })
     
    const proofs = blobsToProofs({ 
      blobs,
      commitments,
      kzg, 
    })</content>
</page>

<page>
  <title>commitmentToVersionedHash</title>
  <url>https://viem.sh/docs/utilities/commitmentToVersionedHash</url>
  <content>Transform a commitment to it's versioned hash.

Import
------

    import { commitmentToVersionedHash } from 'viem'

Usage
-----

    import { 
      blobsToCommitments, 
      commitmentToVersionedHash, 
      toBlobs 
    } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x1234' })
    const [commitment] = blobsToCommitments({ blobs, kzg })
    const versionedHashes = commitmentToVersionedHash({  
      commitment,  
    }) 

Returns
-------

`Hex | ByteArray`

Versioned hash corresponding to the commitment.

Parameters
----------

### commitment

*   **Type:** `Hex | ByteArray`

Commitment to transform into a versioned hash.

    const blobs = toBlobs({ data: '0x1234' })
    const [commitment] = blobsToCommitments({ blobs, kzg })
    const versionedHashes = commitmentToVersionedHash({ 
      commitment,  
    })

### to

*   **Type:** `"bytes" | "hex"`

The output type.

    const blobs = toBlobs({ data: '0x1234' })
    const [commitment] = blobsToCommitments({ blobs, kzg })
    const versionedHashes = commitmentToVersionedHash({ 
      commitment, 
      to: 'bytes'
    })
    const versionedHashes: ByteArrayversionedHashes 
     

### version

*   **Type:** `number`
*   **Default:** `1`

Version to tag onto the hash. Defaults to `1`.

    const blobs = toBlobs({ data: '0x1234' })
    const [commitment] = blobsToCommitments({ blobs, kzg })
    const versionedHashes = commitmentToVersionedHash({ 
      commitment, 
      version: 69, 
    })</content>
</page>

<page>
  <title>commitmentsToVersionedHashes</title>
  <url>https://viem.sh/docs/utilities/commitmentsToVersionedHashes</url>
  <content>Transform a list of commitments to their versioned hashes.

Import
------

    import { commitmentsToVersionedHashes } from 'viem'

Usage
-----

    import { 
      blobsToCommitments, 
      commitmentsToVersionedHashes, 
      toBlobs 
    } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x1234' })
    const commitments = blobsToCommitments({ blobs, kzg })
    const versionedHashes = commitmentsToVersionedHashes({  
      commitments,  
    }) 

Returns
-------

`Hex[] | ByteArray[]`

List of versioned hashes corresponding to the input commitments.

Parameters
----------

### commitments

*   **Type:** `Hex[] | ByteArray[]`

List of commitments to transform into versioned hashes.

    const blobs = toBlobs({ data: '0x1234' })
    const commitments = blobsToCommitments({ blobs, kzg })
    const versionedHashes = commitmentsToVersionedHashes({ 
      commitments,  
      kzg, 
    })

### to

*   **Type:** `"bytes" | "hex"`

The output type.

    const blobs = toBlobs({ data: '0x1234' })
    const commitments = blobsToCommitments({ blobs, kzg })
    const versionedHashes = commitmentsToVersionedHashes({ 
      commitments, 
      to: 'bytes'
    })
    const versionedHashes: readonly ByteArray[]versionedHashes 
     

### version

*   **Type:** `number`
*   **Default:** `1`

Version to tag onto the hashes. Defaults to `1`.

    const blobs = toBlobs({ data: '0x1234' })
    const commitments = blobsToCommitments({ blobs, kzg })
    const versionedHashes = commitmentsToVersionedHashes({ 
      commitments, 
      version: 69, 
    })</content>
</page>

<page>
  <title>fromBlobs</title>
  <url>https://viem.sh/docs/utilities/fromBlobs</url>
  <content>Transforms Viem-shaped blobs into the originating data.

Import
------

    import { fromBlobs } from 'viem'

Usage
-----

    import { fromBlobs } from 'viem'
     
    const data = fromBlobs({ blobs: ['0x...'] })

Returns
-------

`Hex | ByteArray`

Data extracted from blobs.

Parameters
----------

### blobs

*   **Type:** `Hex[] | ByteArray[]`

Transforms blobs into the originating data.

    import { fromBlobs } from 'viem'
     
    const data = fromBlobs({ 
      blobs: ['0x...'] 
    })

### to

*   **Type:** `"bytes" | "hex"`

The output type.

    import { fromBlobs } from 'viem'
     
    const data = fromBlobs({ 
      blobs: ['0x...'],
      to: 'bytes'
    })
     
    data</content>
</page>

<page>
  <title>sidecarsToVersionedHashes</title>
  <url>https://viem.sh/docs/utilities/sidecarsToVersionedHashes</url>
  <content>Transforms a list of sidecars to their versioned hashes.

Import
------

    import { sidecarsToVersionedHashes } from 'viem'

Usage
-----

    import { toBlobSidecars, sidecarsToVersionedHashes } from 'viem'
    import { kzg } from './kzg'
     
    const sidecars = toBlobSidecars({ data: '0x...', kzg })
    const versionedHashes = sidecarsToVersionedHashes({ sidecars }) 

Returns
-------

`Hex[] | ByteArray[]`

Versioned hashes from the input sidecars.

Parameters
----------

### sidecars

*   **Type:** `BlobSidecars<Hex | ByteArray>`

Sidecars to transform to versioned hashes.

    import { toBlobSidecars, sidecarsToVersionedHashes } from 'viem'
    import { kzg } from './kzg'
     
    const sidecars = toBlobSidecars({ data: '0x...', kzg })
     
    const versionedHashes = sidecarsToVersionedHashes({ 
      sidecars, 
    })

### to

*   **Type:** `"bytes" | "hex"`

Commitments corresponding to the input blobs.

    import { toBlobSidecars, sidecarsToVersionedHashes } from 'viem'
    import { kzg } from './kzg'
     
    const sidecars = toBlobSidecars({ data: '0x...', kzg })
     
    const versionedHashes = sidecarsToVersionedHashes({ 
      sidecars,
      to: 'bytes', 
    })
    const versionedHashes: readonly ByteArray[]versionedHashes  
     

### version

*   **Type:** `number`
*   **Default:** `1`

Version to tag onto the hashes. Defaults to `1`.

    import { toBlobSidecars, sidecarsToVersionedHashes } from 'viem'
    import { kzg } from './kzg'
     
    const sidecars = toBlobSidecars({ data: '0x...', kzg })
     
    const versionedHashes = sidecarsToVersionedHashes({ 
      sidecars,
      version: 69, 
    })</content>
</page>

<page>
  <title>blobsToCommitments</title>
  <url>https://viem.sh/docs/utilities/blobsToCommitments</url>
  <content>Compute commitments from a list of blobs.

Import
------

    import { blobsToCommitments } from 'viem'

Usage
-----

    import { blobsToCommitments, toBlobs } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x1234' })
    const commitments = blobsToCommitments({ blobs, kzg }) 

Returns
-------

`Hex[] | ByteArray[]`

List of commitments corresponding to the input blobs.

Parameters
----------

### blobs

*   **Type:** `Hex[] | ByteArray[]`

List of blobs to transform into commitments.

    import { blobsToCommitments, toBlobs } from 'viem'
     
    const commitments = blobsToCommitments({ 
      blobs: toBlobs({ data: '0x1234' }), 
      kzg, 
    }) 

### kzg

*   **Type:** `KZG`

KZG implementation. See [`setupKzg`](https://viem.sh/docs/utilities/setupKzg) for more information.

    import * as cKzg from 'c-kzg'
    import { blobsToCommitments, setupKzg, toBlobs } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const commitments = blobsToCommitments({ 
      blobs: toBlobs({ data: '0x1234' }),  
      kzg, 
    }) 

### to

*   **Type:** `"bytes" | "hex"`

The output type.

    import { blobsToCommitments, toBlobs } from 'viem'
     
    const commitments = blobsToCommitments({ 
      blobs: toBlobs({ data: '0x1234' }),
      kzg, 
      to: 'bytes', 
    }) 
     
    const commitments: readonly ByteArray[]commitments</content>
</page>

<page>
  <title>toBlobs</title>
  <url>https://viem.sh/docs/utilities/toBlobs</url>
  <content>Transforms arbitrary data into Viem-shaped blobs.

Import
------

    import { toBlobs } from 'viem'

Usage
-----

    import { toBlobs } from 'viem'
     
    const blobs = toBlobs({ data: '0x...' })

Returns
-------

`Hex[] | ByteArray[]`

Blobs from the input data.

Parameters
----------

### data

*   **Type:** `Hex | ByteArray`

Data to transform into blobs.

    import { toBlobs } from 'viem'
     
    const blobs = toBlobs({ 
      data: '0x...'
    })

### to

*   **Type:** `"bytes" | "hex"`

The output type.

    import { toBlobs } from 'viem'
     
    const blobs = toBlobs({ 
      data: '0x...',
      to: 'bytes'
    })
     
    const blobs: readonly ByteArray[]blobs</content>
</page>

<page>
  <title>extractChain</title>
  <url>https://viem.sh/docs/utilities/extractChain</url>
  <content>Extracts a type-safe chain by ID from a set of chains.

Usage
-----

    import { extractChain } from 'viem'
    import { mainnet, base, optimism, zora } from 'viem/chains'
     
    const optimism = extractChain({
      chains: [mainnet, base, optimism, zora],
      id: 10,
    })
     
    optimism.id
    //       ^? (property) id: 10
    optimism.name
    //       ^? (property) name: "OP Mainnet"

It is also possible to use **all chains** from the `viem/chains` module:

    import { extractChain } from 'viem'
    import { mainnet, base, optimism, zora } from 'viem/chains'
    import * as chains from 'viem/chains'
     
    const optimism = extractChain({
      chains: [mainnet, base, optimism, zora], 
      chains: Object.values(chains), 
      id: 10,
    })
     
    optimism.id
    //       ^? (property) id: 10
    optimism.name
    //       ^? (property) name: "OP Mainnet"

Returns
-------

*   **Type:** `Chain` (inferred)

The extracted chain.

Parameters
----------

### chains

*   **Type:** `readonly Chain[]`

The set of chains where the chain will be extracted from.

### id

*   **Type:** `number`

The ID of the chain to extract.</content>
</page>

<page>
  <title>concat</title>
  <url>https://viem.sh/docs/utilities/concat</url>
  <content>Concatenates a set of hex values or byte arrays.

Install
-------

    import { concat } from 'viem'

Usage
-----

    import { concat } from 'viem'
     
    concat(['0x00000069', '0x00000420'])
    // 0x0000006900000420
     
    concat([new Uint8Array([69]), new Uint8Array([420])])
    // Uint8Array [69, 420]

Returns
-------

`Hex | ByteArray`

The concatenated value.</content>
</page>

<page>
  <title>toBlobSidecars</title>
  <url>https://viem.sh/docs/utilities/toBlobSidecars</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/toBlobSidecars#vocs-content)

Transforms arbitrary data (or blobs, commitments, & proofs) into a blob sidecar array.

Import
------

    import { toBlobSidecars } from 'viem'

Usage
-----

### With Arbitrary Data

You can generate blob sidecars from arbitrary data without having to compute the blobs, commitments, and proofs first (that's done internally).

    import { toBlobSidecars } from 'viem'
    import { kzg } from './kzg'
     
    const sidecars = toBlobSidecars({ data: '0x...', kzg }) 

### With Blobs, Commitments, and Proofs

Alternatively, you can reach for the lower-level API and insert the blobs, commitments, and proofs directly.

    import { 
      blobsToCommitments, 
      blobsToProofs,
      toBlobSidecars, 
      toBlobs 
    } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x...' })
    const commitments = blobsToCommitments({ blobs, kzg })
    const proofs = blobsToProofs({ blobs, commitments, kzg })
    const sidecars = toBlobSidecars({ blobs, commitments, proofs }) 

Returns
-------

`BlobSidecars`

Blob sidecars from the input data.

Parameters
----------

### blobs

*   **Type:** `Hex[] | ByteArray[]`

Blobs to transform into blob sidecars.

    import { 
      blobsToCommitments, 
      blobsToProofs,
      toBlobSidecars, 
      toBlobs 
    } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x...' }) 
    const commitments = blobsToCommitments({ blobs, kzg })
    const proofs = blobsToProofs({ blobs, commitments, kzg })
     
    const sidecars = toBlobSidecars({ 
      blobs, 
      commitments,
      proofs,
    })

### commitments

*   **Type:** `Hex[] | ByteArray[]`

Commitments corresponding to the input blobs.

    import { 
      blobsToCommitments, 
      blobsToProofs,
      toBlobSidecars, 
      toBlobs 
    } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x...' })
    const commitments = blobsToCommitments({ blobs, kzg }) 
    const proofs = blobsToProofs({ blobs, commitments, kzg })
     
    const sidecars = toBlobSidecars({ 
      blobs,
      commitments, 
      proofs,
    })

### data

*   **Type:** `Hex | ByteArray`

Data to transform into blob sidecars.

    import { toBlobSidecars } from 'viem'
    import { kzg } from './kzg'
     
    const sidecars = toBlobSidecars({ 
      data: '0x...', 
      kzg,
    })

### kzg

*   **Type:** `KZG`

KZG implementation. See [`setupKzg`](https://viem.sh/docs/utilities/setupKzg) for more information.

    import * as cKzg from 'c-kzg'
    import { toBlobSidecars, setupKzg } from 'viem'
    import { mainnetTrustedSetupPath } from 'viem/node'
     
    const kzg = setupKzg(cKzg, mainnetTrustedSetupPath) 
     
    const sidecars = toBlobSidecars({ 
      data: '0x...',
      kzg, 
    }) 

### proofs

*   **Type:** `Hex[] | ByteArray[]`

Proofs corresponding to the input blobs.

    import { 
      blobsToCommitments, 
      blobsToProofs,
      toBlobSidecars, 
      toBlobs 
    } from 'viem'
    import { kzg } from './kzg'
     
    const blobs = toBlobs({ data: '0x...' })
    const commitments = blobsToCommitments({ blobs, kzg })
    const proofs = blobsToProofs({ blobs, commitments, kzg }) 
     
    const sidecars = toBlobSidecars({ 
      blobs,
      commitments,
      proofs, 
    })

### to

*   **Type:** `"bytes" | "hex"`

The output type.

    import { toBlobSidecars, toBlobs } from 'viem'
     
    const sidecars = toBlobSidecars({ 
      data: '0x1234',
      kzg, 
      to: 'bytes', 
    }) 
     
    sidecars</content>
</page>

<page>
  <title>isBytes</title>
  <url>https://viem.sh/docs/utilities/isBytes</url>
  <content>Checks whether the value is a byte array or not.

Install
-------

    import { isBytes } from 'viem'

Usage
-----

    import { isBytes } from 'viem'
     
    isBytes(new Uint8Array([1, 69, 420]))
    // true
     
    isBytes([1, 69, 420])
    // false

Returns
-------

`boolean`

Returns truthy is the value is a byte array.</content>
</page>

<page>
  <title>isHex</title>
  <url>https://viem.sh/docs/utilities/isHex</url>
  <content>Checks whether the value is a hex value or not.

Install
-------

    import { isHex } from 'viem'

Usage
-----

    import { isHex } from 'viem'
     
    isHex('0x1a4')
    // true
     
    isHex('0x1a4z')
    isHex('foo')
    // false

Returns
-------

`boolean`

Returns truthy is the value is a hex value.

Parameters
----------

### value

*   **Type:** `unknown`

The value to check.

### options.strict

*   **Type:** `boolean`
*   **Default:** `true`

When enabled, checks if the value strictly consists of only hex characters (`"0x[0-9a-fA-F]*"`). When disabled, checks if the value loosely matches hex format (`value.startsWith('0x')`).

    isHex('0xlol', { strict: false })
    // true
     
    isHex('0xlol', { strict: true })
    // false
     
    isHex('lol', { strict: false })
    // false</content>
</page>

<page>
  <title>pad</title>
  <url>https://viem.sh/docs/utilities/pad</url>
  <content>Pads a hex value or byte array with leading or trailing zeros.

Install
-------

    import { pad } from 'viem'

Usage
-----

By default, `pad` will pad a value with leading zeros up to 32 bytes (64 hex chars).

    import { pad } from 'viem'
     
    pad('0xa4e12a45')
    // 0x00000000000000000000000000000000000000000000000000000000a4e12a45
     
    pad(new Uint8Array([1, 122, 51, 123]))
    // Uint8Array [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,122,51,123]

Returns
-------

`Hex | ByteArray`

The value with padded zeros.

Parameters
----------

### dir

*   **Type:** `"left" | "right"`
*   **Default:** `"left"`

The direction in which to pad the zeros – either leading (left), or trailing (right).

    pad('0xa4e12a45', {
      dir: 'right'
    })
    // 0xa4e12a4500000000000000000000000000000000000000000000000000000000

### size

*   **Type:** `number`
*   **Default:** `32`

Size (in bytes) of the targeted value.

    pad('0xa4e12a45', {
      size: 16
    })
    // 0x000000000000000000000000a4e12a45</content>
</page>

<page>
  <title>trim</title>
  <url>https://viem.sh/docs/utilities/trim</url>
  <content>Trims the leading or trailing zero byte data from a hex value or byte array.

Install
-------

    import { trim } from 'viem'

Usage
-----

By default, `trim` will trim the leading zero byte data from a hex value or byte array.

    import { trim } from 'viem'
     
    trim('0x00000000000000000000000000000000000000000000000000000001a4e12a45')
    // 0x01a4e12a45
     
    trim(new Uint8Array([0, 0, 0, 0, 0, 0, 1, 122, 51, 123]))
    // Uint8Array [1,122,51,123]

Returns
-------

`Hex | ByteArray`

The trimmed value.

Parameters
----------

### dir

*   **Type:** `"left" | "right"`
*   **Default:** `"left"`

The direction in which to trim the zero byte data – either leading (left), or trailing (right).

    trim('0xa4e12a4510000000000000000000000000000000000000000000000000000000', {
      dir: 'right'
    })
    // 0xa4e12a4510</content>
</page>

<page>
  <title>size</title>
  <url>https://viem.sh/docs/utilities/size</url>
  <content>Retrieves the size of the value (in bytes).

Install
-------

    import { size } from 'viem'

Usage
-----

    import { size } from 'viem'
     
    size('0xa4') // 1
    size('0xa4e12a45') // 4
    size(new Uint8Array([1, 122, 51, 123])) // 4

Returns
-------

`number`

The size of the value (in bytes).

Parameters
----------

### value

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex) | `ByteArray`

The value (hex or byte array) to retrieve the size of.</content>
</page>

<page>
  <title>fromRlp</title>
  <url>https://viem.sh/docs/utilities/fromRlp</url>
  <content>Decodes a [Recursive-Length Prefix (RLP)](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp) value into a decoded hex value or byte array.

Import
------

    import { fromRlp } from 'viem'

Usage
-----

    import { fromRlp } from 'viem'
     
    fromRlp('0x850123456789', 'hex')
    // "0x123456789"
     
    fromRlp('0xc67f7f838081e8', 'hex')
    // ['0x7f', '0x7f', '0x8081e8']
     
    fromRlp('0x89010203040506070809', 'bytes')
    //  Uint8Array [1, 2, 3, 4, 5, 6, 7, 8, 9]
     
    fromRlp(new Uint8Array ([133, 1, 35, 69, 103, 137]), 'hex')
    // "0x123456789"

Returns
-------

`Hex | ByteArray`

The hex value or byte array.

Parameters
----------

### value

*   **Type:** `Hex | ByteArray`

The RLP value to decode.

### to

*   **Type:** `"bytes" | "hex"`

The output type.</content>
</page>

<page>
  <title>slice</title>
  <url>https://viem.sh/docs/utilities/slice</url>
  <content>Returns a section of the hex or byte array given a start/end bytes offset.

Install
-------

    import { slice } from 'viem'

Usage
-----

    import { slice } from 'viem'
     
    slice('0x0123456789', 1, 4)
    // 0x234567
     
    slice(new Uint8Array([1, 122, 51, 123]), 1, 3)
    // Uint8Array [122, 51]

Returns
-------

`Hex | ByteArray`

The section of the sliced value.

Parameters
----------

### value

*   **Type:** `Hex | ByteArray`

The hex or byte array to slice.

    slice(
      '0x0123456789', 
      1,
      4
    )

### start (optional)

*   **Type:** `number`

The start offset (in bytes).

    slice(
      '0x0123456789', 
      1
    )

### end (optional)

*   **Type:** `number`

The end offset (in bytes).

    slice(
      '0x0123456789', 
      1,
      4
    )

#### options.strict (optional)

*   **Type:** `boolean`
*   **Default:** `false`

Whether or not the end offset should be inclusive of the bounds of the data.

    slice('0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678', 0, 20, { strict: true })
    // [SliceOffsetOutOfBoundsError] Slice ending at offset "20" is out-of-bounds (size: 19).
     
    slice('0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC', 0, 20, { strict: true })
    // 0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC</content>
</page>

<page>
  <title>fromHex</title>
  <url>https://viem.sh/docs/utilities/fromHex</url>
  <content>Decodes a hex value to a string, number or byte array.

Shortcut Functions:

*   [hexToNumber](https://viem.sh/docs/utilities/fromHex#hextonumber)
*   [hexToBigInt](https://viem.sh/docs/utilities/fromHex#hextobigint)
*   [hexToString](https://viem.sh/docs/utilities/fromHex#hextostring)
*   [hexToBytes](https://viem.sh/docs/utilities/fromHex#hextobytes)
*   [hexToBool](https://viem.sh/docs/utilities/fromHex#hextobool)

Import
------

    import { fromHex } from 'viem'

Usage
-----

    import { fromHex } from 'viem'
     
    fromHex('0x1a4', 'number')
    // 420
     
    fromHex('0xc5cf39211876fb5e5884327fa56fc0b75', 'bigint')
    // 4206942069420694206942069420694206942069n
     
    fromHex('0x48656c6c6f20776f726c642e', 'string')
    // "Hello world"
     
    fromHex('0x48656c6c6f20576f726c6421', 'bytes')
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
     
    fromHex('0x1', 'boolean')
    // true

Returns
-------

`string | bigint | number | ByteArray`

The targeted type.

Parameters
----------

### hex

*   **Type:** `Hex`

The hex value to decode.

### toOrOptions

*   **Type:** `"string" | "hex" | "number" | "bigint" | "boolean" | Options`

The output type or options.

    fromHex(
      '0x48656c6c6f20776f726c642e', 
      'string'
    )
    // 'Hello world'

    fromHex(
      '0x48656c6c6f20776f726c642e0000000000000000000000000000000000000000', 
      { 
        size: 32, 
        to: 'string'
      } 
    )
    // 'Hello world'

Shortcut Functions
------------------

### hexToNumber

*   **Type:** `Hex`

Decodes a hex value to a number.

    import { hexToNumber } from 'viem'
     
    hexToNumber('0x1a4')
    // 420
     
    hexToNumber(
      '0x00000000000000000000000000000000000000000000000000000000000001a4', 
      { size: 32 }
    )
    // 420

### hexToBigInt

*   **Type:** `Hex`

Decodes a hex value to a bigint.

    import { hexToBigInt } from 'viem'
     
    hexToBigInt('0xc5cf39211876fb5e5884327fa56fc0b75')
    // 4206942069420694206942069420694206942069n
     
    hexToBigInt(
      '0x0000000000000000000000000000000c5cf39211876fb5e5884327fa56fc0b75', 
      { size: 32 }
    )
    // 4206942069420694206942069420694206942069n

### hexToString

*   **Type:** `Hex`

Decodes a hex value to a string.

    import { hexToString } from 'viem'
     
    hexToString('0x48656c6c6f20576f726c6421')
    // "Hello World!"
     
    hexToString(
      '0x48656c6c6f20576f726c64210000000000000000000000000000000000000000',
      { size: 32 }
    )
    // "Hello World!"

### hexToBytes

*   **Type:** `Hex`

Decodes a hex value to a byte array.

    import { hexToBytes } from 'viem'
     
    hexToBytes('0x48656c6c6f20576f726c6421')
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
     
    hexToBytes(
      '0x48656c6c6f20576f726c64210000000000000000000000000000000000000000',
      { size: 32 }
    )
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

### hexToBool

*   **Type:** `Hex`

Decodes a hex value to a boolean.

    import { hexToBool } from 'viem'
     
    hexToBool('0x1')
    // true
     
    hexToBool(
      '0x00000000000000000000000000000000000000000000000000000000000001',
      { size: 32 }
    )
    // true</content>
</page>

<page>
  <title>fromBytes</title>
  <url>https://viem.sh/docs/utilities/fromBytes</url>
  <content>Decodes a byte array to a string, hex value, boolean or number.

Shortcut Functions:

*   [bytesToHex](https://viem.sh/docs/utilities/fromBytes#bytestohex)
*   [bytesToString](https://viem.sh/docs/utilities/fromBytes#bytestostring)
*   [bytesToNumber](https://viem.sh/docs/utilities/fromBytes#bytestonumber)
*   [bytesToBigInt](https://viem.sh/docs/utilities/fromBytes#bytestobigint)
*   [bytesToBool](https://viem.sh/docs/utilities/fromBytes#bytestobool)

Import
------

    import { fromBytes } from 'viem'

Usage
-----

    import { fromBytes } from 'viem'
     
    fromBytes(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33]), 
      'string'
    )
    // 'Hello world'
     
    fromBytes(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33]), 
      'hex'
    )
    // '0x48656c6c6f20576f726c6421'
     
    fromBytes(new Uint8Array([1, 164]), 'number')
    // 420
     
    fromBytes(new Uint8Array([1]), 'boolean')
    // true

Returns
-------

`string | Hex | number | bigint | boolean`

The targeted type.

Parameters
----------

### value

*   **Type:** `ByteArray`

The byte array to decode.

### toOrOptions

*   **Type:** `"string" | "hex" | "number" | "bigint" | "boolean" | Options`

The output type or options.

    fromBytes(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33]), 
      'string'
    )
    // 'Hello world'

    fromBytes(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]), 
      { 
        size: 32, 
        to: 'string'
      } 
    )
    // 'Hello world'

Shortcut Functions
------------------

### bytesToHex

*   **Type:** `Hex`

Decodes a byte array to a hex value.

    import { bytesToHex } from 'viem'
     
    bytesToHex( 
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
    )
    // '0x48656c6c6f20576f726c6421'
     
    bytesToHex( 
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]), 
      { size: 32 }
    )
    // '0x48656c6c6f20576f726c64210000000000000000000000000000000000000000'

### bytesToString

*   **Type:** `Hex`

Decodes a byte array to a string.

    import { bytesToString } from 'viem'
     
    bytesToString( 
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
    )
    // 'Hello world'
     
    bytesToString( 
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]), 
      { size: 32 }
    )
    // 'Hello world'

### bytesToNumber

*   **Type:** `number`

Decodes a byte array to a number.

    import { bytesToNumber } from 'viem'
     
    bytesToNumber(new Uint8Array([1, 164])) 
    // 420
     
    bytesToNumber( 
      new Uint8Array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 164]), 
      { size: 32 }
    )
    // 420

### bytesToBigInt

*   **Type:** `number`

Decodes a byte array to a number.

    import { bytesToBigInt } from 'viem'
     
    bytesToBigInt( 
      new Uint8Array([12, 92, 243, 146, 17, 135, 111, 181, 229, 136, 67, 39, 250, 86, 252, 11, 117])
    )
    // 4206942069420694206942069420694206942069n
     
    bytesToBigInt( 
      new Uint8Array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 12, 92, 243, 146, 17, 135, 111, 181, 229, 136, 67, 39, 250, 86, 252, 11, 117]),
      { size: 32 }
    )
    // 4206942069420694206942069420694206942069n

### bytesToBool

*   **Type:** `boolean`

Decodes a byte array to a boolean.

    import { bytesToBool } from 'viem'
     
    bytesToBool(new Uint8Array([1])) 
    // true
     
    bytesToBool( 
      new Uint8Array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]),
      { size: 32 }
    ) 
    // true</content>
</page>

<page>
  <title>toRlp</title>
  <url>https://viem.sh/docs/utilities/toRlp</url>
  <content>Encodes a hex value or byte array into a [Recursive-Length Prefix (RLP)](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp/) encoded value.

Import
------

    import { toRlp } from 'viem'

Usage
-----

    import { toRlp } from 'viem'
     
    toRlp('0x123456789')
    // "0x850123456789"
     
    toRlp(['0x7f', '0x7f', '0x8081e8'])
    // "0xc67f7f838081e8"
     
    toRlp(new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9]))
    // "0x89010203040506070809"
     
    toRlp('0x123456789', 'bytes')
    // Uint8Array [133, 1, 35, 69, 103, 137]

Returns
-------

`Hex | ByteArray`

The hex value or byte array.

Parameters
----------

### value

*   **Type:** `Hex | ByteArray`

The value to RLP encode.

### to

*   **Type:** `"bytes" | "hex"`
*   **Default:** `"hex"`

The output type.

    toRlp('0x123456789', 'bytes')
    // Uint8Array [133, 1, 35, 69, 103, 137]</content>
</page>

<page>
  <title>toBytes</title>
  <url>https://viem.sh/docs/utilities/toBytes</url>
  <content>Encodes a string, hex value, number or boolean to a byte array.

Shortcut Functions:

*   [hexToBytes](https://viem.sh/docs/utilities/toBytes#hextobytes)
*   [stringToBytes](https://viem.sh/docs/utilities/toBytes#stringtobytes)
*   [numberToBytes](https://viem.sh/docs/utilities/toBytes#numbertobytes)
*   [boolToBytes](https://viem.sh/docs/utilities/toBytes#booltobytes)

Import
------

    import { toBytes } from 'viem'

Usage
-----

    import { toBytes } from 'viem'
     
    toBytes('Hello world')
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
     
    toBytes('0x48656c6c6f20576f726c6421')
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
     
    toBytes(420)
    // Uint8Array([1, 164])
     
    toBytes(true)
    // Uint8Array([1])

Returns
-------

`ByteArray`

The byte array represented as a `Uint8Array`.

Parameters
----------

### value

*   **Type:** `string | Hex`

The value to encode as bytes.

    toBytes(
      'Hello world'
    )
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])

### options

    toBytes(
      'Hello world', 
      { size: 32 } 
    )
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

Shortcut Functions
------------------

### hexToBytes

*   **Type:** `Hex`

Encodes a hex value to a byte array.

    import { hexToBytes } from 'viem'
     
    hexToBytes('0x48656c6c6f20576f726c6421') 
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
     
    hexToBytes('0x48656c6c6f20576f726c6421', { size: 32 }) 
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

### stringToBytes

*   **Type:** `Hex`

Encodes a string to a byte array.

    import { stringToBytes } from 'viem'
     
    stringToBytes('Hello world') 
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
     
    stringToBytes('Hello world', { size: 32 }) 
    // Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

### numberToBytes

*   **Type:** `number | bigint`

Encodes a number to a byte array.

    import { numberToBytes } from 'viem'
     
    numberToBytes(420) 
    // Uint8Array([1, 164])
     
    numberToBytes(420, { size: 32 }) 
    // Uint8Array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 164])

### boolToBytes

*   **Type:** `boolean`

Encodes a boolean to a byte array.

    import { boolToBytes } from 'viem'
     
    boolToBytes(true) 
    // Uint8Array([1])
     
    boolToBytes(true, { size: 32 }) 
    // Uint8Array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1])</content>
</page>

<page>
  <title>keccak256</title>
  <url>https://viem.sh/docs/utilities/keccak256</url>
  <content>Calculates the [Keccak256](https://en.wikipedia.org/wiki/SHA-3) hash of a byte array or hex value.

This function is a re-export of `keccak_256` from [`@noble/hashes`](https://github.com/paulmillr/noble-hashes) – an audited & minimal JS hashing library.

Install
-------

    import { keccak256 } from 'viem'

Usage
-----

    import { keccak256 } from 'viem'
     
    keccak256(new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
    // 0x3ea2f1d0abf3fc66cf29eebb70cbd4e7fe762ef8a09bcc06c8edf641230afec0
     
    keccak256('0xdeadbeef')
    // 0xd4fd4e189132273036449fc9e11198c739161b4c0116a9a2dccdfa1c492006f1
     
    // hash utf-8 string
    keccak256(toHex('hello world'))
    // 0x3ea2f1d0abf3fc66cf29eebb70cbd4e7fe762ef8a09bcc06c8edf641230afec0

Returns
-------

`Hex | ByteArray`

The hashed value.

Parameters
----------

### value

*   **Type:** `Hex | ByteArray`

The hex value or byte array to hash.

### to

*   **Type:** `"bytes" | "hex"`
*   **Default:** `"hex"`

The output type.

    import { keccak256 } from 'viem'
     
    keccak256(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33],
      'bytes'
    )
    // Uint8Array [62, 162, 241, 208, 171, 243, 252, 102, 207, 41, 238, 187, 112, 203, 212, 231, 254, 118, 46, 248, 160, 155, 204, 6, 200, 237, 246, 65, 35, 10, 254, 192]</content>
</page>

<page>
  <title>toHex</title>
  <url>https://viem.sh/docs/utilities/toHex</url>
  <content>Encodes a string, number, boolean or byte array to a hex value value.

Shortcut Functions:

*   [numberToHex](https://viem.sh/docs/utilities/toHex#numbertohex)
*   [stringToHex](https://viem.sh/docs/utilities/toHex#stringtohex)
*   [bytesToHex](https://viem.sh/docs/utilities/toHex#bytestohex)
*   [boolToHex](https://viem.sh/docs/utilities/toHex#booltohex)

Import
------

    import { toHex } from 'viem'

Usage
-----

    import { toHex } from 'viem'
     
    toHex(420)
    // "0x1a4"
     
    toHex('Hello world')
    // "0x48656c6c6f20776f726c642e"
     
    toHex(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
    )
    // "0x48656c6c6f20576f726c6421"
     
    toHex(true)
    // "0x1"

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The hex value.

Parameters
----------

### value

*   **Type:** `string | number | bigint | ByteArray`

The value to hex encode.

    toHex(
      'Hello world'
    )
    // '0x48656c6c6f20776f726c642e'

### options

    toHex(
      'Hello world', 
      { size: 32 } 
    )
    // '0x48656c6c6f20776f726c642e0000000000000000000000000000000000000000'

Shortcut Functions
------------------

### numberToHex

*   **Type:** `number | bigint`

Encodes a number value to a hex value.

    import { numberToHex } from 'viem'
     
    numberToHex(420)
    // "0x1a4"
     
    numberToHex(4206942069420694206942069420694206942069n)
    // "0xc5cf39211876fb5e5884327fa56fc0b75"
     
    numberToHex(420, { size: 32 })
    // "0x00000000000000000000000000000000000000000000000000000000000001a4"
     
    numberToHex(4206942069420694206942069420694206942069n, { size: 32 })
    // "0x0000000000000000000000000000000c5cf39211876fb5e5884327fa56fc0b75"

### stringToHex

*   **Type:** `string`

Encodes a UTF-8 string value to a hex value.

    import { stringToHex } from 'viem'
     
    stringToHex('Hello World!')
    // "0x48656c6c6f20576f726c6421"
     
    stringToHex('Hello World!', { size: 32 })
    // "0x48656c6c6f20576f726c64210000000000000000000000000000000000000000"

### bytesToHex

*   **Type:** `ByteArray`

Encodes a byte array to a hex value.

    import { bytesToHex } from 'viem'
     
    bytesToHex(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33]),
    )
    // "0x48656c6c6f20576f726c6421"
     
    bytesToHex(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33]),
      { size: 32 }
    )
    // "0x48656c6c6f20576f726c64210000000000000000000000000000000000000000"

### boolToHex

*   **Type:** `boolean`

Encodes a boolean to a hex value.

    import { boolToHex } from 'viem'
     
    boolToHex(true)
    // "0x1"
     
    boolToHex(true, { size: 32 })
    // "0x0000000000000000000000000000000000000000000000000000000000000001"</content>
</page>

<page>
  <title>ripemd160</title>
  <url>https://viem.sh/docs/utilities/ripemd160</url>
  <content>Calculates the [Ripemd160](https://en.wikipedia.org/wiki/RIPEMD) hash of a byte array or hex value.

This function is a re-export of `ripemd160` from [`@noble/hashes`](https://github.com/paulmillr/noble-hashes) – an audited & minimal JS hashing library.

Install
-------

    import { ripemd160 } from 'viem'

Usage
-----

    import { ripemd160 } from 'viem'
     
    ripemd160(new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
    // 0x8476ee4631b9b30ac2754b0ee0c47e161d3f724c
     
    ripemd160('0xdeadbeef')
    // 0x226821c2f5423e11fe9af68bd285c249db2e4b5a

Returns
-------

`Hex | ByteArray`

The hashed value.

Parameters
----------

### value

*   **Type:** `Hex | ByteArray`

The hex value or byte array to hash.

### to

*   **Type:** `"bytes" | "hex"`
*   **Default:** `"hex"`

The output type.

    import { ripemd160 } from 'viem'
     
    ripemd160(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33],
      'bytes'
    )
    // Uint8Array [132, 118, 238, 70, 49, 185, 179, 10, 194, 117, 75, 14, 224, 196, 126, 22, 29, 63, 114, 76]</content>
</page>

<page>
  <title>sha256</title>
  <url>https://viem.sh/docs/utilities/sha256</url>
  <content>Calculates the [Sha256](https://en.wikipedia.org/wiki/SHA-256) hash of a byte array or hex value.

This function is a re-export of `sha256` from [`@noble/hashes`](https://github.com/paulmillr/noble-hashes) – an audited & minimal JS hashing library.

Install
-------

    import { sha256 } from 'viem'

Usage
-----

    import { sha256 } from 'viem'
     
    sha256(new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33])
    // 0x7f83b1657ff1fc53b92dc18148a1d65dfc2d4b1fa3d677284addd200126d9069
     
    sha256('0xdeadbeef')
    // 0x5f78c33274e43fa9de5659265c1d917e25c03722dcb0b8d27db8d5feaa813953

Returns
-------

`Hex | ByteArray`

The hashed value.

Parameters
----------

### value

*   **Type:** `Hex | ByteArray`

The hex value or byte array to hash.

### to

*   **Type:** `"bytes" | "hex"`
*   **Default:** `"hex"`

The output type.

    import { sha256 } from 'viem'
     
    sha256(
      new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33],
      'bytes'
    )
    // Uint8Array [95, 120, 195, 50, 116, 228, 63, 169, 222, 86, 89, 38, 92, 29, 145, 126, 37, 192, 55, 34, 220, 176, 184, 210, 125, 184, 213, 254, 170, 129, 57, 83]</content>
</page>

<page>
  <title>toEventHash</title>
  <url>https://viem.sh/docs/utilities/toEventHash</url>
  <content>Returns the hash (of the event signature) for a given event definition.

Install
-------

    import { toEventHash } from 'viem'

Usage
-----

    import { toEventHash } from 'viem'
     
    const hash_1 = toEventHash('event Transfer(address,address,uint256)')
    Output: 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef const hash_2 = toEventHash({
      name: 'Transfer',
      type: 'event',
      inputs: [
        { name: 'from', type: 'address', indexed: true },
        { name: 'to', type: 'address', indexed: true },
        { name: 'amount', type: 'uint256', indexed: false },
      ],
    })
    Output: 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The hash of the event signature.

Parameters
----------

### event

*   **Type:** `string` | [`AbiEvent`](https://abitype.dev/api/types#abievent)

The event to generate a hash for.</content>
</page>

<page>
  <title>toEventSelector</title>
  <url>https://viem.sh/docs/utilities/toEventSelector</url>
  <content>Returns the event selector for a given event definition.

Install
-------

    import { toEventSelector } from 'viem'

Usage
-----

    import { toEventSelector } from 'viem'
     
    const selector_1 = toEventSelector('Transfer(address,address,uint256)')
    Output: 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef const selector_2 = toEventSelector('Transfer(address indexed from, address indexed to, uint256 amount)')
    Output: 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef // or from an `AbiEvent` on your contract ABI
    const selector_3 = toEventSelector({
      name: 'Transfer',
      type: 'event',
      inputs: [
        { name: 'from', type: 'address', indexed: true },
        { name: 'to', type: 'address', indexed: true },
        { name: 'amount', type: 'uint256', indexed: false },
      ],
    })
    Output: 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The selector as a hex value.

Parameters
----------

### event

*   **Type:** `string |`[`AbiEvent`](https://abitype.dev/api/types#abievent)

The event to generate a selector for.</content>
</page>

<page>
  <title>toEventSignature</title>
  <url>https://viem.sh/docs/utilities/toEventSignature</url>
  <content>Returns the signature for a given event definition.

Install
-------

    import { toEventSignature } from 'viem'

Usage
-----

    import { toEventSignature } from 'viem'
     
    // from event definition
    const signature_1 = toEventSignature('event Transfer(address indexed from, address indexed to, uint256 amount)')
    Output: Transfer(address,address,uint256) // from an `AbiEvent` on your contract ABI
    const signature_2 = toEventSignature({
      name: 'Transfer',
      type: 'event',
      inputs: [
        { name: 'address', type: 'address', indexed: true },
        { name: 'address', type: 'address', indexed: true },
        { name: 'uint256', type: 'uint256', indexed: false },
      ],
    })
    Output: Transfer(address,address,uint256)

Returns
-------

`string`

The signature as a string value.

Parameters
----------

### definition

*   **Type:** `string | AbiEvent`

The event definition to generate a signature for.</content>
</page>

<page>
  <title>toFunctionHash</title>
  <url>https://viem.sh/docs/utilities/toFunctionHash</url>
  <content>Returns the hash (of the function signature) for a given function definition.

Install
-------

    import { toFunctionHash } from 'viem'

Usage
-----

    import { toFunctionHash } from 'viem'
     
    const hash_1 = toFunctionHash('function ownerOf(uint256)')
    Output: 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef // or from an `AbiEvent` on your contract ABI
    const hash_2 = toFunctionHash({
      name: 'ownerOf',
      type: 'function',
      inputs: [{ name: 'tokenId', type: 'uint256' }],
      outputs: [],
      stateMutability: 'view',
    })
    Output: 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The hash of the function signature.

Parameters
----------

### function

*   **Type:** `string` | [`AbiFunction`](https://abitype.dev/api/types#abifunction)

The function to generate a hash for.</content>
</page>

<page>
  <title>toFunctionSignature</title>
  <url>https://viem.sh/docs/utilities/toFunctionSignature</url>
  <content>Returns the signature for a given function definition.

Install
-------

    import { toFunctionSignature } from 'viem'

Usage
-----

    import { toFunctionSignature } from 'viem'
     
    // from function definition
    const signature_1 = toFunctionSignature('function ownerOf(uint256 tokenId)')
    Output: ownerOf(uint256) // from an `AbiFunction` on your contract ABI
    const signature_2 = toFunctionSignature({
      name: 'ownerOf',
      type: 'function',
      inputs: [{ name: 'tokenId', type: 'uint256' }],
      outputs: [],
      stateMutability: 'view',
    })
    Output: ownerOf(uint256)

Returns
-------

`string`

The signature as a string value.

Parameters
----------

### definition

*   **Type:** `string | AbiFunction`

The function definition to generate a signature for.</content>
</page>

<page>
  <title>compactSignatureToSignature</title>
  <url>https://viem.sh/docs/utilities/compactSignatureToSignature</url>
  <content>Parses a [EIP-2098](https://eips.ethereum.org/EIPS/eip-2098) compact signature into signature format.

Import
------

    import { compactSignatureToSignature } from 'viem'

Usage
-----

    import { compactSignatureToSignature } from 'viem'
     
    compactSignatureToSignature({ 
      r: '0x68a020a209d3d56c46f38cc50a33f704f4a9a10a59377f8dd762ac66910e9b90',
      yParityAndS:
        '0x7e865ad05c4035ab5792787d4a0297a43617ae897930a6fe4d822b8faea52064',
    })
    // {
    //   r: '0x68a020a209d3d56c46f38cc50a33f704f4a9a10a59377f8dd762ac66910e9b90',
    //   s: '0x7e865ad05c4035ab5792787d4a0297a43617ae897930a6fe4d822b8faea52064',
    //   yParity: 0,
    // }

Returns
-------

[`Signature`](https://viem.sh/docs/glossary/types#signature)

The signature.

Parameters
----------

### compactSignature

The compact signature.

*   **Type:** [`CompactSignature`](https://viem.sh/docs/glossary/types#CompactSignature)</content>
</page>

<page>
  <title>hashMessage</title>
  <url>https://viem.sh/docs/utilities/hashMessage</url>
  <content>Calculates an Ethereum-specific hash in [EIP-191 format](https://eips.ethereum.org/EIPS/eip-191): `keccak256("\x19Ethereum Signed Message:\n" + len(message) + message))`.

Import
------

    import { hashMessage } from 'viem'

Usage
-----

    import { hashMessage } from 'viem'
     
    hashMessage('hello world') 
    // 0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68
     
    // Hash a hex data value.  
    hashMessage({ raw: '0x68656c6c6f20776f726c64' })
    // 0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68
     
    // Hash a bytes data value.  
    hashMessage({ 
      raw: Uint8Array.from([
        104, 101, 108, 108, 111, 32, 119, 111, 114, 108, 100,
      ])})
    // 0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The hashed message.

Parameters
----------

### message

Message to hash.

*   **Type:** `string | { raw: Hex | ByteArray }`</content>
</page>

<page>
  <title>toFunctionSelector</title>
  <url>https://viem.sh/docs/utilities/toFunctionSelector</url>
  <content>Returns the function selector (4 byte encoding) for a given function definition.

Install
-------

    import { toFunctionSelector } from 'viem'

Usage
-----

    import { toFunctionSelector } from 'viem'
     
    const selector_1 = toFunctionSelector('function ownerOf(uint256 tokenId)')
    Output: 0x6352211e const selector_2 = toFunctionSelector('ownerOf(uint256)')
    Output: 0x6352211e // or from an `AbiFunction` on your contract ABI
    const selector_3 = toFunctionSelector({
      name: 'ownerOf',
      type: 'function',
      inputs: [{ name: 'tokenId', type: 'uint256' }],
      outputs: [],
      stateMutability: 'view',
    })
    Output: 0x6352211e

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The selector as a hex value.

Parameters
----------

### function

*   **Type:** `string |`[`AbiFunction`](https://abitype.dev/api/types#abifunction)

The function to generate a selector for.</content>
</page>

<page>
  <title>hashTypedData</title>
  <url>https://viem.sh/docs/utilities/hashTypedData</url>
  <content>Calculates an Ethereum-specific hash in [EIP-712 format](https://eips.ethereum.org/EIPS/eip-712): `keccak256("\x19\x01" ‖ domainSeparator ‖ hashStruct(message))`.

Import
------

    import { hashTypedData } from 'viem'

Usage
-----

    import { hashTypedData } from 'viem'
     
    hashTypedData({
      domain: {
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The hashed message.

Parameters
----------

### domain

**Type:** `TypedDataDomain`

The typed data domain.

    const hash = hashTypedData({
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### types

The type definitions for the typed data.

    const hash = hashTypedData({
      domain,
      types: { 
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### primaryType

**Type:** Inferred `string`.

The primary type to extract from `types` and use in `value`.

    const hash = hashTypedData({
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [ 
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })

### message

**Type:** Inferred from `types` & `primaryType`.

    const hash = hashTypedData({
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: { 
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
    })</content>
</page>

<page>
  <title>isErc6492Signature</title>
  <url>https://viem.sh/docs/utilities/isErc6492Signature</url>
  <content>Checks whether the signature is in [ERC-6492](https://eips.ethereum.org/EIPS/eip-6492) format.

Import
------

    import { isErc6492Signature } from 'viem/utils'

Usage
-----

    import { isErc6492Signature } from 'viem/utils'
     
    const result = isErc6492Signature('0x000000000000000000000000cafebabecafebabecafebabecafebabecafebabe000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000004deadbeef000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000041a461f509887bd19e312c0c58467ce8ff8e300d3c1a90b608a760c5b80318eaf15fe57c96f9175d6cd4daad4663763baa7e78836e067d0163e9a2ccf2ff753f5b1b000000000000000000000000000000000000000000000000000000000000006492649264926492649264926492649264926492649264926492649264926492')

Returns
-------

`boolean`

Whether the signature is in ERC-6492 format.

Parameters
----------

### signature

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The signature to check.</content>
</page>

<page>
  <title>parseErc6492Signature</title>
  <url>https://viem.sh/docs/utilities/parseErc6492Signature</url>
  <content>Parses a hex-formatted [ERC-6492](https://eips.ethereum.org/EIPS/eip-6492) flavoured signature.

If the signature is not in ERC-6492 format, then the underlying (original) signature is returned.

Import
------

    import { parseErc6492Signature } from 'viem/utils'

Usage
-----

    import { parseErc6492Signature } from 'viem/utils'
     
    const { 
      address,
      data,
      signature,
    } = parseErc6492Signature('0x000000000000000000000000cafebabecafebabecafebabecafebabecafebabe000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000004deadbeef000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000041a461f509887bd19e312c0c58467ce8ff8e300d3c1a90b608a760c5b80318eaf15fe57c96f9175d6cd4daad4663763baa7e78836e067d0163e9a2ccf2ff753f5b1b000000000000000000000000000000000000000000000000000000000000006492649264926492649264926492649264926492649264926492649264926492')
    /**
     * {
     *   address: '0xCafEBAbECAFEbAbEcaFEbabECAfebAbEcAFEBaBe',
     *   data: '0xdeadbeef',
     *   signature: '0xa461f509887bd19e312c0c58467ce8ff8e300d3c1a90b608a760c5b80318eaf15fe57c96f9175d6cd4daad4663763baa7e78836e067d0163e9a2ccf2ff753f5b1b'
     * }
     */

Returns
-------

`ParseErc6492SignatureReturnType`

The ERC-6492 signature components.

Parameters
----------

### signature

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)

The ERC-6492 signature in hex format.</content>
</page>

<page>
  <title>parseCompactSignature</title>
  <url>https://viem.sh/docs/utilities/parseCompactSignature</url>
  <content>Parses a hex formatted compact signature into a structured ("split") compact signature.

Import
------

    import { parseCompactSignature } from 'viem'

Usage
-----

    import { parseCompactSignature } from 'viem'
     
    parseCompactSignature('0x9328da16089fcba9bececa81663203989f2df5fe1faa6291a45381c81bd17f76939c6d6b623b42da56557e5e734a43dc83345ddfadec52cbe24d0cc64f550793') 
    /**
     * {
     *   r: '0x9328da16089fcba9bececa81663203989f2df5fe1faa6291a45381c81bd17f76',
     *   yParityAndS: '0x939c6d6b623b42da56557e5e734a43dc83345ddfadec52cbe24d0cc64f550793'
     * }
     */

Returns
-------

[`CompactSignature`](https://viem.sh/docs/glossary/types#compactsignature)

The structured ("split") compact signature.

Parameters
----------

### signatureHex

The compact signature in hex format.

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)</content>
</page>

<page>
  <title>parseSignature</title>
  <url>https://viem.sh/docs/utilities/parseSignature</url>
  <content>Parses a hex formatted signature into a structured ("split") signature.

Import
------

    import { parseSignature } from 'viem'

Usage
-----

    import { parseSignature } from 'viem'
     
    parseSignature('0x6e100a352ec6ad1b70802290e18aeed190704973570f3b8ed42cb9808e2ea6bf4a90a229a244495b41890987806fcbd2d5d23fc0dbe5f5256c2613c039d76db81c') 
    /**
     * {
     *   r: '0x6e100a352ec6ad1b70802290e18aeed190704973570f3b8ed42cb9808e2ea6bf',
     *   s: '0x4a90a229a244495b41890987806fcbd2d5d23fc0dbe5f5256c2613c039d76db8',
     *   yParity: 1
     * }
     */

Returns
-------

[`Signature`](https://viem.sh/docs/glossary/types#signature)

The structured ("split") signature.

Parameters
----------

### signatureHex

The signature in hex format.

*   **Type:** [`Hex`](https://viem.sh/docs/glossary/types#hex)</content>
</page>

<page>
  <title>recoverAddress</title>
  <url>https://viem.sh/docs/utilities/recoverAddress</url>
  <content>Recovers the original signing address from a hash & signature.

Usage
-----

    import { recoverAddress } from 'viem'
     
    const address = await recoverAddress({
      hash: '0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68',
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })
    // 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266

Returns
-------

[`Address`](https://viem.sh/docs/glossary/types#address)

The signing address.

Parameters
----------

### hash

*   **Type:** `string`

The hash that was signed.

    const address = await recoverAddress({ 
      hash: '0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68', 
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })

### signature

*   **Type:** `Hex | ByteArray | Signature`

The signature of the hash.

    const address = await recoverAddress({ 
      hash: '0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68',
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })</content>
</page>

<page>
  <title>recoverPublicKey</title>
  <url>https://viem.sh/docs/utilities/recoverPublicKey</url>
  <content>Recovers the original signing 64-byte public key from a hash & signature.

Usage
-----

    import { recoverPublicKey } from 'viem'
     
    const publicKey = await recoverPublicKey({
      hash: '0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68',
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })
    // 0x048318535b54105d4a7aae60c08fc45f9687181b4fdfc625bd1a753fa7397fed753547f11ca8696646f2f3acb08e31016afac23e630c5d11f59f61fef57b0d2aa5

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The signing public key.

Parameters
----------

### hash

*   **Type:** `string`

The hash that was signed.

    const publicKey = await recoverPublicKey({ 
      hash: '0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68', 
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })

### signature

*   **Type:** `Hex | ByteArray | Signature`

The signature of the hash.

    const publicKey = await recoverPublicKey({ 
      hash: '0xd9eba16ed0ecae432b71fe008c98cc872bb4cc214d3220a36f365326cf807d68',
      signature: '0x66edc32e2ab001213321ab7d959a2207fcef5190cc9abb6da5b0d2a8a9af2d4d2b0700e2c317c4106f337fd934fbbb0bf62efc8811a78603b33a8265d3b8f8cb1c'
    })</content>
</page>

<page>
  <title>recoverTransactionAddress</title>
  <url>https://viem.sh/docs/utilities/recoverTransactionAddress</url>
  <content>Recovers the original signing address from a transaction & signature.

    import { recoverTransactionAddress } from 'viem'
    import { walletClient } from './client'
     
    const request = await walletClient.prepareTransactionRequest({
      to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8',
      value: 1000000000000000000n
    })
     
    const serializedTransaction = await walletClient.signTransaction(request)
     
    const address = await recoverTransactionAddress({ 
      serializedTransaction,
    })

The signing address.

The RLP serialized transaction.

The signature.</content>
</page>

<page>
  <title>recoverTypedDataAddress</title>
  <url>https://viem.sh/docs/utilities/recoverTypedDataAddress</url>
  <content>Recovers the original signing address from EIP-712 typed data & signature.

Useful for obtaining the address of a message that was signed with [`signTypedData`](https://viem.sh/docs/actions/wallet/signTypedData).

Usage
-----

    import { recoverTypedDataAddress } from 'viem'
    import { account, walletClient } from './client'
     
    const message = {
      from: {
        name: 'Cow',
        wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
      },
      to: {
        name: 'Bob',
        wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
      },
      contents: 'Hello, Bob!',
    } as const
     
    const signature = await walletClient.signTypedData({
      account,
      domain,
      types,
      primaryType: 'Mail',
      message,
    })
     
    const address = await recoverTypedDataAddress({ 
      domain,
      types,
      primaryType: 'Mail',
      message,
      signature,
    })

Returns
-------

[`Address`](https://viem.sh/docs/glossary/types#address)

The signing address.

Parameters
----------

### domain

**Type:** `TypedDataDomain`

The typed data domain.

    const address = await recoverTypedDataAddress({
      domain: { 
        name: 'Ether Mail',
        version: '1',
        chainId: 1,
        verifyingContract: '0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC',
      },
      types,
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...'
    })

### types

The type definitions for the typed data.

    const address = await recoverTypedDataAddress({
      domain,
      types: { 
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail',
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...'
    })

### primaryType

**Type:** Inferred `string`.

The primary type to extract from `types` and use in `value`.

    const address = await recoverTypedDataAddress({
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [ 
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: {
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...'
    })

### message

**Type:** Inferred from `types` & `primaryType`.

    const address = await recoverTypedDataAddress({
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: { 
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...'
    })

### signature

*   **Type:** `Hex | ByteArray`

The signature of the typed data.

    const address = await recoverTypedDataAddress({
      domain,
      types: {
        Person: [
          { name: 'name', type: 'string' },
          { name: 'wallet', type: 'address' },
        ],
        Mail: [
          { name: 'from', type: 'Person' },
          { name: 'to', type: 'Person' },
          { name: 'contents', type: 'string' },
        ],
      },
      primaryType: 'Mail', 
      message: { 
        from: {
          name: 'Cow',
          wallet: '0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826',
        },
        to: {
          name: 'Bob',
          wallet: '0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB',
        },
        contents: 'Hello, Bob!',
      },
      signature: '0x...'
    })</content>
</page>

<page>
  <title>serializeCompactSignature</title>
  <url>https://viem.sh/docs/utilities/serializeCompactSignature</url>
  <content>Serializes a [EIP-2098](https://eips.ethereum.org/EIPS/eip-2098) compact signature into hex format.

Import
------

    import { serializeCompactSignature } from 'viem'

Usage
-----

    import { serializeCompactSignature } from 'viem'
     
    serializeCompactSignature({ 
      r: '0x68a020a209d3d56c46f38cc50a33f704f4a9a10a59377f8dd762ac66910e9b90',
      yParityAndS:
        '0x7e865ad05c4035ab5792787d4a0297a43617ae897930a6fe4d822b8faea52064',
    })
    // "0x68a020a209d3d56c46f38cc50a33f704f4a9a10a59377f8dd762ac66910e9b907e865ad05c4035ab5792787d4a0297a43617ae897930a6fe4d822b8faea52064"

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The hex formatted signature.

Parameters
----------

### compactSignature

The compact signature.

*   **Type:** [`CompactSignature`](https://viem.sh/docs/glossary/types#CompactSignature)</content>
</page>

<page>
  <title>serializeSignature</title>
  <url>https://viem.sh/docs/utilities/serializeSignature</url>
  <content>Serializes a structured signature into hex format.

Import
------

    import { serializeSignature } from 'viem'

Usage
-----

    import { serializeSignature } from 'viem'
     
    serializeSignature({
      r: '0x6e100a352ec6ad1b70802290e18aeed190704973570f3b8ed42cb9808e2ea6bf',
      s: '0x4a90a229a244495b41890987806fcbd2d5d23fc0dbe5f5256c2613c039d76db8',
      yParity: 1
    }) 
    // "0x6e100a352ec6ad1b70802290e18aeed190704973570f3b8ed42cb9808e2ea6bf4a90a229a244495b41890987806fcbd2d5d23fc0dbe5f5256c2613c039d76db81c"

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The hex formatted signature.

Parameters
----------

### signature

The signature.

*   **Type:** [`Signature`](https://viem.sh/docs/glossary/types#signature)</content>
</page>

<page>
  <title>formatGwei</title>
  <url>https://viem.sh/docs/utilities/formatGwei</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/formatGwei#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Converts numerical wei to a string representation of gwei.

Import
------

    import { formatGwei } from 'viem'

Usage
-----

    import { formatGwei } from 'viem'
     
    formatGwei(1000000000n) 
    // '1'

Returns
-------

`string`

Parameters
----------

### value

*   **Type:** `bigint`

The wei value.</content>
</page>

<page>
  <title>serializeErc6492Signature</title>
  <url>https://viem.sh/docs/utilities/serializeErc6492Signature</url>
  <content>Serializes a [ERC-6492](https://eips.ethereum.org/EIPS/eip-6492) flavoured signature into hex format.

Import
------

    import { serializeErc6492Signature } from 'viem/utils'

Usage
-----

    import { serializeErc6492Signature } from 'viem/utils'
     
    serializeErc6492Signature({ 
      address: '0xcafebabecafebabecafebabecafebabecafebabe',
      data: '0xdeadbeef',
      signature: '0x41a461f509887bd19e312c0c58467ce8ff8e300d3c1a90b608a760c5b80318eaf15fe57c96f9175d6cd4daad4663763baa7e78836e067d0163e9a2ccf2ff753f5b1b',
    })
    // "0x000000000000000000000000cafebabecafebabecafebabecafebabecafebabe000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000004deadbeef000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000041a461f509887bd19e312c0c58467ce8ff8e300d3c1a90b608a760c5b80318eaf15fe57c96f9175d6cd4daad4663763baa7e78836e067d0163e9a2ccf2ff753f5b1b000000000000000000000000000000000000000000000000000000000000006492649264926492649264926492649264926492649264926492649264926492"

Returns
-------

[`Hex`](https://viem.sh/docs/glossary/types#hex)

The hex formatted signature.

Parameters
----------

### address

*   **Type:** `Address`

The ERC-4337 Account Factory or preparation address to use for counterfactual verification.

### data

*   **Type:** `Hex`

Calldata to pass to deploy the ERC-4337 Account (if not deployed) for counterfactual verification.

### signature

*   **Type:** `Hex`

The original signature.</content>
</page>

<page>
  <title>signatureToCompactSignature</title>
  <url>https://viem.sh/docs/utilities/signatureToCompactSignature</url>
  <content>Parses a signature into a [EIP-2098](https://eips.ethereum.org/EIPS/eip-2098) compact signature.

Import
------

    import { signatureToCompactSignature } from 'viem'

Usage
-----

    import { signatureToCompactSignature, Signature } from 'viem'
     
    signatureToCompactSignature({  
      r: '0x68a020a209d3d56c46f38cc50a33f704f4a9a10a59377f8dd762ac66910e9b90',
      s: '0x7e865ad05c4035ab5792787d4a0297a43617ae897930a6fe4d822b8faea52064' 
      yParity: 0
    })
    // {
    //   r: '0x68a020a209d3d56c46f38cc50a33f704f4a9a10a59377f8dd762ac66910e9b90',
    //   yParityAndS: '0x7e865ad05c4035ab5792787d4a0297a43617ae897930a6fe4d822b8faea52064',
    // }

Returns
-------

[`CompactSignature`](https://viem.sh/docs/glossary/types#compactsignature)

The compact signature.

Parameters
----------

### signature

The signature.

*   **Type:** [`Signature`](https://viem.sh/docs/glossary/types#signature)</content>
</page>

<page>
  <title>parseGwei</title>
  <url>https://viem.sh/docs/utilities/parseGwei</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/parseGwei#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Converts a string representation of gwei to numerical wei.

Import
------

    import { parseGwei } from 'viem'

Usage
-----

    import { parseGwei } from 'viem'
     
    parseGwei('420') 
    // 420000000000n

Returns
-------

`bigint`

Parameters
----------

### value

*   **Type:** `string`

The string representation of gwei.</content>
</page>

<page>
  <title>parseEther</title>
  <url>https://viem.sh/docs/utilities/parseEther</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/parseEther#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Converts a string representation of ether to numerical wei.

Import
------

    import { parseEther } from 'viem'

Usage
-----

    import { parseEther } from 'viem'
     
    parseEther('420') 
    // 420000000000000000000n

Returns
-------

`bigint`

Parameters
----------

### value

*   **Type:** `string`

The string representation of ether.</content>
</page>

<page>
  <title>formatUnits</title>
  <url>https://viem.sh/docs/utilities/formatUnits</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/formatUnits#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Divides a number by a given exponent of base 10 (10exponent), and formats it into a string representation of the number.

Import
------

    import { formatUnits } from 'viem'

Usage
-----

    import { formatUnits } from 'viem'
     
    formatUnits(420000000000n, 9) 
    // '420'

Returns
-------

`string`

Parameters
----------

### value

*   **Type:** `bigint`

The number to divide.

### exponent

*   **Type:** `number`

The exponent.</content>
</page>

<page>
  <title>parseUnits</title>
  <url>https://viem.sh/docs/utilities/parseUnits</url>
  <content>[Skip to content](https://viem.sh/docs/utilities/parseUnits#vocs-content)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

[Docs](https://viem.sh/docs/getting-started)

[Examples](https://github.com/wevm/viem/tree/main/examples)

Multiplies a string representation of a number by a given exponent of base 10 (10exponent).

Import
------

    import { parseUnits } from 'viem'

Usage
-----

    import { parseUnits } from 'viem'
     
    parseUnits('420', 9) 
    // 420000000000n

Returns
-------

`bigint`

Parameters
----------

### value

*   **Type:** `string`

The string representation of the number to multiply.

### exponent

*   **Type:** `number`

The exponent.</content>
</page>