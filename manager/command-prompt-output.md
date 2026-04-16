# Terraform Getting Started - Complete Terminal Session

This document shows a complete terminal session of installing Terraform, creating a Docker-based infrastructure configuration, and managing its lifecycle.

## Initial Docker Check

### First attempt (Docker not found)

```shell
$ docker
```

```
zsh: command not found: docker
```

### After Docker installation

```shell
$ docker
```

```
Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Common Commands:
  run         Create and run a new container from an image
  exec        Execute a command in a running container
  ps          List containers
  build       Build an image from a Dockerfile
  bake        Build from a file
  pull        Download an image from a registry
  push        Upload an image to a registry
  images      List images
  login       Authenticate to a registry
  logout      Log out from a registry
  search      Search Docker Hub for images
  version     Show the Docker version information
  info        Display system-wide information

Management Commands:
  agent*      Docker AI Agent Runner
  ai*         Docker AI Agent - Ask Gordon
  builder     Manage builds
  buildx*     Docker Buildx
  compose*    Docker Compose
  container   Manage containers
  context     Manage contexts
  debug*      Get a shell into any image or container
  desktop*    Docker Desktop commands
  dhi*        CLI for managing Docker Hardened Images
  extension*  Manages Docker extensions
  image       Manage images
  init*       Creates Docker-related starter files for your project
  manifest    Manage Docker image manifests and manifest lists
  mcp*        Docker MCP Plugin
  model*      Docker Model Runner
  network     Manage networks
  offload*    Docker Offload
  plugin      Manage plugins
  sandbox*    Docker Sandbox
  sbom*       View the packaged-based Software Bill Of Materials (SBOM) for an image
  scout*      Docker Scout
  system      Manage Docker
  volume      Manage volumes

Swarm Commands:
  swarm       Manage Swarm

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  import      Import the contents from a tarball to create a filesystem image
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes


Global Options:
      --config string      Location of client config files (default
                           "/Users/sonrics/.docker")
  -c, --context string     Name of the context to use to connect to the
                           daemon (overrides DOCKER_HOST env var and
                           default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host string        Daemon socket to connect to
  -l, --log-level string   Set the logging level ("debug", "info",
                           "warn", "error", "fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default
                           "/Users/sonrics/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default
                           "/Users/sonrics/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default
                           "/Users/sonrics/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Run 'docker COMMAND --help' for more information on a command.

For more help on how to use Docker, head to https://docs.docker.com/go/guides/
```

## Navigate to Project Directory

```shell
$ cd Documents
$ cd Jorge
$ cd Hashicorp
```

## Install Terraform via Homebrew

### Add HashiCorp tap

```shell
$ brew tap hashicorp/tap
```

```
==> Tapping hashicorp/tap
✔︎ JSON API cask.jws.json                                            Downloaded   15.4MB/ 15.4MB
✔︎ JSON API formula.jws.json                                         Downloaded   32.0MB/ 32.0MB
==> Tapping hashicorp/tap
Cloning into '/opt/homebrew/Library/Taps/hashicorp/homebrew-tap'...
remote: Enumerating objects: 6526, done.
remote: Counting objects: 100% (1048/1048), done.
remote: Compressing objects: 100% (303/303), done.
remote: Total 6526 (delta 918), reused 749 (delta 745), pack-reused 5478 (from 3)
Receiving objects: 100% (6526/6526), 1.15 MiB | 12.91 MiB/s, done.
Resolving deltas: 100% (4714/4714), done.
Tapped 2 casks and 32 formulae (99 files, 1.6MB).
```

### First install attempt (typo in command)

```shell
$ brew install hashicorpt/tap/terraform
```

