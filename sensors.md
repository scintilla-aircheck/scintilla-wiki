# Sensors

*Note: Up-to-date data on sensors and sourcing is available on the [Google spreadsheet](https://docs.google.com/spreadsheets/d/1Mnqxya5YkDIkScoZPxakQ6ZnZfguzx2Y-9sy020iXRE/edit?usp=sharing).*

**Current sensor loadout:**

* Temperature - TH02
* Humidity - DHT22
* Carbon Monoxide [CO] - [MiCS-6814](#MiCS-6814)
* Ammonia [NH3] - ...
* Methane [CH4] - ...
* Propane [C3H8] - ...
* Iso-Butane [C4H10] - ...
* Nitrogen Dioxide [NO2] - ...
* Ozone [O3] - [MiCS-2614](#MiCS-2614)
* Sulfur Dioxide [SO2] - [3SP_SO2_20 C Package 110-602](#3SP_SO2_20 C Package 110-602)
* Dust/Aerosol [PM 2.5/10] - [SDS021](#Inovafit Laser Dust Sensor (SDS 021/018/011))
* Lead (?)

### Design Considerations

* According to SPEC documentation, "When dealing with very reactive gases, such as H2S, NO2, SO2 and O3, material selection is important. Care must be used in selecting all materials, including but not limited to enclosures, tubing, manifolds, pumps and valves." This is likely why the MiCS FAQ called for a Teflon filter.

----

## Gas Sensors

**Principal design considerations:**

* Limit air flow - FAQ reccomends Teflon filter to mitigate error caused by air cooling the sensors
* Limit dust exposure - Nonspecific dust filter reqiurements (implies major dust? > PM 10)

### MiCS-6814

A tiny, all-in-one gas sensor with a comprehensive [datasheet](documents/MiCS-6814.pdf).

**Gasses:**

* Carbon monoxide (CO) `1 – 1000ppm`
* Nitrogen dioxide (NO2) `0.05 – 10ppm`
* Ethanol (C2H5OH) `10 – 500ppm`
* Hydrogen (H2) `1 – 1000ppm`
* Ammonia (NH3) `1 – 500ppm`
* Methane (CH4) `>1000ppm`
* Propane (C3H8) `>1000ppm`
* Iso-butane (C4H10) `>1000ppm`

**Documents:**
* Datasheet: [MiCS-6814.pdf](documents/MiCS-6814.pdf)

### MiCS-2614

A tiny ozone gas detector with a comprehensive [datasheet](documents/MiCS-2614.pdf)

**Gasses:**

*  Ozone (O3) `10 – 1000ppb`

**Documents:**
* Datasheet: [MiCS-2614.pdf](documents/MiCS-2614.pdf)

### 3SP_SO2_20 C Package 110-602

A tiny sulfir dioxide sensor with a c comprehensive [datasheet](documents/3SP_SO2_20-C-Package-110-602.pdf).

**Gasses:**

* Sulfur Dioxide (SO2) - `0 - 22ppm`

**Documents:**
* Datasheet: [3SP_SO2_20-C-Package-110-602.pdf](documents/3SP_SO2_20-C-Package-110-602.pdf)

----

## Dust Sensors

Relatively accurate laser scattering sensors can be aquired from Chinese distributors. These sensors require an active
air flow to achieve accurate results. Most provide integrated fans to this end, which increases the power demands of
the sensor.

**Principal design considerations:**

* Must provide major dust filter on housing (> PM 10)
* Active air flow dust sensors can be used to pull air through entire housing
* Some sensors are sensitive to vibration and orientation

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

**Documents:**
* Faux Datasheet: [PMS5003_LOGOELE.pdf](documents/PMS5003_LOGOELE.pdf)

### Inovafit Laser Dust Sensor (SDS 021/018/011)

The Inovafit line of dust sensors use laser scattering to determine the count and density of dust particles in the
`PM 2.5` and `PM 10` range. The Inovafit sensors opted to trade size for accuracy, resulting in a larger sensor that
provides more reliable data. No data is available for the most recent model (`SDS 021`), however the updated housing
is intended to extend the operating life of the sensor. Various sources (storefronts, etc.) place the service life at
`8,000 hrs` (~1 year), which can be extended by putting the sensor to sleep for large periods of time, given a `30 s` spin-up
before a reading is made.

**Sources:**

* [SDS 021 - $33.00](http://www.aliexpress.com/item/NOVA-PM2-5-Air-particle-dust-sensor-SDS021-laser-inside-digital-output-SDS021-Laser-PM2-5/32638192686.html?spm=2114.01010208.3.2.5WLRNu&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=c4ec533a-68d6-42cc-abdc-142fff967eff)
* [SDS 018 - $32.00](http://www.aliexpress.com/item/PM2-5-Air-particle-dust-sensor-SDS018-laser-inside-digital-output-SAMPLE/32669257200.html?spm=2114.01010208.3.2.PMVmDH&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=ef18e8bc-5287-49f3-be6e-777f9e727015)
* [SDS 011 - $24.80](http://www.aliexpress.com/item/Nova-PM-sensor-SDS011-High-precision-laser-pm2-5-air-quality-detection-sensor-module-Super-dust/32606349048.html?spm=2114.01010208.3.2.kOp9l1&ws_ab_test=searchweb201556_0,searchweb201602_3_10017_301_406,searchweb201603_11&btsid=3df6cf05-6547-4532-befc-906caf4e6bbc)

The SDS011 laser dust sensor is similar to the PMS X003 model, however it is designed to provide more accurate readings
through a larger form factor. The sensor provides data for `PM 2.5` and `PM 10` sized particles.

Datasheets exist for [v.1.0](http://inovafitness.com/upload/file/20150311/14261262164716.pdf) and
[v.1.3](http://inovafitness.com/software/SDS011%20laser%20PM2.5%20sensor%20specification-V1.3.pdf) of the sensor.

**Documents:**
* Datasheet: [SDS021-V1.0.pdf](documents/SDS021-V1.0.pdf)
