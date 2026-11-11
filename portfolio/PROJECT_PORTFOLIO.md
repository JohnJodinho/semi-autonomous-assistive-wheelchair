# Engineering Portfolio: Design & Development of a Semi-Autonomous Motorised Wheelchair

> **Application Attachment & Physical Project Proof**  
> **Project Role:** Team Lead & Mechanical / Mechatronics Design Engineer  
> **Individual Ownership:** Did the Computer-Aided Design (SolidWorks 3D Modeling) and Finite Element Analysis (FEA Simulation); collaborated closely with a 7-person team on workshop fabrication, electronics integration, software, and field testing.  
> **Institution:** Department of Mechanical Engineering, University of Jos  
> **National Recognition:** 🥈 **2nd Place — Kenol Creativity Challenge** (NSE National Conference, Abuja, Dec 2024) | 4th Place — Young Engineers Innovative Competition (YEFoN/NSE, 2024)

---

## 1. Executive Summary

This project showcases the end-to-end design, FEA structural validation, hands-on fabrication, embedded circuit prototyping, and multi-terrain validation of an affordable, semi-autonomous motorised wheelchair tailored for low-resource infrastructure and rough outdoor environments.

```
+---------------------------------------------------------------------------------------------------+
|                                   SYSTEM ARCHITECTURE OVERVIEW                                    |
+---------------------------------------------------------------------------------------------------+
|  [MECHANICAL SUBSYSTEM]                                                                           |
|   * Galvanized steel tubing (25.4mm & 19.05mm) + Recycled cast-iron battery basement (45% salvaged) |
|   * 4-point suspension: 2 coil springs (5 active coils) + 2 pneumatic rebound dampers             |
|   * Dual 24V 450W brushed DC motors (1500 RPM) driving 14" puncture-proof rear wheels             |
|                                                                                                   |
|  [CONTROL & EMBEDDED SYSTEM]                                                                      |
|   * Shark MK5-SPJ+ proportional joystick input + Shark 6 industrial power stage                  |
|   * Arduino Mega 2560 central controller for telemetry, sensor fusion & supervisor logic         |
|   * Safety array: HC-SR04 ultrasonic obstacle sonar (30cm zone) + MPU6050 6-DOF IMU tilt monitor |
|   * Remote Telemetry: HC-05 Bluetooth + u-blox NEO-6M GPS linked to custom Flutter mobile app     |
+---------------------------------------------------------------------------------------------------+
```

### Key Technical Specifications Achieved:
* **Rated Payload:** 100 kg (Validated on test bench and field trials with a factor of safety of 1.5).
* **Maximum Speed & Range:** 8.1 km/h top speed; 12.2 km continuous range (smooth tile) / 6.9 km (gravel).
* **Power Source:** 24V 35Ah Lithium-ion battery pack (840 Wh capacity).
* **Turning Radius:** 0.85 m (smooth tile) / 1.00 m (concrete).


---

## 2. The Final Assembled Product

The completed prototype integrates mechanical stability, multi-terrain shock absorption, high-torque propulsion, and intelligent safety cutoffs into a field-ready mobility device.

![Completely Fabricated Automated Wheelchair](../media/Completely%20Fabricated%20Automated%20Wheelchair%20(complete%20and%20ready%20for%20test%20driving).png)
*Figure 1: Fully fabricated semi-autonomous wheelchair ready for performance field trials, showing chassis geometry, front caster forks, cushioned ergonomics, drive wheels, and user joystick interface.*

---

## 3. Computer-Aided Design (CAD) & Finite Element Analysis (FEA)

*(Did all: 3D parametric CAD modeling, assembly design, and all FEA simulations).*

Having taught myself SolidWorks from scratch, I independently developed the complete 3D parametric assembly to ISO 7176 wheelchair standards, followed by structural FEA under maximum static and dynamic load conditions.

