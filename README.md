# VSCode-Neovim Configuration

A comprehensive VSCode setup that emulates LazyVim's functionality by integrating Neovim keybindings within VSCode.

## ℹ️ Overview

This repository enhances Visual Studio Code with Neovim's powerful modal editing capabilities using the `vscode-neovim` extension. It integrates pre-configured keybindings that provide a LazyVim-like experience, facilitating an efficient and streamlined workflow.

## 📂 Repository Structure

```
.
├── README.md                  # Complete setup documentation
├── settings.json              # VSCode user settings and configurations  
├── keybindings.json           # Custom keybindings for VSCode-Neovim integration
├── vscode-neovim-keymaps.lua  # Neovim keymaps optimized for VSCode environment
├── vscode-extensions.md       # Curated list of recommended VSCode extensions
└── custom-vscode/             # VSCode UI customizations
    ├── custom-vscode.css      # Custom CSS for VSCode interface styling
    └── custom-vscode.js       # Custom JavaScript for VSCode functionality
```

## 📋 File Descriptions

### Core Configuration Files

#### `settings.json`
**Purpose**: VSCode user settings that configure the editor behavior, appearance, and extension-specific settings.

**Key configurations**:
- Neovim executable paths for different operating systems
- VSCode-Neovim extension settings and initialization paths
- Editor preferences (font, theme, formatting)
- Language-specific settings and formatters
- Git integration and terminal configurations

#### `keybindings.json`
**Purpose**: Custom keybinding mappings that resolve conflicts between VSCode defaults and Neovim modal editing.

**Key features**:
- Space-based leader key implementation
- Explorer navigation that works with Space leader
- Multi-command sequences for complex workflows
- Disabled conflicting VSCode default shortcuts
- Modal editing support across different VSCode contexts

#### `vscode-neovim-keymaps.lua`
**Purpose**: Lua configuration that bridges Neovim keybindings with VSCode commands through the vscode-neovim extension.

**Key functionality**:
- LazyVim-inspired keybinding mappings
- VSCode command integration via `require('vscode').action()`
- Environment detection (`vim.g.vscode`) for VSCode-specific behavior
- Window/pane navigation and management
- File operations and quick access commands

#### `vscode-extensions.md`
**Purpose**: Comprehensive list of recommended VSCode extensions with installation commands and usage notes.

**Contents**:
- Essential extensions for Neovim integration
- Development productivity tools
- Language-specific extensions
- UI/UX enhancement extensions
- Installation scripts for batch setup

### UI Customization Files

#### `custom-vscode/custom-vscode.css`
**Purpose**: Custom CSS styles for modifying VSCode's visual appearance beyond what's available in settings.

**Typical customizations**:
- Color scheme overrides and theme enhancements
- Font adjustments and typography improvements
- Interface element spacing and sizing modifications
- Custom animations and visual transitions
- UI element visibility and layout changes

#### `custom-vscode/custom-vscode.js`
**Purpose**: Custom JavaScript for extending VSCode functionality and adding interactive behaviors.

**Common use cases**:
- Custom commands and keyboard shortcuts
- Enhanced UI interactions and behaviors
- Automated workflows and productivity macros
- Integration with external tools and services
- Performance optimizations and tweaks

**Note**: CSS and JS customizations require extensions like "Custom CSS and JS Loader" to be applied to VSCode.

### Backup Your Current Settings

Before applying these settings, make sure to backup your current VS Code configuration:

```bash
# macOS
cp ~/Library/Application\ Support/Code/User/settings.json ~/settings.json.backup
cp ~/Library/Application\ Support/Code/User/keybindings.json ~/keybindings.json.backup
```

## 🚀 Key Features

### How vscode-neovim-keymaps.lua Works

The `vscode-neovim-keymaps.lua` file bridges Neovim keybindings with VSCode commands using the `vscode-neovim` extension. It works by:

1. **Detecting VSCode Environment**: The extension sets `vim.g.vscode` when running in VSCode
2. **Mapping Vim Keys to VSCode Actions**: Uses `require('vscode').action()` to execute VSCode commands
3. **Preserving Neovim Modal Editing**: Maintains all Vim motions and modes within VSCode

### LazyVim-Style Keybindings

The configuration provides comprehensive LazyVim-inspired keybindings:

#### Core Navigation

