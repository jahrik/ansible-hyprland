# ansible-hyprland

[![CICD](https://github.com/jahrik/ansible-hyprland/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-hyprland/actions/workflows/cicd.yml)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-jahrik.hyprland-blue?logo=ansible)](https://galaxy.ansible.com/ui/standalone/roles/jahrik/hyprland/)

Install and configure [Hyprland](https://hyprland.org/) — a dynamic tiling Wayland compositor — along with a full suite of supporting packages (waybar, wofi, mako, kitty, swww, etc.) and deploy config files to `~/.config/hypr/`.

## OS Support

| Platform | Install method |
|---|---|
| Arch Linux | AUR (`hyprland`, `swaylock-effects`, `swww`, `wlogout`) + pacman (`waybar`, `wofi`, `mako`, `kitty`, etc.) via `jahrik.yay` |
| Debian / Ubuntu | `apt install hyprland` |

macOS and SteamOS are not supported — Hyprland is a Wayland compositor that requires a compatible kernel.

## Requirements

- Arch Linux: depends on `jahrik.yay` role for AUR packages

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `install` | `true` | Set to `false` to uninstall hyprland and remove `~/.config/hyprland` |

## Dependencies

- `jahrik.yay` (Arch Linux only) — installs AUR packages including hyprland, waybar-hyprland, sddm-git, swaylock-effects, etc.

## Example Playbook

```yaml
- hosts: workstations
  roles:
    - role: jahrik.hyprland
```

To uninstall:

```yaml
- hosts: workstations
  roles:
    - role: jahrik.hyprland
      vars:
        install: false
```

## Testing

```bash
uv sync
source .venv/bin/activate
yamllint .
ansible-lint
molecule test
```

## License

GPLv2

## Author Information

jahrik@gmail.com
