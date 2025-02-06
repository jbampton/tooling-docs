# Release Lifecycle

A Release will go through a lifecycle of **stages** and **phases**.

Stages include **Build**, **Candidate**, **Current**, and **Archived**.
The ATR does not manage build stage and legacy releases. It takes over on the transition from the build to the candidate stage.
Stages control where on the **ATR** Website a release can be found.

Phases are states or activities during a Release's life cycle.

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
    A -->|gha to api| C
    BB -->|api or web page| C
    B -->|web page| C
    subgraph Release Candidate Stage
    D@{ shape: processes, label: "Evaluate Claims" }
    C --> D
    GG@{ shape: processes, label: "Distribute (Test)" }
    E@{ shape: sl-rect, label: "Release Vote" }
    JJJ@{ shape: circ, label: "Passes" }
    F@{ shape: dbl-circ, label: "Failed" }
    E -->|pass| JJJ
    E -->|fail| F
    GG -->|fail| F
    D -->|fail| F
    F -->|new candidate| C
    D -->|pass| GG
    GG --> E
    end
    II[Migration]
    subgraph Current Release Stage
    JJ@{ shape: docs, label: "Release" }
    JJJ --> JJ
    G@{ shape: processes, label: "Distribute" }
    G --> I
    I[Announce Release]
    JJ --> G
    J@{ shape: dbl-circ, label: "Released" }
    I -->|announced| J
    end
    B -->|migration| II
    II -->|current| J
    subgraph Archived Release Stage
    K@{ shape: dbl-circ, label: "Archived" }
    end
    G -->|failure| K
    J -->|archive| K
    II -->|archived| K
    end
```

## Phases

**[Announce Release](https://www.apache.org/legal/release-policy.html#release-announcements)**
: Send a compliant announcement of the release. This template will include release metadata and should point to our static release download page. That page should refer back to the project's website.

**Archived**
: A Release in this stage/phase has been archived, revoked, or abandoned.

**[ATR Platform](./platform.md)**
: Apache Trusted Release is a service with a web UI and REST API for managing the lifecycle of project releases.

**[Distribute](./distributions.md)**
: Release and Test distributions will be automated for many channels. An email will be sent about package managers which need manual distribution.
Once that is complete the Release Manager will need to move to the next Phase. If all distributions automatically complete then moving to the next phase is automatic.

**[Evaluate Claims](./evaluate.md)**
: Evaluate claims on the Candidate by performing numerous checks for policy compliance. Fails if compliance minimums are unmet.

**Failed**
: A Release Candidate may end in this state. The project can either abandon it or update and resubmit it.
 The Release Manager will need to decide the next phase.

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
