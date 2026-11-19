# Contributing to x402-avm

Thank you for your interest in contributing to the x402-avm project. This organization maintains open-source SDKs, tools, and examples for integrating the x402 payment protocol on the Algorand Virtual Machine (AVM).

This guide outlines our development processes, testing tiers, coding standards, and pull request workflow across all repositories in the organization.

---

## Repositories

The organization comprises the following core repositories:

- [`ai-economy-sdk`](https://github.com/x402-avm/ai-economy-sdk): High-level Python SDK providing payment middleware for Model Context Protocol (MCP) servers and paid client sessions.
- [`x402-algorand`](https://github.com/x402-avm/x402-algorand): Python plugin for the official `x402` package implementing the Algorand exact payment scheme.
- [`x402-avm-js`](https://github.com/x402-avm/x402-avm-js): Browser and Node.js TypeScript client for resolving 402 responses with standard Algorand wallets.
- [`examples`](https://github.com/x402-avm/examples): Standalone, runnable code examples for LocalNet, TestNet, and MainNet in Python and TypeScript.
- [`marketplace-demo`](https://github.com/x402-avm/marketplace-demo): Demonstration marketplace illustrating multi-vendor MCP routing, settlement, and verification.

---

## Development Setup

### Python Repositories (`ai-economy-sdk`, `x402-algorand`)

Prerequisites:
- Python 3.10, 3.11, 3.12, or 3.13 (Python 3.12 recommended)
- `uv` (recommended) or standard `pip` and `venv`

Setup steps:

```bash
git clone https://github.com/x402-avm/<repo-name>.git
cd <repo-name>

# Create and activate a virtual environment
uv venv -q --python 3.12 .venv
source .venv/bin/activate

# Install package in editable mode with development dependencies
uv pip install -e ".[dev]"
```

If using standard pip:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -e ".[dev]"
```

### TypeScript Repository (`x402-avm-js`)

Prerequisites:
- Node.js 18.x, 20.x, or 22.x
- `npm` 9.x or higher

Setup steps:

```bash
git clone https://github.com/x402-avm/x402-avm-js.git
cd x402-avm-js

# Install dependencies
npm install

# Compile TypeScript to ESM and CommonJS
npm run build
```

---

## Test Tiers

To balance rapid development feedback with thorough on-chain verification, tests are organized into three distinct tiers:

### 1. Offline Tests (Default)

Offline tests validate unit logic, input parsing, cryptographic signatures, and error handling without contacting any external network or local daemon.

- **Python**:
  ```bash
  pytest -q
  ```
- **TypeScript**:
  ```bash
  npm test
  ```

Every pull request must pass all offline tests before merge.

### 2. LocalNet Integration Tests (`LOCALNET=1`)

LocalNet tests execute end-to-end payment flows, group transaction sponsorship, settlement verification, and replay resistance against a local Algorand node.

Prerequisites:
- AlgoKit installed: `pipx install algokit`
- LocalNet running:
  ```bash
  algokit localnet start
  ```
- Verify standard endpoints:
  - Algod: `http://localhost:4001` (Header: `X-Algo-API-Token: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`)
  - KMD: `http://localhost:4002` (Header: `X-KMD-API-Token: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`)
  - Indexer: `http://localhost:8980`

Execution:
- **Python**:
  ```bash
  LOCALNET=1 pytest -q
  ```
- **TypeScript**:
  ```bash
  LOCALNET=1 npm test
  ```

All LocalNet tests create isolated ephemeral accounts and fund them using the LocalNet KMD dispenser. Tests must never depend on fixed pre-existing balances or external state files.

### 3. Public Network Verification (`PUBLIC_NETS=1`)

Public network tests verify compatibility against live Algorand TestNet and MainNet infrastructure.

- Public endpoints default to AlgoNode (`https://testnet-api.algonode.cloud`, `https://mainnet-api.algonode.cloud`).
- **Strict Read-Only Policy**: These tests use Algod transaction simulation (`simulate`) and Indexer queries. They **never** broadcast transactions, spend live tokens, or require private keys funded with real assets.
- Execution:
  ```bash
  PUBLIC_NETS=1 pytest -q
  ```

---

## Code Quality and Standards

All code submitted to x402-avm repositories must satisfy automated linting and formatting checks.

### Python Standards

- **Formatter & Linter**: Ruff
- Format code:
  ```bash
  ruff format .
  ```
- Check lint rules:
  ```bash
  ruff check .
  ```
- **Docstrings**: Public APIs must include NumPy-style docstrings describing parameters, return values, raised exceptions, on-chain effects, and offline doctests.

### TypeScript Standards

- **Type Safety**: No compiler errors under strict mode:
  ```bash
  npx tsc --noEmit
  ```
- **Formatter & Linter**:
  ```bash
  npm run lint
  npm run format:check
  ```
- **Documentation**: Public exports must include TSDoc annotations.

---

## Commit Style

We follow the Conventional Commits specification for git commit messages:

- Format: `<type>(<scope>): <short description>`
- Allowed types: `feat`, `fix`, `docs`, `refactor`, `test`, `perf`, `chore`.
- Examples:
  - `feat(client): add spend controls to paid mcp session`
  - `fix(network): handle 32-character caip-2 prefix in normalize_network`
  - `docs(api): document genesis_hash_for helper`
  - `test(gate): add unit test for replay db locking`

Keep the subject line concise (under 72 characters), imperative, and in lower case.

---

## Pull Request Process

1. **Fork and Branch**:
   - Fork the relevant repository to your personal GitHub account.
   - Create a descriptive feature branch from `main`:
     ```bash
     git checkout -b feat/my-feature-description
     ```
2. **Implement and Test**:
   - Write clear, focused commits.
   - Include corresponding unit and integration tests.
   - Run the local test suite (both offline and `LOCALNET=1`).
3. **Open a Pull Request**:
   - Open a PR against the `main` branch of the upstream repository.
   - Fill out the Pull Request Template completely.
   - Link any associated GitHub issues.
4. **Review and Merge**:
   - Maintainers will review your PR.
   - All CI checks (linting, matrix unit tests, LocalNet integration) must pass before merging.
   - Once approved, PRs are squash-merged into `main`.

---

## Developer Certificate of Origin (DCO)

A formal Developer Certificate of Origin (DCO) sign-off (`git commit -s`) is **not required**.

By submitting a pull request, you agree that your contributions are made under the open-source license governing the target repository:
- `ai-economy-sdk`: MIT License
- `x402-algorand`: Apache 2.0 License
- `x402-avm-js`: MIT License
- `examples`: MIT License
- `marketplace-demo`: MIT License
