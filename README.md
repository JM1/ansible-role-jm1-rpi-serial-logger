# Ansible Role `jm1.rpi_serial_logger`

This role helps to setup serial console logging on Raspberry Pi.

*Details*
- A systemd service `rpi-serial-logger.service` is installed and started at boot that reads from a tty and dumps all
  characters to a daily rotated log file.

**Tested OS images**
- [`Ubuntu 20.04 LTS` (`arm64`) for Raspberry Pi 2B and later](http://cdimage.ubuntu.com/releases/20.04/release/)

Available on Ansible Galaxy: [jm1.rpi_serial_logger](https://galaxy.ansible.com/jm1/rpi_serial_logger)

## Requirements

Download and flash an OS image to a (micro) SD card,
e.g. use the [guide on ubuntu wiki](https://wiki.ubuntu.com/ARM/RaspberryPi) to setup your Raspberry Pi with
[`Ubuntu 20.04 LTS` (`arm64`) for Raspberry Pi 2B and later](http://cdimage.ubuntu.com/releases/20.04/release/).

Establish a serial connection between Raspberry Pi and a remote host. Instructions on how to do that can be found
in the official docs about [The Raspberry Pi UARTs](https://www.raspberrypi.org/documentation/configuration/uart.md)
and on [elinux.org](https://elinux.org/RPi_Serial_Connection). An easy and solderless way to connect your Raspberry
Pi to your PC is via [RS232 (COM) interface](https://en.wikipedia.org/wiki/RS-232) and
[DB9](https://en.wikipedia.org/wiki/DE-9_connector) cable(s), using e.g. a
[Joy-IT RS232 Breakout Kit](https://joy-it.net/en/products/RB-RS232) or a
[ModMyPi Serial HAT (RS232)](https://thepihut.com/blogs/raspberry-pi-tutorials/how-to-use-the-modmypi-serial-hat).

You might have to disable kernel and systemd output to serial console on your Raspberry Pi first. To do so, you have to
change your kernel cmdline as described in the official docs about
[The Raspberry Pi UARTs](https://www.raspberrypi.org/documentation/configuration/uart.md). Altering the kernel cmdline
can be accomplished with Ansible role [`jm1.rpi_cmdline`](https://galaxy.ansible.com/jm1/rpi_cmdline).

## Variables

| Name   | Default value                                            | Required | Description                                                                   |
| ------ | -------------------------------------------------------- | -------- | ----------------------------------------------------------------------------- |
| `baud` | 9600                                                     | no       | Serial tty input and output speeds in bauds                                   |
| `log`  | `/var/log/{{ tty\|default('tty', true)\|basename }}.log` | no       | Absolute path to log file. A timestamp is automatically appended to that path |
| `tty`  | `/dev/ttyUSB0`                                           | no       | Serial tty device                                                             |

## Dependencies

TODO.

## Example Playbook

```
- hosts: all
  tasks:
    - import_role:
        name: jm1.rpi_serial_logger
      vars:
        tty: '/dev/ttyS0'
```

For instructions on how to run Ansible playbooks have look at Ansible's
[Getting Started Guide](https://docs.ansible.com/ansible/latest/network/getting_started/first_playbook.html).

## License

GNU General Public License v3.0 or later

See [LICENSE.md](LICENSE.md) to see the full text.

## Author

Jakob Meng
@jm1 ([github](https://github.com/jm1), [galaxy](https://galaxy.ansible.com/jm1), [web](http://www.jakobmeng.de))
