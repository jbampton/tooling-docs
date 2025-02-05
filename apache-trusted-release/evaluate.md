# Evaluate Claims Phase

In this phase the ATR will check claims about the release artifacts to enforce policy.

## Policies

- [Proper application of license](https://www.apache.org/legal/apply-license.html)
- [Release Policy](https://www.apache.org/legal/release-policy.html)
- [Signing Releases](https://infra.apache.org/release-signing.html)
- [Source Header and Copyright Notice Policy](https://apache.org/legal/src-headers.html)
- [3rd Party License Policy](https://apache.org/legal/resolved.html)

## Claims

1. Source files have the correct license headers.
2. LICENSE and NOTICE are provided in the correct location in every artifact.
3. Dependencies are acceptably licensed.
4. Release artifacts have correct GPG detached signatures and checksums.
5. Reproducible build claims are validated.
6. SBOMs are well formed and have proper claims.

## Tasks

1. Validate Packaging.
2. Validate License Headers including double checking "RAT excludes" to check for valid excludes.
3. Validate LICENSE and NOTICE.
4. Validate Dependency Licensing.
5. Validate Reprodicible Build Packaging.
6. Validate SBOMs (generate?).
