# Connecting a WM8782 Stereo ADC Board (I2S 24-bit, 192kHz) to a DSP

This guide explains how to connect a WM8782-based I2S ADC board to a DSP board, including the I2S data lines, master clock, and power supply. It also details the necessary configuration of switches and jumpers.

## Board Overview

![Pasted image 20250312121219](https://github.com/user-attachments/assets/0b138d6e-fb02-41b8-9e43-da8d0486fd7f)


---

## 1. Configure the DSP for I2S Input

Set up the I2S input on the DSP using SigmaStudio:

| Pin | Function         | Description                                                                                                                |
|-----|------------------|----------------------------------------------------------------------------------------------------------------------------|
| MP0 | `Sdata_in0`      | Input data — corresponds to channels 2 and 3 in SigmaStudio input block. Channels 4 and 5 go to `MP1` (`Sdata_in1`).      |
| MP4 | `Lrclk_in`       | Input left-right clock.                                                                                                     |
| MP5 | `Bclk_in`        | Input bit clock.                                                                                                            |

![register_setup_adau_i2s_input](https://github.com/user-attachments/assets/5d73d7c8-cdd0-4e19-9ba6-2a492fa0cc49)


---

## 2. Connect I2S Lines

Use the following wiring between the I2S ADC board and the DSP board:

| Signal           | I2S Board | DSP Board | Cable Color         |
|------------------|-----------|-----------|----------------------|
| Data             | `D`       | `MP0`     | Violet               |
| Left-Right Clock | `LR`      | `MP4`     | Gray                 |
| Bit Clock        | `B`       | `MP5`     | White                |


![I2S Wiring](https://github.com/user-attachments/assets/6f71f128-e674-49c0-93df-be0c06b57373)
![I2S Wiring Close-up](https://github.com/user-attachments/assets/e923b1b5-3b01-4b4a-9613-01b442448913)

---

## 3. Connect the Master Clock

Set the **I2S board as the master** and the **DSP board as the slave**. Enable external clock mode on the DSP board.

![Slave Clock Setup on DSP](https://github.com/user-attachments/assets/752d9fa1-073f-42a1-8ede-89efb3530ba7)

Wire the master clock as follows:

| Signal       | I2S Board | DSP Board | Cable Color         |
|--------------|-----------|-----------|----------------------|
| Master Clock | `CLK`     | `MCLK`    | Orange               |

![Master Clock Connection](https://github.com/user-attachments/assets/72117c92-bd01-4418-b9d4-9e18a7b306e0)
![Master Clock Close-up](https://github.com/user-attachments/assets/4055852a-5d0e-46e9-ad3d-6626667053bc)

---

## 4. Power Supply Connections

Supply both boards with +5V:

| Signal  | I2S Board | DSP Board       | Cable Color         |
|---------|-----------|------------------|----------------------|
| GND     | `GND`     | Any GND pin      | White                |
| +5V     | `+5V`     | `+5V`            | Green                |

![Power Wiring](https://github.com/user-attachments/assets/30b7cf80-b088-45e2-a8bb-647df8ca37ea)
![Power Wiring Close-up](https://github.com/user-attachments/assets/bfcb5f01-142c-47ba-afa8-cc5c72a49c4f)

---

## 5. Configure I2S Board Switches & Jumpers

Set the jumpers and DIP switches on the I2S board as follows:

- **Jumper J6**: `M` (Master Mode)
- **Jumper J1**: `24` (24.576 MHz)
- **Jumper J2**: `1/2 CLK` (12.288 MHz output)

**DIP Switches:**

| Switch | Position | Function            |
|--------|----------|---------------------|
| SW1    | `+`      | Main Mode           |
| SW2    | `0`      | I2S Protocol        |
| SW3    | `–`      | 48 kHz Sample Rate  |
| SW4    | `0`      | 24-bit Data         |

![I2S Board Configuration](https://github.com/user-attachments/assets/54e35d5d-95f9-4afa-8733-15de062fab43)
