# ZMK Configuration Template
Wireless Cyboard keyboard configuration repository template for using ZMK firmware. [Instructions for use are located on our documentation site](https://docs.cyboard.digital/user-manual/quick-start/configure-layout).

## ZMK version
This template pins the latest **stable** ZMK release (currently `v0.3.0`), which matches the firmware stack behind [studio.cyboard.digital](https://studio.cyboard.digital). If you want to track current ZMK `main` (Zephyr 4.1) instead, edit `config/west.yml`: set the `zmk` revision to `main` and the `zmk-keyboards` revision to `zephyr-4.1`.