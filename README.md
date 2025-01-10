# Ansible Pull Configuration

This repository contains Ansible configuration for automatic server provisioning using ansible-pull. It sets up a complete development environment with Fish shell, Rust, Neovim, Tmux, and other development tools.

## Quick Start

On a new server, run:

```bash
# Install required packages
apt-get update && apt-get install -y ansible git

# Run ansible-pull (replace with your repo URL)
ansible-pull -U <YOUR_REPO_URL> -C main
```

## What Gets Installed

### Core Development Tools
- **Fish Shell** with custom configuration
- **Starship** prompt with custom theme
- **Rust** (stable toolchain) via rustup
- **Build essentials** and common development tools

### Neovim Setup
- Latest Neovim built from source
- Custom Neovim configuration from [nvim-rust](https://github.com/uberbalogun/nvim-rust)
- Mason plugins:
  - `stylua` - Lua formatter
  - `codelldb` - Debug adapter for LLDB
  - `lua-language-server` - LSP for Lua
  - `rust-analyzer` - LSP for Rust

### Tmux Configuration
- Custom prefix: `Ctrl-a`
- Mouse support enabled
- Plugins:
  - `tmux-sensible` - Basic tmux settings
  - `tmux-resurrect` - Save/restore sessions
  - `tmux-continuum` - Automatic save/restore
  - `tmux-floax` - Floating terminal
  - `tmux-sessionx` - Session manager
  - Dracula theme

## Usage Guide

### Fish Shell
- Fish is set as the default shell
- Custom aliases and environment variables configured
- Starship prompt enabled with Git, Rust, and Node.js indicators

### Neovim
The Neovim configuration comes from [nvim-rust](https://github.com/uberbalogun/nvim-rust). Refer to that repository for detailed keybindings and features.

Key features include:
- Full Rust development environment with rust-analyzer
- Debug support with codelldb
- Code completion with nvim-cmp
- Git integration
- Smart code folding with nvim-ufo
  - `<space>ft` - Toggle code folding
  - Automatic fold detection using treesitter
  - Visual fold column indicator

### Tmux

#### Basic Commands
- `Ctrl-a` - Prefix key (instead of default `Ctrl-b`)
- `Prefix + c` - Create new window
- `Prefix + ,` - Rename window
- `Prefix + w` - List windows
- `Prefix + &` - Kill window

#### Plugin Features

**Tmux Sessionx** (`Prefix + o`):
- Quick session switcher
- Fuzzy finding for sessions
- Integrated with zoxide for smart directory jumping
- Window dimensions: 85% height, 75% width
- Default projects path: `~/projects`

**Tmux Floax** (`Prefix + f`):
- Creates floating terminal windows
- Window dimensions: 85% height, 75% width
- Perfect for quick commands or file viewing

**Session Management**:
- Sessions are automatically saved every 15 minutes
- Sessions are automatically restored when tmux starts
- `Prefix + Ctrl-s` - Save session manually
- `Prefix + Ctrl-r` - Restore session manually

## Customization

### Adding New Tools
1. Edit `roles/dev-tools/tasks/main.yml`
2. Add new tasks for tool installation and configuration
3. Push changes to your repository
4. Run ansible-pull again on target servers

### Updating Configurations
1. For Neovim: Update your configuration in the [nvim-rust](https://github.com/uberbalogun/nvim-rust) repository
2. For Tmux/Fish: Edit the respective configuration sections in `roles/dev-tools/tasks/main.yml`
3. Push changes and re-run ansible-pull

## Troubleshooting

If you encounter issues:

1. **Neovim Plugins**: 
   ```bash
   # Manually install Mason plugins
   nvim --headless -c "MasonInstall stylua codelldb lua-language-server rust-analyzer" -c qall
   ```

2. **Tmux Plugins**:
   ```bash
   # Manually install plugins
   ~/.tmux/plugins/tpm/bin/install_plugins
   ```

3. **Fish Shell**:
   ```bash
   # Verify Fish is default shell
   echo $SHELL
   # Change default shell if needed
   chsh -s /usr/bin/fish
   ```

## Adding New Servers

1. Ensure the server has internet access
2. Install ansible and git
3. Run the ansible-pull command
4. The server will automatically configure itself based on the playbook

For any issues or feature requests, please open an issue in the repository.
