# ansible-hyprland

Installs [Hyprland](https://hyprland.org/) Wayland compositor and a full desktop environment stack on Arch Linux. Deploys `hyprland.conf` and `background.jpg` to `~/.config/hypr/`. Supports uninstall via the `install` variable.

## Key Variables

| Variable | Default | Description |
|---|---|---|
| `install` | `true` | Set to `false` to uninstall hyprland and remove `~/.config/hyprland` |

## Task Flow

`tasks/main.yml` → `install.yml` or `uninstall.yml` based on `install | bool`

**install.yml:**
1. Include `archlinux.yml` or `debian.yml` for OS-specific package install
2. Create `~/.config/hypr/` directory
3. Copy `hyprland.conf` and `background.jpg` to `~/.config/hypr/`
4. Create `~/screenshots/` directory

**archlinux.yml:** `community.general.pacman` installs base packages; `jahrik.yay` installs AUR packages (hyprland, waybar-hyprland, sddm-git, swaylock-effects, swww, wlogout, etc.)

**debian.yml:** `ansible.builtin.apt` installs hyprland + basic extras

**uninstall.yml:** removes `hyprland` package and `~/.config/hyprland` directory

## Testing

```bash
yamllint .
ansible-lint
molecule test
molecule converge
molecule destroy
```

## CI

- **Lint**: yamllint + ansible-lint
- **Molecule**: Arch Linux via Docker (Wayland verify checks binary presence only)
- **Release**: publishes to Ansible Galaxy on merge to `main`
