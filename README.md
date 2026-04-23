# 🚦 SDN-Based Access Control System

## 📌 Project Overview
This project implements an **Access Control System using Software Defined Networking (SDN)** with the **Ryu Controller**.  
The goal is to **allow communication only between authorized hosts** and block all unauthorized traffic in the network.

---

## 🎯 Problem Statement
In traditional networks, enforcing access control is complex and distributed.  
This project solves the problem by:
- Centrally controlling traffic using SDN
- Allowing only trusted hosts (whitelist)
- Blocking unauthorized communication automatically

---

## 🧠 Key Concept
The controller:
- Maintains a **whitelist of IP addresses**
- Inspects every incoming packet
- Applies rules:
  - ✅ Allow → if both source and destination are in whitelist  
  - ❌ Block → otherwise  

---

## ⚙️ Technologies Used
- Python
- Ryu SDN Controller
- Mininet
- OpenFlow 1.3
- Ubuntu/Linux

---

## 🏗️ Network Topology
h1 , h2 , h3 --- Hosts || 
s1 ---- Controller (Ryu)


---

## 🔐 Access Control Policy
python
WHITELIST = ["10.0.0.1", "10.0.0.2"]
| Source | Destination | Result    |
| ------ | ----------- | --------- |
| h1     | h2          | ✅ Allowed |
| h1     | h3          | ❌ Blocked |
| h2     | h3          | ❌ Blocked |

---

## 🚀 How to Run the Project
1️⃣ Install Dependencies
---
sudo apt update
sudo apt install mininet
pip install ryu

---

2️⃣ Activate Virtual Environment
---
source sdn-env/bin/activate

---

3️⃣ Run Ryu Controller
---
ryu-manager access_control.py

---

4️⃣ Start Mininet
---
sudo mn --topo single,3 --mac --controller remote

---

5️⃣ Test Connectivity
---
pingall

---

📊 Expected Output
---
Controller Logs - Terminal 1

ALLOWED: 10.0.0.1 -> 10.0.0.2
BLOCKED: 10.0.0.1 -> 10.0.0.3
BLOCKED: 10.0.0.2 -> 10.0.0.3

Mininet Output - Terminal 2

Results: 66% dropped (2/6 received)

---

🔍 Code Explanation
---
🔹 Flow Installation
*Default rule sends packets to controller

---

🔹 Packet Handling
*Extract Ethernet + IP packet
*Learn MAC addresses
*Apply access control logic

---

🔹 Access Control Logic
if ip_pkt.src in WHITELIST and ip_pkt.dst in WHITELIST:
    # Allow
else:
    # Drop
    
---

🧪 Testing & Verification
---
✔ Verified allowed communication (h1 ↔ h2)
✔ Verified blocked communication (h1 ↔ h3, h2 ↔ h3)
✔ Regression tested for consistent policy enforcement

---

⚠️ Known Issues
---
->Bash warning:
->not a valid identifier
➝ Caused by typo in .bashrc (does not affect execution)

---

📈 Future Improvements
---
->Dynamic whitelist updates (REST API)
->GUI dashboard
->Role-based access control (RBAC)
->Logging & analytics

---

📚 Learning Outcomes
---
->Understanding SDN architecture
->Working with Ryu controller
->OpenFlow rule management
->Network security using SDN

---

👨‍💻 Author
---
Manish Ranga Chinnala

---
