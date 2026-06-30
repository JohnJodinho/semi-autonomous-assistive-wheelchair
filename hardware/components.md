# Hardware Components Reference

This document provides comprehensive technical specifications and integration guidance for every component in the automated wheelchair system.

## Complete Component Inventory

| Component                           | Model / Specification                                                     | Qty     | Voltage/Power                                  | Role in System                                                                                                           | Configuration Notes                                                                                                                                       |
| ----------------------------------- | ------------------------------------------------------------------------- | ------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Processing & Control**            |
| Microcontroller                     | Arduino Mega 2560                                                         | 1       | 7V regulated input (via buck converter)        | Central processing unit; sensor fusion algorithm; motor PWM control; Bluetooth command reception                         | 54 digital I/O pins; 16 analog inputs; dual serial ports for HC-05 and debug; runs at 16 MHz; sketch memory 256KB; sufficient for rule-based control loop |
| Joystick Controller                 | Shark MK5-SPJ+                                                            | 1       | 5V (from Arduino)                              | Primary user input; directional control (4-axis analog); pressure sensitivity for speed modulation                       | Plugged directly into analog inputs A0-A3 (X, Y, pressure, reserve); calibration required on setup                                                        |
| Motor Driver Module                 | Shark 6 Power Module                                                      | 1       | 24V input (from battery)                       | High-current power distribution; PWM speed control; independent left/right motor control                                 | Drives both 450W motors; rated for 100A continuous; includes thermal protection; accepts PWM duty cycle 0-255 from Arduino pins 5 & 6                     |
| **Motors & Actuation**              |
| DC Motor (Left Rear)                | 24V, 450W, 4-pole brushed, 1500 RPM                                       | 1       | 24V                                            | Independent left rear wheel propulsion; high torque output at low speeds                                                 | 760mm shielded cable; stall current 100A; efficiency ~75% at rated load; mounted on left side of cast iron battery case; direct wheel coupling            |
| DC Motor (Right Rear)               | 24V, 450W, 4-pole brushed, 1500 RPM                                       | 1       | 24V                                            | Independent right rear wheel propulsion; mirrors left motor for balanced thrust                                          | 760mm shielded cable; stall current 100A; mirrored installation on right side; enables differential speed for turning                                     |
| Motor Cable Assembly                | 16 AWG shielded, 760mm length, connectors                                 | 2       | 24V rated                                      | Robust connection from motor to power module; EMI protection for control signals                                         | Shielding grounded at motor end only (prevent ground loop); twisted pair inside shield for data lines                                                     |
| **Power & Battery**                 |
| Battery Pack                        | 24V Li-ion, 35Ah capacity, 90% DoD                                        | 1       | 24V nominal (25.2V max, 21V min)               | Primary power source; nominal 840Wh energy; ~12 hours typical lifespan at daily use cycle                                | Potted epoxy enclosure; internal BMS with overcharge/overdischarge protection; 100A continuous capability; mounted in cast iron battery case              |
| Battery Charger                     | 24V, 2A Li-ion smart charger                                              | 1       | 100-240V AC input                              | Safe recharging with temperature monitoring; automatic constant-current/constant-voltage (CC-CV) profile                 | Charging time: ~18 hours from 0-100% (conservative for battery longevity); recommended every 48 hours for daily use                                       |
| DC-DC Converter                     | 24V to 7V buck converter, 3A continuous                                   | 1       | 24V input, 7V output                           | Power conditioning for Arduino Mega and sensor circuit (MPU6050, HC-05, GPS); noise filtering for clean analog reference | Mounted on separate 5V rail; linear regulator inefficient; switched converter chosen for thermal efficiency                                               |
| **Sensors**                         |
| Ultrasonic Sensor (Front)           | HC-SR04, 2cm-400cm range, 15° beam width                                  | 1       | 5V                                             | Front obstacle detection; triggers alert at 30cm threshold                                                               | Mounted at wheelchair front center; trig/echo pins on Arduino digital I/O 7,8                                                                             |
| Ultrasonic Sensor (Left Rear)       | HC-SR04, 2cm-400cm range, 15° beam width                                  | 1       | 5V                                             | Left-rear obstacle detection; lateral hazard awareness                                                                   | Mounted on left side, rear quarter; trig/echo on digital pins 9,10                                                                                        |
| Ultrasonic Sensor (Right Rear)      | HC-SR04, 2cm-400cm range, 15° beam width                                  | 1       | 5V                                             | Right-rear obstacle detection; lateral hazard awareness                                                                  | Mounted on right side, rear quarter; trig/echo on digital pins 11,12                                                                                      |
| IMU Sensor Module                   | MPU6050 (6-DOF: gyroscope + accelerometer)                                | 1       | 5V (I²C power), data via 3.3V logic            | Tilt-angle sensing; dynamic stability monitoring; gyroscope calibration for vehicle frame orientation                    | I²C interface (SDA on A4, SCL on A5); includes temperature sensor; sampling rate 200Hz; sensitivity ±2g / ±250°/s (configurable)                          |
| GPS Module                          | u-blox NEO-6M, SiRF protocol                                              | 1       | 5V                                             | Outdoor position determination; route guidance data; optional waypoint navigation                                        | UART serial (RX/TX on pins 18,19); acquisition time 45s cold start, 1s warm start; accuracy ±2.5m typical; update rate 1Hz                                |
| **Communication & Alerts**          |
| Bluetooth Module                    | HC-05, SPP profile, 100m range                                            | 1       | 5V (command/data), 24V external power optional | Wireless link to Flutter mobile app; transmits sensor data & receives user commands                                      | UART serial (RX/TX on pins 16,17); 9600 baud default; module enters AT command mode on boot for config                                                    |
| Buzzer (Audible Alarm)              | 5V piezo, 85dB, 2.3kHz tone                                               | 1       | 5V digital output                              | Obstacle detection alert; tilt-angle warning; battery low notification                                                   | Connected to digital pin 13 via 2N2222 transistor (buzzer draws ~100mA); PWM control for variable tone/urgency                                            |
| **Wheels & Suspension**             |
| Rear/Drive Wheel (Left)             | 14×3.00" puncture-proof, silver hub with bearings                         | 1       | —                                              | Left-side propulsion contact point; multi-terrain traction                                                               | Designed for non-pneumatic (solid) construction; rated 100kg per wheel; 356mm outer diameter; coupled to left motor via gear reducer                      |
| Rear/Drive Wheel (Right)            | 14×3.00" puncture-proof, silver hub with bearings                         | 1       | —                                              | Right-side propulsion contact point; mirrors left wheel                                                                  | Identical to left wheel; independent motor allows differential turning; ~0.85m turning radius on smooth surface                                           |
| Caster Wheel (Front Left)           | 6×2" swivel wheel with bearings, silver hub                               | 1       | —                                              | Front-left steering contact; directional stability                                                                       | 152mm outer diameter; swivel bearing allows free rotation; reduces steering effort; positioned 908mm ahead of rear wheel axle                             |
| Caster Wheel (Front Right)          | 6×2" swivel wheel with bearings, silver hub                               | 1       | —                                              | Front-right steering contact; lateral balance                                                                            | Mirrors left caster; symmetrical placement ensures balanced load distribution                                                                             |
| **Suspension System**               |
| Coil Spring (Left)                  | 7-coil (5 active), high-strength steel, 6.37mm wire diameter              | 1       | —                                              | Left-side vertical compliance; shock absorption during wheel strikes                                                     | Mean coil diameter 35.44mm; spring constant 75.83 N/mm; deflection capacity 8.11mm; transmits 62kg load (half of suspension share)                        |
| Coil Spring (Right)                 | 7-coil (5 active), high-strength steel, 6.37mm wire diameter              | 1       | —                                              | Right-side vertical compliance; mirrors left spring for balanced ride                                                    | Identical specification to left spring; torsional shear stress 21.96 N/mm² (well below 59.5 N/mm² yield limit)                                            |
| Pneumatic Damper                    | Adjustable pressure, 3-position valve                                     | 1       | Pre-charged (no external supply)               | Rebound control; oscillation dampening; prevents endless spring oscillation                                              | Pre-charged air cavity; three stiffness settings for user preference; mounted between frame and suspension pickup                                         |
| **Frame & Structure**               |
| Lower Frame (Seat Support)          | Galvanized steel tubing, 25.4mm OD, 2.0mm wall                            | 1 set   | —                                              | Primary load-bearing structure; seat frame attachment                                                                    | Welded construction; forms rectangular base 0.6m × 0.5m; supports 100kg payload with safety factor 1.5 (verified via FEA)                                 |
| Upper Frame (Backrest & Armrest)    | Galvanized steel tubing, 19.05mm OD, 1.6mm wall                           | 1 set   | —                                              | User support structure; ergonomic back/arm positioning                                                                   | Lighter gauge than lower frame; pinned joints for armrest mobility; adjustable recline angle                                                              |
| Battery Enclosure (Basement)        | Cast iron (recycled Invacare), 50mm depth                                 | 1       | —                                              | Robust protection for battery and motor controllers; acts as ballast                                                     | Provides ~8kg additional mass for stability; excellent vibration damping; corrosion protection via paint finish                                           |
| Seat Frame with Foam                | Galvanized steel frame + 100mm polyurethane foam                          | 1       | —                                              | User seating surface; comfort and posture support                                                                        | Contoured foam distributes pressure; removable upholstery for cleaning; seat height 0.45m (standard wheelchair height)                                    |
| Backrest                            | Galvanized steel frame + 80mm polyurethane foam                           | 1       | —                                              | Lumbar support; spine stabilization                                                                                      | Adjustable recline angle 0-15°; foam density 25 kg/m³ for medium firmness; removable upholstery                                                           |
| Armrest (Left & Right)              | Galvanized steel tubing + foam padding                                    | 2       | —                                              | Upper body support; transfer assistance; prevents tipping from lateral shift                                             | Removable via pin joints; height adjustable 0.65-0.75m from floor; foam density 20 kg/m³ for comfort                                                      |
| Footrest                            | Aluminum alloy platform                                                   | 1       | —                                              | Foot support and positioning; lightweight design reduces inertia                                                         | Dimensions 0.35m × 0.25m; adjustable height 0.25-0.35m; reduces wheelbase static moment arm                                                               |
| **Mechanical Fasteners & Assembly** |
| Bolts, Nuts, Washers                | Stainless steel 316L (M6, M8, M10, M12 assorted)                          | 100+    | —                                              | Corrosion-resistant frame assembly throughout                                                                            | Stainless steel chosen for humid Nigerian environment; all major joints double-locked with safety wire                                                    |
| Welding Electrode                   | E6013 (mild steel)                                                        | 50 rods | —                                              | Frame fabrication; joint strength                                                                                        | Used for galvanized steel welding; post-weld zinc re-coat applied for corrosion protection                                                                |
| Wiring Harness                      | 16 AWG shielded multi-conductor cable, 50m total                          | —       | 24V rated                                      | Power distribution and signal integrity                                                                                  | Routed through loom; thermal fuses (20A) on main battery feed; separate 5V return path for sensor common                                                  |
| Connectors                          | Anderson Power Pole (battery), motor spade terminals, JST micro (sensors) | 20+     | 24V/5V rated                                   | Modular assembly; quick-disconnect capability for service                                                                | Color-coded: red=positive, black=ground, yellow=24V, blue=5V signal return                                                                                |
| Heat Shrink Tubing                  | Assorted sizes (1.5mm - 6mm), dual-wall adhesive-lined                    | 5m      | —                                              | Solder joint protection; wire bundle organization; moisture seal                                                         | Heat applied with controlled temperature gun to prevent component damage                                                                                  |
| Thermal Fuses                       | 20A, solder-in cartridge type                                             | 2       | Rated 24V DC                                   | Overcurrent protection on main battery feed and backup circuit                                                           | Melts at ~165°C (solder melting point); prevents catastrophic short-circuit damage                                                                        |
| **Electrical Infrastructure**       |
| Main Battery Switch                 | Rotary disconnect, 100A rated                                             | 1       | 24V DC                                         | Manual power cutoff for safety and maintenance                                                                           | Yellow knob for visibility; latch prevents accidental activation; located on right side battery case                                                      |
| Indicator LEDs                      | 5mm, assorted colors (green/yellow/red), 20mA                             | 5       | 5V via 470Ω resistor                           | Visual status indication (power OK, charging, warning, error, Bluetooth connected)                                       | Mounted on control panel; updated every 500ms by Arduino                                                                                                  |
| Reset Button                        | Momentary push-button, 12mm diameter                                      | 1       | 5V logic                                       | Arduino soft reset for troubleshooting                                                                                   | Located on top of battery enclosure; prevents accidental press                                                                                            |

