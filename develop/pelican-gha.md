# Pelican GHA

To test Pelican GitHub Actions, install [`act`](https://github.com/nektos/act). `act` is a Go program which runs GitHub Actions locally. You can [install it from Nix](https://search.nixos.org/packages?channel=unstable&show=act&from=0&size=50&sort=relevance&type=packages&query=act), from your preferred package manager, or from Go source.

You will need a GitHub PAT. Read the [instructions for issuing a fine-grained PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token). Get one from [your PAT settings page](https://github.com/settings/personal-access-tokens) once logged in to GitHub.

The PAT is necessary because the Pelican GHA reads from this repository. You will therefore need to issue a PAT which has public read access to all repositories. Choose a suitable expiry date; long expiries for read only PATs are probably fine.

Run the Pelican GHA using:

```shell
DOCKER_HOST=unix:///.../docker.sock act \
   --container-architecture linux/amd64 \
   --container-daemon-socket - \
   -s GITHUB_TOKEN \
   push
```

You don't need to specify the container architecture if you're already using `linux/amd64`.
