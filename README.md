# **Full Circuit Diagram - Line Follower Robot**

Unga components: **Arduino Uno + N20 1000RPM Motors (2) + 8 IR Sensor Array + TB6612FNG Motor Driver + 7.4V LiPo Battery (2x 3.7V series)**

##  **Complete Wiring Diagram - Text Format**

```
                    [3.7V LiPo Batt 1]     [3.7V LiPo Batt 2]
                         +          -          +          -
                         |          |          |          |
                         |          +----------+          |
                         |                               |
                         +---------------+---------------+
                                         |
                                    [7.4V OUTPUT]
                                         |
                    +--------------------+-----------------------+
                    |                    |                       |
              [DC Jack]              [VM Pin]               [Common Ground]
              (Arduino)           (TB6612FNG)                    |
                    |                    |                       |
              [Arduino Uno]          [TB6612FNG] <---------------+
              (VIN - 7.4V)            (Motor Driver)              
                    |                    |                       |
                    | (5V out)            | (VCC - 5V)            |
                    +--------------------+                       |
                                         |                       |
                    +--------------------+                       |
                    |                    |                       |
              [8 IR Sensors]         [Control Pins]              |
              (VCC - 5V)           (to Arduino)                  |
                    |                    |                       |
                    +--------------------+-----------------------+
                                         |
                                   [Common GND]
```

## **Detailed Pin-to-Pin Connections**

### **1. POWER SECTION**
```
Battery Connections (2x 3.7V in SERIES):
┌─────────────────────────────────────────────────┐
│ Batt1 (+) ─────┬─────► Arduino VIN (7.4V)       │
│                ├─────► TB6612FNG VM (Pin 1)      │
│ Batt1 (-) ─────┴─────► Batt2 (+)                  │
│ Batt2 (-) ───────────► Common GND                 │
└─────────────────────────────────────────────────┘
```

### **2. ARDUINO UNO to TB6612FNG**
```
TB6612FNG Pin    →    Arduino Uno Pin    →    Wire Color (Suggested)
────────────────────────────────────────────────────────────────
VM (Pin 1)       →    Battery 7.4V (+)   →    Red (Thick)
VCC (Pin 2)      →    5V                 →    Orange
GND (Pin 3)      →    GND                →    Black
PWMA (Pin 4)     →    Pin 5 (PWM)        →    Yellow
AIN1 (Pin 5)     →    Pin 7              →    Green
AIN2 (Pin 6)     →    Pin 8              →    Blue
PWMB (Pin 7)     →    Pin 6 (PWM)        →    Yellow/Black
BIN1 (Pin 8)     →    Pin 9              →    Green/Black
BIN2 (Pin 9)     →    Pin 10             →    Blue/Black
STBY (Pin 10)    →    Pin 11 (or 5V)     →    White
AO1 (Pin 11)     →    Motor A (+)        →    Red
AO2 (Pin 12)     →    Motor A (-)        →    Black
BO1 (Pin 13)     →    Motor B (+)        →    Red
BO2 (Pin 14)     →    Motor B (-)        →    Black
GND (Pin 15)     →    Battery GND        →    Black (Thick)
────────────────────────────────────────────────────────────────
```

### **3. 8 IR SENSOR ARRAY to ARDUINO**
```
IR Sensor Array    →    Arduino Uno Pin    →    Wire Color
─────────────────────────────────────────────────────────
VCC (5V)           →    5V                 →    Red
GND                →    GND                →    Black
Sensor Out 1       →    A0                 →    White
Sensor Out 2       →    A1                 →    Gray
Sensor Out 3       →    A2                 →    Purple
Sensor Out 4       →    A3                 →    Blue
Sensor Out 5       →    A4                 →    Green
Sensor Out 6       →    A5                 →    Yellow
Sensor Out 7       →    A6                 →    Orange
Sensor Out 8       →    A7                 →    Brown
─────────────────────────────────────────────────────────
```

##  **Visual Circuit Diagram (ASCII Art)**

