# Operating-Systems-in-Automation-Project

I had to create an application that reads temperature using a thermistor every 200 ms and converts the read value. A PWM(Pulse Width Modulation)a duty cycle directly proportional to the temperature value read.
When a button is pressed, the task that reads the temperature no longer sends commands to the task that modifies the PWM signal's duty cycle, and when the button is pressed again, it returns to normal operation.

Hardware components: STM32F4 microcontroller, 10kΩ NTC thermistor, pull-up resistor, 10kΩ potentiometer, one LED, diodes, and resistors.

Temperature Measurement (Automatic Mode)
Every X milliseconds (e.g., 200ms), a FreeRTOS task reads the voltage from the thermistor via ADC.
The voltage is converted into temperature (using the NTC formula).
The temperature is then converted into a duty cycle for the PWM.
The PWM controls an LED connected to an output pin (e.g., TIM3_CH1).

Switching Between Modes (Button B1)
At every button press (with software debounce implemented), the application:
Switches between automatic mode ↔ manual mode.
For this, the variable buttonPressed is toggled with each press.

Return to Automatic Mode
If the button is pressed again, the application:
Toggles buttonPressed back to 0.
PWM control based on temperature (ADC_CHANNEL_4) resumes.