## Wiring and Integration Notes

### Power Distribution Strategy

The battery pack (24V, 35Ah) serves as the primary power source with two distinct distribution branches:

**High-Power Branch (Motors):**

- Battery → 20A thermal fuse → main battery switch → Shark 6 power module → dual 450W motors
- AWG 4 cable recommended for main battery feed (minimize voltage drop)
- Motor return path isolated on separate cable to prevent ground loop

**Low-Power Branch (Control & Sensors):**

- Battery → DC-DC buck converter (24V→7V, 3A max) → Arduino Mega, HC-05, GPS, IMU, buzzer circuits
- Arduino 7V input feeds internal 5V regulator for GPIO and analog circuits
- Sensor I²C/UART lines buffered via logic-level converters (5V Arduino ↔ 3.3V sensor modules when needed)

**Topology Advantages:**

- Isolated 5V sensor rail prevents motor switching noise from coupling into ADC reference
- Fused battery feed protects against main short-circuit
- Redundant soft-off: Arduino can command motor driver shutdown via GPIO (enables limp-home mode)

### Motor Control Interconnection

Each motor receives PWM duty-cycle commands from Arduino pins 5 (left) and 6 (right), routed through the Shark 6 module:

1. Arduino digital output (0-5V, 8-bit PWM) → Shark 6 PWM input
2. Shark 6 processes PWM and applies high-current switching to motor terminals
3. Motor current feedback (optional diagnostic line) back to Arduino for stall detection
4. Freewheeling diodes in Shark 6 suppress back-EMF spikes during motor deceleration

