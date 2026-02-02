### Rodrigo's comments
We want the stepper motor (NEMA 23 stepper motor: 23HS22-1504S) to be able to turn 180 degrees and back again to the starting point. 

The motor needs a power supply of **12V**. The Arduino can be powered by **5V**.

> [!NOTE] Goal
> Build the physical circuit and transfer the code that enables the motor to turn


### Parts we have
- [ ] Arduino UNO
- [ ] NEMA 23 stepper motor: 23HS22-1504S stepper motor
- [ ] External power supply
- [ ] Stepper driver (DRV8825)

![[img/Skærmbillede 2025-11-20 kl. 11.37.53.png]]

## How to get a (single) stepper motor to move 
```c
/*
* Simple demo, should work with any driver board
*
* Connect STEP, DIR as indicated
*
* Copyright (C)2015-2017 Laurentiu Badea
*
* This file may be redistributed under the terms of the MIT license.
* A copy of this license has been included with this distribution in the file LICENSE.
*/

#include <Arduino.h>
#include "BasicStepperDriver.h"

// Motor steps per revolution. Most steppers are 200 steps or 1.8 degrees/step

#define MOTOR_STEPS 200
#define RPM 120 // lower number makes it slower

// Since microstepping is set externally, make sure this matches the selected mode
// If it doesn't, the motor will move at a different RPM than chosen
// 1=full step, 2=half step etc.

#define MICROSTEPS 1

// All the wires needed for full functionality
#define DIR 8
#define STEP 9

//Uncomment line to use enable/disable functionality
//#define SLEEP 13

// 2-wire basic config, microstepping is hardwired on the driver

BasicStepperDriver stepper(MOTOR_STEPS, DIR, STEP);

//Uncomment line to use enable/disable functionality
//BasicStepperDriver stepper(MOTOR_STEPS, DIR, STEP, SLEEP);

void setup() {
	stepper.begin(RPM, MICROSTEPS);
	// if using enable/disable on ENABLE pin (active LOW) instead of SLEEP uncomment next line
	// stepper.setEnableActiveState(LOW);
} 

void loop() {
	// energize coils - the motor will hold position
	// stepper.enable();
	/*
	* Moving motor one full revolution using the degree notation
	*/
	
	stepper.rotate(90);

	/*
	* Moving motor to original position using steps
	*/
	// stepper.move(-MOTOR_STEPS*MICROSTEPS);
	// pause and allow the motor to be moved by hand
	// stepper.disable();
	delay(1000);
	stepper.rotate(-90);
	delay(1000);
}
```
In this program `stepper` holds space for one motor driver.

![[Skærmbillede 2025-12-04 kl. 11.41.46.png]]

### Notes from Rodrigo
- Remember to do survey
- Remember to study exam questions. because they might include topics that are not part of our final project. 