# beingtomgreen.prowlarr_docker

A simple ansible role for running [Prowlarr](https://prowlarr.com/) via Docker compose using the [LinuxServer.io Prowlarr image](https://docs.linuxserver.io/images/docker-prowlarr).

For additional information on how to best handle your media paths see information on [wiki.servarr.com](https://wiki.servarr.com/docker-guide#consistent-and-well-planned-paths) and [trash-guides.info](https://trash-guides.info/File-and-Folder-Structure/Hardlinks-and-Instant-Moves/).

## Installation

Given that Galaxy seems to have abandoned roles, I suggest referencing this repository directly in your projects `requirements.yml`:

```yaml
---

roles:
  - name: beingtomgreen.prowlarr_docker
    src: https://github.com/BeingTomGreen/ansible-role-prowlarr-docker.git

collections: []
```

You can then install it alongside your other requirements as normal:

```bash
ansible-galaxy install -r requirements.yml
```

## Example usage

### Basic usage

```yaml
---

- hosts: prowlarr
  become: true
  vars:
    prowlarr_docker_env_puid: 5000
    prowlarr_docker_env_pgid: 5000

    prowlarr_docker_env_timezone: 'Europe/London'
  roles:
    - role: beingtomgreen.prowlarr_docker
```

### Want the kitchen sink?

Seriously, take a look at [`defaults/main.yml`](defaults/main.yml), it's obnoxiously commented, just for you.

```yaml
---

- hosts: prowlarr
  become: true
  vars:
    prowlarr_docker_cap_add:
      - CAP_WAKE_ALARM
      - CAP_AUDIT_CONTROL
    prowlarr_docker_cap_drop:
      - CAP_CHECKPOINT_RESTORE

    prowlarr_docker_container_name: 'prowlarr_container'

    prowlarr_docker_depends_on:
      - 'my-little service'

    prowlarr_docker_devices:
      - '/dev/dri:/dev/dri'
      - '/dev/kfd:/dev/kfd'

    prowlarr_docker_env_puid: 5000
    prowlarr_docker_env_pgid: 5000

    prowlarr_docker_env_timezone: 'Europe/London'

    prowlarr_docker_extra_environment_vars:
      SOME_OTHER_VAR: 'A_VALUE'

    prowlarr_docker_image_tag: '10.10.6'

    prowlarr_docker_labels:
      traefik.enable: 'true'
      traefik.http.routers.traefik-https.entrypoints: 'https'

    # Network mode
    prowlarr_docker_network_mode: 'service:glutun'

    # Or external networks:
    prowlarr_docker_external_networks:
      - 'my-little-network'

    # Or the default ports
    prowlarr_docker_ports:
      - '8989:8989'

    prowlarr_docker_pull_policy: 'weekly'

    prowlarr_docker_restart_policy: 'always'

    prowlarr_docker_additional_volumes:
      - '/path/to/tv:/tv'
      - '/path/to/usenet:/usenet'
      - '/path/to/torrents:/torrents'

    prowlarr_docker_base_directory: '/opt/prowlarr_docker'

    prowlarr_docker_prune_images: True
    prowlarr_docker_prune_until: '24h'

  roles:
    - role: beingtomgreen.prowlarr_docker
```

## Role Variables

See [`defaults/main.yml`](defaults/main.yml) for more details.

## Requirements

- Docker & docker compose installed on the target host
- ansible_user will also need to be in the docker group

## Dependencies

- community.docker

## License

[MIT](LICENSE)

## Author Information

[Tom Green](https://github.com/BeingTomGreen)