**Speed Control:**

- PWM frequency: 490 Hz (default Arduino) provides sufficient bandwidth for smooth ramp
- Dead-band: 10% on each end (0-25 and 230-255 PWM values) = stopped condition
- Acceleration ramp: software-limited to 50 PWM units/second (prevents abrupt jerks)

### Sensor Integration

**Ultrasonic Array (Obstacle Detection):**

- Trigger pins (7, 9, 11) pulled low by Arduino for 10 microseconds to initiate measurement
- Echo pins (8, 10, 12) measured via pulseIn() function; time interval converted to distance
- Sensors polled at 10 Hz (every 100ms) to balance CPU load and responsiveness
- False-positives filtered: require 3 consecutive detections below 30cm threshold before alert

**IMU (MPU6050):**

- I²C interface: address 0x68 (default); operates at 400kHz bus speed
- Gyroscope calibration: first 30 seconds after boot while wheelchair stationary
- Accelerometer tilt angle calculated via arctangent(ax/az); complementary filter fuses gyro data
- Measurement rate 200 Hz internally; Arduino reads at 20 Hz via I²C (sufficient for tilt thresholds)

**GPS (u-blox NEO-6M):**

- NMEA protocol via UART: 9600 baud, 8 data bits, 1 stop bit
- Parses GPGGA and GPRMC sentences for latitude, longitude, heading, velocity
- Cold start: 45 seconds typical; warm start: 1 second (assists from almanac cache)
- Routes GPS data to Flutter app via Bluetooth; displays live map in real-time

