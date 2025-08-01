# VSCode Configuration

This repository contains my personal Visual Studio Code configuration files and settings.

## Contents

### Core Configuration Files
- **`settings.json`** - Main VS Code settings and preferences
- **`keybindings.json`** - Custom keyboard shortcuts and keybindings

## Usage

### Installation
1. Clone this repository
2. Copy the configuration files to your VS Code user directory:
   - **macOS**: `~/Library/Application Support/Code/User/`
   - **Windows**: `%APPDATA%\Code\User\`
   - **Linux**: `~/.config/Code/User/`

### Backup Your Current Settings
Before applying these settings, make sure to backup your current VS Code configuration:
```bash
# macOS
cp ~/Library/Application\ Support/Code/User/settings.json ~/settings.json.backup
cp ~/Library/Application\ Support/Code/User/keybindings.json ~/keybindings.json.backup
```

## Features

This configuration includes customizations for:
- **Editor appearance and behavior**
  - Clean editor interface with disabled minimap and whitespace rendering
  - Hidden overview ruler indicators for distraction-free coding
- **Custom keybindings for improved workflow**
  - Enhanced terminal toggle (`cmd+j`) that works when terminal is focused
  - File explorer navigation with `j/k` keys and Enter to open files
  - Quick split functionality in Explorer (`shift+\` for vertical, `-` for horizontal)
  - Improved quick open navigation with `j/k` for up/down movement
- **Extension configurations**
  - Optimized vscode-neovim settings with disabled ctrl key handling
  - MultiCommand extension setup for advanced file operations
- **Terminal and navigation enhancements**
  - Streamlined file management workflow
  - Keyboard-centric navigation patterns

## Recent Updates

### Latest Changes (July 2025)
- Enhanced terminal toggle keybinding to work when terminal is focused
- Added file split keybindings in Explorer for quick window management
- Improved navigation keybindings for quick open functionality
- Cleaned up editor interface by hiding visual indicators in overview ruler
- Updated vscode-neovim extension settings for better performance
- Added new multiCommand configurations for advanced file operations

## Compatibility

Tested with Visual Studio Code version 1.x and later.
Requires the following extensions for full functionality:
- vscode-neovim
- multi-command

## Contributing

Feel free to suggest improvements or report issues!

## License

Personal configuration - use at your own discretion.
