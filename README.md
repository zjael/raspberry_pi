# raspberry pi ansible role

Supports:
- Update and Upgrade each node.
- Change node user password.
- Change hostnames specified by prefix and index from inventory file.
- Change GPU memory split.
- Change timezone.
- Change locale.
- Change SSH Port
- Install log2ram.
- Install specified packages.
- Disable HDMI to preserve power.
- Disable IPv6 of specified interfaces.
- Disallow SSH root login and empty passwords.
- Disallow SSH password authentication, if SSH key is provided.
- Allows SSH password authentication, within ip range, if specified.

By default:
- Updates and upgrades each node.
- Disallows SSH root login and empty passwords.
- Installs log2ram, with 40mb RAM size for log folder.
- Sets gpu_mem to 16mb.
- Disables HDMI.
- Disables IPv6 on wlan0 and eth0
- Installs unattended upgrades

## Role Variables

```yaml
---
# All uncommented lines are default settings

#locale: 'en_DK.UTF-8'
#timezone: 'UTC'

# Password to assign ansible nodes current user, generate password using: openssl passwd -1 -salt $(openssl rand -base64 6) password_here
#new_password: '$1$Mxb8A8pk$Kj2j7KGoBxvux/JvB5OS41'

# Ex. 'node' will result in, node0, node1, node2...
#hostname_prefix: 'node'

# Addiontional packages to install
#packages:
#- git
#- tmux

# Changes SSH port
#ssh_port: 22

# Copies public key from host to ansible nodes
#ssh_public_key: ~/.ssh/id_rsa.pub

# Allow ssh access with password from specified ip range
#ssh_allow_password_ip_range: '192.168.*.*'

# RAM size for log2ram folder in megabytes
log2ram_size: '40'

# GPU memory split in megabytes
gpu_mem: '16' # 16, 64, 128 or 256

# Disable HDMI to preserve power
disable_hdmi: true

# Disable IPv6 on specified interfaces
disable_ipv6_interfaces:
  - wlan0
  - eth0

# Unattended-upgrade variables
unattended_origins_patterns:
  - 'origin=Raspbian,codename=${distro_codename},label=Raspbian'
```

## Example Playbook

```yaml
---
- hosts: all
  become: true

  vars_files:
  - config.yml

  roles:
    - zjael.raspberry_pi
```

## Credits

Huge thanks to [jnv](https://github.com/jnv) for his awesome [unattended-upgrades](https://github.com/jnv/ansible-role-unattended-upgrades) ansible role.

## License

MIT