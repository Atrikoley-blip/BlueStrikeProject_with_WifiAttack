# ESP32 Wi-Fi Security Lab — Deauthentication Demonstration

> **Educational/authorized testing only.** Deauthentication frames can disconnect devices and disrupt a network. Test only on a network you own or have explicit written permission to assess. Do not target public, campus, office, or neighbouring Wi-Fi networks.

## 1. Project overview

This project uses an **ESP32 development board** firmware to study Wi-Fi management frames and demonstrate why wireless networks need appropriate protections.

**My contribution**
- Prepared the ESP32 firmware files.
- Flashed the firmware to the ESP32 using the required flash offsets.
- Recorded the board/firmware setup and reviewed the security implications of deauthentication.
- Focused on learning, controlled testing, and defensive recommendations.

## 2. Hardware and software

- ESP32 development board compatible with the firmware (the upstream project documents ESP32-DEVKITC-32E / ESP32-WROOM-32).
- USB data cable and a computer.
- Firmware binaries from the project repository.
- Espressif flashing utility (for example, ESP-IDF `idf.py` or `esptool`).

### ESP32 board

![ESP32 development board](doc/images/mini.jpg)<img width="2256" height="1693" alt="mini" src="https://github.com/user-attachments/assets/6f4c2064-fe4f-41aa-b25c-887a97243f85" />


*Image is from the upstream project archive included with this repository. Confirm your exact ESP32 model before flashing.*

## 3. Firmware files and flash offsets

I used these three binary files:

| Binary file | Flash offset | Purpose |
|---|---:|---|
| `bootloader.bin` | `0x1000` | Starts the firmware boot process |
| `partition-table.bin` | `0x8000` | Describes the flash-memory partitions |
| `esp32-wifi-penetration-tool.bin` | `0x10000` | Main application firmware |

**Important:** File names and locations can differ between repository versions. Use the binaries that match the same firmware build, and verify the offsets against that build's documentation. Do not mix binaries from unrelated builds.

## 4. Flashing workflow

1. Download or clone the upstream repository.
2. Extract the archive and locate the `build` folder.
3. Check that all three binary files exist and match the offsets listed above.
4. Connect the ESP32 using a USB data cable.
5. Identify the correct serial/COM port in your operating system.
6. Use the flashing tool's interface to select each binary and assign its matching offset.
7. Start the flash operation and wait for it to finish.
8. Restart the ESP32 and record whether it boots successfully.

Do not copy a COM-port value from someone else's setup; choose the port shown on your own computer. If flashing fails, verify the board model, USB cable/driver, port, binary compatibility, and offset values.

## 5. Lab validation and evidence

For a project report, record the following without targeting unrelated networks:

- ESP32 board model and firmware/repository version.
- Flash tool and version used.
- The three file names and offsets.
- Flashing result (success/failure) and any error message.
- A photo of your own board and a screenshot of the flashing tool with sensitive details hidden.
- Observations from a controlled test environment and the defensive steps taken.

### Suggested results table

| Test item | Expected observation | Actual result |
|---|---|---|
| Firmware flashing | Tool reports completion | Fill in your result |
| ESP32 restart | Board starts without a boot error | Fill in your result |
| Controlled lab observation | Record only the authorised test's result | Fill in your result |
| Defensive check | Verify that network equipment supports protected management frames (PMF/802.11w) | Fill in your result |

Do not claim a test passed unless you observed and recorded the result yourself.

## 6. Security lessons and mitigation

Deauthentication abuse can interrupt wireless connectivity. Recommended defensive measures include:

- Enable **Protected Management Frames (PMF / 802.11w)** where supported; use *required* mode when compatible with all clients.
- Keep router/access-point firmware updated.
- Use WPA2-AES or WPA3 security and strong Wi-Fi credentials.
- Monitor for repeated deauthentication/disassociation events and unexpected client disconnects.
- Run wireless security tests only in an isolated lab or during an approved assessment window.

## 7. Limitations

- An ESP32 board and this firmware do not automatically prove that a Wi-Fi network is vulnerable.
- Results depend on the ESP32 variant, firmware build, access point, client devices, and their security settings.
- A successful flash only confirms that firmware was written; it does not by itself confirm a security finding.

## 8. Reference
- Refer to the upstream repository's license and documentation before redistributing or modifying its code.

## 9. Disclaimer

This repository write-up documents an educational wireless-security lab. The author is not responsible for unauthorised use. Obtain permission before any security assessment and stop immediately if testing affects devices or networks outside the approved scope.
