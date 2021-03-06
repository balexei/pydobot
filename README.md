[![CircleCI](https://circleci.com/gh/luismesas/pydobot.svg?style=svg)](https://circleci.com/gh/luismesas/pydobot)

Python library for Dobot Magician
===

Based on Communication Protocol V1.1.4 (_latest version [here](https://www.dobot.cc/downloadcenter.html?sub_cat=72#sub-download)_)


Installation
---

```
pip install pydobot
```

Example
---

```python
from serial.tools import list_ports

from pydobot import Dobot

port = list_ports.comports()[0].device
device = Dobot(port=port, verbose=True)

(x, y, z, r, j1, j2, j3, j4) = device.pose()
print(f'x:{x} y:{y} z:{z} j1:{j1} j2:{j2} j3:{j3} j4:{j4}')

device.move_to(x + 20, y, z, r, wait=False)
device.move_to(x, y, z, r, wait=True)  # we wait until this movement is done before continuing

device.close()
```

Methods
---

* **Dobot(port, verbose=False)** Creates an instance of dobot connected to given serial port.
    * **port**: _string_ with name of serial port to connect
    * **verbose**: _bool_ will print to console all serial comms
  
* **.pose()** Returns the current pose of dobot, as a tuple (x, y, z, r, j1, j2, j3, j4)
    * **x**: _float_ current x cartesian coordinate 
    * **y**: _float_ current y cartesian coordinate
    * **z**: _float_ current z cartesian coordinate
    * **r**: _float_ current effector rotation 
    * **j1**: _float_ current joint 1 angle 
    * **j2**: _float_ current joint 2 angle 
    * **j3**: _float_ current joint 3 angle 
    * **j4**: _float_ current joint 4 angle 
* **.move_to(x, y, z, r, wait=False)** queues a translation in dobot to given coordinates
    * **x**: _float_ x cartesian coordinate to move 
    * **y**: _float_ y cartesian coordinate to move 
    * **z**: _float_ z cartesian coordinate to move 
    * **r**: _float_ r effector rotation 
    * **wait**: _bool_ waits until command has been executed to return to process
* **.speed(velocity, acceleration)** changes velocity and acceleration at which the dobot moves to future coordinates
    * **velocity**: _float_ desired translation velocity 
    * **acceleration**: _float_ desired translation acceleration 
* **.suck(enable)**
    * **enable**: _bool_ enables/disables suction
* **.grip(enable)**
    * **enable**: _bool_ enables/disables gripper
* **.wait(ms)**
    * **ms**: _integer_ milliseconds to wait before the next command
    * **wait**: _bool_ waits until command has been executed to return to process
* **.start_stepper(pps, motor=0, wait=False)**
    * **pps**: _integer_ pulses per second sent to e-motor (0 or 1)
    * **motor**: _integer_ position of the e-motor
    * **wait**: _bool_ waits until command has been executed to return to process
* **.stop_stepper(motor=0, wait=False)**
    * **motor**: _integer_ position of the e-motor (0 or 1)
    * **wait**: _bool_ waits until command has been executed to return to process
* **.start_conveyor(speed, motor=0, wait=False)**
    * **speed**: _float_ speed in m/s
    * **motor**: _integer_ position of the conveyor belt (0 or 1)
    * **wait**: _bool_ waits until command has been executed to return to process
* **.set_io_mode(address, mode, wait=False)**
    * **address**: _integer_ EIO port number
    * **mode**: _str_ I/O mode (Dummy, PWM, DO, DI, ADC)
    * **wait**: _bool_ waits until command has been executed to return to process
* **.set_pwm_output(address, frequency, duty_cycle, wait=False)**
    * **address**: _integer_ EIO port number
    * **frequency**: _float_ pulse frequency
    * **duty_cycle**: _float_ pulse duty cycle (0 to 100)
    * **wait**: _bool_ waits until command has been executed to return to process
