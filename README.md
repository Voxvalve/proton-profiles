# proton-profiles

Community game profiles for Game Control Hub.
They power the **✦ Optimize** button: one click applies the launch options below for the player's graphics card.

## Format

```json
{
  "app_id": "1091500",
  "name": "Cyberpunk 2077",
  "recommended": {
    "amd":     "MESA_SHADER_CACHE_MAX_SIZE=10G gamemoderun %command% --launcher-skip",
    "nvidia":  "gamemoderun %command% --launcher-skip",
    "default": "gamemoderun %command% --launcher-skip"
  },
  "notes": "Plain-language tips, shown to players under Advanced."
}
```

- **`app_id`**: the game's Steam App ID (the number in its store URL).
- **`recommended`**: Steam launch options, written exactly as you would type them into Steam: variables, then wrappers like `gamemoderun`, then `%command%`, then game arguments. `amd` and `nvidia` are used on those cards, `default` on everything else (Intel, or an unknown card). Launch options from ProtonDB or a forum can be pasted in as they are.
- **`notes`**: short, plain-language tips. Write for players, not for Linux experts.

### How the app reads a profile

The app reads `recommended` the same way it reads a game's existing launch options:

- **Variables and wrappers it knows** turn into its own switches, for example `MESA_SHADER_CACHE_MAX_SIZE=10G` turns on "Shader Cache". Each one is checked for the player's computer first: a setting for another graphics card or a missing tool is skipped. On CachyOS, `gamemoderun` becomes `game-performance` automatically.
- **Anything else** is kept as it is and added under Expert → Extra launch arguments.

To see how the app understands a launch line, paste it into a game's Extra launch arguments, or press Optimize, and look at which switches turn on.

## What belongs in Optimize

Keep it to launch options that are safe for everyone and genuinely help that game:

- ✅ `gamemoderun`; game-specific fixes like launcher skips (`--launcher-skip`, `--skip-launcher`) or `--use-d3d11` where it helps; and the larger shader cache (`MESA_SHADER_CACHE_MAX_SIZE=10G`) for big games on AMD/Intel. The cache size only matters for Steam games when Steam's Shader Pre-Caching is off, and it never hurts.
- ❌ **Personal preferences**: the FPS overlay (`MANGOHUD=1`, `mangohud`) and HDR (`DXVK_HDR=1`). Players turn these on themselves; mention them in `notes` instead.
- ❌ **GE-Proton / Proton-CachyOS only**: `PROTON_FSR4_UPGRADE`, `PROTON_MLFG_UPGRADE`, `PROTON_DLSS_UPGRADE`, `PROTON_XESS_UPGRADE` and `PROTON_ENABLE_WAYLAND` (Valve's Proton has no Wayland driver). Optimize must work on Steam's default Proton.
- ❌ **Now defaults**:
  - `PROTON_USE_NTSYNC=1`: Proton 11 uses NTSync by itself.
  - `PROTON_ENABLE_NVAPI=1`: on by default since Proton 9, so DLSS and Reflex work without it.
  - `AMD_VULKAN_ICD=RADV`: AMDVLK was discontinued in 2025.
  - `RADV_PERFTEST=…`: RADV turns these on itself.
  - `VKD3D_CONFIG=dxr` / `dxr11`: on by default since VKD3D-Proton 2.11.
  - `ENABLE_HDR_WSI=1`: only needed on NVIDIA drivers older than 595.
- ❌ **Doesn't exist in Proton**:
  - `DXVK_ASYNC=1`: not in current GE-Proton / Proton-CachyOS.
  - `PROTON_USE_VDESKTOP=1` and `PROTON_NO_D3D12=1`.
- ❌ **Debugging and troubleshooting**: `PROTON_LOG=1`, `PROTON_NO_ESYNC=1` and `PROTON_NO_FSYNC=1`.

Every setting is still available to players in the app. A profile only decides what Optimize turns on.
