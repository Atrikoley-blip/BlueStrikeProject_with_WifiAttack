# ESP32 Wi-Fi Security Lab — Arduino IDE + Firmware Flashing

> **Educational and authorized testing only.** The supplied Arduino sketch includes deauthentication-related functionality and an access-point/web-form flow that could be misused to disrupt Wi-Fi or collect passwords. Do not run it against networks or people without explicit written permission. Do not collect or store real credentials. Use a dedicated isolated lab and a safe, clearly labelled demonstration.

## Project overview

This repository documents two parts of an ESP32 wireless-security learning project:

1. **Prebuilt firmware flashing** using the `esp32-wifi-penetration-tool` project and matching `.bin` files.
2. **Arduino IDE sketch** (`wifi.ino`) using the ESP32 Arduino core, Wi-Fi, HTTP web-server, and DNS-server libraries.

The purpose of the write-up is to document the hardware/software setup, build/flash process, observations, limitations, and defensive lessons.

## Images

### Arduino IDE and ESP32 — illustrative overview

![Arduino IDE and ESP32 illustration](images/arduino-ide-esp32.svg)

*Illustration for documentation; it is not a screenshot of an actual running device.*

### ESP32 development board

![ESP32 development board](images/esp32-board.jpg)

*Board image bundled with the upstream project archive. Confirm your exact board model before flashing.*

## Hardware and software

- ESP32 development board compatible with the selected firmware (check the upstream project documentation for supported variants).
- USB data cable.
- Arduino IDE 2.x for compiling the `.ino` sketch.
- Espressif ESP32 Arduino board package.
- Matching prebuilt firmware binaries if using the flashing workflow.

## Part A — Arduino IDE setup

1. Install Arduino IDE from the official [Arduino Software](https://www.arduino.cc/en/software) page.
2. In **Tools → Board → Boards Manager**, search for **esp32 by Espressif Systems** and install it.
3. Open `wifi.ino` in Arduino IDE.
4. Select the board that matches your hardware in **Tools → Board**.
5. Select the correct serial port in **Tools → Port**.
6. Use **Verify** to compile and record any errors. Upload only a reviewed, safe version in an isolated lab.

### Libraries referenced by `wifi.ino`

| Library | Purpose |
|---|---|
| `Arduino.h` | Arduino runtime |
| `WiFi.h` | ESP32 Wi-Fi API |
| `WebServer.h` | Local HTTP server |
| `DNSServer.h` | DNS service for an access point |

### High-level code overview

- **Wi-Fi setup:** configures Wi-Fi mode and a local access point.
- **HTTP routes:** defines local web routes.
- **DNS handling:** responds to DNS queries in the local AP context.
- **Network scan data:** keeps a limited list of discovered network names and radio details.
- **Risk note:** the supplied sketch also includes a password form, credential-related handling, and deauthentication/Evil-Twin-style behavior. Do not deploy these features against real networks. Remove credential collection and disruption functionality for a safe demonstration.

## Part B — Prebuilt firmware and flash offsets

The original firmware workflow you described used these files and offsets:

| Binary file | Flash offset | Role |
|---|---:|---|
| `bootloader.bin` | `0x1000` | Starts the firmware boot process |
| `partition-table.bin` | `0x8000` | Defines flash-memory partitions |
| `esp32-wifi-penetration-tool.bin` | `0x10000` | Main application firmware |

**Check the exact filenames and offsets against the documentation for the same firmware build.** Do not mix binaries from different builds. Flash offsets are memory addresses, not passwords.

### Flashing checklist

1. Download the upstream project from [Atrikoley-blip/esp32-wifi-penetration-tool](https://github.com/Atrikoley-blip/esp32-wifi-penetration-tool).
2. Locate the build outputs and confirm that all required binaries are present.
3. Connect the ESP32 with a USB data cable and identify its COM/serial port.
4. Use a compatible Espressif flashing tool and enter the matching file/offset pairs above.
5. Wait for the tool to report completion, then restart the board.
6. Record the firmware version, board model, flash tool version, and observed result.

A successful flash only means that the binary data was written; it does not prove that a Wi-Fi network is vulnerable or that a test succeeded.

## Testing and results

Record only tests performed on devices and networks you own or are authorized to assess.

| Test | Expected observation | Actual result |
|---|---|---|
| Arduino sketch compilation | Verify succeeds or reports actionable compiler errors | Fill in your result |
| Firmware flashing | Flash tool reports completion | Fill in your result |
| ESP32 restart | No boot error is observed | Fill in your result |
| Defensive configuration check | Confirm whether PMF is available/enabled on the lab router | Fill in your result |

Do not claim a test passed unless you observed and recorded the result yourself. Do not include passwords, private network details, or other people's device identifiers in screenshots or logs.

## Defensive recommendations

- Enable **Protected Management Frames (PMF / IEEE 802.11w)** where supported; use required mode when compatible with all legitimate clients.
- Keep router/access-point firmware up to date.
- Prefer WPA3 or WPA2-AES and a strong, unique passphrase.
- Teach users to avoid entering Wi-Fi credentials into unexpected captive portals or “firmware update” pages.
- Monitor for repeated deauthentication/disassociation events and unexpected client disconnects.
- Test only within a written scope and an isolated lab.

## Troubleshooting

- **Board or port not visible:** check the USB data cable, driver, board selection, and COM port.
- **Compile errors:** confirm the ESP32 board package is installed and the selected board matches the hardware.
- **Upload/flash errors:** verify the serial port, binary compatibility, offsets, and USB connection.
- **Unexpected behavior:** disconnect the device from the test network and review the sketch before continuing.

## References

- [ESP32 Arduino core](https://github.com/espressif/arduino-esp32)
- [Arduino IDE download](https://www.arduino.cc/en/software)
## Disclaimer

This repository is for education and authorized wireless-security testing. It is not permission to disrupt networks, impersonate access points, or collect credentials. Follow applicable law and the network owner's rules.
