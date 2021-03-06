Act as a simple VNC server, extracting keypress and mouse movements as usable
events.

Expected to be paired with a tool like x2vnc.

# Hardware required

This has been tested on both an Orangepi Zero and a Raspberry Pi Zero W
(but it should work on any other Linux device with USB device port and
a UDC driver)

- In these steps, the Linux system running the vnc2hid is refered to as
  the "device"
- The system you wish to remote-control is refered to as "host"


# Setup steps

- Plug your device in to the host system and wait until it has booted up.
  You will need to SSH to the device
- Run `./setup_udc_hid`, it will suggest the correct UDC driver name
- Run `./setup_udc_hid` with the correct driver name
- You should see a new keyboard and mouse plugged into the host

The device now has `/dev/hidg0` and `/dev/hidg1` nodes available for it to
send USB information to the host

The setup steps are only needed to be done straight after bootup and will
persist until the next boot.

## Raspberry Pi

Some of the Raspberry Pi boards have a USB Device port.  All the Zeros have
the correct connector as well and can be quickly used.  The model A devices
and the Raspberry Pi 4 USB-C connector can also be used.

To enable the device port, edit your `/boot/config.txt` to add `dtoverlay=dwc2`

# Normal usage

Run the `./vnc2hid` program with no options to get a simple usage summary.
Determine the correct options and start it.

Eg: For a host with a 1080p screen resolution, use:

    ./vnc2hid 5900 1920 1080 /dev/hidg0 /dev/hidg1

Connect to your device with a vncviewer.  You will only see a black screen,
but any mouse movements and keyboard entries will be sent to the host as if
a local keyboard or mouse was used.

For a more natural use, install `x2vnc` and use that to extend your virtual
desktop to the host computer.
