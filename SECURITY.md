# Security Policy

The x402-avm project takes the security of its payment protocols, client SDKs, and server middleware seriously. This document outlines supported versions, vulnerability reporting procedures, testing boundaries, and security scope.

---

## Supported Versions

Security updates and vulnerability patches are actively provided for the following releases:

| Package | Supported Versions | Status | Notes |
| :--- | :--- | :--- | :--- |
| `ai-economy-sdk` | `>= 0.4.0, < 0.5.0` | Supported | Compatible with official x402 2.28+ and CAIP-2 short IDs |
| `x402-algorand` | `>= 0.2.0, < 0.3.0` | Supported | Algorand mechanism plugin for official x402 |
| `x402-avm-js` | `>= 0.3.0, < 0.4.0` | Supported | TypeScript client with CAIP-2 short ID support |

Versions prior to those listed above (e.g., `ai-economy-sdk` < 0.4.0, `x402-algorand` < 0.2.0, `x402-avm-js` < 0.3.0) are deprecated and no longer receive bug fixes or security patches. Users should upgrade to the latest supported release.

---

## Reporting a Vulnerability

If you discover a security vulnerability in any x402-avm package, please disclose it responsibly via GitHub Private Vulnerability Reporting:

1. Navigate to the **Security** tab of the affected repository and click **Report a vulnerability** (`/security/advisories/new`):
   - [`ai-economy-sdk` Vulnerability Report](https://github.com/x402-avm/ai-economy-sdk/security/advisories/new)
   - [`x402-algorand` Vulnerability Report](https://github.com/x402-avm/x402-algorand/security/advisories/new)
   - [`x402-avm-js` Vulnerability Report](https://github.com/x402-avm/x402-avm-js/security/advisories/new)
   - For organization-wide or cross-cutting issues: [`.github` Vulnerability Report](https://github.com/x402-avm/.github/security/advisories/new)
2. Include the following details in your report:
   - Affected package name and exact version.
   - Comprehensive description of the vulnerability and attack vector.
   - Proof-of-concept code or step-by-step reproduction instructions.
   - Analysis of potential impact (e.g., funds loss, payment bypass, replay, denial of service).
   - Any suggested mitigations or patches.

---

## Security Scope

### In-Scope

The following components and behaviors are within scope for security review:

- **Payment Verification**: Flaws in `x402Facilitator` or `PaymentGate` validation logic, including fee checking, asset ID mismatches, sender spoofing, receiver mismatches, or genesis hash discrepancies.
- **Atomic Group Integrity**: Exploits in 2-transaction fee-payer atomic groups that allow payment theft, fee drainage, or unauthorized transaction execution.
- **Replay Resistance**: Bypasses of `ReplayStore` (SQLite or in-memory) permitting double-spending or replay of previously settled payment payloads.
- **Identity Proofs**: Flaws in `sign_identity_txn` or `verify_identity_txn` allowing signature forgery, replay past 120 seconds, or round-window manipulation.
- **Spend Controls**: Flaws allowing unauthorized spending beyond configured caps or for unwhitelisted assets.

### Out-of-Scope

- Attacks requiring local root access, physical device access, or compromise of the host operating system.
- Denial of service attacks against public RPC endpoints (e.g., rate-limiting public AlgoNode instances).
- Vulnerabilities within external Algorand node implementations (Algod, Indexer, KMD) or consensus mechanics.
- Social engineering or phishing attacks targeting developers or end users.

---

## Strict Testing Rules and MainNet Prohibition

When investigating potential vulnerabilities:

1. **NEVER test on MainNet using funds or accounts that do not belong to you.**
2. **NEVER execute attacks against live third-party services, merchants, or user funds.**
3. All vulnerability testing and exploit verification must be conducted strictly on:
   - **LocalNet**: Isolated local node instances spun up via AlgoKit (`algokit localnet start`) using the KMD dispenser.
   - **TestNet**: Using test accounts funded through the public Algorand TestNet dispenser.

Violation of these rules will disqualify reports from responsible disclosure recognition and safe harbor protections.

---

## Response Timeline and Safe Harbor

- **Acknowledgment**: Maintainers will acknowledge receipt of reports within 48 hours.
- **Assessment & Triage**: An initial severity assessment and confirmation will be provided within 5 business days.
- **Remediation**: Patches will be developed and released within a coordinated disclosure window (typically 14 to 30 days depending on severity).
- **Public Disclosure**: A public GitHub Security Advisory and CVE identifier (if applicable) will be published following release of the patch.

If you conduct your research in good faith and comply with this policy, we will not pursue legal action against you or request law enforcement investigation.
