# BeamMP Launcher for macOS (CrossOver/Wine)

This document provides instructions for running BeamMP Launcher on macOS using Wine or CrossOver.

## Prerequisites

1. **BeamNG.drive** installed via Steam on Wine/CrossOver
2. **Wine** (via Homebrew) or **CrossOver** (commercial) installed on your Mac
3. **BeamMP Launcher** macOS binary

## Supported Configurations

The BeamMP Launcher now supports the following macOS setups:

### Wine Installations
- Standard Wine prefix: `~/.wine`
- Custom Wine prefixes
- Homebrew Wine installations

### CrossOver Bottles
- Steam bottle: `~/Library/Application Support/CrossOver/Bottles/Steam`
- BeamNG bottle: `~/Library/Application Support/CrossOver/Bottles/BeamNG`
- Custom bottles

### Other Compatibility Layers
- **Whisky**: Fork of Wine that works seamlessly
- Other Wine-based solutions

## Installation Instructions

### Option 1: Using Homebrew Wine

1. Install Wine via Homebrew:
   ```bash
   brew install --cask wine-stable
   ```

2. Install Steam in Wine and then BeamNG.drive through Steam

3. Download the BeamMP Launcher macOS binary

4. Make it executable:
   ```bash
   chmod +x BeamMP-Launcher
   ```

5. Run the launcher:
   ```bash
   ./BeamMP-Launcher
   ```

### Option 2: Using CrossOver

1. Install CrossOver from [CodeWeavers](https://www.codeweavers.com/crossover)

2. Create a bottle and install Steam

3. Install BeamNG.drive through Steam in CrossOver

4. Download the BeamMP Launcher macOS binary

5. Run the launcher directly - it will automatically detect your CrossOver installation

## Path Detection

The launcher automatically searches for your BeamNG.drive installation in:

1. **Standard Wine prefix**:
   - `~/.wine/drive_c/Program Files (x86)/Steam/steamapps/common/BeamNG.drive`

2. **CrossOver bottles**:
   - `~/Library/Application Support/CrossOver/Bottles/Steam/drive_c/Program Files (x86)/Steam/steamapps/common/BeamNG.drive`
   - `~/Library/Application Support/CrossOver/Bottles/BeamNG/drive_c/Program Files (x86)/Steam/steamapps/common/BeamNG.drive`

3. **User data paths**:
   - Wine: `~/.wine/drive_c/users/{username}/Local Settings/Application Data/BeamNG/BeamNG.drive`
   - CrossOver: `~/Library/Application Support/CrossOver/Bottles/{bottle}/drive_c/users/crossover/AppData/Local/BeamNG/BeamNG.drive`

## Known Issues & Solutions

### Issue: "Game directory was not found"
**Solution**: 
- Ensure BeamNG.drive is installed and has been run at least once
- Check that the `integrity.json` file exists in your BeamNG.drive installation folder
- Verify your Steam library folders if using multiple drives/locations

### Issue: "Failed to launch the game"
**Solution**:
- Ensure Wine is installed and accessible from command line
- Try running: `which wine64` or `which wine` to verify Wine installation
- For CrossOver, the launcher will try to use CrossOver's Wine automatically

### Issue: Mods not loading
**Solution**:
- The launcher automatically handles this by placing mods in lowercase (`beammp.zip` instead of `BeamMP.zip`)
- Ensure the mods folder has write permissions
- Manually verify that `mods/multiplayer/beammp.zip` exists in your BeamNG user folder

### Issue: Multiple vehicles spawning or vehicles not visible
**Solution**:
- This is a known Wine/CrossOver compatibility issue with the game itself, not the launcher
- Ensure you're using the latest version of Wine/CrossOver
- Check the BeamMP forums for game-specific Wine compatibility issues

## Building from Source

To build the macOS version yourself:

1. Install dependencies via vcpkg:
   ```bash
   vcpkg install zlib nlohmann-json openssl cpp-httplib[openssl] curl
   ```

2. Build with CMake:
   ```bash
   mkdir build-macos
   cd build-macos
   cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=[path-to-vcpkg]/scripts/buildsystems/vcpkg.cmake
   cmake --build . --config Release
   ```

3. The executable will be in `build-macos/BeamMP-Launcher`

## Troubleshooting

### Enable Debug Logging

Run the launcher with verbose output to see detailed path detection:
```bash
./BeamMP-Launcher 2>&1 | tee beammp-debug.log
```

### Manual Path Configuration

If automatic detection fails, you can try setting the user path manually:
```bash
./BeamMP-Launcher --user-path "/path/to/BeamNG/user/folder"
```

### Check Wine Installation

Verify Wine is working:
```bash
wine64 --version
```

For CrossOver, check the bottles:
```bash
ls -la ~/Library/Application\ Support/CrossOver/Bottles/
```

## Contributing

If you encounter issues or have improvements for macOS support, please:
1. Check existing issues on GitHub
2. Create a detailed bug report with your system configuration
3. Include the debug log output

## Additional Resources

- [BeamMP Documentation](https://docs.beammp.com/)
- [BeamMP Forum](https://forum.beammp.com/)
- [BeamMP Discord](https://discord.gg/beammp)
- [CrossOver Support](https://www.codeweavers.com/support)
- [Wine HQ](https://www.winehq.org/)

## Credits

macOS/Wine/CrossOver support added based on community feedback and GitHub issues:
- Issue #64: Add support for MacOS Wine - Especially for CrossOver
- Issue #83: Mods not loading up on Mac CrossOver
- Issue #163: Client failed to start on mac

Special thanks to the BeamMP community for testing and feedback!
