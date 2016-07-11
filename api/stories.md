# User Stories

## Configuring a Static Sensor

**Summary:** A single static sensor with built-in GPS and WIFI modules connects to the server and pushes sensor data every 10 minutes.

A static sensor arrives on the end-user's doorstep. They open the box and find a simple set of instructions guiding them to plug it in and connect to it (via USB or adhoc WIFI). They are instructed to open the configuration page on their browser that guides them through the setup.

The setup process requires a device API key, which can either be obtained automatically by logging in through the device (which does not save credentials), or manually by logging in through the user interface and registering a new device.

Once a device has its own API key, it is also registered with a unique device ID. Once a device is set up, it's basic configurations are available through its own web interface:

* Continally sync GPS location (for dones, etc.) `bool:false`
* Post sensor data every `int:10` minutes
* Log previous `int:20` sync requests
