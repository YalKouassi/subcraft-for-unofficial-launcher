# SubCraft for Craft Unofficial Launcher

**An unofficial mirror** of [SubCraft](https://github.com/Aalzard/subcraft) releases, maintained by
[YalKouassi](https://github.com/YalKouassi), so that
[Craft Unofficial Launcher](https://github.com/YalKouassi/craft-unofficial-launcher) can install
and update SubCraft.

This repo is **not affiliated with, endorsed by or supported by Aalzard** (the authors of SubCraft),
**or by ArtCraft**. Report problems with SubCraft itself upstream at
<https://github.com/Aalzard/subcraft>; report problems with this mirror here.

## What this repo publishes

The packages in this repo's releases are **SubCraft's own builds**, as published on
[Aalzard/subcraft's releases](https://github.com/Aalzard/subcraft/releases). Nothing is rebuilt and no program file is
changed. Each release here:

- downloads upstream's packages and verifies each one before using it;
- renames them to the launcher's `<id>-<version>-<os>-<arch>` naming and, only where the launcher
  couldn't install an archive's layout, repacks that archive (the same files with the same bytes,
  in different folders);
- adds `craft-app.json`, the icon, `SHA256SUMS.txt`, and upstream's licence files from the same tag.

The notes of each release list every file, the upstream asset it came from, its SHA-256, and
whether it was repacked, so you can compare it with upstream's release.

### For SubCraft

- `SubCraft-<v>-linux-x86_64.tar.gz` is **renamed** to `subcraft-<v>-linux-x86_64.tar.gz` and
  otherwise mirrored byte for byte (the launcher accepts its `subcraft` binary where it is).
- `SubCraft-<v>-windows-x64.zip` becomes `subcraft-<v>-windows-x64-portable.zip` and is
  **repacked**: upstream's zip stores its folder names with `\` separators, which the launcher
  refuses as unsafe, so the bridge rewrites it with `/` separators and `SubCraft.exe` at its root.
  It holds the same files with the same bytes; only the folder layout and compression change.

Every download is checked against upstream's `SHA256SUMS.txt` first. Upstream has no reverse-DNS
app id, so this bridge uses `io.github.aalzard.subcraft`.

Not mirrored: the Inno Setup installer (`SubCraft-<v>-setup.exe`) and the optional `SubCraft-extra-environments.zip` pack.

## How it runs

[`.github/workflows/bridge.yml`](.github/workflows/bridge.yml) runs every 30 minutes. It uses
[craft-bridge](https://github.com/YalKouassi/craft-bridge) with [`bridge.toml`](bridge.toml) to
check upstream's latest release and mirror it if this repo doesn't have it yet. If upstream starts
publishing its own `craft-app.json`, the bridge stops publishing, and the launcher should point at
upstream directly.

Using this mirror means trusting its maintainer as well as upstream; see
[craft-bridge's Trust section](https://github.com/YalKouassi/craft-bridge#trust).

## Licences

SubCraft is licensed by its authors under Apache-2.0 OR MIT; each release attaches upstream's licence files.
This repo's own files (the config, workflow and this README) are available under MIT OR
Apache-2.0 ([LICENSE-MIT](LICENSE-MIT), [LICENSE-APACHE](LICENSE-APACHE)).
