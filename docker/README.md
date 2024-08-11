# env-setup docker image

A Dockerfile setup that can build a Ubuntu linux image that installs `env-setup`
and all its prerequisites. The image can be configured with a few build arguments:

- `VER`: The default version of the base OS image.
- `PASS`: The default password of `user` (default `password`)
- `ENVSETUP_REPO_SSH`: The default repo of `env-setup` (default `git@github.com:Luciditi/env-setup.git`)
- `ENVSETUP_DOTFILES_REPO_SSH`: The default repo of public dotfiles (default `git@github.com:Luciditi/env-setup-dotfiles.git`)
- `ENVSETUP_DOTFILES_PRV_REPO_SSH`: The default repo of private dotfiles (default `git@github.com:Luciditi/env-setu-dotfilesp.git`)
- `ENVSETUP_CONFIG`: The location of the `env-setup` config manifest.
- `ENVSETUP_VERSION`: The version tag of the `env-setup` image.


`docker run -it --rm --platform linux/amd64 -v "$HOME/.ssh/id_rsa:/home/user/.ssh/id_rsa" env-setup:latest`

```
SSH_KEY=$HOME/.ssh/id_rsa
ENVSETUP_CONFIG=docker/default.config.yml
ENVSETUP_VERSION=0.0.0
DOCKERFILE=docker/Dockerfile
#DOCKER_PLATFORMS=linux/amd64,linux/arm64
DOCKER_PLATFORMS=linux/amd64
DOCKER_TAG=$ENVSETUP_VERSION-default

docker buildx build --secret id=ssh,src="$SSH_KEY" \ 
  --platform $DOCKER_PLATFORMS \ 
  --build-arg="ENVSETUP_CONFIG=$ENVSETUP_CONFIG" \
  --build-arg="ENVSETUP_VERSION=$ENVSETUP_VERSION" \
  --label "org.opencontainers.image.ref.name=luciditi/env-setup-$DOCKER_TAG"
  --label "org.opencontainers.image.version=$ENVSETUP_VERSION"
  -t "env-setup:$DOCKER_TAG" . -f "$DOCKERFILE"
```

# Prerequisites
- An environment that can build a docker image from a `Dockerfile`

# Notes

