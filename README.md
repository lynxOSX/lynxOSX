# lynxOS

A macOS-like Linux distribution: an Arch Linux base with macOS-style
directories, app bundles and a custom desktop environment.

- **Arch base, macOS directories.** Uses Arch Linux under the hood, with
  macOS top-level directories (`/System`, `/Library`, `/Applications`,
  `/Users`, `/Volumes`) added as symlinks over the standard FHS root, so
  normal Arch packages and pacman keep working unmodified.
- **macOS app bundles.** Apps are bundles:
  `MyApp.app/Contents/{Info.json, Resources/, lynxOS/MyApp}` — built with
  [`AppBuilder`](https://github.com/lynxOSX/AppBuilder) (TOML project config
  compiled into the bundle's JSON manifest).
- **Qt for app GUIs.** WindowServerWM is a window manager, not a toolkit —
  it draws window chrome (the macOS X title bar), apps draw their own
  content. **Every app should use Qt** (Qt 6, Widgets) as its GUI toolkit,
  wrapped in [`AppKit`](https://github.com/lynxOSX/AppKit) (the
  10.6-SDK-style naming — `NSApplication`, `NSWindow`, `NSMenu`); the
  custom desktop components (SystemUIServer, Finder, Dock) use it too.
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
| [`rootFSBuilder`](https://github.com/lynxOSX/rootFSBuilder) | builds the lynxOS rootfs |
| [`WindowServerWM`](https://github.com/lynxOSX/WindowServerWM) | openbox fork rendering the macOS X title bar |
| [`BootPanel`](https://github.com/lynxOSX/BootPanel) | plymouth-like KMS/DRM (or legacy fbdev) |
| [`AppBuilder`](https://github.com/lynxOSX/AppBuilder) | builds app bundles from source |
| [`SystemUIServer`](https://github.com/lynxOSX/SystemUIServer) | the menu bar: Apple menu, global app menu, menu extras (`.menu` bundles) |
| (future) | Finder, Dock, an installer |

## TO-DO

- [x] make custom rootfs builder
- [x] boot panel (plymouth-alike) - [BootPanel](https://github.com/lynxOSX/BootPanel)
- [x] window manager based on openbox - [WindowServerWM](https://github.com/lynxOSX/WindowServerWM)
- [ ] start working on said custom programs (SystemUIServer, Finder, Dock)
- [ ] build an installer / bootable image from the rootfs tarball
- ... more
