# 🏭 Room Comfort Control System (PLC-Based HVAC)

## 📌 Project Overview
This project implements a **PLC-based Room Comfort Control System** designed to maintain room temperature stability using **staged fan and compressor control**.  
The control logic follows **industrial HVAC best practices**, emphasizing **safety, stability, and equipment protection**.

Developed using **ladder logic**, this project is suitable for **simulation, learning, and automation engineering portfolios**.

---

## 🎯 System Objectives
- 🌡️ Maintain room temperature within defined comfort limits  
- 🔁 Prevent frequent ON–OFF switching (hunting)  
- ⚡ Provide immediate response during critical temperature conditions  
- 🛡️ Protect equipment using delay and interlock logic  
- 🚨 Detect faults and perform safe shutdown  
- 🔄 Support Auto and Manual operating modes  

---

## 🔄 Operating Modes

### 🤖 Auto Mode
- System operates automatically based on room temperature.
- All outputs are controlled by PLC logic.
- Enabled only when system permissive conditions are met.

### 🛠️ Manual Mode
- Auto logic is disabled.
- Outputs can be controlled manually for maintenance or testing.

⚠️ Auto and Manual modes are **mutually exclusive**.

---

## ✅ System Permissive (`System_OK`)
All automatic control logic is enabled only when:
- ✔ Auto mode is active  
- ❌ Emergency Stop is not active  
- ❌ No fan or compressor faults are present  

If `System_OK = FALSE`:
- 🔌 All outputs are turned OFF  
- 🚨 Alarm is activated if a fault exists  

---

## 🌡️ Temperature Classification (Status Layer)
Room temperature is continuously classified into the following conditions:

- 🟢 `Temp_Low`  
- 🔵 `Temp_Normal`  
- 🟡 `Temp_High`  
- 🔴 `Temp_Critical`  

These classifications are used for **monitoring, indication, and escalation**, not for direct output control.

---

## 🧠 Control Logic Philosophy

### 🔁 Low Mode with Hysteresis
To avoid unstable ON–OFF behavior, buffered control logic is applied:
- 🔼 `Low_Mode` is **SET** when temperature ≥ **25°C**
- 🔽 `Low_Mode` is **RESET** when temperature < **23°C**

This ensures stable fan and compressor operation.

---

### 🌀 Fan Control Logic
- **Fan Low** is activated when `Low_Mode` is active.
- **Fan High** is activated immediately when `Temp_Critical` is detected.
- During critical temperature conditions, **Fan High overrides Fan Low**.

---

### ❄️ Compressor Control Logic
- Compressors are enabled **only after fans are running**.
- ⏱️ A **15-second ON-delay timer** is applied before compressor startup.

Control strategy:
- `Low_Mode` active → **Compressor 1 ON**
- `Temp_Critical` active → **Compressor 1 and Compressor 2 ON**

---

## ⏱️ Delay & Equipment Protection
- Compressor startup delay prevents short cycling.
- Reduces mechanical stress and extends equipment lifetime.

---

## 🚨 Feedback & Fault Handling
Each actuator is monitored using feedback signals:
- Fan Low feedback  
- Fan High feedback  
- Compressor 1 feedback  
- Compressor 2 feedback  

If a commanded device fails to respond within the defined time:
- ❗ A corresponding fault is triggered  
- ⛔ `System_OK` becomes FALSE  
- 🔌 All outputs are shut down safely  
- 🚨 Alarm is activated  

---

## 🔔 Alarm Management
- Alarms are **latched** when a fault occurs.
- Alarm reset is allowed only after the fault condition is cleared.
- Prevents unnoticed intermittent faults.

---

## 🛡️ Safety Features
- Emergency Stop override  
- Immediate fan escalation during critical temperature  
- Fault-based system shutdown  
- Auto–Manual mode interlocking  

---

## 🔍 Typical Control Flow
1. Check Auto mode, Emergency Stop, and fault status  
2. Read room temperature  
3. Classify temperature condition  
4. Activate fans based on control logic  
5. Apply delay and start compressors if required  
6. Monitor feedback signals  
7. Trigger alarm and safe shutdown on fault  

---

## 📈 Project Status
- ✔ Control logic validated  
- ✔ Safety logic implemented  
- ✔ Ready for simulation and demonstration  
- ✔ Suitable for automation and PLC engineering portfolios  

---

## 📝 Notes
This project focuses on **control logic design and safety philosophy**.  
Physical hardware integration is represented through **simulated inputs and outputs**.

---

## 👤 Author
**Hilmi Dzakiana Maulidia**  
Bachelor of Engineering in Engineering Physics – Universitas Gadjah Mada  
Email: hilmi14dzakiana@gmail.com  
LinkedIn: [hilmidzakianamaulidia](https://www.linkedin.com/in/hilmidzakianamaulidia)
