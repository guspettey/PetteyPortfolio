---
layout: post
title:  "Paper Development Process: Part Three"
date:   2022-03-17 17:23:00 +0000
tags: [PaperDevelopment, PhD, ProblemSolving]
---

# Paper Development Part Three
## A short intermission
A lot of time has passed since my last update to this series...
Returning to lab-work, competing objectives, other projects meant this site did not get used as often as first intended, but there's still time to turn that around.
As of writing this, I have a fully realised particle virtualization process, which is beginning to show some great outputs.
However, I think its worth finishing what I started so picking up where I left off...

## Develop a reliable motor and camera control application
As a reminder, I need a way to take images around the circumference of an object on the end of a M5 bolt at specified angles.
This task is then split up into subtasks:
- Turning the motor through a specified number of steps.
- Pulling an image from a Gigabit Ethernet (GigE) connected camera.

Luckily, controlling a stepper motor over serial connection is simple enough, although as it turned out controlling a GigE camera was sufficiently hard that I'll include that process elsewhere as its own standalone guide. 
It enforced the use of the [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/about), which works nicely in the laboratory workflows currently being used.

So to run the motor precisely through each stop on its full revolution, some initial calculations are needed.
The stepper motor is set up with a 1:125 ratio gearbox and can be run in half, quarter, eighth, sixteenth or thirty-two-th(?) step configuration. 
This information is needed to calculate the number of steps the motor needs to drive to pass one full revolution.
Helpfully, the Nanotec motor being used has a handy piece of software to program the settings, and after consideration of the gearbox its found that 2560000 steps are required for one full revolution. 
The programming manual for the Nanotec motors allows the following code to be written in python.

```python
import serial

# create a function to communicate over Serial

def query(serialPort,string):
	command="#1"+string+"\r"
	ser.write(bytes(command, 'utf-8'))
	stri = ser.read_until(b"\r")
	print(stri)
	return stri

ser = serial.Serial('/dev/ttyS4',baudrate=115200,
	bytesize=serial.EIGHTBITS,
	parity=serial.PARITY_NONE,
	stopbits=serial.STOPBITS_ONE,
	timeout=20)

# create n number of stops per revolution
n=8

# on the serial connection:
print('opening serial connection')
query(ser,"J1") # open connection
query(ser,"s+"+str(int(2560000/n))) # step by total steps per rev/n
query(ser,"o+32000") # set speed


for step in range(n):
	print('stop %d of %s' % (step+1,n))
	query(ser,"p1")
	query(ser,"A")
	ser.read_until(b"\r")

	# Operations to take place each stop

```

Here, the motor is detected on the ttyS4 serial port and the `query` helper function writes commands to the port in a more *'pythonic'* manner.
The motor is told to move through $2560000/n$ steps for each 'drive' command received - in other words, the angle to move each stop - and the speed is set.
The `for` loop then drives the motor through each angle, and any operations can take place at that point, in my case triggering the GigE camera. 
[The full script is available on github.](https://github.com/Gustafferson/particleVirtualization/blob/191a32c2c132606b3b3b8718c2959e94a86630ce/main.py)

So that's one item ticked off the list pretty easily.
Thankfully being able to work with python and the WSL came in handy here, avoiding the use of systems like Labview which seem (to my mind) overcomplicate things.

Next time I'll take a look at my method to reconstruct the 3D objects from just a series of 2D images.

## Review
- [x] Develop an apparatus allowing for computer imaging different angles of a particle
- [x] Develop a reliable motor and camera control application
- [ ] Develop a framework to stitch together a 3D virtual particle from 2D images of different angles
- [ ] Extend the capabilities of 2D shape analyses to work on our 3D virtual particle
- [ ] Use the 3D virtual grain in a virtual particle shear experiment