```
==> Auto-updating Homebrew...
Adjust how often this is run with `$HOMEBREW_AUTO_UPDATE_SECS` or disable with
`$HOMEBREW_NO_AUTO_UPDATE=1`. Hide these hints with `$HOMEBREW_NO_ENV_HINTS=1` (see `man brew`).
==> Tapping hashicorpt/tap
Cloning into '/opt/homebrew/Library/Taps/hashicorpt/homebrew-tap'...
Username for 'https://github.com': sonrics11
Password for 'https://sonrics11@github.com':
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/hashicorpt/homebrew-tap/'
Error: Failure while executing; `git clone https://github.com/hashicorpt/homebrew-tap /opt/homebrew/Library/Taps/hashicorpt/homebrew-tap --origin=origin --template= --config core.fsmonitor=false` exited with 128.
```

### Configure Git to use SSH

```shell
$ git config --global url."git@github.com:".insteadOf "https://github.com/"
```

### Second install attempt (still with typo)

```shell
$ brew install hashicorpt/tap/terraform
```

```
==> Auto-updating Homebrew...
Adjust how often this is run with `$HOMEBREW_AUTO_UPDATE_SECS` or disable with
`$HOMEBREW_NO_AUTO_UPDATE=1`. Hide these hints with `$HOMEBREW_NO_ENV_HINTS=1` (see `man brew`).
==> Auto-updated Homebrew!
Updated 2 taps (homebrew/core and homebrew/cask).
==> New Formulae
paneru: Sliding, tiling window manager for MacOS
pocket-id: Open-source identity provider for secure user authentication
==> New Casks
google-gemini: Native desktop AI assistant from Google
unblocked: AI-powered developer collaboration platform

You have 11 outdated formulae and 1 outdated cask installed.

==> Tapping hashicorpt/tap
Cloning into '/opt/homebrew/Library/Taps/hashicorpt/homebrew-tap'...
ERROR: Repository not found.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
Error: Failure while executing; `git clone https://github.com/hashicorpt/homebrew-tap /opt/homebrew/Library/Taps/hashicorpt/homebrew-tap --origin=origin --template= --config core.fsmonitor=false` exited with 128.
```

### Correct the tap name

```shell
$ brew tap hashicorp/tap
```

```
✔︎ JSON API formula.jws.json                                                           Downloaded   32.0MB/ 32.0MB
✔︎ JSON API cask.jws.json                                                              Downloaded   15.4MB/ 15.4MB
```

### Install Terraform (correct command)

```shell
$ brew install hashicorp/tap/terraform
```

```
==> Auto-updating Homebrew...
Adjust how often this is run with `$HOMEBREW_AUTO_UPDATE_SECS` or disable with
`$HOMEBREW_NO_AUTO_UPDATE=1`. Hide these hints with `$HOMEBREW_NO_ENV_HINTS=1` (see `man brew`).
==> Fetching downloads for: terraform
✔︎ Formula terraform (1.14.8)                                                          Verified     28.7MB/ 28.7MB
==> Installing terraform from hashicorp/tap
Warning: A newer Command Line Tools release is available.
hcl
Update them from Software Update in System Settings.

If that doesn't show you any updates, run:
  sudo rm -rf /Library/Developer/CommandLineTools
  sudo xcode-select --install

Alternatively, manually download them from:
  https://developer.apple.com/download/all/.
You should download the Command Line Tools for Xcode 26.3.



This is a Tier 2 configuration:
  https://docs.brew.sh/Support-Tiers#tier-2
