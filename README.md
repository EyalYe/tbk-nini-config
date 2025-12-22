# ZMK Configuration for TBK NiNi Keyboard

This repository contains the ZMK firmware configuration for the TBK NiNi split keyboard.
![TBK NiNi Keyboard](pics/EYL09802.png)

## Hardware

| Component | Link |
| :--- | :--- |
| TBK MINI Shell (get everything except PCBs and right plate) | [TBK Mini repo](https://github.com/Bastardkb/TBK-Mini/tree/master) |
| Dactyl flexible PCB (for hot swap) | [dactyl-flex-pcb](https://oshwlab.com/janakasoft/dactyl-flex-pcb)
|Hot swat sockets | [Kaih hot swappable sockets](https://he.aliexpress.com/item/1005006105603269.html?spm=a2g0o.order_list.order_list_main.138.121918025lt7z1&gatewayAdapt=glo2isr)|
|diodes | the same as in TBK Mini repo (1N4148 sod123) |
| nice nano v2 (I bought cheap clones on Aliexpress) | [nice_nano_v2](https://he.aliexpress.com/item/1005007205026373.html?spm=a2g0o.productlist.main.4.4a85wxukwxuk1P&aem_p4p_detail=202512220612275858536249159380003551026&algo_pvid=3a048f00-9455-4fe2-a4ad-22cfd1ce6b4e&algo_exp_id=3a048f00-9455-4fe2-a4ad-22cfd1ce6b4e-3&pdp_ext_f=%7B%22order%22%3A%22234%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21ILS%2111.89%2111.89%21%21%2125.57%2125.57%21%402140f53817664127473445222e6beb%2112000039797470328%21sea%21IL%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3A18111f82%3Bm03_new_user%3A-29895&curPageLogUid=lENcYEyTsifx&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005007205026373%7C_p_origin_prod%3A&search_p4p_id=202512220612275858536249159380003551026_1) |
| PMW3610 Trackball Sensor | [PMW3610](https://he.aliexpress.com/item/1005006913778101.html?spm=a2g0o.productlist.main.10.7b142ebeAlwx4I&algo_pvid=f76023a4-b749-4855-acb3-c0ef7b3ba098&algo_exp_id=f76023a4-b749-4855-acb3-c0ef7b3ba098-9&pdp_ext_f=%7B%22order%22%3A%2228%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21ILS%2138.20%2138.20%21%21%2182.16%2182.16%21%4021015e8517664128644403965ead31%2112000039386900014%21sea%21IL%210%21ABX%211%210%21n_tag%3A-29910%3Bd%3A18111f82%3Bm03_new_user%3A-29895&curPageLogUid=WM15tk6ORvSy&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005006913778101%7C_p_origin_prod%3A)
|M.2\*3\*3.2 brass inserts and screws| I count on you to find them yourself :) |
| right plate | [right_plate.step](3d_files/right_plate.step) |
| trackball mount | [trackball_mount.step](3d_files/trackball_mount_pmw3610.step) |
| Ceramic Bearing Ball | [Ceramic Bearing Ball](https://he.aliexpress.com/item/1005007048525968.html?spm=a2g0o.order_list.order_list_main.70.121918025lt7z1&gatewayAdapt=glo2isr) |

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

## Pinout

### Matrix

| Pin Function | Pro Micro Pin |
| :--- | :--- |
| **Row 1** | 21 |
| **Row 2** | 18 |
| **Row 3** | 5 |
| **Row 4** | 4 |

#### Left Half Columns
| Column | Pro Micro Pin |
| :--- | :--- |
| Col 1 | 8 |
| Col 2 | 7 |
| Col 3 | 6 |
| Col 4 | 10 |
| Col 5 | 20 |
| Col 6 | 19 |

#### Right Half Columns
| Column | Pro Micro Pin |
| :--- | :--- |
| Col 1 | 19 |
| Col 2 | 20 |
| Col 3 | 10 |
| Col 4 | 6 |
| Col 5 | 7 |
| Col 6 | 8 |

### PMW3610 (Right Half)

The trackball sensor is connected via SPI to the right half.

| Sensor Pin | nRF52 Pin | Note | Pro Micro Pin |
| :--- | :--- | :--- | :--- |
| **IRQ** | P0.06 | Interrupt | 1 |
| **SCK** | P0.08 | | 0 |
| **MOSI/MISO** | P0.17 | Shared Data Line | 2 |
| **CS** | P0.20 | Chip Select | 3 |

