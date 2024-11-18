# armbian-bakery

Customize the configuration of a base Armbian image

## Concept

configure [base Armbian image](https://armbian.com/download) [Autoconfig] for these goals:

* root password
* user account with password
* WiFi enabled for one SSID

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

[Autoconfig]: (https://docs.armbian.com/User-Guide_Autoconfig/)
