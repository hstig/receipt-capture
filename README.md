# receipt-capture
An embedded device that photographs receipts from several angles and stores the images together with metadata.

Status: Version 0.1 in progress. See the roadmap and the open issues.

## Goal

A receipt is placed on the platform, the device takes N photos from fixed angles and stores them with a timestamp and the capture parameters.

Three cameras are planned (overhead, left, right) that share one DCMI bus. The active camera is selected through its PWDN pin. Multi-camera operation is not yet verified. The open questions are listed in docs/wiring.md.

## Hardware
| Part | Model | Notes |
|---|---|---|
| Main board | STM32F746G-DISCO (MB1191 B-02) | Cortex-M7, display, camera connector (DCMI), microSD, 16 MB SDRAM |
| Camera (planned: 3) | OV2640 modules [enter exact module] | Connected in parallel via DCMI; individual camera selection via I²C and PWDN. Check pin assignment in board manual UM1907. |
| Control board (optional) | STM32L476 | Lighting and mechanics, later |
| Lighting | [optional] | |
| Mechanics | [optional: mount, turntable] | |


Photo of the setup: docs/setup.jpg (to follow). The image is an AI-generated concept image, not a photo of the real setup.
<img width="1672" height="941" alt="Dreifach-Kamera-Belegscanner mit STM32F7" src="https://github.com/user-attachments/assets/e610bdc2-e12c-4b97-a104-9ab06c97eb83" />


## Software
Language: C
Operating system: Zephyr RTOS (built with west), Zephyr board name: stm32f746g_disco
Camera capture: DCMI and the Zephyr video API [feasibility to be checked]
Display: live preview on the board's display
Storage: files with metadata (JSON) on microSD
Optional: MQTT connection, control of the L476 via UART or I²C

## Quick start

To be added once milestone 0 is done.

## Roadmap
 - [ ] Milestone 0: Set up the Zephyr toolchain, run a sample program on the board, test the display
 - [ ] Milestone 1: Connect one OV2640 via DCMI and capture an image
 - [ ] Milestone 1b: Live preview on the display
 - [ ] Milestone 2: Save an image with metadata to the microSD card
 - [ ] Milestone 3a: Resolve the open hardware questions and measure them (tri-state data lines, SCCB in power-down)
 - [ ] Milestone 3b: Switch to a second camera via PWDN
 - [ ] Milestone 3c: Third camera, capture from three angles
 - [ ] Milestone 4: Lighting and mechanics via the STM32L476
 - [ ] Milestone 5: Optional: transfer via MQTT

## Limitations
- Running several cameras on one DCMI bus has not been tested yet. If it does not work, there are fallbacks (see docs/wiring.md).
- It has not yet been checked whether Zephyr supports DCMI capture with this sensor on this board.

## Project structure
src/        Source code (C)
docs/       Setup, wiring (wiring.md), photos, notes
boards/     Board configuration (to follow)
Note

Only test receipts without personal data are used for testing.

## License
MIT, see LICENSE.
