# ZMK Configuration Template
Wireless Cyboard keyboard configuration repository template for using ZMK firmware. [Instructions for use are located on our documentation site](https://docs.cyboard.digital/user-manual/quick-start/configure-layout).

## ZMK version
This template pins the latest **stable** ZMK release (currently `v0.3.0`), which matches the firmware stack behind [studio.cyboard.digital](https://studio.cyboard.digital). If you want to track current ZMK `main` (Zephyr 4.1) instead, edit `config/west.yml`: set the `zmk` revision to `main` and the `zmk-keyboards` revision to `zephyr-4.1`.

## Selecting your keyboard model

The keymap selects your keyboard variant with a chosen **physical layout** node, e.g.:

```dts
chosen { zmk,physical-layout = &physical_layout_imprint_number_row; };
```

The available Imprint layouts are defined in
[`zmk-keyboards`](https://github.com/Cyboard-DigitalTailor/zmk-keyboards/blob/main/boards/shields/imprint/imprint-layouts.dtsi);
the `config/default keymaps/` folders contain a matching keymap for each. The
Dactyl and legacy single-arc keymaps still use the older
`zmk,matrix-transform` chosen node, as those models predate the physical
layout definitions.

## Updating a config repo created before July 2026

Older configs track ZMK `main` and select the keyboard model with a
`zmk,matrix-transform` chosen node. To move one onto the current stable stack:

1. In `config/west.yml`, set the `zmk` revision from `main` to `v0.3.0`
   (leave `zmk-keyboards` on `main`).
2. In `.github/workflows/build.yml`, change `@main` to `@v0.3.0`.
3. In your `config/imprint.keymap`, replace the chosen node

   ```dts
   chosen { zmk,matrix-transform = &imprint_<your model>; };
   ```

   with

   ```dts
   chosen { zmk,physical-layout = &physical_layout_imprint_<your model>; };
   ```

   Step 3 matters: with a chosen `zmk,matrix-transform`, ZMK ignores the
   physical layouts that the current `zmk-keyboards` shields are built
   around, and the firmware is not compatible with ZMK Studio.