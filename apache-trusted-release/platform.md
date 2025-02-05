# Platform Service

https://releases.apache.org

## Datastore

1. Release Storage. A large filesystem with folders for each release's files. The release folder path is immutable.
2. Metadata Database. An sql database on the server with the metadata schema.

See [Data Model](./data-model.md) for a discussion of the objects managed by the ATR.

## Web Service

1. `asfquart` based asynchronous python web service.
2. Fronted by `httpd`.
3. Static content may be served without going through `asfquart`.
4. Monolithic.
5. Fronted by a CDN. The caching policies need to properly defined.

## Legacy Redirect Rules

1. Redirect from https://downloads.apache.org
2. Redirect from https://archives.apache.org
   
### Release Stages

1. Build Releases - while not managed by the ATR there are bridges.
2. Candidate Releases
3. Current Releases
4. Archived / Revoked / EOL / Atticked Releases

> “Nightlies” is for a later phase.

### Release Phases

See [Release Lifecycle](./lifecycle.md) for how phases are chained together to perform a Release.

### Release co-ordinates

The co-ordinates make up the external path to objects. The metadata database provides the map to the local path.

1. Stage (Candidate, Current, Archived, …)
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

2. CRUD on 
   - Releases - Delete is not removal. It is a stage.
   - Public Signing Keys - Delete only if unused.
   - Votes - Store each vote in metadata.
   - SBOMs - Special files stored in the release folder.

3. POST Phases - Transitions, Activities, and Communication
   - Transition into Phase.
   - Perform Phase activity.
   - Optionally email phase status.

   See [Release Lifecycle](./lifecycle.md) for how phases are chained together to perform a Release.

4. POST Templated Emails
   - Announcements
   - Votes
   - Status
   - Transitions

### Web UI

1. Directory Pages
   - Project directory (_main page_)
   - Project release directory

2. Release Page
   - Static public version for Current and Archived Stages.
   - Overwise dyanmic for Candidate stage and when accessed from the PMC Management Page. 
   - Release level metadata
   - Download package from directory of release
   - Maintenance actions
   - History of events

4. PMC Management Page
   - PMC level metadata and releases
   - Product level metadata and releases
   - Manage releases

5. Audit Page
   - ASF event history
   - Project event history
   - Product event history

6. Page Template
   - Responsive with Header(Hamburger)/Content/Footer.
   - Include Search in Header(Hamburger)


