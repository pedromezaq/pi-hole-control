# pi-hole-control
 
Control [Pi-hole](https://pi-hole.net/) with a push button. 

Enables and disables Pi-hole with a physical push button connected on GPIO pin 40. Two LEDs on pins 36 (OFF) and 38 (ON) shows the current state.

Tested with: 
- Pi-hole 5.18.2
- Python 3.9.2
- Raspberry Pi 3 Model B Plus Rev 1.3 running Raspbian GNU/Linux 11 (bullseye) armv7l 

## Features
- Uses the command line utility pihole to enable and disable DNS blocking
- Status polling to set LED state if Pi-hole was disabled through web interface
- Runs as system service (see scripts/init.d)

## Installation
1. Install Pi-hole ad-blocking software: 
    ```
    curl -L install.pi-hole.net | bash
    ```
1. Clone this the project to your home folder.


   or wherever you prefer, e.g. /usr/local/bin
1. Connect button and LED:
   * wire a normally open push button to GPIO pin 40 and ground
   * wire a green LED to a resistor to GPIO pin 38 and ground
   * wire a red LED to a resistor to GPIO pin 36 and ground
1. Install script as system service:

   if this script was not installed in /home/pi: change $DIR and $LOG_DIR in pihole-control script.
    ```
    sudo copy ./scripts/init.d/pihole-control /etc/init.d/
    sudo chmod 755 /etc/init.d/pihole-control
    sudo update-rc.d pihole-control defaults
    ```
1. Start daemon
    ```
    sudo service pihole-control start
    ```
1. Press the button to disable/enable Pi-hole DNS blocking as needed
  
## TODO
- Use Pi-hole API once released instead of pihole utility 
