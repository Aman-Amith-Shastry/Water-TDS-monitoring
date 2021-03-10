# Water-TDS-monitoring
Check the TDS value of water WITHOUT any TDS meter

Circuit:

Arduino

Connect 5V of Arduino to one power rail of the breadboard
Connect the ground of Arduino to the other power rail of the breadboard
Connect one end of a 1k-ohm resistor to ground, and the other end to the breadboard. Connect the analog pin A0 on the Arduino to the resistor. Finally, connect a wire to the resistor and another wire to 5V. Connect the free ends of these wires to the crocodile clips.


LCD Display

Connect VSS pin to the ground rail
Connect VDD pin to 5V rail
Connect V0 to the center pin of the potentiometer
Connect ends of the potentiometer to 5V and ground
Connect RS pin to Arduino pin 7
Connect R/W pin to Arduino pin 8
Connect D4 to Arduino pin 10
Connect D5 to Arduino pin 11
Connect D6 to Arduino pin 12
Connect D7 to Arduino pin 13


HC-05 Bluetooth module

Connect VCC pin to 5V rail
Connect GND pin to ground
Connect TX pin to Arduino pin 3 (Serves as RX)
Connect RX pin to Arduino pin 2 (Serves as TX)


RGB LED

Connect the common cathode (longest pin) to ground
Connect the red pin (right of cathode pin) to PWM pin 9 on Arduino through a 330-ohm resistor
Connect green pin (left of cathode pin) to PWM pin 6 on Arduino through a 330-ohm resistor
Connect blue pin (extreme left) to PWM pin 5 on Arduino through a 330-ohm resistor
