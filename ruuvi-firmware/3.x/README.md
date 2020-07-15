---
description: 'Lifecycle: Alpha'
---

# 3.X

The 3.x firmwares are the bleeding edge versions, which means that they have new features but also they cannot be considered stable. Always confirm with Ruuvi team before starting to work on top of 3.x to avoid any surprises in development, or fork the project to yourself to maintain a stable version.

The firmware supports nrF52832 and nRF52811 officially, and it runs on nRF52840. Firmware is divided into one main repository which contains subrepositories. The reasoning for the separation is to support several different firmware and board variants and to allow all the projects contribute fixes to a common codebase. 

The main features of the firmware are based around sensor functionality: The firmware beacons sensor data and keeps a short internal buffer of historic values. The historic values can be read over Bluetooth GATT connection.

