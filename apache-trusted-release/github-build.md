# GitHub Build

Under certain conditions release candidates may be created using a properly reviewed GHA workflow.

## Policy

- [Automated Release Signing](https://infra.apache.org/release-signing.html#automated-release-signing)

## Tasks

1. There needs to be a GHA to upload a Release Candidate to the ATR from an [ASF GHA Action](https://github.com/apache/infrastructure-actions).
2. This action should be blocked if the PMC has not been approved.
3. During the **Evaluate Claims** phase release candidates will be checked to prove that the builds are reproducible.
