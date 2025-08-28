## 1.Title, Student Name, Date

| Student Name | Title | Date |
| --- | --- | --- |
| Irankunda Ezechiel | Home Security System Challenge | 28/08/2025 |

## 2. Introduction

**Short Description:**  
This project simulates a Home Security System using Arduino UNO and multiple sensors/actuators. The system is designed to secure entry points and weak spots in a home and provide safety features such as smoke and fire detection.

**The Problem Being Solved:**  
Traditional home security systems can be expensive or lack features like environmental monitoring (smoke/fire/gas). This project addresses the need for an affordable, multi-sensor security system with both intrusion and environmental hazard detection that can be remotely monitored and operated.

**Importance:**  
Home and property safety is crucial. Integrating detection for fire, gas leaks, and unauthorized entry increases safety and reduces risks of property loss, injury, or fatality. The project demonstrates how microcontroller-driven systems can democratize access to affordable, customizable home security.

---

## 3. Objectives

**Main Goal:**  
To design, build, and simulate a cost-effective, remotely monitored home security system using an Arduino microcontroller.

**Specific Objectives:**
1. Detect smoke, gas, or fire and alert residents.
2. Detect unauthorized entry or motion in restricted zones.
3. Provide real-time feedback via LCD and remote control panel.
4. Activate alarms (LED, buzzer) and take action (e.g., trigger sprinkler) when hazards are detected.
5. Build a system that can be upgraded with more features (e.g., mobile notifications).

---

## 4. System Design

**Block Diagram:**  
![System Diagram](https://github.com/eiranstudio/Challeng-Home-Security-System/blob/master/Challenge%20Home%20Security%20System.png)

**Hardware Components:**
- Arduino UNO (microcontroller)
- Gas sensor (for smoke/gas detection)
- Temperature sensor (for fire detection)
- PIR Motion sensor (for movement detection)
- Ultrasonic sensor (for proximity/intrusion detection)
- LED (visual alert)
- Piezo buzzer (audible alarm)
- LCD display (real-time status)
- Servo motor (to trigger sprinklers)
- Power supply

**Software Tools Used:**
- Arduino IDE (for code development and upload)
- Adafruit_LiquidCrystal library (LCD control)
- Servo library (servo control)
- Tinkercad (simulation and circuit design)

---

## 5. Implementation

**How the System Was Built:**  
Sensors and actuators are connected to the Arduino UNO according to the block diagram. The code initializes all components, continuously reads sensor values, and executes actions (e.g., alarm, sprinkler) when thresholds are exceeded.

**Circuit Diagram / Wiring Image:**  
See [System Diagram](https://github.com/eiranstudio/Challeng-Home-Security-System/blob/master/Challenge%20Home%20Security%20System.png)

**Key Code Snippet:**
```cpp
void setup() {  
  lcd_1.begin(16, 2);
  pinMode(led, OUTPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(trigger, OUTPUT); // Ultrasonic
  pinMode(echo, INPUT);
  pinMode(pir, INPUT);      // PIR
  pinMode(gas, INPUT);      // Gas
  pinMode(temp, INPUT);     // Temp
  servo.attach(motor);
  servo.write(0);
  Serial.begin(9600);
  lcd_1.clear();
}

// Main loop: Read sensors, trigger alarms
void loop() {
  int gasSensorValue = analogRead(A0); 
  float tempSensorValue = analogRead(temp);
  float temperature = ((tempSensorValue/1023)*5000 - 500)/10; // degC
  float pirSensorValue = analogRead(pir);

  if(gasSensorValue >= 150 && temperature < 75) {
    alert(); // Sound buzzer
    lcd_1.print("Smoke Detected!!");
  }
  if(temperature >= 90 && gasSensorValue >= 150) {
    alert_led();
    lcd_1.print("Fire Alert!!");
    lcd_1.print("Starting sprayer");
    // Servo activates sprinkler
  }
  if(pirSensorValue > 0) {
    alert_led();
    lcd_1.print("Motion Detected!!");
  }
}
```

**Pictures of Prototype:**  
As this is a simulation-based project, a functional prototype image is available in the repo:  
![Prototype](https://github.com/eiranstudio/Challeng-Home-Security-System/blob/master/Screenshotofworkingsystem.png)

---

## 6. Results

**System Behavior When Tested:**  
- When smoke or gas is detected, the buzzer sounds and the LCD displays an alert.
- High temperature triggers a fire alert and, if combined with smoke, activates the servo to trigger a sprinkler.
- Motion/proximity detection triggers alarms for possible intrusion.
- All events are displayed on the LCD and can be monitored remotely (in simulation).

**Screenshots of the Working System:**  
See the image above

---

## 7. Conclusion

**Summary of Achievements:**  
- Integrated multiple sensors for comprehensive home safety.
- Achieved real-time detection and alerting of fire, gas, and intrusion risks.
- Successfully simulated remote monitoring and control via a central control panel.

**Real-Life Need and Applicability:**  
This system addresses real-world needs for affordable, flexible home security and can be further customized for different environments.

**Limitations:**  
- Lacks direct internet/mobile notification (currently simulated only).
- No data logging; system resets after each event.
- Limited to the sensors and actuators physically connected.

---

## 8. Future Work

- Develop a mobile app for real-time incident logging and notifications.
- Add time/date module for time-stamped events and scheduling.
- Integrate cloud connectivity for remote alerts and data logging.
- Expand sensor suite (e.g., window break sensor, camera).
- Improve power management for real-world deployment.