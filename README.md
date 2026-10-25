# lynxOS

A macOS-like Linux distribution: an Arch Linux base with macOS-style
directories, app bundles and a custom desktop environment.

- **Arch base, macOS directories.** Uses Arch Linux under the hood, with
  macOS top-level directories (`/System`, `/Library`, `/Applications`,
  `/Users`, `/Volumes`) added as symlinks over the standard FHS root, so
  normal Arch packages and pacman keep working unmodified.
- **macOS app bundles.** Apps are bundles:
  `MyApp.app/Contents/{Info.json, Resources/, lynxOS/MyApp}` (see
  `scripts/apply-skel.sh` in `rootFSBuilder/`).
- **X11, [WindowServerWM](https://github.com/lynxOSX/WindowServerWM)** —
  the window manager, an openbox fork; the openbox preferences window
  should be removed and the theme location hard-coded (not decided yet).
- **Custom desktop environment**, written from scratch:
  - **SystemUIServer** — the panel/menu bar
  - **Finder** — file manager, and it also manages the desktop
  - **Dock** — the macOS dock
- More components/features — to be added.

## Repository layout

| | |
|---|---|
| [`rootFSBuilder/`](https://github.com/lynxOSX/rootFSBuilder) | builds the lynxOS rootfs (proot + pacman into a tarball — see its README) |
| [`WindowServerWM/`](https://github.com/lynxOSX/WindowServerWM) | the window manager — openbox fork rendering the macOS X title bar |
| [BootPanel](https://github.com/lynxOSX/BootPanel) | the boot panel — plymouth-like KMS/DRM (or legacy fbdev) splash: `#BFBFBF`, logo centered, spinner 185 px below center |
| (future) | SystemUIServer, Finder, Dock, an installer |

## Building the root filesystem

```sh
cd rootFSBuilder
./lynx-build all      # fetch → rootfs → install → bundle
```

Produces `out/lynxos-rootfs-<date>-x86_64.tar.gz`. Host requirements are
proot, zstd, curl, GNU tar, gzip, coreutils — no root, no VM, and the host
distro doesn't matter (developed on Alpine). See `rootFSBuilder/README.md`.

## TO-DO

- [x] make custom rootfs builder
- [x] boot panel (plymouth-alike) — [BootPanel](https://github.com/lynxOSX/BootPanel)
- [ ] start working on said custom programs (SystemUIServer, Finder, Dock)
- [ ] boot panel: started by an early boot stage in the rootfs, stopped when SystemUIServer is up
- [ ] build an installer / bootable image from the rootfs tarball
- [ ] openbox: remove preferences window, hard-code theme location
- ... more
