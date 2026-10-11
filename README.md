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

## Manual setup (without Ansible)

Download and review the official installer before running it as root:

```bash
sudo apt install curl
curl -fL https://tailscale.com/install.sh -o /tmp/tailscale-install.sh
```

After reviewing it:

```bash
sudo sh /tmp/tailscale-install.sh
rm /tmp/tailscale-install.sh
sudo tailscale up
```

The last command provides interactive login. To match the role's optional
auth-key login, use `sudo tailscale up --auth-key="$TAILSCALE_KEY"` with an
auth key supplied securely in your environment. Never commit that key.
HTTPS certificate errors must be fixed in network policy or the trusted CA
store, not by disabling certificate verification.

## License

MIT

## Author

Varssos