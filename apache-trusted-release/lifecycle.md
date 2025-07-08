# Release Lifecycle

A Release goes through a lifecycle of **stages**.

Stages include **Build**, **Candidate**, **Vote**, **Finish**, **Released**, and **Archived**.
The ATR does not manage build stage and legacy releases. It takes over the relase process on the transition to the candidate stage.
Stages are the states of a release in the **ATR**.

```mermaid
flowchart TD
    subgraph Build Stage
    A[GHA Secure Build]
    BB[RM Local Build]
    end
    subgraph Legacy
    B[Legacy SVN Dist]
    end
    subgraph Apache Trusted Release
    C@{ shape: docs, label: "Release Candidate" }
    A -->|client/openapi| C
    BB -->|client/openapi or web ux| C
    B -->|web ux| C
    subgraph Candidate Stage
    D@{ shape: processes, label: "Evaluate Claims" }
    C --> D
    end
    subgraph Vote Stage
    GG@{ shape: processes, label: "Distribute (Test)" }
    E@{ shape: processes, label: "Release Vote" }
    E -->|fail| C
    D -->|vote| GG
    GG --> E
    end
    II[Migration]
    subgraph Finish Stage
    G@{ shape: processes, label: "Reorganize" }
    E -->|pass| G
    I[Announce Release]
    G --> I
    end
    subgraph Released Stage
    J@{ shape: docs, label: "Released" }
    I -->|announced| J
    end
    B -->|migration| II
    II -->|current| J
    subgraph Archived Stage
    K@{ shape: docs, label: "Archived" }
    end
    J -->|archive| K
    II -->|archived| K
    end
```

## Phases

**[Announce Release](https://www.apache.org/legal/release-policy.html#release-announcements)**
: Send a compliant announcement of the release. This template will include release metadata and should point to our static release download page. That page should refer back to the project's website.

**Archived Stage**
: A Release in this stage/phase has been archived, revoked, or abandoned.

**[ATR Platform](./platform.md)**
: Apache Trusted Releases is a service with a web UI and REST API for managing the lifecycle of project releases.

**[Distribute](./distributions.md)**
: _in progress_ Release and Test distributions will be automated for many channels. An email will be sent about package managers which need manual distribution.
Once that is complete the Release Manager will need to move to the next Phase. If all distributions automatically complete then moving to the next phase is automatic.

**[Evaluate Claims](./evaluate.md)**
: Evaluate claims on the Candidate by performing numerous checks for policy compliance. Fails if compliance minimums are unmet.

**[GHA Secure Build](./github-build.md)**
: In a GitHub workflow the release candidate is built and validated following the Security Release Policy.

**[Legacy SVN Dist](./svn-dist.md)**
: This is our current SVN repository process for setting up a release candidate. Trigger the ATR automation by including release metadata.

**[Migration](./svn-dist.md)**
: We need a phase for migration of existing current and archived releases from the legacy platform into the ATR data store.

**Passes**
: The Release Candidate has been accepted. Convert the candidate into a Release and proceed to Distribute and Announce the Release.

**[Release](./data-model.md)**
: The release is a folder of files including metadata, SBOMs, public keys, signatures, and checksums.

**[Release Candidate](./data-model.md)**
: A release candidate consists of a folder of release files including metadata, SBOMs, public keys, signatures, and checksums.

**[Release Vote](./vote.md)**
: Release policy requires a Vote on the project's dev list. The ATR records votes in the platform and also on the mailing list. The Vote will be summarized and the PMC Vote recorded in the releases metadata.

**Released**
: Once the Release is distributed and announced, this Release should remain in this phase as long as it is available.

**[RM Local Build](./platform.md)**
: Release Managers upload or push a release candidate into the ATR using either an API or a web page.
