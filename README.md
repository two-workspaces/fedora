# Deploy and Host Fedora on Railway

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/fedora-linux?referralCode=sLjDXb&utm_medium=integration&utm_source=button&utm_campaign=fedora-linux)

This template runs a full Fedora 44 desktop with the Xfce environment in the cloud, streamed to any device through the [linuxserver.io Webtop](https://docs.linuxserver.io/images/docker-webtop/) Selkies web interface. Open your Railway domain, log in, and you have a real Fedora desktop with a terminal, file manager, browser, `dnf` and `sudo`. Files and settings in the home directory persist between visits.

## About Hosting Fedora

The service streams a GPU-less Xfce desktop over WebSockets with the linuxserver.io Selkies stack. Fedora also publishes Xfce as an official spin. Access is gated by HTTP basic auth (`CUSTOM_USER` and a generated `PASSWORD`), and the user's home persists on a volume at `/config`. Set `TITLE` to change the browser tab name.

## Common Use Cases

- Try Fedora without installing it: current packages, `dnf`, and the Red Hat family's tooling
- Test software, scripts or packaging on Fedora before shipping to RHEL-family systems
- A persistent Linux workstation reachable from an iPad, Chromebook, phone or locked-down work laptop
- A disposable sandbox for opening untrusted files or links away from your real machine

## Dependencies for Fedora Hosting

- None. Single service, no database.

### Deployment Dependencies

- [linuxserver.io Webtop image docs](https://docs.linuxserver.io/images/docker-webtop/)
- [Selkies project](https://github.com/selkies-project)

### Implementation Details

**First use:** open your Railway domain and log in with `CUSTOM_USER` and the generated `PASSWORD`, which are in the service's Variables tab. The desktop appears. On touch devices, use the sidebar for keyboard and gestures. The desktop user `abc` has passwordless `sudo`, so `sudo dnf install` works from the built-in terminal.

Notes and limits:

- Keep the login strong: the password is the whole security model for a desktop with sudo.
- Only `/config` (the home directory) persists. Packages installed with `dnf` live outside it and are gone after a redeploy. Reinstall them, or keep a setup script in your home.
- Rendering runs on the CPU, since Railway has no GPU. That's fine for desktop apps and light video, not for 3D or heavy media work.
- This is Fedora's userland in a container. Railway's kernel runs it, so kernel, bootloader and SELinux settings are not yours to change.
- The idle footprint is about 230–250 MB, so it boots fine on the 512 MB Trial plan. Give it 1–2 GB if you run a browser or an IDE inside.
- The virtual screen is capped at 4K (`MAX_RES=3840x2160`), and the desktop still resizes to your browser window.
- There is no Docker daemon inside the desktop.
- Prefer another distro? The same author publishes Linux Desktops on [Ubuntu](https://railway.com/deploy/linux-desktop?referralCode=sLjDXb), [Debian](https://railway.com/deploy/linux-desktop-debian?referralCode=sLjDXb), [Arch](https://railway.com/deploy/linux-desktop-arch?referralCode=sLjDXb) and [Alpine](https://railway.com/deploy/linux-desktop-alpine?referralCode=sLjDXb), and a [Linux](https://railway.com/deploy/linux?referralCode=sLjDXb) server template.

## Why Deploy Fedora on Railway?

Railway is a singular platform to deploy your infrastructure stack. Railway will host your infrastructure so you don't have to deal with configuration, while allowing you to vertically and horizontally scale it.

By deploying Fedora on Railway, you are one step closer to supporting a complete full-stack application with minimal burden. Host your servers, databases, AI agents, and more on Railway.
