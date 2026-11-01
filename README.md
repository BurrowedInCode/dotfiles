# dotfiles

My current Niri, Neovim, Zsh, and Ghostty configuration. Packages use a
GNU Stow-compatible layout; the installer only needs Bash and standard Linux tools.

| Package | Contents |
| --- | --- |
| `niri` | Compositor config, keybindings, and existing DMS settings |
| `nvim` | LazyVim setup, plugin lockfile, and custom plugins/themes |
| `zsh` | `.zshrc`, `.zshenv`, and Starship prompt settings |
| `ghostty` | Zsh terminal, Rosé Pine Moon / Catppuccin Latte, and local theme |

## Install

```sh
bash ~/dotfiles/install.sh --dry-run
bash ~/dotfiles/install.sh
```

Select individual packages with `bash ~/dotfiles/install.sh zsh nvim`.
The installer links app configs under `${XDG_CONFIG_HOME:-$HOME/.config}` and
shell startup files in `$HOME`. Existing configs, including broken symlinks,
are moved to a unique backup under
`${XDG_STATE_HOME:-$HOME/.local/state}/dotfiles/backups/`.
Already-linked configs are left alone, and dry runs do not write anything.
No software is installed, no apps are started, and the login shell is not changed.
Keep this checkout in place while its symlinks are in use.

To undo an install, remove only the symlink created by the installer and move
the printed backup back to its original location.

## Local setup

- **Zsh:** uses Oh My Zsh with `zsh-autosuggestions` and
  `zsh-syntax-highlighting`, Starship, and zoxide. Install these separately.
  NVM is loaded lazily if installed. Zellij starts automatically when available;
  its config is no longer managed here.
- **Private settings:** put API keys needed by all shells in `~/.zshenv.local`;
  interactive-only settings and credential-bearing project aliases belong in
  `~/.zshrc.local`. Both are loaded by the tracked startup files and ignored by
  Git. Set their permissions to `600`. Before installing Zsh, move private
  settings from your existing startup files into these local files; credentials
  were deliberately excluded from this snapshot.
- **Ghostty:** uses `/usr/bin/zsh` and `JetBrainsMono Nerd Font Mono`.
- **Niri:** `Super+T` opens Ghostty, `Super+D` opens DMS spotlight, and `Super+B`
  opens Brave. Waybar and `wl-paste --watch cliphist store` start with the session.
  Install the referenced programs separately. The `dms/` files preserve existing
  generated settings, including machine-specific outputs; adjust them on other
  machines. External DMS settings are not part of this repo.
- **Neovim:** uses LazyVim and downloads plugins on first launch. See
  `nvim/.config/nvim/lua/config/lazy.lua` and the plugin files for the current setup.

Other previously managed configs were preserved as standalone live copies,
but are no longer included here. The rebuild did not install the new Zsh files
or change the live Niri, Neovim, Ghostty, or shell configuration contents.
The original repository (including Git metadata and uncommitted work) and shell
startup files were backed up privately under `~/dotfiles-backups/`.
Do not publish that backup. Existing Git history has not been rewritten; review
it for private information before publishing.

## Checks

```sh
python3 -m unittest discover -s tests -v
bash -n install.sh
zsh -n zsh/.zshrc zsh/.zshenv
```

Tests use disposable homes and do not start applications or change live configs.

## License

Original contributions use the [MIT License](LICENSE). Third-party code,
themes, and configurations retain their respective licenses.
# dotfiles
