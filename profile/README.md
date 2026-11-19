# x402-avm

SDKs for paying for APIs and AI tools per call on Algorand, using the x402 protocol (HTTP 402 Payment Required). No accounts, API keys or subscriptions: the server names a price, the client pays, and the payment settles only if the tool succeeds.

## Packages

| Package | What it does | Install |
|---|---|---|
| [`ai-economy-sdk`](https://github.com/x402-avm/ai-economy-sdk) | Python. Turns an MCP server into a paid service and pays for tools as a client, with spend controls. | `pip install ai-economy-sdk` |
| [`x402-algorand`](https://github.com/x402-avm/x402-algorand) | Python. The Algorand exact payment scheme for the official x402 SDK. | `pip install x402-algorand` |
| [`x402-avm-js`](https://github.com/x402-avm/x402-avm-js) | TypeScript. Pays 402 responses from the browser or Node with any Algorand wallet. | `npm install x402-avm-js algosdk` |

Works on MainNet, TestNet, LocalNet and private networks, with ALGO or USDC.

## Start here

- Documentation: https://x402-avm.github.io
- Examples: [x402-avm/examples](https://github.com/x402-avm/examples) (runnable on LocalNet, TestNet and MainNet)
- Demo: [x402-avm/marketplace-demo](https://github.com/x402-avm/marketplace-demo), a marketplace of 64 paid AI tools from 4 vendors on LocalNet
- Overview and architecture: [x402-avm/x402-avm](https://github.com/x402-avm/x402-avm)

## Built on

The [x402 protocol](https://github.com/x402-foundation/x402) and its official SDK, [GoPlausible/x402-avm](https://github.com/GoPlausible/x402-avm), and [Algorand](https://algorand.co).
