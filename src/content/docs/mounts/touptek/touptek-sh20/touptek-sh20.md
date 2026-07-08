---
title: TOUPTEK SH20 Equatorial Mount
categories: ["mounts"]
description: Driver for the TOUPTEK SH20 equatorial mount.
thumbnail: ./touptek-sh20.webp
---

## Features

The TOUPTEK SH20 telescope driver supports:

-   USB serial connection
-   Equatorial and azimuth mount type selection
-   10 slew rates from 0.25x to 1440x
-   Manual motion control in north, south, west, and east directions
-   Goto and sync coordinates
-   Sidereal, solar, and lunar tracking modes
-   Track on/off control
-   Park and unpark
-   Home find and home go actions
-   Site and time synchronization from INDI clients
-   Pier side reporting in equatorial mode
-   Timed pulse guiding
-   Configurable guiding rate
-   Buzzer control
-   Meridian flip settings in equatorial mode

## Installation

The TOUPTEK SH20 telescope driver is available as `indi_touptek_sh20`.

To run the driver after installation:

```bash
indiserver indi_touptek_sh20
```

When testing from a build tree, run the driver through the `indi_touptek_sh20` executable or symbolic link so the LX200 generic loader can select the SH20 implementation:

```bash
cd build/drivers/telescope
ln -sf indi_lx200generic indi_touptek_sh20
indiserver ./indi_touptek_sh20
```

## Operation

Connect the SH20 mount to the host computer with a USB serial cable. Start the driver with `indiserver indi_touptek_sh20` or select `TOUPTEK SH20` from an INDI client such as KStars/Ekos.

In the Connection tab, select the serial port assigned to the mount, for example `/dev/ttyUSB0` or `/dev/ttyACM0`, then press Connect. After connection, the driver reads startup data from the mount, including mount type, track mode, guide rate, buzzer state, and meridian flip settings when available.

### Main Control tab

The Main Control tab provides the standard telescope controls:

-   Connect and disconnect the mount
-   Track, slew, and sync commands
-   RA/DEC coordinate display and target entry
-   Abort motion
-   Tracking mode selection
-   Park and unpark
-   Pier side display in equatorial mode
-   Mount type selection

### Motion Control tab

The Motion Control tab provides manual movement and rate settings:

-   Motion N/S and Motion W/E buttons for manual slewing
-   Reverse controls for north/south and west/east movement
-   Slew rate selection from 0.25x to 1440x
-   Guide rate configuration from 0.1x to 0.9x sidereal rate

### Site Management tab

The Site Management tab is used by INDI clients to send observer location information to the mount. Time and date are synchronized from the INDI client as part of the standard telescope driver operation.

### Options tab

The Options tab includes the SH20 buzzer control. The buzzer can be set to off, low, or high.

### Meridian Flip tab

The Meridian Flip tab is available in equatorial mode. It provides meridian flip enable/disable, after-meridian behavior, and meridian limit configuration.

## Issues

-   The driver must be started as `indi_touptek_sh20`. Starting the shared `indi_lx200generic` executable directly loads the generic LX200 driver instead.
-   Mount type changes are sent to the mount immediately. Reconnect the driver after changing mount type so client-visible properties match the selected mode.
