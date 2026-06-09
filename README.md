# ansible-hyprland

[![CICD](https://github.com/jahrik/ansible-hyprland/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-hyprland/actions/workflows/cicd.yml)

Install and configure [Hyprland](https://hyprland.org/) — a dynamic tiling Wayland compositor — along with a full suite of supporting packages (waybar, wofi, mako, kitty, swww, etc.) and deploy config files to `~/.config/hypr/`.

Supports **Arch Linux** (primary, via AUR packages through `jahrik.yay`) and **Debian/Ubuntu** (basic install only).

## Requirements

- Arch Linux: depends on `jahrik.yay` role for AUR packages
- Debian: `hyprland` must be available in your apt sources

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
# Lint
yamllint .

# Full molecule test (Arch container)
molecule test

# Iterative
molecule converge
molecule destroy
```

## License

GPLv2