**Bluetooth (HC-05):**

- AT command mode: hold key pin high on power-up to enter configuration
- Default baud rate: 9600 (Arduino uses SoftwareSerial or hardware serial on pins 16,17)
- JSON message format: `{"cmd":"obs","dist":25,"lat":9.1234,"lon":7.5678}`
- Transmit rate: 10 messages/second (sufficient for app responsiveness without saturation)

### Chassis Ground Topology

All return paths consolidated at battery negative terminal to prevent ground loops:

- Motor returns: direct to battery common (shortest path, minimizes EMI)
- 7V regulator ground: returned to battery common via separate wire
- Arduino ground: connected to both 7V regulator common and battery common (dual-point return at battery)
- Sensor ground: shared with Arduino 5V return to maintain voltage reference stability

### Environmental Conditioning

**Moisture Protection:**

- All solder joints sealed with conformal coating or potting epoxy
- Connector contacts protected with dielectric grease
- Battery case sealed with epoxy; internal BMS potted for moisture isolation
- Wire harnesses routed in cable loom with drain holes (allows water to escape rather than pool)

**Vibration Isolation:**

- Motor mounting: rubber dampers between motor bracket and cast iron case (reduce bearing wear)
- Electronics: potted in epoxy or mounted on vibration-damping foam (minimizes solder fracture risk)
- Battery: secured with straps and potting (internal BMS highly susceptible to shock damage)

