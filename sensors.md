# Sensors

## Dust Sensor

The first model used the [Sharp GP2Y1010AU0F](https://www.sparkfun.com/products/9689), which has an undefined particle
size. We may want to switch to the [DFRobot PM 2.5 Sensor Module - Laser Sensing](http://www.dfrobot.com/index.php?route=product/product&product_id=1272#.V3vcGfkrJ_M).

### Sharp IR Dust Sensor

* **Max Current:** `20mA`
* **Typical Current:** `11mA`

The Sharp Dust Sensor datasheet and other related documents do not specify a particle size range. It appears this
sensor simply gathers information on general dust in the air, however [hobbiest testing](http://lantaukwcounter.blogspot.com/2016/01/shinyei-and-sharp-dust-sensors-looking.html)
has indicated the device favors smaller particles. The sensor also has a multitude of low-end accuracy problems. IR
bleed from external light sources can interfere with the sensor's accuracy. Even in a textbook environment, however,
internal reflection of the IR diode causes a minimum false positive at the low end (`0.5 volts`).

### DFRobot Laser Dust Sensor

* **Voltage:** `4.95v ~ 5.05v`
* **Max Current:** `120mA`
* **Typical Current:** `unk`
* **Standby current:** `≤200 uA`

The DFRobot PM 2.5 Sensor Module (Laser Sensing) is uses light scattering to gather specific information on dust
particles and aerosols in the atmosphere. According to the [product wiki](http://www.dfrobot.com/wiki/index.php?title=PM2.5_laser_dust_sensor_SKU:SEN0177),
which seems to serve as the sensor's datasheet, it will provide specific data on the density and number of particles.

Further tests are needed to determine the accuracy of this sensor.

**Pros:**
* Outputs specific data on all of the relevant PM ranges (including `PM 1`, `PM 2.5` and ` PM 10`)
* Apparently outputs actual partical counts

**Cons:**
* Can't find datasheet
* Sensor outputs I2C only
* Built in fan (higher power consumption)
