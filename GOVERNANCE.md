# Governance Model

This document outlines the governance structure, decision-making processes, and maintenance roles for the repositories within the x402-avm organization.

---

## 1. Project Organization and Roles

The project operates under an open, community-oriented governance model with two primary roles:

### Maintainers

- **Team**: AI Economy Team (`x402-avm` maintainers)
- **Responsibilities**:
  - Reviewing, testing, and merging Pull Requests.
  - Maintaining CI/CD workflows, build infrastructure, and documentation sites.
  - Publishing official package releases to PyPI (`ai-economy-sdk`, `x402-algorand`) and npm (`x402-avm-js`).
  - Triaging bug reports, feature requests, and community discussions.
  - Enforcing the Code of Conduct and managing confidential security advisories.

### Contributors

- **Community**: Any developer who reports issues, contributes documentation, submits code improvements, or engages in discussions.
- **Participation**: Everyone is encouraged to participate by opening issues, proposing enhancements, or reviewing pull requests.

---

## 2. Decision-Making Process

We follow a consensus-driven approach centered around GitHub Pull Requests and Discussions:

### Routine Changes

- Standard bug fixes, documentation improvements, test enhancements, and non-breaking feature additions proceed via normal Pull Request review.
- A PR may be merged once it has:
  1. Passed all required automated CI checks (linting, offline unit tests, and LocalNet integration tests).
  2. Received approval from at least one maintainer.
  3. Resolved any outstanding review comments or requested changes.

### Significant Changes and RFCs

- Architectural shifts, protocol alterations, new package proposals, or breaking API changes should begin as a proposal in GitHub Discussions or an Issue marked `RFC` (Request for Comments).
- RFC discussions remain open for community input for at least 7 days before maintainers finalize the design direction.
- In the rare event of irreconcilable disagreement, the core maintainers make the final binding determination in the best long-term interest of the project.

---

## 3. Release Management

- Packages adhere strictly to [Semantic Versioning 2.0.0](https://semver.org/):
  - **Major** releases for backward-incompatible API changes.
  - **Minor** releases for backward-compatible additions or enhancements.
  - **Patch** releases for backward-compatible bug fixes and security patches.
- The `main` branch of every repository is expected to remain stable, fully tested, and releasable at all times.
- Official releases are tagged in git and pushed to official package registries by maintainers.