**Thermal Management:**

- DC-DC converter: mounted on aluminum heat sink (20°C rise from 40W dissipation at full load)
- Motor drivers: thermal fuses integrated (de-rate at >80°C to prevent runaway heating)
- Ventilation: battery case vented to allow convective cooling without ingress of standing water

---

## Field Maintenance Procedures

### Motor Inspection (Every 50 hours)

1. Spin wheels freely to check for bearing noise (smooth operation expected)
2. Check cable connections at motor and power module for corrosion (apply dielectric grease if oxidized)
3. Measure back-EMF voltage when wheel spun by hand with motor unpowered (confirms internal winding integrity)

### Battery Health Assessment (Monthly)

1. Record voltage with multimeter under no-load condition (should read 24.0-25.2V for healthy Li-ion)
2. Monitor charge time: should reach 100% in ~18 hours (longer time indicates aging)
3. Check for physical swelling or leakage from battery case (immediate replacement if observed)
4. Optional: load test with dummy resistor for 10 minutes, measure voltage sag (>10% sag indicates reduced capacity)

### Sensor Calibration (Quarterly)

1. **Ultrasonic**: Verify detection at 30cm mark using ruler; adjust sensitivity threshold if ±3cm drift observed
2. **IMU**: Re-run 30-second gyro calibration with wheelchair on level surface; replace if drift persists
3. **GPS**: If accuracy degraded, clear AGPS data via u-blox ubxcfg tool; allows fresh satellite acquisition

### Electrical Safety Check (Before Every Deployment)

- Confirm all fasteners tight, no loose cables
- Verify thermal fuses not blown (continuity test with multimeter)
- Check main battery switch function (on/off)
- Confirm buzzer produces sound when test button on Arduino pressed
- Validate Bluetooth pairing with mobile app

---

## Replacement & Upgrade Paths

**Motor Failure**: Order identical Shark-compatible 450W 24V brushed motor; cable and connector transfer from failed unit

**Battery Aging**: 24V lithium-ion packs widely available; specify 35Ah capacity and 90% DoD rating for drop-in compatibility

**Sensor Upgrade**: MPU6050 can be replaced with MPU9250 (adds magnetometer for heading). Arduino sketch requires minimal changes to I²C address.

**Bluetooth to WiFi**: HC-05 can be swapped for ESP32 module (offers higher bandwidth, on-board processing); requires firmware rewrite but maintains UART interface compatibility

---

_This document provides maintenance technicians and field engineers with complete reference data for the automated wheelchair hardware platform. All component selections prioritize long-term reliability, environmental resilience, and modularity for iterative system improvements._
