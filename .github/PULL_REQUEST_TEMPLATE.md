## Summary

<!-- Briefly describe the purpose of this pull request and the problem it solves. -->

## Related Issues

<!-- Reference related issues below (e.g. Fixes #123, Closes #456). -->
Fixes #

## Changes Made

<!-- Provide a bulleted summary of key changes in this PR. -->
- 

## Test Tier Verification

Please confirm that the appropriate test tiers have been run and passed:

- [ ] **Offline Tests** (`pytest` or `npm test`): All offline unit tests pass without network access.
- [ ] **LocalNet Tests** (`LOCALNET=1 pytest` or `LOCALNET=1 npm test`): Integration tests pass against a local Algorand node (if changes affect on-chain behavior or settlement).
- [ ] **Public Networks Tests** (`PUBLIC_NETS=1 pytest`): Read-only simulation tests pass against public TestNet/MainNet endpoints (if changes affect network resolution or client configuration).

## Quality Checklist

- [ ] Code follows project formatting and linting rules (`ruff format` / `ruff check` or `npm run lint`).
- [ ] Type checks pass without errors (`tsc --noEmit` for TypeScript).
- [ ] Public functions, classes, and methods have up-to-date NumPy-style docstrings (Python) or TSDoc comments (TypeScript).
- [ ] Documentation and runnable examples have been updated if API signatures or behaviors changed.
- [ ] Commit messages follow conventional commit guidelines (`feat:`, `fix:`, `docs:`, etc.).
