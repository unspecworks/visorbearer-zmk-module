# Visorbearer ZMK Module

This is the ZMK module for the Visorbearer keyboard - a 32-key split keyboard featuring dual RGB LED status bars powered by LP5012 drivers.

## Usage

Add these lines to `config/west.yml` in your `zmk-config` repository:

```yaml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: carrefinho                            # <---
      url-base: https://github.com/carrefinho     # <---
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: visorbearer-zmk-module                # <---
      remote: carrefinho                          # <---
      revision: main                              # <---
  self:
    path: config
```

Then add the `visorbearer` shield to your `build.yaml`:

```yaml
---
include:
  - board: seeeduino_xiao_ble
    shield: visorbearer
    snippet: studio-rpc-usb-uart
  - board: seeeduino_xiao_ble
    shield: settings_reset
```

For more information on ZMK Modules and building locally, see [the ZMK docs page on modules.](https://zmk.dev/docs/features/modules)

## LED Features

Visorbearer features two independent LED bars:

**Connection Bar (Bar A):**
- **White**: Connected Bluetooth profile
- **Cyan (Breathing)**: Paired but not connected
- **Yellow (Breathing)**: Open profile, advertising
- **Dim White**: Active modifier keys (Shift/Ctrl/Alt/GUI)

**Battery Bar (Bar B):**
- **White**: Normal battery level
- **Yellow**: Low battery
- **Red**: Critical battery
- **Green**: Charging

## Configuration

Customize LED behavior by adding options to your `config/visorbearer.conf` file:

```ini
# Animation speeds (higher = faster)
CONFIG_VISORBEARER_LED_BAR_FADE_STEP_SIZE=8
CONFIG_VISORBEARER_LED_BAR_BREATH_STEP_SIZE=3

# Display timing (milliseconds)
CONFIG_VISORBEARER_LED_BAR_EVENT_DISPLAY_TIME_MS=3000
CONFIG_VISORBEARER_LED_BAR_STARTUP_DISPLAY_TIME_MS=6000

# Battery thresholds (percentage)
CONFIG_VISORBEARER_LED_BAR_BATTERY_CRITICAL_THRESHOLD=8
CONFIG_VISORBEARER_LED_BAR_BATTERY_LOW_THRESHOLD=15
```

See `Kconfig` for all available configuration options.