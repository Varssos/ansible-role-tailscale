# tailscale

Ansible role to install and configure [Tailscale](https://tailscale.com/) VPN on Debian/Ubuntu systems.

## Requirements

- Debian or Ubuntu host
- `become: true` privileges (sudo)

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `tailscale_auth_key` | `{{ lookup('env', 'TAILSCALE_KEY') }}` | Auth key for `tailscale up`. Login skipped if empty |
| `tailscale_install_script_url` | `https://tailscale.com/install.sh` | URL of the official install script |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: tailscale
```

Set the auth key via environment variable before running:
```bash
export TAILSCALE_KEY="tskey-auth-..."
ansible-playbook run.yml -K
```

## License

MIT

## Author

Varssos