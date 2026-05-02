# DIY Active Sim Racing Belt Tensioner: Complete Build Guide

## 1. Introduction

**What is an Active Belt Tensioner?**  
In sim racing, a belt tensioner physically pulls your shoulder straps (or a harness) tight during braking and loosens during acceleration, adding a realistic G-force feel. Unlike a static harness, an *active* tensioner uses motors to dynamically adjust tension based on telemetry data from your sim.

**How This Project Works**  
This design uses two **hoverboard motors** driven by an **ODESC (open-source ODrive clone)** controller. The motors wind bicycle brake cables around 3D-printed spools, pulling on your harness straps. The ODESC receives commands from **SimHub** (popular sim racing telemetry software), which interprets game data (G-forces, engine vibration, gear shift kick) to control motor torque.

**Source Repository:** [github.com/garyrtl/Active-Sim-Racing-Belt-Tensioner](https://github.com/garyrtl/Active-Sim-Racing-Belt-Tensioner)

---

## 2. Bill of Materials (BOM) with Estimated Costs

| Item | Approx. Cost |
|------|---------------|
| ODESC 3.6 Dual-drive, 56V version (required for hoverboard motors) | $55 |
| 24V 20A PSU (generic) | $30 |
| 2 used hoverboard motors | $30 |
| 2 SK16 supports | $16 |
| 2 Bicycle brake cables | $5 |
| PETG Filament | $4 |
| 16 M4 20mm bolts | $3 |
| 6 M5 25mm bolts | $2 |
| 6 M5 nuts | $2 |
| 4 M5 or M6 4040 T-nuts | $2 |


> **Cost-Saving Tips:**
> - Buy **used hoverboard motors** from broken hoverboards (often $10–20 each)

---

## 3. Step-by-Step Build Guide

### Step 1: 3D Print the Pulley Spools

- Download `pulley-spool.stl` from the [GitHub repo](https://github.com/garyrtl/Active-Sim-Racing-Belt-Tensioner/blob/main/pulley-spool.stl) or open the [Tinkercad design](https://www.tinkercad.com/things/5T1yV7gz4mY-active-belt-tensioner)
- **Print settings:** 100% infill (for strength), PLA or PETG
- You need **two spools** – one for each shoulder strap

### Step 2: Prepare Hoverboard Motors

- Remove the tire from each hoverboard motor, leaving only the metal hub with the motor windings
- Remove 6 phillip screws from the motor hub. Install the spool to the motor. Fasten spool with 6 x M4 20mm bolts
- You should see **3 thick phase wires** (usually yellow, blue, green) and **5 thin sensor wires** (red, black, and three signal wires)
- Keep the hall sensor wires – the ODESC can use them for smoother control
- Solder or crimp spade connectors onto the phase wires

### Step 3: Wire the Electronics

> ⚠️ **Safety:** 24V at 20A is dangerous. Double-check polarity and use thick wires.

**Power connections:**
- Power supply AC input → wall outlet (with ground)
- Power supply DC output (+24V) → ODESC "PV" terminal (power input)
- Power supply DC output (GND) → ODESC "GND" terminal

**Motor connections (repeat for both motors):**
- ODESC "M0" (U, V, W) → Motor phase wires (any order initially – we'll tune later)
- ODESC "M0 Hall" → Motor hall sensors (match colors if possible, refer to ODrive guide)

**USB:** Connect ODESC to your PC via micro-USB

### Step 4: Mount Motors and Linear Supports

- **Mount SK16 shaft supports** to 4040 aluminum extrusions using M5 or M6 bolts and t-nuts. Mount hoverboard motors to SK16 shaft supports.
  
  **DO NOT** connect bicycle brake cables yet!
  <img width="600" alt="IMG_4249" src="https://github.com/user-attachments/assets/43eb55a9-5360-4e20-98b8-2227e728602d" />

### Step 5: Configure ODESC for Hoverboard Motors

1. Install ODrive tools on your PC (Python + odrivetool)
2. Run `odrivetool` and connect to the ODESC
3. Calibrate each motor: 
Follow the [ODrive hoverboard motor guide](https://docs.odriverobotics.com/v/0.5.6/hoverboard.html) but adapt for ODESC:

### Step 6: Assemble the Cable & Spool Mechanism

1. Insert the bicycle brake cable through M5 bolts in the spool
   <img width="600" alt="IMG_4180" src="https://github.com/user-attachments/assets/8e04973b-9a4f-4941-8bc8-45806ae354ce" />
2. Attach the other end of the cable to the harness strap anchor bracket.
   <img width="600" height="4032" alt="IMG_4268" src="https://github.com/user-attachments/assets/e7368e75-6ac2-4b95-9c9f-45fd2688481a" />

###Step 7: Set Up SimHub (Telemetry to Tensioner)
Download and install SimHub

1. In SimHub, go to Custom Serial Device. Add a new device
2. Click "Import" and select the file belt-tensioner-settings.shsds from the GitHub repo
3. Set Serial Port to the COM port of your ODESC (look for "ODrive 3.6 CDC")

