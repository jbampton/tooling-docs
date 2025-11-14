# Distribute Phase

Support will be added to the ATR for distribution of release and test packages to distribution channels in a priority order.

## Policies

- [Release Distribution Policy](https://infra.apache.org/release-distribution.html)
- [Docker Hub Policy](https://infra.apache.org/docker-hub-policy.html)

## Distribution Channels

1. Maven Central
2. PyPi
3. jFrog
4. DockerHub
5. Node
6. NuGet
7. ... and many more

Channels may have a TEST distribution channel.
PMCs choose in their Product Line configuration which channels to distribute TEST and Release Artifacts.

> For the first phase we will only support the first 2 - 4 Channels.

## Tasks

1. Automatically distribute release artifacts that are properly typed for the channel.
2. If any channels are not automated then send an email to the dev mailing list telling the Release Manager (RM)
   which packages and channels they need to manually distribute. Once complete the RM will need to start the next phase
3. If they were errors in distribution then send an error report to the RM on the dev mailing list so that they can take
   the correct action.
