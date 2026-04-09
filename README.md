# ESP32 Audio & Weather Monitor

This project successfully integrates an **INMP441 I2S Microphone** and a **DHT11 Temperature/Humidity Sensor** using an ESP32-S (NodeMCU). 

<img width="1279" height="882" alt="image" src="https://github.com/user-attachments/assets/2ee4e1cf-a480-46be-9012-92a4ebcd87c2" />



https://github.com/user-attachments/assets/db256745-30d1-4de7-838c-bce71d615b78


## ⚠️ Hardware Warning
* **Do not use ESP32 DevKit V1 (Rev 1 chips)**: They have a known APLL clock bug that prevents the INMP441 from syncing properly. Use an ESP32-S or NodeMCU (Rev 3).
* **Power**: Power the sensors directly from the `3V3` pin, not via GPIOs.

## 🔌 Pinout Configuration

| Component | Sensor Pin | ESP32 Pin | Function / Note |
| :--- | :--- | :--- | :--- |
| **INMP441** | **SCK** | **GPIO 18** | I2S Serial Clock |
| | **WS** | **GPIO 19** | I2S Word Select |
| | **SD** | **GPIO 21** | I2S Serial Data |
| | **L/R** | **GND** | Selects Left Channel (Crucial) |
| | **VDD** | **3V3** | Main Power |
| | **GND** | **GND** | Ground |
| | | | |
| **DHT11** | **DATA** | **GPIO 4** | Temp/Humidity Data |
| | **VCC** | **3V3** | Main Power |
| | **GND** | **GND** | Ground |

## 📐 Circuit Diagram

```mermaid
graph LR
    subgraph ESP32 ["ESP32-S (NodeMCU-32S)"]
        direction TB
        P_3V3(["3V3 (Power)"])
        P_GND(["GND (Ground)"])
        P_18["GPIO 18 (SCK)"]
        P_19["GPIO 19 (WS)"]
        P_21["GPIO 21 (SD)"]
        P_04["GPIO 4 (DHT Data)"]
    end

    subgraph MIC ["INMP441 Microphone"]
        direction TB
        M_VDD["VDD"]
        M_GND["GND"]
        M_LR["L/R (Channel Select)"]
        M_SCK["SCK"]
        M_WS["WS"]
        M_SD["SD"]
    end

    subgraph DHT ["DHT11 Sensor"]
        direction TB
        D_VCC["VCC"]
        D_GND["GND"]
        D_DATA["DATA"]
    end

    P_3V3 === M_VDD
    P_3V3 === D_VCC
    P_GND === M_GND
    P_GND === M_LR
    P_GND === D_GND

    P_18 --- M_SCK
    P_19 --- M_WS
    P_21 --- M_SD
    P_04 --- D_DATA

    linkStyle 0,1 stroke:red,stroke-width:3px;
    linkStyle 2,3,4 stroke:black,stroke-width:3px;
    
    style ESP32 fill:#e3f2fd,stroke:#1565c0,stroke-width:2px
    style MIC fill:#fff3e0,stroke:#e65100,stroke-width:2px
    style DHT fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px

```

### Did the hardware part
### Integration and Software was done by sidoit(Sidhart Sajith)
