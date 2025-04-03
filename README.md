# armbian-bakery

Customize the configuration of a base Armbian image

## Concept

configure [base Armbian image](https://armbian.com/download) [Autoconfig] for these goals:

* root password
* user account with password
* WiFi enabled for one SSID
* minimum to run [ansible-bakery](https://github.com/jkt628/ansible-bakery)

## Set up

this repository avoids committing secrets by `.gitignore` so requires some set up.

```bash
TARGET=jkt-rv-ha # choose one of multiple configurations
mkdir -p secrets/$TARGET
cp .not_logged_in_yet secrets/$TARGET/.not_logged_in_yet
${VISUAL:vi} secrets/$TARGET/.not_logged_in_yet
```

## Process

* burn a base image to removable media
* mount the media to desktop
* update [Autoconfig]

  ```bash
  sudo tee /media/$USER/armbi_root/root/.not_logged_in_yet <secrets/$TARGET/.not_logged_in_yet >/dev/null
  ```

* umount the media
* transfer the media to `$TARGET` and boot

## radxa-zero3

### [Autoconfig]

with `Armbian_24.11.1_Radxa-zero3_bookworm_vendor_6.1.75-homeassistant_minimal` the radxa-zero3 will not complete [Autoconfig] via
[armbian-firstlogin](https://github.com/armbian/build/blob/main/packages/bsp/common/usr/lib/armbian/armbian-firstlogin).  one way to complete this step is to `ssh root@radxa-zero3`
using, interestingly, the `PRESET_ROOT_PASSWORD` from [.not_logged_in_yet](./.not_logged_in_yet).

[Autoconfig]: (https://docs.armbian.com/User-Guide_Autoconfig/)
