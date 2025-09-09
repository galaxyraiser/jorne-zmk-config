### Prepare workspace

[Getting started](https://zmk.dev/docs/development/local-toolchain/setup/native)

Current SDK version is 0.17.0 due to bump of picolib in 0.17.1 which is causing compilation failure.

```
cd ~ && wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.17.0/zephyr-sdk-0.17.1_linux-x86_64.tar.xz && tar xvf zephyr-sdk-0.17.0_linux-x86_64.tar.xz
zephyr-sdk-0.17.0/setup.sh
```

# !!! The modern SDK versions have a new changes in picolib which cause compilation errors.
https://forum.golioth.io/t/thingy91x-unable-to-build-examples-with-zephyr/1442/5

# On the Arch, we have a problem with native dtc from sdk host tools:
```
pacman -S dtc
rm -f ~//zephyr-sdk-0.17.0/sysroots/x86_64-pokysdk-linux/usr/bin/dtc
ln -s /usr/bin/dtc ~/zephyr-sdk-0.17.0/sysroots/x86_64-pokysdk-linux/usr/bin/dtc
```

### Build

```
west build -s app/ --pristine -- -DBOARD=nice_nano_v2 -DSHIELD=skeletyl_v2_elitec_<right/left> -DZMK_CONFIG=$(pwd)/zmk-config/config
```

To enable debug console need to append this lines:

```
-DEXTRA_DTC_OVERLAY_FILE=$(pwd)/zmk-config/config/boards/shields/skeletyl_v2_elitec/debug.overlay -DOVERLAY_CONFIG=$(pwd)/zmk-config/config/boards/shields/skeletyl_v2_elitec/skeletyl_v2_elitec_debug.conf
```

This will inject cdc usb device to our dts.

### Central side changed
We need to reset nvs storage on both sides using special shield `-DSHIELD=settings_reset` instead of target one.
The provisioning image should be written to each side before target fw.

