#  Precrash Seatbelt System – CANoe Project

This project demonstrates the simulation of an intelligent **Precrash Seatbelt System** in a CANoe environment, showcasing how sensor-driven crash detection triggers automated seatbelt pretensioning to enhance occupant safety and reduce injury risks before a collision occurs.

---

![image](https://github.com/user-attachments/assets/4f858986-d436-42d3-8a67-9bb32d7e8dc7)

Image Source : extension://efaidnbmnnnibpcajpcglclefindmkaj/https://zf-dev.aryxe.tech/uploads/67_27_ESV_Machens_Hy_DRA_8d43436605.pdf

Image Source : https://thecarseatlady.com/car-seats/5steptest/


##  Functional Overview
![ScreenRecording2025-06-22093242-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/9f11919e-76aa-4553-a927-80f8fab4388d)


### 1. Detection of Impending Crash
The system monitors a range of vehicle dynamics using:
- Radar Sensors
- Camera Systems
- Lidar
- ESC & ABS feedback
- Accelerometers

These sensors detect sudden decelerations and hazardous scenarios ahead of time.

### 2. Activation of Seatbelt Pretensioner
When an emergency situation is judged, the ECU engages a motorized pretensioner, retracting the shoulder belt to provide both protection and a sense of security.

### 3. Passenger Positioning & Load Adjustment
The system subtly adjusts belt tension for optimal occupant posture and airbag compatibility.

---

##  Benefits

![image](https://github.com/user-attachments/assets/96dd5b4f-6526-4ccc-98cc-f0a074f78271)

Image Source : https://zf-dev.aryxe.tech/uploads/67_27_ESV_Machens_Hy_DRA_8d43436605.pdf

- Enhanced passenger protection
- Reduced airbag-related injuries
- Works across multiple emergency types
- Provides maximum restraint before crash onset

##  Limitations
- High component and integration cost
- Potential for false activations
- System complexity and calibration needs
- Sensor-dependent performance

---

##  Operation Conditions

![image](https://github.com/user-attachments/assets/9d80c83e-4df7-4c9f-b894-e2132f9fe635)

Image Source : http://www.sgcarmart.com/news/article.php?AID=1901

###  Activation Conditions
- Emergency braking detected
- No operation prohibition state active

###  Operation Prohibition Conditions
- Seatbelt is unfastened
- Vehicle speed ≤ 15 km/h
- Pretensioner triggered 3 times successively (requires ~7-minute cooldown)
- Fail-safe state triggered

---

##  CAN Signals

- `Seatbelt_Lock_Signal`  - whether the seatbelt is latched or unlatched
- `Seatbelt_Rotation_Signal` - detects the rotational movement of the seatbelt spool or retractor mechanism
- `Brake_Pedal_Signal` – varies with stroke
- `Accelerator_Signal` – represents throttle input

---

##  Project Structure

### 1. Simulation
![Screenshot 2025-06-22 093430](https://github.com/user-attachments/assets/93e42018-0043-4d54-afc0-68e1030443f6)
![Screenshot 2025-06-22 093440](https://github.com/user-attachments/assets/c9afa65b-5a07-46d3-9676-c0e4302fab4d)

Includes CANoe configuration files for Precrash ECU and Tester ECU to emulate real-time CAN communication. Enables simulation of crash detection logic and seatbelt actuation flow.

### 2. Database Creation
![Screenshot 2025-06-22 093542](https://github.com/user-attachments/assets/5fb2317a-c484-4e92-b9d2-76e606dd646e)

Contains the `.dbc` file defining CAN signals and message structures. Ensures consistent interpretation of data across all simulation nodes and tools.

### 3. Panel Design
![Screenshot 2025-06-22 093729](https://github.com/user-attachments/assets/4f0d2205-23d3-4079-9cee-0c8ea1e345cd)

Custom visual interface for real-time monitoring and control. Displays ECU activity, sensor input status, and seatbelt operation indicators.

### 4. CAPL Scripting
![Screenshot 2025-06-22 093815](https://github.com/user-attachments/assets/6d9db0c0-742a-4630-887d-394a273c53f5)

Automation logic implemented in CAPL to simulate sensor behavior, activate diagnostics, and control seatbelt mechanisms. Scripts validate system performance under various test scenarios.

---

##  Diagnostic System Design

### Precrash ECU
1. Listens to CAN messages continuously  
2. On threshold brake input: fastens belt within 0.5 seconds  
3. On accelerator = 0: releases belt  

### Tester ECU
1. Periodically sends CAN messages  
2. Sends MSB = 15 signal to simulate brake input  
3. Verifies lock signal from Precrash ECU  
4. Sends acceleration message  
5. Confirms belt reset condition  



---

##  Test Scenarios

1. System detects valid brake signal voltage  
2. Seatbelt locks within 0.5 seconds  
3. Release occurs when acceleration = 0  
4. Validates ECU response over CAN  

---

## 📄 License

This project is open source and intended for educational purposes.  
You are welcome to use, adapt, and share the content. 
