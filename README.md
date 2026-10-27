# proton-profiles

Community game profiles for [Game Control Hub](https://github.com/Voxvalve/Proton-Launch-Manager).
They power the **✦ Optimize** button: one click applies the settings below for the player's graphics card.

## Format

```json
{
  "app_id": "1091500",
  "name": "Cyberpunk 2077",
  "recommended": {
    "amd":     ["gamemode", "ntsync", "proton_wayland", "redlauncher_skip", "mesa_shader_cache_10g"],
    "nvidia":  ["gamemode", "ntsync", "proton_wayland", "redlauncher_skip", "nvapi"],
    "default": ["gamemode", "ntsync", "proton_wayland", "redlauncher_skip"]
  },
  "notes": "Plain-language tips, shown to players under Advanced."
}
```

- **`app_id`** — the game's Steam App ID (the number in its store URL).
- **`recommended`** — setting IDs from the app's `launch_options.json`. `amd` / `nvidia` are used on those cards, `default` on everything else.
- **`notes`** — short, plain-language tips. Write for players, not for Linux experts.

## What belongs in Optimize

Keep it to settings that are safe for everyone and genuinely help that game:

- ✅ Performance basics (`gamemode`, `ntsync`, `proton_wayland`), game-specific fixes (launcher skips, `force_dx11` where it helps), `nvapi` **only** for games with DLSS or Reflex, the larger shader cache for big AMD/Intel open worlds.
- ❌ **Personal preferences** — the FPS overlay, HDR. Players turn these on themselves; mention them in `notes` instead.
- ❌ **GE-Proton / Proton-CachyOS-only settings** (upscaler upgrades, frame generation, DXVK async). Optimize must work on Steam's default Proton.
- ❌ **Settings that are now defaults** — `amd_radv_icd` (AMDVLK was discontinued in 2025), `radv_perftest_*` (RADV turns these on itself), `vkd3d_dxr*` (on by default since VKD3D-Proton 2.11), `hdr_wsi`.
- ❌ **Debug or troubleshooting options** — `proton_log`, `no_esync`, `no_fsync`.

Every setting is still available to players under Advanced in the app — a profile only decides what Optimize turns on.
