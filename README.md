# matlab-serial-boost-converter
Control an Arduino DC-DC boost converter and tune PI parameters directly from MATLAB via serial communication.
# Control an Arduino Boost Converter from MATLAB

A beginner's step-by-step guide to controlling a DC-DC boost converter using an Arduino Uno and MATLAB. Set your target voltage ($V_{ref}$), proportional gain ($K_p$), and integral gain ($K_i$) directly from MATLAB, view live telemetry in the Command Window and plots, and even run an auto-tuning script to find the optimal controller parameters[cite: 1].

---

## 🚀 What You Will Build
* Run a PI controller on an Arduino Uno that regulates a boost converter's output voltage to a target value[cite: 1].
* Send parameters (`VREF`, `KP`, `KI`, `RESET`) from MATLAB via serial communication without needing to re-upload Arduino code[cite: 1].
* Monitor real-time performance with a command window telemetry table and live plotting of voltage and duty cycle[cite: 1].
* Automatically test multiple $K_p$ and $K_i$ combinations using an auto-tuning script to find the best configuration[cite: 1].

---

## 🛠️ What You Need

| Item | Notes |
| :--- | :--- |
| **Arduino Uno** | With a USB cable[cite: 1]. |
| **Boost Converter Power Stage** | Inductor, diode, output capacitor, and a MOSFET switch module (e.g., LR7843) driven by the Arduino[cite: 1]. |
| **Voltage Divider** | $R_{TOP} = 40\text{ k}\Omega$, $R_{BOT} = 10\text{ k}\Omega$. The Arduino sees $V_{out} / 5$[cite: 1]. |
| **Potentiometer (optional)** | Manual target knob on `A4` (used only until MATLAB sends a target)[cite: 1]. |
| **MATLAB** | R2019b or newer (uses the `serialport` function). No extra toolbox needed[cite: 1]. |
| **Arduino IDE** | To upload the code once[cite: 1]. |

---

## 🔌 Wiring Guide

| Arduino Pin | Connect To |
| :--- | :--- |
| **D9** | Signal input of the MOSFET module (PWM output)[cite: 1]. |
| **A5** | Middle point of the voltage divider (between the $40\text{ k}\Omega$ and $10\text{ k}\Omega$ resistors)[cite: 1]. |
| **A4** | Middle pin of the potentiometer (ends go to $5\text{ V}$ and $\text{GND}$)[cite: 1]. |
| **GND** | Ground of the converter and the divider's bottom resistor. **All grounds must be common.**[cite: 1] |

*Note: The converter output goes to the top of the $40\text{ k}\Omega$ resistor, then $40\text{ k}\Omega$, then the `A5` junction, then $10\text{ k}\Omega$, then $\text{GND}$. If you use other resistor values, update `R_TOP` and `R_BOT` in the Arduino code[cite: 1].*

---

## 💻 Quick Start Guide

### Step 1: Upload the Arduino Code
1. Open the Arduino IDE, create a new sketch, and paste the code found in `arduino/boost_controller/boost_controller.ino`[cite: 1].
2. Choose **Tools > Board > Arduino Uno** and select your appropriate **COM port**[cite: 1].
3. Click **Upload**, then **close the Serial Monitor** (MATLAB needs exclusive access to the port)[cite: 1].

### Step 2: Run the Manual Control Script
1. Open MATLAB and open `matlab/boost_manual.m`[cite: 1].
2. Find your port by typing `serialportlist` in the MATLAB Command Window and update the `port` variable (e.g., `"COM10"`)[cite: 1].
3. Set your desired `Vref`, `Kp`, `Ki`, and `runTime` values[cite: 1].
4. Click the green **Run** button to execute the script and observe live telemetry and summary plots[cite: 1].

### Step 3: (Optional) Run the Auto-Tuner
1. Open `matlab/boost_autotune.m`[cite: 1].
2. Ensure the `port` matches your setup[cite: 1].
3. Click **Run** to automatically sweep through specified $K_p$ and $K_i$ lists, evaluate performance metrics, and determine the optimal parameters[cite: 1].

---

## ⚠️ Safety Warning
* Start with low voltages and a small load[cite: 1].
* Never set a target above your capacitor and load ratings. The scripts include a safety stop if $V_{out}$ exceeds $20\text{ V}$, but they cannot protect components rated lower[cite: 1].
* Keep hands away from live connections; boost converter output voltages are higher than the input[cite: 1].
* Never leave a running converter unattended[cite: 1].

---

## 📄 License
This project is open-source and available under the [MIT License](LICENSE).
