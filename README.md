# High Performance 30W PD Power Bank (3S 21700)

A professional-grade, high-performance 30W Power Delivery (PD) power bank design. This project features a modular architecture combining fast charging, robust multi-cell battery management, and an efficient synchronous buck controller.

## Technical Specifications

- **Input:** 15W Fast Charging (12.6V/1.2A) via IP2326 Boost Converter architecture.
- **Output:** Up to 30W Power Delivery (PD) via SW3518 Buck Converter.
- **Battery Configuration:** 3S (3 cell) 21700 Li-ion battery pack (approx. 5000mAh/cell, 50Wh total energy capacity).
- **Protection & Management:** Low-side switching BMS powered by BM3451, supporting over-charge, over-discharge, short-circuit, over-current protection, and active cell balancing.
- **Target BOM Budget:** Under 500,000 VND.

## System Architecture & Current Flow

### 1. Charging Mode (Input)
- **IC utilized:** IP2326 (configured for a 3S cell system via a 1kΩ resistor).
- **Current Pathway:** USB-C Input → IP2326 VIN → Internal Boost Switching (via Inductor L2) → VOUT → Battery Cell Positive (+) → Through 3S Battery Cells → Battery Cell Negative (-) → BMS Protection MOSFETs → System Ground (P-) → IP2326 PGND → USB-C Ground return.

### 2. Discharging Mode (Output)
- **IC utilized:** SW3518 (Synchronous Buck Controller).
- **Current Pathway:** Battery Positive (+) → SW3518 VIN → Internal Synchronous Buck Switching (High/Low-side MOSFETs) → Buck Inductor (L1) → Current Shunt Resistor → USB Type-C Port → External Load/Device → Device Ground Return → System Ground (P-) → BMS Protection MOSFETs → Battery Negative (-).

## Hardware Component Configurations
- **IP2326 Charge Current:** Configured via `RISET = 75kΩ` at the ISET pin to cap maximum input charge current at 1.2A.
- **Inductor L2 (Boost):** Requires a saturation current ($I_{SAT}$) of at least 5A.
- **BMS Protection MOSFETs:** Dual NMOS configured with $I_D > 10A$ and ultra-low $R_{DS(on)} < 10mΩ$ to ensure thermal stability and prevent burnout during continuous 3.33A discharge cycles (calculated at the 9V lower cutoff limit).

## Repository Directory Structure
- `/Hardware`: Contains the KiCad schematic (`.kicad_sch`), PCB layout (`.kicad_pcb`), and manufacturing files.
- `/Documentation`: Contains component datasheets and reference files.