### 3.1 SolidWorks 3D Parametric Modeling
![Original 3D Modeling of Automated Wheelchair](../media/Original%203D%20Modeling%20of%20Automated%20Wheelchair.jpg)
*Figure 2: Complete 3D parametric CAD assembly in SolidWorks, detailing frame clearances, motor mount points, seating inclination, and suspension attachment geometry.*

### 3.2 Finite Element Simulation Results (100 kg Central Payload)
Before procurement and metal cutting, SOLIDWORKS Simulation was run using nonlinear structural analysis with fixed supports at ground contact points.

| Analysis Type | Visual Representation | Result Value & Interpretation |
| :--- | :--- | :--- |
| **Factor of Safety (FOS)** | ![Factor of Safety](../media/Simulation%20result%20of%20factor%20of%20safety%20analysis.jpg) | **Min FOS = 3.15** on seat rails; global structural safety factor verified well above the 1.5 design threshold. |
| **Von-Mises Stress Distribution** | ![Von-Mises Stress](../media/Simulation%20result%20of%20Von-misses%20stress%20analysis.jpg) | Peak stress localized at frame joints at **111.4 MPa**, safely below the 250 MPa yield strength of galvanized steel. |
| **Resultant Displacement** | ![Resultant Displacement](../media/Simulation%20result%20of%20resultant%20displacement%20analysis.jpg) | Maximum deflection of only **1.06 mm** observed under peak 100 kg loading, confirming optimal structural stiffness. |

---

## 4. Hands-On Fabrication & Mechanical Assembly

To minimize cost and maximize durability on rugged Nigerian terrain, we sourced 45% of the frame foundation from salvaged Invacare wheelchair components, modifying and fabricating the rest from heavy-duty galvanized steel tubing.

### 4.1 Frame Sourcing, Cutting, and Preparation
```
         [Salvaged Scrap Wheelchair]                     [Galvanized Steel Stock]
                     │                                              │
         Disassembly & Inspection                       Angle Grinder Cut & Notch
                     │                                              │
                     └──────────────────────┬───────────────────────┘
                                            ▼
                           [Bench Vice Precision Bending]
                                            ▼
                           [Manual Metal Arc (MMA) Welding]
```

![Salvaging Old Wheelchair Parts](../media/Engineering%20Team%20Collaborating%20on%20Salvaging%20old%20parts%20for%20caster%20and%20suspension%20Integration.jpg)
*Figure 3: Engineering team collaborating to strip, inspect, and qualify salvaged structural parts for caster brackets and suspension integration.*

<br/>

| Metal Cutting & Sizing | Tubing Bending & Shaping |
| :---: | :---: |
| ![Metal Cutting with Angle Grinder](../media/Fabrication%20Phase%20-%20Metal%20Cutting%20with%20Angle%20Grinder.jpg) | ![Shaping Tubing with Bench Vice](../media/Fabrication%20Phase%20-%20Shaping%20Tubing%20using%20Bench%20Vice%20and%20Grinder.jpg) |
| *Figure 4A: Precision cutting of galvanized pipe sections using an angle grinder.* | *Figure 4B: Cold forming and tube notch shaping using a heavy-duty bench vice and grinder.* |

### 4.2 Structural Welding & Drive Chassis Integration
![Arc Welding Frame](../media/Fabrication%20Phase%20-%20Arc%20Welding%20the%20Galvanized%20Steel%20Frame%20Tubing.jpg)
*Figure 5: Manual Metal Arc (MMA) welding of the primary load-bearing galvanized steel chassis.*

![Suspension & Motor Mounting](../media/Fabrication%20Phase%20-%20Rear%20Suspension%20Assembly%20%26%20Motor%20Mounting%20on%20Salvaged%20Cast-Iron%20Basement.jpg)
*Figure 6: Mounting the dual 24V 450W motors and assembling the rear coil spring suspension onto the heavy cast-iron lower base.*

