# AI Agent Instructions for macos-virtualbox

This repository contains a push-button installer for macOS on VirtualBox. Here are the key aspects AI agents should understand to work effectively with this codebase:

## Project Architecture

The project consists of a single main Bash script `macos-guest-virtualbox.sh` that handles the entire macOS installation process. Key components:

- **Installation Stages**: Script is organized into discrete stages executed sequentially (e.g., `check_dependencies`, `create_vm`, `configure_vm`, etc.)
- **Core Functions**: Helper functions for VM management, disk operations, and user interaction
- **NVRAM/EFI Handling**: Specialized functions for creating and managing NVRAM variables and EFI settings

## Critical Workflows

1. **Installation Process**:
   - Downloads macOS from Apple servers
   - Creates and configures VirtualBox VM
   - Handles disk image creation and population
   - Manages EFI and NVRAM settings

2. **Key Commands**:
   - Basic usage: `./macos-guest-virtualbox.sh`
   - Stage-specific execution: `./macos-guest-virtualbox.sh <stage_name>`
   - Documentation: `./macos-guest-virtualbox.sh documentation`

3. **Dependency Requirements**:
   - GNU bash ≥ 4.3 or zsh ≥ 5.5
   - VirtualBox ≥ 6.1.6
   - GNU coreutils ≥ 8.22
   - Other tools: dmg2img, wget, xxd

## Project Conventions

1. **Error Handling**:
   - Extensive checks for required dependencies and tools
   - Version compatibility verification for VirtualBox and shell
   - Early exit on critical errors with informative messages

2. **File Organization**:
   - All temporary files use prefixes based on VM name or macOS release
   - VISO files for installation media
   - Separate EFI and NVRAM binary files for Apple services

3. **Variable Naming**:
   - VM-specific variables prefixed with `vm_`
   - macOS-specific variables include `macOS_release_name`
   - EFI/NVRAM variables follow Apple naming conventions

## Integration Points

1. **VirtualBox Integration**:
   - Uses VBoxManage CLI for VM operations
   - Handles storage controller configuration
   - Manages VM settings and EFI parameters

2. **Apple Services**:
   - Configures NVRAM variables for iCloud/iMessage
   - Downloads installation files from Apple servers
   - Manages system identifiers and serials

3. **Host System Integration**:
   - Detects and adapts to Windows, macOS, or Linux hosts
   - Handles path differences between operating systems
   - Manages host-specific tool requirements

## Important Files

- `macos-guest-virtualbox.sh`: Main script containing all functionality
- Generated files:
  - `*.viso`: VirtualBox installation media
  - `*.bin`: NVRAM variable files
  - `*.${storage_format}`: VM disk images

## Common Tasks

1. **Adding New macOS Version Support**:
   - Update `sucatalog` URLs in `set_variables()`
   - Add version-specific checks in `check_dependencies()`
   - Test compatibility with VirtualBox versions

2. **Modifying VM Configuration**:
   - Edit variables in `set_variables()`
   - Update `configure_vm()` for new VirtualBox settings
   - Modify EFI/NVRAM parameters as needed

3. **Debugging Installation Issues**:
   - Use `troubleshoot` command to gather system info
   - Check VirtualBox logs
   - Verify file checksums and dependencies

Remember to always check the VM state and use appropriate error handling when making changes to the installation process.