### Prepare workspace

[Getting started](https://zmk.dev/docs/development/local-toolchain/setup/native)

### Build

```
west build -s app/ --pristine -- -DBOARD=nice_nano_v2 -DSHIELD=skeletyl_v2_elitec_<right/left> -DZMK_CONFIG=$(pwd)/zmk-config/config
```

To enable debug console need to append this lines:

```
-DEXTRA_DTC_OVERLAY_FILE=$(pwd)/zmk-config/config/boards/shields/skeletyl_v2_elitec/debug.overlay -DOVERLAY_CONFIG=$(pwd)/zmk-config/config/boards/shields/skeletyl_v2_elitec/skeletyl_v2_elitec_debug.conf
```

This will inject cdc usb device to our dts.
