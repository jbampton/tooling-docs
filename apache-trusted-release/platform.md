# Platform

https://releases.apache.org

OR

https://artifacts.apache.org

## Web Service

1. `asfquart` based asynchronous python web service.
2. Fronted by `httpd`.
   
## Storage

1. Release Storage. A large filesystem with folders for each release's files. The release folder path is immutable.
2. Metadata Database. An sql database on the server with the metadata schema.

## Store metadata and files for Releases

1. Current Releases
2. Candidate Releases
3. Revoked / EOL / Attic Releases
4. “Nightlies” is it in or out of scope?

## Store metadata and public signing keys of Release Managers

1. Collate Keys by Committer
2. Link Committer Keys to Signed Releases

## Store metadata about Release CVEs

1. CVE metadata
2. Effected releases
3. Release that resolves CV

## Release co-ordinates

The co-ordinates make up the external path to objects. The metadata database provides the map to the local path.

1. Stage (Candidate, Current, Revoked, …)
2. Project (Responsible TLP)
3. Product (Main, Sub-projects)
4. Version (String, latest)
5. Files, Metadata (A release is a folder of one or more files or sub-folders)

- Latest main product release: `/<stage>/<project>/latest/<file>`
- Main product by version: `/<stage>/<project>/<version>/<file>`
- Latest product release: `/<stage>/<project>/<product>/latest/<file>`
- Product release by version: `/<stage>/<project>/<product>/<version>/<file>`

## User Roles

1. Project PMC Member
   - binding vote
   - manage release
   - manage metadata
   - manage keys
   - perform actions
2. Project Committer
   - vote
   - manage their keys
3. Individual (“anonymous”, “none”)
   - download
   - vote with optional email
   - view release events
4. ASF Member
   - view all events
5. Admin (“root”)
   - manage release
   - manage metadata
   - manage keys
   - perform actions
   - view all events

> The authorization and authentication for `GitHub PATs` will be specific and fine-grained. The details are to be developed during implementation.

## Restful API

1. GET/HEAD
   - Metadata
   - Release
   - Package files including SBOMs
   - Signing keys
   - CVEs

2. CRUD
   - Releases - Delete is not removal. It is a stage.
   - Public Signing Keys - Delete only if unused.
   - Votes - Store each vote in metadata.
   - SBOMs - Special files stored in the release folder.
   - CVEs - CVE metadata and release linkage.

3. Asynchronous Actions - several transformative actions as POST/PUT/GET
   - Analyze
   - Vote
   - Distribute - Push to Package Repositories
   - Stage transitions
   - Push / Pull with dist.apache.org
   - Emails
     - Votes
     - Status
     - Transitions
   - _Not an exhaustive list._

## Web UI

1. Directory Pages
   - Project directory (_main page_)
   - Project release directory

2. Release Page
   - Changes according to Stage and Role.
   - Release level metadata
   - CVE metadata
   - Download package from directory of release
   - Maintenance actions
   - History of events

3. Project Configuration Page
   - Project level metadata and releases
   - Product level metadata and releases

4. Audit Page
   - ASF event history
   - Project event history
   - Product event history

5. Page Template
   - Responsive with Header(Hamburger)/Content/Footer.
   - Include Search in Header(Hamburger)
