# BirdBox X4 Controller

Smart ESP32-based bird deterrent controller with 4 PWM outputs, local web control, MQTT integration, saved pattern presets, OTA firmware updates, runtime safety limits, and optional admin password protection.

Built for targeted, humane bird deterrent control on rooftops, solar arrays, and other problem areas.

## Features

- 4 independent PWM-controlled output channels
- Local web dashboard for live status and control
- 4 saved pattern presets with:
  - mode
  - speed
  - selected outputs
  - optional timer
  - runtime limit
- MQTT control and status topics
- Home Assistant MQTT discovery
- OTA firmware upload from the web UI
- Runtime safety timeout
- Optional night lockout window
- Optional admin password protection for critical actions
- AP fallback mode for local setup if Wi-Fi is unavailable

## Pattern Modes

The controller supports the following pattern modes:

- **Manual**  
  Holds selected outputs at a fixed level until stopped or timed out.

- **Short Pulse**  
  Pulses selected outputs using configured on/off timing.

- **Random Burst**  
  Randomly triggers selected outputs using configurable random timing ranges.

- **Staggered**  
  Cycles through selected outputs in sequence.

## Hardware

### Platform
- ESP32

### Outputs
- 4 PWM outputs for MOSFET-driven deterrent devices such as buzzers, motors, or vibration units

### Pin Mapping
- Output 1: GPIO 16
- Output 2: GPIO 17
- Output 3: GPIO 26
- Output 4: GPIO 27
- Status LED: GPIO 23

## Main Functions

### Local Web UI
The built-in web interface provides:

- live controller status
- manual output control
- preset testing
- device and network settings
- timing and pattern tuning
- admin password entry for protected actions
- OTA firmware upload page

### Presets
The controller stores 4 configurable presets.  
Each preset includes:

- mode
- speed
- selected outputs mask
- timer enabled or disabled
- runtime in milliseconds

### MQTT Integration
The controller supports MQTT for:

- direct output control
- starting and stopping patterns
- running presets
- reboot control
- status reporting
- availability reporting
- Home Assistant auto-discovery

### OTA Updates
Firmware can be uploaded through the web interface using a compiled `.bin` file. Successful upload reboots the controller automatically. OTA access is protected by the admin password system.

## MQTT Topics

Base topic is configurable and defaults to:

```text
birdbox

birdbox/cmd/output1
birdbox/cmd/output2
birdbox/cmd/output3
birdbox/cmd/output4
birdbox/cmd/all
birdbox/cmd/mode
birdbox/cmd/start
birdbox/cmd/preset1
birdbox/cmd/preset2
birdbox/cmd/preset3
birdbox/cmd/preset4
birdbox/cmd/stop
birdbox/cmd/reboot

birdbox/state/output1
birdbox/state/output2
birdbox/state/output3
birdbox/state/output4
birdbox/state/mode
birdbox/state/active
birdbox/status
birdbox/availability
birdbox/info

birdbox/cmd/preset1
birdbox/cmd/preset2
birdbox/cmd/preset3
birdbox/cmd/preset4


Typical payloads:

start preset: 1
stop active pattern: off, 0, or stop

Only one preset or pattern runs at a time. Starting a new preset replaces the currently active pattern.

Security

The controller supports an optional admin password.

When configured, the password protects actions such as:

saving settings
manual output changes
preset test runs
reconnect commands
AP mode switching
clearing settings
OTA firmware update access

The dashboard remains usable for status viewing, and the browser can temporarily remember the admin password for the current session using session storage.

Safety Features
global max runtime safety timeout
per-preset optional timer
startup outputs forced off
night lockout option to block output activity during configured hours
AP fallback mode if normal Wi-Fi connection fails
Default Wi-Fi Setup Behavior

On boot:

device attempts to connect to configured Wi-Fi
if connection fails, it starts its own AP mode
AP name and password are configurable in settings
Example Use Cases
rooftop bird deterrent systems
solar panel protection
vibration motor triggering
buzzer-based deterrents
camera-triggered automation via MQTT and Frigate
Home Assistant integrated pest control workflows
Web UI Overview

The dashboard includes:

Admin Access
Live Controller Status
Manual Output Control
Preset Test Panel
Controller Setup
Company Info
Useful MQTT Topics
Flashing / Updating
Initial flash

Flash the compiled firmware to the ESP32 using your preferred method.

OTA update
Open the controller web UI
Enter admin password if protection is enabled
Open the OTA update page
Upload the compiled .bin file
Wait for the controller to reboot automatically
Project Status

This project is a dedicated firmware and control platform for the BirdBox X4 controller and is designed to support future refinements, firmware releases, and customer deployments.

Author / Brand

Nelson AI Solutions
AI-powered bird and pest control systems
Nelson, New Zealand
