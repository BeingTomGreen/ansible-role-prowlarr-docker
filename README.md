# beingtomgreen.prowlarr_docker

A simple role for running Prowlarr via Docker compose.

## Installation & usage

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

Now you're free to use it within your project:

```yaml
---

- hosts: prowlarr
  become: true
  vars:
    prowlarr_docker_environment:
      PUID: '6900'
      PGID: '6900'
      TZ: 'Europe/London'

    prowlarr_docker_networks:
      - 'arrrrrr'

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
