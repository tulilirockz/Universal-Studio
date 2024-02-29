<div style="display: flex; align-items: center; justify-content: center;">
  <img src="./assets/studio-blob.png" alt="drawing" width="200rem"/>
</div>
<div style="display: flex; align-items: center; justify-content: center;">
<p style="font-size: 48px; margin-left: 0.1em;">Universal Studio</p>
</div>

---

Want Ubuntu Studio but in a reproducible and atomic environment? Then Universal Studio is for you! We provide all the same packages that you would get with Ubuntu Studio, but in a stable, atomic and reliable for all your content creation needs.

This image is distributed in two flavours: Plasma and Gnome, they have the same applications, but some minor differentes in theming, and some adapted aplications for better system integration (like `qpwgraph` <-> `helvum`). You can install this image by either installing the Offline ISO in [Releases](https://github.com/tulilirockz/Universal-Studio/releases) or by rebasing your system to one of them.

> This operating system image is not affilitated with Ubuntu or Fedora at all! We just use the Fedora base and get some inspirations from the Ubuntu Studio project. If you like this project, make sure to check out Ubuntu Studio proper!

## Rebasing

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/tulilirockz/universal-studio:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/tulilirockz/universal-studio:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

### Want to just copy and paste a command?

```shell
# Latest Plasma version
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/tulilirockz/universal-studio:latest

# Latest Plasma version + Nvidia
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/tulilirockz/universal-studio-nvidia:latest

# Latest Gnome version
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/tulilirockz/universal-studio-gnome:latest

# Latest Gnome version + Nvidia
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/tulilirockz/universal-studio-gnome-nvidia:latest
```

> Note: If these commands do not work first time, you are probably on a vanilla Fedora Atomic system, please run these but, instead of `ostree-image-signed:docker://`, use `ostree-unverified-registry:`, like the follwing command:
>```shell
># Unsigned version, please refrain from using this! - Only rebase to this first, then rebase to a signed image if you arent on a Universal Blue system
>rpm-ostree rebase ostree-unverified-registry:ghcr.io/tulilirockz/universal-studio:latest
>```


## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/blue-build/legacy-template
```