```
                             7.4V SERIES BATTERY PACK
                         ┌─────────────────────────────┐
                         │  [3.7V]      [3.7V]         │
                         │  +   -       +   -          │
                         │  │   │       │   │          │
                         │  │   └───────┘   │          │
                         │  │               │          │
                         │  └───────┬───────┘          │
                         │          │                  │
                         └──────────┼──────────────────┘
                                    │ 7.4V
                  ┌─────────────────┼──────────────────┐
                  │                 │                  │
              [VIN]             [VM]│              [GND]
              ┌──┴──┐           ┌───┴───┐           ┌──┴──┐
              │     │           │       │           │     │
         ┌────▼────┐    ┌───────▼───────┴───────┐   │     │
         │ ARDUINO │    │                      │   │     │
         │   UNO   │    │   TB6612FNG          │   │     │
         │         │    │   MOTOR DRIVER       │   │     │
         │ 5V──────┼────┼──►VCC                │   │     │
         │ GND─────┼────┼──►GND◄───────────────┼───┘     │
         │         │    │   PWMA (5)◄──────────┼──Pin 5  │
         │         │    │   AIN1 (7)◄──────────┼──Pin 7  │
         │         │    │   AIN2 (8)◄──────────┼──Pin 8  │
         │         │    │   PWMB (6)◄──────────┼──Pin 6  │
         │         │    │   BIN1 (9)◄──────────┼──Pin 9  │
         │         │    │   BIN2 (10)◄─────────┼──Pin 10 │
         │         │    │   STBY (11)◄─────────┼──Pin 11 │
         │         │    │                      │         │
         │         │    │   AO1────┬───────────┼──Motor A│
         │         │    │   AO2────┘           │   (+)   │
         │         │    │                      │   (-)   │
         │         │    │   BO1────┬───────────┼──Motor B│
         │         │    │   BO2────┘           │   (+)   │
         └────┬────┘    └──────────────────────┘   (-)   │
              │                                              │
         ┌────┴─────────────────────────────────────────────┘
         │
    ┌────▼─────────────────────────────────────────────────┐
    │ 8 IR SENSOR ARRAY                                     │
    │ VCC──────►5V (from Arduino)                           │
    │ GND──────►GND (common)                                │
    │ S1───────►A0                                          │
    │ S2───────►A1                                          │
    │ S3───────►A2                                          │
    │ S4───────►A3                                          │
    │ S5───────►A4                                          │
    │ S6───────►A5                                          │
    │ S7───────►A6                                          │
    │ S8───────►A7                                          │
    └───────────────────────────────────────────────────────┘
```

##  **Power Distribution Summary**

```
                    ┌─────────────────┐
                    │  7.4V Battery   │
                    │  (2x 3.7V series)│
                    └────────┬────────┘
                             │
            ┌────────────────┼────────────────┐
            │                │                │
            ▼                ▼                ▼
    ┌───────────────┐ ┌──────────────┐ ┌──────────────┐
    │ Arduino VIN   │ │ TB6612 VM    │ │ Common GND   │
    │ (7.4V input)  │ │ (Motor Power)│ │ (All GNDs)   │
    └───────┬───────┘ └──────────────┘ └──────┬───────┘
            │                                  │
            ▼ (5V regulated)                   │
    ┌───────────────┐                          │
    │ Arduino 5V    ├──────────────────────────┘
    │ Output        │
    └───────┬───────┘
            │
    ┌───────┴───────┐
    ▼               ▼
┌─────────┐   ┌─────────┐
│TB6612   │   │ 8 IR    │
│VCC (5V) │   │Sensors  │
└─────────┘   │VCC (5V) │
              └─────────┘
```

##  **Protection Components (Optional but Recommended)**

```
Add these for safety and stability:

1. Capacitors across battery terminals (near driver):
   ┌────[100μF]────┐
   │               │
   [+] Batt      [-]
   │               │
   └────[0.1μF]────┘

2. Fuse (2A-3A) on battery positive:
   Battery (+) ────[Fuse]────► Circuit

3. Power switch:
   Battery (+) ────[Switch]────► Circuit
```

##  **Quick Reference Table**

| Component | Power Source | Signal Pins | GND |
|-----------|-------------|-------------|-----|
| Arduino Uno | VIN (7.4V) | - | Battery GND |
| TB6612FNG (VM) | Battery 7.4V | - | Battery GND |
| TB6612FNG (VCC) | Arduino 5V | PWM 5,6,7,8,9,10,11 | Arduino GND |
| IR Sensors | Arduino 5V | A0-A7 | Arduino GND |
| Motor A | TB6612 AO1/AO2 | - | - |
| Motor B | TB6612 BO1/BO2 | - | - |

##  **Final Connection Checklist**

- [ ] 3.7V batteries series la connect aachaa? (Check voltage: 7.4V-8.4V)
- [ ] Battery (+) to Arduino VIN connect aachaa?
- [ ] Battery (+) to TB6612 VM connect aachaa?
- [ ] Battery GND to Arduino GND connect aachaa?
- [ ] Battery GND to TB6612 GND connect aachaa?
- [ ] Arduino 5V to TB6612 VCC connect aachaa?
- [ ] Arduino 5V to IR Sensors VCC connect aachaa?
- [ ] All control signals properly connected?
- [ ] Motors to TB6612 outputs connect aachaa?
- [ ] Double-check for shorts before power on?

##  **Power-On Sequence**

1. Double-check all connections
2. Measure battery voltage (should be 7.4V-8.4V)
3. Connect battery
4. Check Arduino power LED (ON)
5. Check TB6612 (should be warm, not hot)
6. Upload code and test
