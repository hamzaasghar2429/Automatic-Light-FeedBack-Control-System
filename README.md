# Automatic-Light-FeedBack-Control-System
An Automatic Light Feedback Control System follows the exact same closed-loop principles as the humidity system, but it reacts much faster and uses different hardware.

Instead of turning a fan on and off, this system monitors ambient light and adjusts an artificial light source to maintain a perfectly consistent illumination level in a room, regardless of whether the sun goes behind a cloud or the blinds are closed.

Here is how the control theory maps to the physical hardware you might hook up to an ESP8266 or NodeMCU:

The Core Components
The Plant (The Environment): The space you are illuminating, like a desk, a smart home living room, or an automated greenhouse.

The Sensor (The Feedback Loop): A light sensor like an LDR (Light Dependent Resistor) or a more precise digital I2C sensor like a BH1750. This continuously measures the ambient lux levels, giving you your Process Variable (PV).

The Controller (The Brain): Your microcontroller storing the desired lux level—your Set Point (SP).

The Error Detector: The logic calculating the difference: Error = Set Point - Process Variable.

The Actuator (The Muscle): The artificial light source. In a modern setup, this is usually a high-power LED array connected to the microcontroller via a MOSFET.

How the Logic Works
Light systems usually employ a much smoother control strategy than basic on/off systems:

Bang-Bang (Streetlight Logic): The simplest form. If it gets dark (drops below Set Point), a relay clicks the lights fully on. If the sun comes up, the relay clicks them fully off. It is cheap and easy, but terrible for indoor lighting.

Proportional Control (PWM Dimming): This is where it gets interesting. Instead of a relay, the controller uses Pulse Width Modulation (PWM) to rapidly pulse the power to an LED. If a cloud passes over and the room dims slightly (a small Error), the controller slightly increases the PWM duty cycle, gently brightening the LED to compensate. If the sun shines brightly through the window, it dims the LED down to save power.
