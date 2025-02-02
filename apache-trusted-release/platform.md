# Platform Services

1. Datastore: https://releases.apache.org
2. Task Runner: https://artifacts.apache.org

> Monitoring the service stack will indicate if the stack split is indicated. Let's make sure that such a split is relatively quick.

## Datastore

1. Release Storage. A large filesystem with folders for each release's files. The release folder path is immutable.
2. Metadata Database. An sql database on the server with the metadata schema.

### Web Service

1. `asfquart` based asynchronous python web service.
2. Fronted by `httpd`.
3. Monolithic.
4. Fronted by a CDN. The caching policies need to properly defined.
5. Avoid long running processes.
   
### Release Metadata and Files

1. Current Releases
2. Candidate Releases
3. Revoked / EOL / Attic Releases

> “Nightlies” is for a later phase.

### Release Manager Signing Keys

1. Collate Keys by Committer
2. Link Committer Keys to Project, Signed Releases

### Release CVE Store

1. CVE metadata
3. Affected releases
4. Release that resolves CVE(s)

### Release co-ordinates

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

### Restful API

1. GET
   - Metadata
   - Release
   - Package files including SBOMs
   - Signing keys
   - CVEs

2. CRUD on 
   - Releases - Delete is not removal. It is a stage.
   - Public Signing Keys - Delete only if unused.
   - Votes - Store each vote in metadata.
   - SBOMs - Special files stored in the release folder.
   - CVEs - CVE metadata and release linkage.

3. POST Actions - Transitions with a Task
   - Analyze
   - Vote Monitor
   - Distribute - Push to Package Repositories
   - Push / Pull with dist.apache.org
   - others?

   See [Release Lifecycle](./lifecycle.md) for how Actions are chained together to perform a Release.

4. POST Templated Release Emails
   - Announcements
   - Votes
   - Status
   - Transitions

### Web UI

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

## Task Runner

1. Runner for processes taking more than a few seconds.
2. Manages an array of concurrent tasks.
3. Provides operational status.
4. Monitor load to avoid saturation and find true limits.

### Web Service

1. `asfquart` based asynchronous python web service.
2. Fronted by `httpd`.
3. Limit web access to ATR Datastore, other Runners, and IRD.

### Restful API

See [Release Lifecycle](./lifecycle.md) for how Action Tasks are chained together to perform tasks related to a Release.

1. GET
   - Status
   - Task

2. CRUD on 
   - Task 

3. Task Types
   - Analyze
   - Test Distribution
   - Vote Monitor
   - Distribution
   - Monitor Manual Distribution
   - Push / Pull with dist.apache.org
   - others?

