# MLAP-ISW-Multi-Line-Automated-Production
Multi-line production and storage system (MLAP-ISW) using Siemens TIA Portal (SCL), Factory I/O, and SCADA.
# 🏭 Multi-Line Automated Production & Storage System (MLAP-ISW)

> **An integrated, multi-line smart manufacturing and automated warehouse system designed with Siemens TIA Portal (SCL) and simulated in Factory I/O 3D environment.**

---

## 📌 Project Overview

The **MLAP-ISW** (Multi-Line Automated Production and Storage System) is an advanced industrial control project showcasing modern smart factory architecture. The system coordinates three concurrent manufacturing lines responsible for processing metal parts in three different colors (Blue, Green, and Gray). 

It features automated material handling, CNC machining, part duplication, pneumatic assembly, crate packaging, collision-free conveyor synchronization, and an intelligent Automated Storage and Retrieval System (ASRS).

---

## 🛠️ Technology Stack & Tools

* **PLC Programming:** Siemens TIA Portal (SCL - Structured Control Language)
* **PLC Hardware Target:** Siemens S7-1200 / S7-1500
* **3D Simulation:** Factory I/O
* **Control Strategy:** Finite State Machines (FSM), Timer-based Synchronization, Collision & Stacking Prevention
* **Supervisory Control:** SCADA Interface (Real-time tracking, Storage Occupancy Matrix)

---

## ⚙️ System Architecture & Workflow

The production process is structured across three synchronized concurrent lines:

1. **Sorting & Material Handling:** Raw metal parts (Blue, Green, Gray) are sorted and transferred to CNC machining units.
2. **Machining & Duplication:** Parts undergo CNC processing, followed by part duplication using conveyor-based alignment.
3. **Pneumatic Assembly System:** High-precision vertical and horizontal pneumatic actuators press two separate components into a unified finished product.
4. **Crate Packaging:** Assembled products are automatically picked up by a multi-axis pneumatic system and placed inside transport crates.
5. **Smart Storage Platform (ASRS):** Crates travel via interlocked conveyors to an automated warehouse. An intelligent positioning algorithm maps crates into predetermined grid coordinates for optimal space utilization.
6. **Safety & Collision Prevention:** Distributed proximity and photoelectric sensors prevent material stacking and conveyor jams.

---

## 💻 Code Structure Highlights

The entire system logic is implemented in **Structured Control Language (SCL)**, emphasizing modularity, robust state handling, and clean execution.

```scl
// Example: State Transition Logic for Automated Pick & Place Assembly
CASE #CurrentState OF
    10: // Wait for Part Presence
        IF "Sensor_Part_In_Position" AND "System_Active" THEN
            "Pneumatic_Clamp" := TRUE;
            #CurrentState := 20;
        END_IF;

    20: // Vertical Press Motion
        "Actuator_Z_Down" := TRUE;
        IF "Sensor_Z_Lower_Limit" THEN
            "Actuator_Z_Down" := FALSE;
            #CurrentState := 30;
        END_IF;
        
    // Additional sequential state execution...
END_CASE;
How to Run the Project
​Prerequisites:
​Siemens TIA Portal V16 or higher.
​Factory I/O (v2.4+ recommended).
​PLCSIM / PLCSIM Advanced.
​Steps:
​Clone this repository: git clone https://github.com/slah87/MLAP-ISW-Multi-Line-Automated-Production.git
​Open the TIA Portal project file located in /TIA_Project.
​Start PLCSIM and download the program block configuration.
​Open the 3D scene file located in /FactoryIO_Scene/MLAP_ISW.factoryio.
​Connect Factory I/O driver to Siemens S7-PLCSIM and press Play.
​👤 Author
​Eng. Salah Almolad
Mechatronics & Industrial Automation Engineer
​Specializing in Industrial Control Systems, PLC/SCADA Programming, and Virtual Commissioning.