- **Leader Key**: `Space` - Primary command prefix
- **Window Navigation**: `<leader>h/j/k/l` - Move between editor groups
- **Quick Access**: `<leader>p` - Quick Open, `<leader>e` - File Explorer

### Keybinding Conflict Resolution

To maintain consistency with the `Space` leader key, several default VSCode keybindings were disabled or modified:

#### Explorer Space Key Conflicts

VSCode's default explorer uses `Space` for file selection, which conflicts with our leader key. The `keybindings.json` includes custom bindings that work around this:

```json
// Custom explorer navigation using space as leader
{
  "key": "space e",
  "command": "multiCommand.closeExplorerAndFocusEditor",
  "when": "explorerViewletVisible && !inputFocus"
},
{
  "key": "space a",
  "command": "multiCommand.closeAuxBarAndFocusEditor",
  "when": "auxiliaryBarVisible && !inputFocus"
}
```

#### Multi-Command Integration

Complex workflows are handled through the `multi-command` extension, allowing sequences of VSCode commands:

```json
{
  "command": "multiCommand.openFileAndCloseExplorer",
  "sequence": ["list.select", "workbench.action.closeSidebar"]
}
```

### VSCode-Neovim Integration Benefits

1. **Modal Editing in VSCode**: Full Vim motions, operators, and text objects
2. **VSCode Features**: IntelliSense, debugging, extensions, git integration
3. **Consistent Workflow**: Same keybindings work across different file types
4. **No Context Switching**: Edit with Vim efficiency without leaving VSCode

## 🛠 Installation & Setup

### Neovim Installation

#### macOS

```bash
brew install neovim
```

#### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install neovim
```

#### Linux (Arch)

```bash
sudo pacman -S neovim
```

#### Windows

```powershell
choco install neovim
# Or via Scoop
scoop install neovim
```

### Setup Configuration

1. **Install the `vscode-neovim` extension:**

2. **Clone this Repository:**

   ```bash
   git clone https://github.com/yourusername/vscode-settings.git
   cd vscode-settings
   ```

3. **Configure VSCode Settings:**

4. **Integrate with Neovim Configuration:**

   - **Create or update Neovim config:**

     ```bash
     mkdir -p ~/.config/nvim
     cp vscode-neovim-keymaps.lua ~/.config/nvim/
     ```

   - **Update your `init.lua` for VSCode integration:**

     ```lua
     if vim.g.vscode then
       require('vscode-neovim-keymaps')
     end
     ```

### VSCode-Neovim Settings

Configure Neovim paths according to your OS in `settings.json`:

- **macOS (Homebrew):**

  ```json
  {
    "vscode-neovim.neovimExecutablePaths.darwin": "/opt/homebrew/bin/nvim",
    "vscode-neovim.neovimInitVimPaths.darwin": "/Users/yourusername/.config/nvim/init.lua"
  }
  ```

- **Linux:**

  ```json
  {
    "vscode-neovim.neovimExecutablePaths.linux": "/usr/bin/nvim",
    "vscode-neovim.neovimInitVimPaths.linux": "/home/yourusername/.config/nvim/init.lua"
  }
  ```

- **Windows:**
  ```json
  {
    "vscode-neovim.neovimExecutablePaths.win32": "C:\\tools\\neovim\\nvim-win64\\bin\\nvim.exe",
    "vscode-neovim.neovimInitVimPaths.win32": "C:\\Users\\yourusername\\AppData\\Local\\nvim\\init.lua"
  }
  ```

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

### Common Issues

**Neovim not found error:**

```
vscode-neovim: Neovim executable not found
```

- Verify Neovim installation: `nvim --version`
- Update the executable path in VSCode settings
- Restart VSCode after making changes

**Keybindings not working:**

- Ensure `vscode-neovim` extension is installed and enabled
- Check that `vscode-neovim-keymaps.lua` is loaded in your `init.lua`
- Verify no conflicting keybindings in VSCode settings
- Check the VSCode Output panel for Neovim extension logs

**Space key conflicts in Explorer:**
If the space key doesn't work as leader in explorer:

- Ensure `keybindings.json` is properly copied
- Restart VSCode after updating keybindings
- Check for conflicting default VSCode keybindings that override space key

### Verifying Setup

To verify everything is working:

1. Open VSCode
2. Press `Space` + `e` - should toggle file explorer
3. Press `Space` + `p` - should open quick open
4. Try some Vim motions like `dw`, `ci"`, `V` for visual line mode

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
