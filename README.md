# CMOS Inverter Layout & Physical Verification 

This project demonstrates the full physical design flow of a CMOS Inverter using the **Cadence Virtuoso** suite and **GPDK 90nm** technology. The workflow includes layout generation, Design Rule Check (DRC), Layout vs. Schematic (LVS), and Parasitic Extraction (RCX).

---

## 🛠 Technical Specifications
* **Process Node:** 90nm CMOS (gpdk090)
* **Supply Voltage ($V_{DD}$):** 1.2 V
* **Metal Layers:** 9-Metal Layer stack
* **Minimum Feature Size:** $90nm$ gate length
* **Tools:** Cadence Virtuoso, Assura/PVS Verification Suite

---

## 1. Environment & Generation Setup
Before drawing, the LSW (Layer Selection Window) and display filters are configured. The generation options are set to ensure proper alignment with the 90nm manufacturing grid.

| Display Preferences | Layout Generation Options |
| :--- | :--- |
| <img width="1211" height="490" alt="Screenshot 2025-08-06 134143" src="https://github.com/user-attachments/assets/8526f135-b1f4-42bf-81a0-d72737434512" />| <img width="1185" height="503" alt="Screenshot 2025-08-06 134203" src="https://github.com/user-attachments/assets/39edbbc0-5531-463f-a9ae-94a9433be253" />
 

---

## 2. Layout Design & Pinning
Pins are imported from the schematic to maintain connectivity. The layout uses standard 90nm layers: **N-well** for PMOS, **Oxide/Active** for diffusion, and **Poly** for the gate.

### Pin Configuration
Pins (`vdd`, `gnd`, `vin`, `vout`) are defined on **Metal1** to allow for standard cell routing.
![Pin Placement]<img width="891" height="442" alt="Screenshot 2025-08-06 134310" src="https://github.com/user-attachments/assets/f49bd22c-4b76-4322-8415-ab06a1b3ef5b" />


### Final Physical Layout
The final inverter layout featuring optimized area and symmetric routing.
<img width="1523" height="662" alt="Screenshot 2025-08-06 134551" src="https://github.com/user-attachments/assets/a7faac26-7349-4d84-bb06-606fdc5815cf" />


---

## 3. Physical Verification (Assura)
Verification ensures the design is free of manufacturing errors and matches the electrical intent.

### Design Rule Check (DRC)
The DRC verifies that all geometric shapes satisfy the GPDK 90nm rules (e.g., minimum poly width, metal spacing, and well enclosure).
* **Process:** The Assura DRC engine scans the GDSII data against the technology's rule deck.
* **Result:** **Clean.** No violations found.
| DRC Run in Progress | DRC Result: Clean |
| :--- | :--- |
|![DRC Progress]<img width="1565" height="806" alt="Screenshot 2025-08-06 134407" src="https://github.com/user-attachments/assets/604d4887-8d9f-4681-a4ee-4ff5538a7c19" /> | ![DRC Pass]<img width="1456" height="683" alt="Screenshot 2025-08-06 134421" src="https://github.com/user-attachments/assets/5d1a8cd7-1a08-4c54-a2cb-c829fabdb662" />

### Layout vs. Schematic (LVS)
LVS extraction identifies the devices and nets in the layout and compares them to the schematic netlist. It checks for:
1. **Device Mismatch:** Correct number of PMOS/NMOS.
2. **Property Mismatch:** Width ($W$) and Length ($L$) values.
3. **Connectivity:** Correct wiring of gates, sources, and drains.
<img width="1121" height="696" alt="Screenshot 2025-08-06 134437" src="https://github.com/user-attachments/assets/92ea73f8-ae32-49a2-8f58-142005cb157d" />


---

## 4. Parasitic Extraction (RCX)
To perform post-layout simulations, parasitic resistance and capacitance are extracted to account for interconnect delays.
<img width="1517" height="817" alt="Screenshot 2025-08-06 134505" src="https://github.com/user-attachments/assets/428411d7-4f2c-439f-99a7-27f5f29d7e3d" />


---

## 💡 Key GPDK 090 Layers Used
| Layer | Name | Purpose |
| :--- | :--- | :--- |
| **NW** | N-Well | Base for PMOS transistors |
| **OD** | Oxide/Active | Defines Source/Drain regions |
| **PO** | Poly | Gate material ($L_{min} = 90nm$) |
| **M1** | Metal 1 | Primary interconnects and Pins |
| **CO** | Contact | Connects Metal to Poly/Active |
