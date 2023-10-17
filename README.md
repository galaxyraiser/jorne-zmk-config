### My Jorne config for the ZMK keymap editor

This config was built with: https://nickcoutsos.github.io/keymap-editor (use it to modify keymap)
Keymap editor source code: https://github.com/nickcoutsos/keymap-editor

### Compilation
Just execute this line under zmk root.
```west build -s app -d build/{right/left} -b nice_nano --pristine -- -DSHIELD=jorne_{right/left} -DZMK_CONFIG="/home/roman/projects/zmk/zmk-config/config"```
