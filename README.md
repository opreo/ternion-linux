# ternion-linux &nbsp; [![bluebuild build badge](https://github.com/luciascarlet/ternion-linux/actions/workflows/build.yml/badge.svg)](https://github.com/luciascarlet/ternion-linux/actions/workflows/build.yml)

See the [BlueBuild docs](https://blue-build.org/how-to/setup/) for quick setup instructions for setting up your own repository based on this template.

This is a highly experimental Fedora Atomic Desktop image featuring the Trinity Desktop Environment.

Use `ternion-linux` for non-NVIDIA systems and `ternion-linux-nvidia` for systems with NVIDIA graphics.

The image is technically usable, but it is not polished at all, and I recommend pinning your existing deployment before rebasing.

## Installation

> **Warning**  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First, rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/luciascarlet/ternion-linux:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/luciascarlet/ternion-linux:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If built on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso).

Unfortunately, these ISOs cannot be distributed on GitHub for free (due to their large sizes), so, for public projects, something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign).

You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/luciascarlet/ternion-linux
```
