# VSCode-Neovim Configuration

LazyVim-inspired Neovim keybindings for VSCode using the `vscode-neovim` extension.

## 🎬 Demo

See the configuration in action:

![VSCode Neovim Configuration Demo](vscode-config-demo.mp4)

## ⚠️ Backup Your Settings First

Before installing, backup your current VSCode configuration:

```bash
# macOS
cp "~/Library/Application Support/Code/User/settings.json" ~/vscode-settings.backup.json
cp "~/Library/Application Support/Code/User/keybindings.json" ~/vscode-keybindings.backup.json

# Linux
cp ~/.config/Code/User/settings.json ~/vscode-settings.backup.json
cp ~/.config/Code/User/keybindings.json ~/vscode-keybindings.backup.json

# Windows
copy "%APPDATA%\Code\User\settings.json" "%USERPROFILE%\vscode-settings.backup.json"
copy "%APPDATA%\Code\User\keybindings.json" "%USERPROFILE%\vscode-keybindings.backup.json"
```

## 📂 What's Included

- `settings.json` - VSCode settings with Neovim paths and configurations
- `keybindings.json` - Custom keybindings that resolve Space key conflicts
- `vscode-neovim-keymaps.lua` - Neovim keymap configuration for VSCode
- `vscode-extensions.md` - Recommended extensions list
- `custom-vscode/` - Optional CSS/JS customizations

## 🚀 Key Features

- **Space Leader Key**: `<Space>` as primary command prefix
- **LazyVim-Style Navigation**: `<leader>h/j/k/l` for window movement
- **Quick Actions**: `<leader>p` (Quick Open), `<leader>e` (File Explorer)
- **Conflict Resolution**: Fixes Space key conflicts in VSCode Explorer
- **Full Modal Editing**: All Vim motions and text objects work in VSCode


## 🛠 Installation & Setup

### 1. Install Neovim

```bash
# macOS
brew install neovim

# Linux (Ubuntu/Debian) 
sudo apt install neovim

# Windows
choco install neovim
```

### 2. Install VSCode Extension

```bash
code --install-extension asvetliakov.vscode-neovim
code --install-extension ryuta46.multi-command
```

### 3. Clone and Apply Configuration

```bash
git clone https://github.com/yourusername/vscode-settings.git
cd vscode-settings

# Copy Neovim config
mkdir -p ~/.config/nvim
cp vscode-neovim-keymaps.lua ~/.config/nvim/

# Copy VSCode settings (backup first!)
cp settings.json "~/Library/Application Support/Code/User/"  # macOS
cp keybindings.json "~/Library/Application Support/Code/User/"  # macOS
```

### 4. Update Neovim init.lua

Add to your `~/.config/nvim/init.lua`:

```lua
if vim.g.vscode then
  require('vscode-neovim-keymaps')
end
```

### 5. Configure Neovim Path (if needed)

Update paths in VSCode settings if Neovim isn't found automatically:

```json
// macOS (Homebrew)
"vscode-neovim.neovimExecutablePaths.darwin": "/opt/homebrew/bin/nvim"

// Linux  
"vscode-neovim.neovimExecutablePaths.linux": "/usr/bin/nvim"

// Windows
"vscode-neovim.neovimExecutablePaths.win32": "C:\\tools\\neovim\\nvim-win64\\bin\\nvim.exe"
```

## ⚠️ Space Key Conflicts

VSCode's Explorer uses `Space` for file selection, which conflicts with our leader key. This configuration includes:

- **Custom keybindings** that resolve Space key conflicts in Explorer
- **Multi-command sequences** that work with Space as leader
- **Proper context handling** to ensure Space works as leader everywhere

**Common conflict symptoms:**
- Space key selects files in Explorer instead of acting as leader
- `<leader>e` doesn't work to toggle Explorer
- Space key appears "stuck" or unresponsive

**Solution:** You may need to remove any default 'space' keybindings that conflict with the configuration.

## 🔧 Customization

### Adding Custom Keybindings

Add your custom keybindings to `vscode-neovim-keymaps.lua`:

```lua
-- Custom keybinding example
keymap("n", "<leader>custom", "<cmd>lua require('vscode').action('your.custom.command')<CR>")

-- Multi-mode keybinding
keymap({"n", "v"}, "<leader>multi", "<cmd>lua require('vscode').action('editor.action.example')<CR>")
```

### Finding VSCode Commands

To discover VSCode command IDs:

1. Open Command Palette (`Cmd+Shift+P`)
2. Open Developer Tools (`Help` → `Toggle Developer Tools`)
3. Execute commands and check the console for command IDs
4. Use `workbench.action.openGlobalKeybindings` to see all available commands

## 🔧 Troubleshooting

**Neovim not found:**
- Verify installation: `nvim --version`
- Update executable path in VSCode settings
- Restart VSCode

**Keybindings not working:**
- Check `vscode-neovim` extension is enabled
- Ensure `vscode-neovim-keymaps.lua` is loaded in `init.lua`
- Check VSCode Output panel for Neovim logs

**Space key conflicts:**
- Ensure `keybindings.json` is copied correctly
- Restart VSCode after updating keybindings
- Remove conflicting VSCode default keybindings

### Quick Test
Verify setup works: `Space + e` (toggle explorer), `Space + p` (quick open), try Vim motions like `dw`, `ci"`

## 📚 Additional Resources

### Recommended Extensions

Install these extensions for the best experience (see `vscode-extensions.md` for complete list):

```bash
# Essential for this setup
code --install-extension asvetliakov.vscode-neovim
code --install-extension ryuta46.multi-command

# Recommended for development
code --install-extension esbenp.prettier-vscode
code --install-extension dbaeumer.vscode-eslint
code --install-extension eamodio.gitlens
code --install-extension tatosjb.fuzzy-search
```

### Learning Resources

- [vscode-neovim GitHub](https://github.com/asvetliakov/vscode-neovim) - Official extension documentation
- [LazyVim](https://www.lazyvim.org/) - Inspiration for keybinding patterns
- [Neovim Documentation](https://neovim.io/doc/) - Complete Neovim reference
- [VSCode Keybinding Reference](https://code.visualstudio.com/docs/getstarted/keybindings) - VSCode keybinding documentation

### Integration with Existing Neovim Config

If you have an existing Neovim configuration, you can integrate this setup by:

```lua
-- In your ~/.config/nvim/init.lua
if vim.g.vscode then
  -- VSCode Neovim specific settings
  require('vscode-neovim-keymaps')

  -- Disable plugins that don't work well in VSCode
  vim.g.loaded_netrw = 1
  vim.g.loaded_netrwPlugin = 1
else
  -- Your normal Neovim configuration
  require('your-normal-config')
end
```

## 🤝 Contributing

Contributions are welcomed! To contribute:

1. **Fork the repository**
2. **Create a feature branch**
3. **Test your changes thoroughly**
4. **Update documentation if needed**
5. **Submit a pull request**

### Areas for Contribution

- Additional keybinding mappings
- Better conflict resolution for VSCode defaults
- Platform-specific improvements
- Documentation improvements
- Extension compatibility fixes

## 📝 License

This setup is licensed under the MIT License. Feel free to use, modify, and distribute.

## Acknowledgments

- [vscode-neovim](https://github.com/asvetliakov/vscode-neovim) - The amazing extension that makes this possible
- [LazyVim](https://github.com/LazyVim/LazyVim) - Inspiration for keybinding patterns and workflow
- [Neovim community](https://neovim.io/)

---

Enjoy the power of Neovim within the comfort of VSCode! 🚀
