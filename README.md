# `rsync` Buildkite Plugin

This repository is inspired by [uw-ipd/rsync-buildkite-plugin](https://github.com/uw-ipd/rsync-buildkite-plugin.git).

A Buildkite plugin for
performing file transfers via
[`rsync`](https://linux.die.net/man/1/rsync). The plugin invokes `rsync`
in the `pre` or `post` command phase to provide an artifact-like upload
and download capacity.

## Examples

Upload a build product directory into a build-specific output directory on
a remote store:

```yml
steps:
  - env:
      SSH_PRIVATE_KEY: "--- PRIVATE KEY ---"
      SERVER_ADDRESS: "SERVER_ADDRESS"
    plugins:
      - thilinaperera/rsync#v1.0.0:
          private_key_env_variable: "SSH_PRIVATE_KEY"
          server_address_env_variable: "SERVER_ADDRESS" # Used for ssh-keyscan
          commands:
            - "-azv -e 'ssh -p 99' ${BUILDKITE_BUILD_CHECKOUT_PATH}/** user@$${SERVER_ADDRESS}:~/path/"
```