### 4.3 Unpainted Prototype Fit-Check & Seating Integration
| Bare Metal Frame Pre-Assembly | Ergonomic Seating & Cushion Integration |
| :---: | :---: |
| ![Unpainted Prototype](../media/Assembly%20Phase%20-%20Unpainted%20Prototype%20Showing%20Caster%20Fork%20Extensions%20and%20Handlebars.jpg) | ![Seating & Cushions](../media/Integration%20Phase%20-%20Mounted%20Seating,%20Armrests,%20and%20Cushions%20Prior%20to%20Final%20Wiring.jpg) |
| *Figure 7A: Dimensional fit-check showing front caster fork extensions, ground clearance, and handlebars.* | *Figure 7B: Ergonomic fitment with custom backrest, padded armrests, and seat base prior to wire harness routing.* |

![Top-Down Integration View](../media/Integration%20Phase%20-%20Top-Down%20View%20of%20Seat%20Base%20and%20Backrest%20Integration.jpg)
*Figure 8: Plan view of the seat framework and battery enclosure alignment ensuring center-of-gravity stabilization.*

---

## 5. Protective Finishing & Anti-Corrosion Coating

Given the high humidity and variable outdoor climate, the fabricated steel frame underwent surface prep, zinc phosphate anti-rust priming, and multi-stage industrial enamel spraying.

| Frame Spraying & Curing | Caster & Mount Inspection |
| :---: | :---: |
| ![Finishing Phase Spraying](../media/Finishing%20Phase%20-%20Frame%20Painting%20and%20Protective%20Coating%20Application%20(Rear%20Angle).jpg) | ![Painted Frame Inspection](../media/Finishing%20Phase%20-%20Painted%20Frame%20Inspection%20with%20Front%20Casters%20and%20Control%20Mounts.jpg) |
| *Figure 9A: Applying protective high-gloss enamel coating in spray booth.* | *Figure 9B: Post-cure inspection of front casters, swivel bearings, and controller brackets.* |

| Freshly Painted Chassis Structure | Coated Battery & Power Enclosure |
| :---: | :---: |
| ![Freshly Sprayed Lower Frame](../media/Freshly%20Sprayed%20Lower%20Frame%20Structure.jpg) | ![Sprayed Frame & Enclosure](../media/Freshly%20Sprayed%20Lower%20Frame%20Structure%20and%20Battery%20Enclosure.jpg) |
| *Figure 10A: Cured lower chassis ready for motor fitment.* | *Figure 10B: Reinforced battery vault offering robust physical & ingress protection.* |

---

## 6. Electronics, Control Hardware & Technical Problem-Solving

### 6.1 The Technical Challenge: Custom MOSFET H-Bridge vs. Industrial Controller
As highlighted in my application responses, we originally designed a custom dual H-bridge motor driver using **IRF3205 MOSFETs** to drive the high-torque 24V 450W motors.

```
[Custom PCB Attempt]                                            [Final Working Solution]
High in-rush current (>30A peak)                                Shark MK5-SPJ+ Joystick
         │                                                               │
Thermal runaway on IRF3205s                                              ▼
(Heat sinks insufficient)      ──[Engineering Pivot]──►         Shark 6 Power Controller
         │                                              (Reliable 50A continuous H-bridge)
Gate driver switching delays                                             │
                                                                         ▼
                                                                Dual 24V 450W Motors
```

![Soldering and Reworking Custom PCB](../media/Soldering%20and%20Reworking%20Custom%20PCB%20Motor%20Driver%20Electronic%20Circuitry.jpg)
*Figure 11: Hands-on debugging and reworking the initial custom PCB driver circuitry on the electronics test bench.*

To prevent project delays while maintaining user safety and high electrical reliability, we made the pragmatic engineering decision to adopt the industrial-grade **Shark 6 Power Module**. This allowed us to dedicate the **Arduino Mega 2560** microcontroller exclusively to supervisory safety: real-time ultrasonic obstacle sensing, IMU tilt tipping prevention, GPS logging, and Bluetooth telemetry.

