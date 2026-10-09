# Optional achievements support

This branch is based on DCCM v35.13.7 (38d1a44). It adds an opt-in setting to preserve the game's achievement flow while keeping leaderboard submission disabled.

Add the following to `coremod/config/modcore.json`, then restart the game:

```json
{
  "EnableAchievements": true,
  "EnableGoldberg": false
}
```

The default remains `EnableAchievements=false`. When enabled at startup, the core does not install its game-level, Steam achievement-manager, or native achievement stubs, and runs the original Steam API synchronization callback. The game retains its own achievement eligibility rules.

The modified core has been built and launched with a real Steam client. Actual achievement unlocking and persistence require separate verification; there is no bulk achievement unlocking feature.

## Build against the matching release

Extract the official v35.13.7 Windows x64 package and run the dedicated NUKE target from this repository:

```powershell
./build.ps1 BuildManagedCorePatch --release-host-root '<release-directory>/core/host' --configuration Release
```

The target compiles ModCore's managed sources against the matching release dependencies, without rebuilding the native runtime. Output: `bin/managed-core-patch/net10.0/ModCore.dll`.

Exit the game and back up the original `coremod/core/host/ModCore.dll` before replacing it. Restore the official DLL to return to upstream behavior. Future Core updates may replace this custom assembly.

## Related mod

AutoParry is maintained separately in [dead-cells-qol](https://github.com/MoTao233/dead-cells-qol), a private repository. The achievements option does not require AutoParry.
