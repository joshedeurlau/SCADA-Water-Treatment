# SCADA-Water-Treatment

## Process Overview using Plant States
The PLC logic uses sequential numbered states to determine the logic sequence. 
* **State 0:** The system is completely off.
* **State 1:** The system turns on, and the intake pump activates to flow water into the tank.
* **State 2:** The mixer motor spins and the chlorine pump is activated for a 5-second treatment cycle.
* **State 3:** The discharge pump activates to move the treated water away.
* **State 99:** Triggered by an E-Stop press or active alarm. All equipment turns off and stays locked out until the manual reset button is pressed.

## Applications used
* **HMI/SCADA Front-End:** Inductive Automation Ignition (Perspective Module).
* **PLC Back-End:** CODESYS V3 using Ladder Logic
* **Communication:** Modbus TPC over Ethernet IP to connect the PLC to the Ignition Gateway.
* **Design Style:** ISA-101
* **Network:** Managed IP address assignment and local port routing for the Modbus TCP driver.

## Key Engineering Features
  - I/O inputs: linked Modbus Discrete Inputs (DI) and Holding Registers (HR) on CODESYS to their corresponding Ignition tags.
  - User-Defined Types (UDTs) to standardize pump instances to ensure it's scalable.
  - Implemented retentive memory in CODESYS for pump runtime even when the PLC is shut-down and turned back on again.
  - Emergency Stop logic as a top-priority Normally Closed (NC) rung in the PLC.
  - Real-time alarming
  - Data historian to create a Trend Chart that visualizes tank levels overtime.
  - Map transforms and Property Bindings to change PLC booleans into easily readable status colors.
  - Troubleshot data collection and tag errors between the PLC and HMI during startup and the simulation.
 
## Project Demonstrations (GIFs Show Bad Quality, go to the Assets Folder to View it Properly)

### 1. Process Lifecycle & Trending
![Full_Process](assets/01_Full_Process.gif)
- Normal Operation phases, alongside Flow Rate monitoring and a Historical Data Plotting Graph

### 2. E-Stop Interlock and Reset
![Safety Override](assets/02_E_Stop_and_Reset.gif)
- Start -> E-Stop -> Reset sequence, the PLC interlock overrides the SCADA "Start" button

### 3. Overflow at 98% with the PLC logic in the Split Screen
![Alarm](assets/03_Overflow_Alarm.gif)
- Shows the CODESYS ladder logic triggering the high level overflow sensor and the resulting critical alarm shown in red in the Ignition Alarm Status Table

