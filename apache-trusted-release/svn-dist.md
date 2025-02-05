# Legacy Releases from SVN Dist

We have three types of Releases to create using a "Pull from 'Dist'" process.

1. Release Candidates from `dist/dev` as the Release Manager requests from within the ATR Web UI.

2. Current Releases from `dist/release` this will be used for the initial migration and may be used from time to time as PMCs use the old methods.

3. Archived Releases which are migrated from the archive if not present in the Current Releases.

## PMC Release Management Page

1. **Create Release Candidate** - upload the packages for a release candidate from `svn:dist/dev`

2. **Legacy Release** - upload an approved release from `svn:dist/release`.

## System Administation Management Page

1. **Synchronise Current Releases** - scan `svn:dist/release` and migrate any not in the ATR.

2. **Sychronize Release Archice** - scan `archive` repository and migrate any archived not in the ATR as a Current or Archived Release.