### 6.2 Drive Train & Actuator Hardware
| 24V 450W DC Motor & Gearbox | Primary Control Architecture |
| :---: | :---: |
| ![Drive Motor](../media/Simulation%20result%20of%20equivalent%20stress%20analysis.jpg) | ![Shark Control Architecture](../media/Wheelchair%20Primary%20Control%20System.jpg) |
| *Figure 12A: 24V 450W brushed DC drive motor with mechanical reduction gearbox and manual push/drive clutch lever.* | *Figure 12B: Primary control wiring layout connecting the Shark MK5 joystick, battery supply, and dual motor channels.* |

---

## 7. Mobile Telemetry & Caregiver Companion App

To ensure caregiver peace of mind and outdoor user independence, we developed a cross-platform mobile application in **Flutter** communicating with the wheelchair's onboard Arduino via **HC-05 Bluetooth**.

```
  [Wheelchair Sensors]
    * NEO-6M GPS          ──(Serial)──► [Arduino Mega 2560]
    * MPU6050 Tilt IMU    ──(I2C)   ──►        │
    * Ultrasonic Array    ──(GPIO)  ──►        ▼
                                         [HC-05 Bluetooth]
                                               │ (Wireless RF ~100m)
                                               ▼
                                   [Caregiver Mobile Phone]
                                       (Flutter App UI)
                                 - Real-time GPS Location
                                 - Tip-over Risk Buzzer / Push Alert
```

| Geolocation & Navigation Testing | Field Testing GPS Trail Over Regional Terrain |
| :---: | :---: |
| ![GPS Navigation App](../media/GPS%20and%20Geolocation%20Mapping%20Interface%20for%20Wheelchair%20Navigation%20Testing.jpg) | ![Field Testing Route Map](../media/Field%20Testing%20Route%20Map%20and%20GPS%20Tracking%20Interface%20over%20Regional%20Terrain.jpg) |
| *Figure 13A: Mobile navigation screen displaying real-time coordinate logging, heading, and turn-by-turn guidance.* | *Figure 13B: Live breadcrumb tracking recorded during outdoor road and terrain validation trials in Jos.* |

---

## 8. Physical Proof of Operation & Demonstration Video

The wheelchair underwent field validation across four real-world ground conditions: smooth indoor tiles, asphalt/concrete roads, open lawn grass, and rough unpaved gravel surfaces.

* 🎬 **Video Demonstration:**  
  [▶ View Test Drive Video File: `media/Video of me test riding the wheelchair.mp4`](../media/Video%20of%20me%20test%20riding%20the%20wheelchair.mp4)  

  [▶ View Test Drive Video File alternative link`](https://www.jouledynamics.me/wheelchair-demo)
  *(Demonstrates smooth joystick response, zero-turn agility, forward/reverse drive, suspension dampening).*

---

## 9. Engineering Competencies Demonstrated

* **Mechanical Engineering & CAD (Solo Ownership):** SolidWorks 3D parametric design, assembly modeling, production drawings, tolerance analysis.
* **Structural Simulation & FEA (Solo Ownership):** Static stress, Von-Mises yield evaluation, displacement limit analysis, factor-of-safety optimization.
* **Manufacturing & Fabrication (Team Collaboration):** Metal cutting, pipe bending, Manual Metal Arc (MMA) welding, assembly fitment, industrial painting.
* **Mechatronics & Embedded Systems (Team Collaboration):** Microcontroller programming (Arduino C++), sensor interfacing (HC-SR04 ultrasonic, MPU6050 6-DOF IMU, u-blox GPS, HC-05 Bluetooth).
* **Power Electronics & Troubleshooting (Team Collaboration):** DC brushed motors, high-current battery management, PCB layout troubleshooting, MOSFET thermal dynamics, industrial power controllers.
* **Software Development (Team Collaboration):** Flutter cross-platform mobile development, asynchronous Bluetooth serial communication, Google Maps API integration.
* **Leadership & Team Orchestration:** Leading a 7-person interdisciplinary engineering team, scrap reclamation, frugal engineering, budget optimization under tight deadlines.