You can report issues with Tier 2 configurations to Homebrew/* repositories!
Read the above document before opening any issues or PRs.

🍺  /opt/homebrew/Cellar/terraform/1.14.8: 5 files, 95.7MB, built in 1 second
==> Running `brew cleanup terraform`...
Disable this behaviour by setting `HOMEBREW_NO_INSTALL_CLEANUP=1`.
Hide these hints with `HOMEBREW_NO_ENV_HINTS=1` (see `man brew`).
```

## Create Project Directory

```shell
$ mkdir terraform-demo
$ cd terraform-demo
$ touch main.tf
$ vi main.tf
```

## Initialize Terraform

### First attempt (with syntax error)

```shell
$ terraform init
```

```
Initializing the backend...
╷
│ Error: Terraform encountered problems during initialisation, including problems
│ with the configuration, described below.
│
│ The Terraform configuration must be valid before initialization so that
│ Terraform can determine which modules and providers need to be installed.
│
│
╵
╷
│ Error: Argument or block definition required
│
│   on main.tf line 1:
│    1: hcl
│
│ An argument or block definition is required here. To set an argument, use the equals sign "=" to introduce the
│ argument value.
╵
```

**Fix:** Remove the `hcl` marker from the beginning of `main.tf`.

```shell
$ vi main.tf
```

### Second attempt (successful)

```shell
$ terraform init
```

```
Initializing the backend...
Initializing provider plugins...
- Finding latest version of kreuzwerker/docker...
- Installing kreuzwerker/docker v4.2.0...
- Installed kreuzwerker/docker v4.2.0 (self-signed, key ID 0DCE698927DAF8EC)

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://developer.hashicorp.com/terraform/cli/plugins/signing

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

## Apply Configuration

### First attempt (attribute error)

```shell
$ terraform apply
```

```
╷
│ Error: Unsupported attribute
│
│   on main.tf line 12, in resource "docker_container" "nginx":
│   12:   image = docker_image.nginx.latest
│
│ This object has no argument, nested block, or exported attribute named "latest".
╵
```

**Configuration at this point:**
```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

**Fix:** Change `docker_image.nginx.latest` to `docker_image.nginx.image_id`.

```shell
$ vi main.tf
```

### Second attempt (rate limit error)

```shell
$ terraform apply
```

```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated
with the following symbols:
  + create

Terraform will perform the following actions:

  # docker_container.nginx will be created
  + resource "docker_container" "nginx" {
      + attach                                      = false
      + bridge                                      = (known after apply)
      + command                                     = (known after apply)
      + container_logs                              = (known after apply)
      + container_read_refresh_timeout_milliseconds = 15000
      + entrypoint                                  = (known after apply)
      + env                                         = (known after apply)
      + exit_code                                   = (known after apply)
      + hostname                                    = (known after apply)
      + id                                          = (known after apply)
      + image                                       = (known after apply)
      + init                                        = (known after apply)
      + ipc_mode                                    = (known after apply)
      + log_driver                                  = (known after apply)
      + logs                                        = false
      + memory_reservation                          = 0
      + must_run                                    = true
      + name                                        = "training"
      + network_data                                = (known after apply)
      + network_mode                                = "bridge"
      + platform                                    = (known after apply)
      + read_only                                   = false
      + remove_volumes                              = true
      + restart                                     = "no"
      + rm                                          = false
      + runtime                                     = (known after apply)
      + security_opts                               = (known after apply)
      + shm_size                                    = (known after apply)
      + start                                       = true
      + stdin_open                                  = false
      + stop_signal                                 = (known after apply)
      + stop_timeout                                = (known after apply)
      + tty                                         = false
      + wait                                        = false
      + wait_timeout                                = 60

      + healthcheck (known after apply)

      + labels (known after apply)

      + ports {
          + external = 80
          + internal = 80
          + ip       = "0.0.0.0"
          + protocol = "tcp"
        }
    }

  # docker_image.nginx will be created
  + resource "docker_image" "nginx" {
      + id          = (known after apply)
      + image_id    = (known after apply)
      + name        = "nginx:latest"
      + repo_digest = (known after apply)
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

docker_image.nginx: Creating...
╷
│ Error: Unable to read Docker image into resource: unable to pull image nginx:latest: error pulling image nginx:latest: Error response from daemon: error from registry: You have reached your unauthenticated pull rate limit. https://www.docker.com/increase-rate-limit
│
│   with docker_image.nginx,
│   on main.tf line 18, in resource "docker_image" "nginx":
│   18: resource "docker_image" "nginx" {
│
╵
```

### Authenticate with Docker Hub

```shell
$ docker login
```

```
Authenticating with existing credentials... [Username: sonrics11]

Login Succeeded
```

### Third attempt (successful)

```shell
$ terraform apply
```

```
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated
with the following symbols:
  + create

Terraform will perform the following actions:

  # docker_container.nginx will be created
  + resource "docker_container" "nginx" {
      + attach                                      = false
      + bridge                                      = (known after apply)
      + command                                     = (known after apply)
      + container_logs                              = (known after apply)
      + container_read_refresh_timeout_milliseconds = 15000
      + entrypoint                                  = (known after apply)
      + env                                         = (known after apply)
      + exit_code                                   = (known after apply)
      + hostname                                    = (known after apply)
      + id                                          = (known after apply)
      + image                                       = (known after apply)
      + init                                        = (known after apply)
      + ipc_mode                                    = (known after apply)
      + log_driver                                  = (known after apply)
      + logs                                        = false
      + memory_reservation                          = 0
      + must_run                                    = true
      + name                                        = "training"
      + network_data                                = (known after apply)
      + network_mode                                = "bridge"
      + platform                                    = (known after apply)
      + read_only                                   = false
      + remove_volumes                              = true
      + restart                                     = "no"
      + rm                                          = false
      + runtime                                     = (known after apply)
      + security_opts                               = (known after apply)
      + shm_size                                    = (known after apply)
      + start                                       = true
      + stdin_open                                  = false
      + stop_signal                                 = (known after apply)
      + stop_timeout                                = (known after apply)
      + tty                                         = false
      + wait                                        = false
      + wait_timeout                                = 60

      + healthcheck (known after apply)

      + labels (known after apply)

      + ports {
          + external = 80
          + internal = 80
          + ip       = "0.0.0.0"
          + protocol = "tcp"
        }
    }

  # docker_image.nginx will be created
  + resource "docker_image" "nginx" {
      + id          = (known after apply)
      + image_id    = (known after apply)
      + name        = "nginx:latest"
      + repo_digest = (known after apply)
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

docker_image.nginx: Creating...
docker_image.nginx: Creation complete after 8s [id=sha256:7f0adca1fc6c29c8dc49a2e90037a10ba20dc266baaed0988e9fb4d0d8b85ba0nginx:latest]
docker_container.nginx: Creating...
docker_container.nginx: Creation complete after 0s [id=3ee8fdd54e48dcfec0e72566cf5cb09362670c53d765b2a822f18d6924adc56e]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
```

## Destroy Infrastructure

```shell
$ terraform destroy
```

```
docker_image.nginx: Refreshing state... [id=sha256:7f0adca1fc6c29c8dc49a2e90037a10ba20dc266baaed0988e9fb4d0d8b85ba0nginx:latest]
docker_container.nginx: Refreshing state... [id=3ee8fdd54e48dcfec0e72566cf5cb09362670c53d765b2a822f18d6924adc56e]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated
with the following symbols:
  - destroy

Terraform will perform the following actions:

  # docker_container.nginx will be destroyed
  - resource "docker_container" "nginx" {
      - attach                                      = false -> null
      - command                                     = [
          - "nginx",
          - "-g",
          - "daemon off;",
        ] -> null
      - container_read_refresh_timeout_milliseconds = 15000 -> null
      - cpu_shares                                  = 0 -> null
      - dns                                         = [] -> null
      - dns_opts                                    = [] -> null
      - dns_search                                  = [] -> null
      - entrypoint                                  = [
          - "/docker-entrypoint.sh",
        ] -> null
      - env                                         = [] -> null
      - group_add                                   = [] -> null
      - hostname                                    = "3ee8fdd54e48" -> null
      - id                                          = "3ee8fdd54e48dcfec0e72566cf5cb09362670c53d765b2a822f18d6924adc56e" -> null
      - image                                       = "sha256:7f0adca1fc6c29c8dc49a2e90037a10ba20dc266baaed0988e9fb4d0d8b85ba0" -> null
      - init                                        = false -> null
      - ipc_mode                                    = "private" -> null
      - log_driver                                  = "json-file" -> null
      - log_opts                                    = {} -> null
      - logs                                        = false -> null
      - max_retry_count                             = 0 -> null
      - memory                                      = 0 -> null
      - memory_reservation                          = 0 -> null
      - memory_swap                                 = 0 -> null
      - must_run                                    = true -> null
      - name                                        = "training" -> null
      - network_data                                = [
          - {
              - gateway                   = "172.17.0.1"
              - global_ipv6_prefix_length = 0
              - ip_address                = "172.17.0.2"
              - ip_prefix_length          = 16
              - mac_address               = "16:39:c4:8a:99:7e"
              - network_name              = "bridge"
            },
        ] -> null
      - network_mode                                = "bridge" -> null
      - platform                                    = "linux" -> null
      - privileged                                  = false -> null
      - publish_all_ports                           = false -> null
      - read_only                                   = false -> null
      - remove_volumes                              = true -> null
      - restart                                     = "no" -> null
      - rm                                          = false -> null
      - runtime                                     = "runc" -> null
      - security_opts                               = [] -> null
      - shm_size                                    = 64 -> null
      - start                                       = true -> null
      - stdin_open                                  = false -> null
      - stop_signal                                 = "SIGQUIT" -> null
      - stop_timeout                                = 1 -> null
      - storage_opts                                = {} -> null
      - sysctls                                     = {} -> null
      - tmpfs                                       = {} -> null
      - tty                                         = false -> null
      - wait                                        = false -> null
      - wait_timeout                                = 60 -> null

      - ports {
          - external = 80 -> null
          - internal = 80 -> null
          - ip       = "0.0.0.0" -> null
          - protocol = "tcp" -> null
        }
    }

  # docker_image.nginx will be destroyed
  - resource "docker_image" "nginx" {
      - id          = "sha256:7f0adca1fc6c29c8dc49a2e90037a10ba20dc266baaed0988e9fb4d0d8b85ba0nginx:latest" -> null
      - image_id    = "sha256:7f0adca1fc6c29c8dc49a2e90037a10ba20dc266baaed0988e9fb4d0d8b85ba0" -> null
      - name        = "nginx:latest" -> null
      - repo_digest = "nginx@sha256:7f0adca1fc6c29c8dc49a2e90037a10ba20dc266baaed0988e9fb4d0d8b85ba0" -> null
    }

Plan: 0 to add, 0 to change, 2 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

docker_container.nginx: Destroying... [id=3ee8fdd54e48dcfec0e72566cf5cb09362670c53d765b2a822f18d6924adc56e]
docker_container.nginx: Destruction complete after 1s
docker_image.nginx: Destroying... [id=sha256:7f0adca1fc6c29c8dc49a2e90037a10ba20dc266baaed0988e9fb4d0d8b85ba0nginx:latest]
docker_image.nginx: Destruction complete after 0s

Destroy complete! Resources: 2 destroyed.
```

## Summary

This session demonstrated:
1. Installing Terraform via Homebrew
2. Creating a Terraform configuration for Docker resources
3. Troubleshooting common errors:
   - Typo in repository name (`hashicorpt` vs `hashicorp`)
   - Markdown syntax in configuration file (`hcl` marker)
   - Invalid attribute reference (`.latest` vs `.image_id`)
   - Docker Hub rate limiting (solved with `docker login`)
4. Successfully applying the configuration to create infrastructure
5. Destroying the infrastructure when no longer needed

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| Repository not found | Verify correct spelling: `hashicorp/tap` not `hashicorpt/tap` |
| `hcl` marker in config file | Remove markdown syntax from `.tf` files |
| Invalid attribute reference | Use `image_id` instead of `latest` for docker_image resource |
| Docker Hub rate limit | Authenticate with `docker login` before pulling images |
