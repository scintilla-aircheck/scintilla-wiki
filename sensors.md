# Sensors

## Dust Sensor

The first model used the [Sharp GP2Y1010AU0F](https://www.sparkfun.com/products/9689), which has an undefined particle
size. We may want to switch to the [DFRobot PM 2.5 Sensor Module - Laser Sensing](http://www.dfrobot.com/index.php?route=product/product&product_id=1272#.V3vcGfkrJ_M).

### Sharp IR Dust Sensor

* **Max Current:** `20mA`
* **Typical Current:** `11mA`

The Sharp sensor has no specific particle size, however hobbiest testing has indicated the device favors smaller
particles towards the `PM 2.5` range. The sensor also has a multitude of low-end accuracy problems. IR bleed from
external light sources can reduce accuracy. Even in a textbook environment, internal reflection of the IR diode
causes a minimum false positive at the low end (`0.5 volts`).

### DFRobot Laser Dust Sensor

* **Voltage:** `4.95v ~ 5.05v`
* **Max Current:** `120mA`
* **Typical Current:** `unk`
* **Standby current:** `≤200 uA`

Th DFRobot dust sensor outputs specific data on all of the relevant PM ranges (including `PM 1`, `PM 2.5` and ` PM 10`).

The DFRobot laser sensor doesn't have a datasheet. According to comments the minimum accuracy is 0.3 micrometers.
One possible downside to the DFRobot sensor is that it outputs I2C.
