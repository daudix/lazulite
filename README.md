# Lazulite

[![enceladus build badge](https://github.com/daudix/enceladus/actions/workflows/build.yml/badge.svg)](https://github.com/daudix/enceladus/actions/workflows/build.yml)

My personal flavors of [Fedora Silverblue](https://fedoraproject.org/atomic-desktops/silverblue/) and [uCore](https://github.com/ublue-os/ucore). They includes a small amount of changes that I always do on my own systems:

- Both
  - Install [fish shell](https://fishshell.com)
- Fedora Silverblue
  - Add all necessary media codecs and thumbnailers
  - Install [Extension Manager](https://flathub.org/apps/com.mattjakeman.ExtensionManager)
  - Install all core GNOME apps
  - Remove default Fedora wallpapers
  - Remove Firefox RPM
  - Remove GNOME Classic session
  - Replace Fedora Flatpaks with the ones from Flathub
  - Replace Sushi Flatpak with system package, so that it can make use of additional codecs
- uCore
  - Install [TuneD](https://tuned-project.org)

As these images are for personal use, I can't guarantee that their scope won't change, in fact it *will* quite often, as I change my own scope just as often.

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

Lazulite has two variants:

 - `latte` - Silverblue-based image (alternatively `desktop`)
 - `espresso` - uCore-based image (alternatively `server`)

To rebase an existing atomic Fedora installation to the latest build of select variant:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/daudix/enceladus:<VARIANT>
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/daudix/enceladus:<VARIANT>
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/daudix/enceladus
```
