═══════════════════════════════════════════════════════
         MATE FLOAT — README / OPERATION GUIDE
═══════════════════════════════════════════════════════

HARDWARE REQUIRED
─────────────────
- Arduino Uno
- Blue Robotics Basic ESC
- Blue Robotics T200 Thruster
- Adafruit MPL3115A2 Pressure Sensor
- HM-10 Bluetooth Module
- 12V NiMH or AGM Battery
- Blade fuse (correct size for your battery)

WIRING
──────
ESC
  White signal wire  →  Arduino Pin 9
  Black ground wire  →  Arduino GND
  Red VCC wire       →  Arduino VIN

HM-10 BLUETOOTH
  VCC  →  Arduino 3.3V
  GND  →  Arduino GND
  TX   →  Arduino Pin 10
  RX   →  Arduino Pin 11

MPL3115A2 PRESSURE SENSOR
  VIN  →  Arduino 5V
  GND  →  Arduino GND
  SDA  →  Arduino A4
  SCL  →  Arduino A5

BEFORE YOU UPLOAD
─────────────────
1. Change COMPANY = "EX01" to your MATE company number
2. Disconnect HM-10 pins 10 and 11 before uploading
3. Select Tools → Board → Arduino Uno
4. Select correct COM port under Tools → Port
5. Click Upload
6. Reconnect HM-10 pins 10 and 11 after upload

TIMING TO TUNE IN POOL
───────────────────────
STARTUP_DELAY = 60000   — time from power on to first descent (ms)
DESCEND_TIME  = 15000   — increase if float does not reach 2.5m
ASCEND_TIME   = 45000   — increase if float does not reach 40cm
HOLD_TIME     = 30000   — do not change — competition requirement

HOW IT WORKS
────────────
Power on
  └→ ESC arms (3 seconds)
  └→ Pre-dive data packet sent
  └→ Waits 60 seconds (deploy float here)
  └→ PROFILE 1 begins
       └→ Descends 15 seconds
       └→ Holds at 2.5m for 30 seconds (motor off)
       └→ Ascends full power for 45 seconds
       └→ Holds at 40cm for 30 seconds (motor off)
  └→ PROFILE 2 begins
       └→ Descends 15 seconds
       └→ Holds at 2.5m for 30 seconds (motor off)
       └→ Ascends full power for 45 seconds
       └→ Holds at 40cm for 30 seconds (motor off)
  └→ Motor stops
  └→ Full dive log transmits over Bluetooth

RECEIVING DATA ON YOUR PC
──────────────────────────
1. Go to Windows Bluetooth settings
2. Pair with HMSoft (PIN 1234 if asked)
3. Open Device Manager → Ports (COM & LPT)
4. Note the COM port number for HMSoft
5. Download PuTTY from putty.org (free)
6. Open PuTTY → Serial → enter COM port → Speed 9600
7. Click Open
8. After float surfaces data streams in automatically

DATA FORMAT
───────────
Each packet looks like this:
EX01 12345ms 101325.0Pa 2.50m 23.4C HOLD_2.5M

Columns in full log:
Company, Time(ms), Phase, Temp(C), Pressure(Pa), Depth(m), Alt(m)

TROUBLESHOOTING
───────────────
ESC gives 2 beeps     →  Disconnect HM-10 pins 10/11, reset Arduino
Motor does not spin   →  Check fuse, check battery charge
Nothing powers on     →  Check VCC wire is in VIN not 5V pin
HM-10 not found       →  Check 3.3V connection, look for blinking LED
MPL3115A2 ERROR       →  Check SDA→A4 and SCL→A5 connections
Upload fails          →  Disconnect pins 10 and 11 before uploading

═══════════════════════════════════════════════════════

