# ZMK Configuration for TBK NiNi Keyboard

This repository contains the ZMK firmware configuration for the TBK NiNi split keyboard.

## Keyboard Layout

![TBK NiNi Keyboard](pics/EYL09802.png)

## Building the Firmware

This firmware uses the [ZMK Firmware](https://zmk.dev/) and can be built using github actions or locally on your machine.

### Prerequisites

1.  **Install `west`:** Follow the instructions on the [ZMK website](https://zmk.dev/docs/getting-started/setup) to install `west` and its dependencies.
2.  **ZMK west modules:** Initialize and update the ZMK modules:
    ```bash
    west init -l config
    west update
    ```

### Local Build

To build the firmware locally, navigate to the `config` directory and run `west build`:

For the left half:
```bash
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=tbk_nini_left
```

For the right half:
```bash
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=tbk_nini_right
```

The generated `.uf2` files will be in `build/zephyr/zmk.uf2`.

### GitHub Actions

This repository includes a GitHub Actions workflow (`.github/workflows/build.yml`) that automatically builds the firmware for both `tbk_nini_left` and `tbk_nini_right` shields whenever changes are pushed to the repository. The compiled firmware files are available as artifacts in the GitHub Actions run.

## Keymap

The keymap for the TBK NiNi is defined in `config/tbk_nini.keymap`. It utilizes several layers to provide extensive functionality:

*   **DEF (Default):** The primary typing layer.
*   **NUM (Numbers):** A layer for numbers and common symbols.
*   **SYM (Symbols):** A layer for various symbols.
*   **SYS (System):** A layer for system-level controls and functions.
*   **GAME (Gaming):** A layer optimized for gaming.
*   **GN (Gaming Numbers):** A sub-layer for gaming-specific number inputs.
*   **ONEHAND (One-Handed):** A layer for one-handed operation.
*   **ONEHAND2 (One-Handed 2):** A secondary layer for one-handed operation.
*   **SCRL (Scroll):** A layer for scrolling functions.
*   **SNYP (Snippets):** A layer for custom snippets or macros.

You can inspect the `config/tbk_nini.keymap` file to see the full key assignments for each layer.
