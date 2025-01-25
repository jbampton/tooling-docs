# Requirements (DRAFT)

While reading consider these Notes:

- This list attempts to avoid implementation details aside from existing practices.
- KEYS file requirements need further discussion before inclusion.
- See the [README](../README.md) for where to discuss these requirements.

## 1. Automate the Release Process

   - Minimize human interaction.
   - Community participation on **Release Votes** remains via email.
   - Record all of the key events for tracking operations and performance.
   - Projects can quickly benefit.

## 2. Apache Trusted Release Platform

   - Incorporate all Project Releases.
     - Download page. (dist/release)
     - Release Candidate pages. (dist/dev)
   - Every project has a management interface. 
     - Current manual release practice is viewable.
     - Automated release status.
     - Release operation and performance.
   - Platform includes a RESTful API.
   - Simple addition of release metadata triggers automation.
   - Replace the SVN Dist Repository? This would be an Infra task.
     _My warning is that any change from SVN not be disruptive._

## 3. Automate Release Process around Compliance

   - Meet Release Policy
     - Legal Policy
     - Infra Policy
     - Security Policy
   - SBOMs and Attestations
     - Include dependency and license compliance.
     - Provide clear attribution and information about Release Votes.
   - Download Page including available SBOM and verification instructions.
   - Announcement Email.

## 4. Automated Actions

   These requirements are by category and are not necessarily ordered.

   - Triggers:
     - Initiation by GH Action and/or GitBox Event.
     - Initiation by metadata commit to the Dist Repository.
     - Manual for steps that may require manual work first.
   - Procedures:
     - Maintain the SBOM.
     - Check compliance:
       - Security Policy.
       - Legal Policy. (to the extent possible)
     - Signing Certificates.
     - Optional Digital Signatures - Windows / macOS.
   - Voting:
     - Perform the Release Vote on the project dev list.
     - PMC votes through ATR, but emails are sent for each.
       (Use a hosted release candidate page that looks like the Download page)
   - Failure:
     - Non-compliance
     - Failed Votes
     - Email status to dev list
   - Distribution:
     - Release to the required Dist Repository.
     - Release to selected optional repositories. (Prioritized list)
       - Maven Central
       - PyPi
       - Node
       - DockerHub
       - Artifactory
       - (A prioritized list)
   - Candidates:
     - Some release candidates may be distributed to test repositories.
       - Apache staging repository
       - Test PyPi
       - (others?)
     - Developers may want to test those artifacts while voting.
   - Release Summary Email.
     - Include instructions about any optional repositories not automated.
     - Once any manual steps are completed manually trigger the next step.
   - Announce Release via Email.

## 5. Participate In the Ecosystem

   - Assure that the ATR platform follows industry best practices.
   - Help lead the industry to better practices.
   - Work within ASF should policy changes be desirable. 
