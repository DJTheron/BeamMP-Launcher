# Using BeamMP Launcher on macOS with CrossOver

This fix allows the **Windows .exe binary** of BeamMP Launcher to work properly when run through CrossOver or Wine on macOS.

## What Was Fixed

The Windows binary now detects when it's running on macOS (via CrossOver/Wine) and skips Linux-specific patches that were causing problems. Per issue #64, these patches are not needed on macOS.

## How to Use

1. **Install CrossOver** on your Mac (or use Wine/Whisky)

2. **Create a Windows bottle** in CrossOver and install:
   - Steam (Windows version)
   - BeamNG.drive (via Steam)

3. **Download the Windows binary** of BeamMP Launcher:
   - Get `BeamMP-Launcher.exe` from the releases page
   - Or build from this branch

4. **Run BeamMP-Launcher.exe** in your CrossOver bottle:
   - The launcher will automatically detect it's running on macOS
   - It will skip the problematic Linux patches
   - It will work normally with your Windows games in CrossOver

## What Happens

When you run the launcher:
```
Wine/CrossOver on macOS detected! Skipping Linux-specific patches.
macOS Wine/CrossOver works best without the Linux patches.
```

The launcher then proceeds to work normally, finding your BeamNG.drive installation and mods through the standard Windows registry and file paths that CrossOver provides.

## Technical Details

The fix works by:
1. Detecting Wine is present (via registry key)
2. Checking the `HOME` environment variable
3. If `HOME` starts with `/Users/` (macOS) instead of `/home/` (Linux), skipping the patches
4. Only applying patches on actual Linux Wine/Proton where they're needed

## Compatibility

- ✅ CrossOver on macOS (Intel & Apple Silicon)
- ✅ Wine on macOS (via Homebrew)
- ✅ Whisky (CrossOver fork)
- ✅ Still works correctly on Windows
- ✅ Still works correctly on Linux Wine/Proton

## Troubleshooting

If you encounter issues:
1. Make sure you're running the Windows .exe in CrossOver, not trying to run a macOS binary
2. Ensure BeamNG.drive is installed and has been run at least once
3. Check the launcher output - it should say "Wine/CrossOver on macOS detected"
4. If it doesn't detect macOS, check your CrossOver HOME environment variable

## References

- Issue #64: Add support for MacOS Wine - Especially for CrossOver
- Issue #83: Mods not loading up on Mac CrossOver
- Issue #163: Client failed to start on mac

## Note

You need the **Windows** binary (.exe), not a macOS native binary. Run it in CrossOver with your Windows games.
