# Sensors

## Gas Sensors

### MICS-6814

A tiny, all-in-one gas sensor with a comprehensive [datasheet](datasheets/MICS-6814.pdf).

**Gasses:**

* Carbon monoxide (CO) `1 – 1000ppm`
* Nitrogen dioxide (NO2) `0.05 – 10ppm`
* Ethanol (C2H5OH) `10 – 500ppm`
* Hydrogen (H2) `1 – 1000ppm`
* Ammonia (NH3) `1 – 500ppm`
* Methane (CH4) `>1000ppm`
* Propane (C3H8) `>1000ppm`
* Iso-butane (C4H10) `>1000ppm`

## Ozone Sensors



## Dust Sensors

Relatively accurate laser scattering sensors can be aquired from Chinese distributors. These sensors require an active
air flow to achieve accurate results. Most provide integrated fans to this end, which increases the power demands of
the sensor.

*Note: Hacky Chinese tests can be found [here](http://aqicn.org/sensor/).*

### Sharp IR Dust Sensor

* **Max Current:** `20mA`
* **Typical Current:** `11mA`

The Sharp Dust Sensor datasheet and other related documents do not specify a particle size range. It appears this
sensor simply gathers information on general dust in the air, however [hobbiest testing](http://lantaukwcounter.blogspot.com/2016/01/shinyei-and-sharp-dust-sensors-looking.html)
has indicated the device favors smaller particles. The sensor also has a multitude of low-end accuracy problems. IR
bleed from external light sources can interfere with the sensor's accuracy. Even in a textbook environment, however,
internal reflection of the IR diode causes a minimum false positive at the low end (`0.5 volts`).

### Planetower Laser Dust Sensor (PMS 7003/5003/3003)

The Planetower PMS line of dust sensors use laser scattering to determine the count and density of dust particles in
the `PM 1`, `PM 2.5` and `PM 10` ranges. Each generation improves the casing and airflow, providing longer running life
cycles and more accurate data.

**Sources:**

* [PMS 7003 - $35.90](http://www.aliexpress.com/item/PLANTOWER-Laser-PM2-5-DUST-SENSOR-PMS7003-High-precision-laser-dust-concentration-sensor-digital-dust-particles/32623909733.html?spm=2114.01010208.3.1.L8QtfN&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=7def28c6-a9dd-4f3b-852e-4e0491205495)
* [PMS 5003 - $24.30](http://www.aliexpress.com/item/PM2-5-Air-particle-dust-sensor-laser-inside-digital-output-module-air-purifier-G5-High-precision/32576299965.html?spm=2114.01010208.3.2.3SFZxT&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=39e3a412-0d84-40a2-a3ad-498c07533f51)
* [PMS 3003 - $36.60](http://www.aliexpress.com/item/Laser-PM2-5-DUST-SENSOR-PMS3003-High-precision-laser-dust-concentration-sensor-digital-dust-particles-G3/32371229255.html?spm=2114.01010208.3.2.yF9PwL&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=480df32f-d3d3-439b-a506-705104ec2900)

The most recent "datasheet" available is for the [PMS 5003](https://github.com/scintilla-aircheck/AQmon/blob/master/Documents/PMS5003_LOGOELE.pdf),
originally provided on GitHub by a developer who posted the docs for each sensor he was using. He also provided a
pinout and corresponding documents for the PMS 3003.

The U.S. market DFRobot laser sensor is actually a PMS 1003 sensor.

**Pros:**
* Outputs specific data on all of the relevant PM ranges (including `PM 1`, `PM 2.5` and ` PM 10`)
* Apparently outputs actual partical counts

**Cons:**
* Can't find datasheet
* Sensor outputs I2C only
* Built in fan (higher power consumption)

### Inovafit Laser Dust Sensor (SDS 021/018/011)

The Inovafit line of dust sensors use laser scattering to determine the count and density of dust particles in the
`PM 2.5` and `PM 10` range. The Inovafit sensors opted to trade size for accuracy, resulting in a larger sensor that
provides more reliable data. No data is available for the most recent model (`SDS 021`), however the updated housing
is intended to extend the operating life of the sensor. Various sources (storefronts, etc.) place the service life at
`8,000 hrs`, which can be extended by putting the sensor to sleep for large periods of time, given a `30 s` spin-up
before a reading is made.

**Sources:**

* [SDS 021 - $33.00](http://www.aliexpress.com/item/NOVA-PM2-5-Air-particle-dust-sensor-SDS021-laser-inside-digital-output-SDS021-Laser-PM2-5/32638192686.html?spm=2114.01010208.3.2.5WLRNu&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=c4ec533a-68d6-42cc-abdc-142fff967eff)
* [SDS 018 - $32.00](http://www.aliexpress.com/item/PM2-5-Air-particle-dust-sensor-SDS018-laser-inside-digital-output-SAMPLE/32669257200.html?spm=2114.01010208.3.2.PMVmDH&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=ef18e8bc-5287-49f3-be6e-777f9e727015)
* [SDS 011 - $24.80](http://www.aliexpress.com/item/Nova-PM-sensor-SDS011-High-precision-laser-pm2-5-air-quality-detection-sensor-module-Super-dust/32606349048.html?spm=2114.01010208.3.2.kOp9l1&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=3df6cf05-6547-4532-befc-906caf4e6bbc)

The SDS011 laser dust sensor is similar to the PMS X003 model, however it is designed to provide more accurate readings
through a larger form factor. The sensor provides data for `PM 2.5` and `PM 10` sized particles.

Datasheets exist for [v.1.0](http://inovafitness.com/upload/file/20150311/14261262164716.pdf) and
[v.1.3](http://inovafitness.com/software/SDS011%20laser%20PM2.5%20sensor%20specification-V1.3.pdf) of the sensor.
