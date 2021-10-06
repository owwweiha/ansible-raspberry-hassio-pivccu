# ansible-raspberry-hassio-pivccu
Install piVCCU (ccu3) and Home Assistant on Raspberry PI OS lite (Debian Buster)
+ Tested on Raspberry PI 4B with Raspberry Pi OS lite installed (e.g., via rpi-imager)
+ Using `HM-MOD-RPI-PCB` or `RPI-RF-MOD` on GPIO header (tested with HM-MOD-RPI-PCB)
+ For the `HB-RF-USB(-2)` and `HB-RF-ETH` this playbook was *not* tested and steps are currently not implemented
+ Static IP assigned to raspberry pi on router
+ Ansible installed (tested with `ansible 2.10.5`)
+ Playbook follows install instructions of https://github.com/alexreinert/piVCCU/blob/master/docs/setup/raspberrypi.md for `HM-MOD-RPI-PCB` or `RPI-RF-MOD` with `bluetooth disabled` and dynamic IP

# Usage
+ Edit `raspberry.ini`, add IP of your raspberry and add password for your `pi` user
+ Run `ansible-playbook --inventory-file raspberry.ini main.yml`
+ Podman tasks might take a while to finish
+ After playbook has finished, configure your piVCCU and add your devices
+ To link hass.io and piVCCU, create/edit `configuration.yml` in `/home/pi/homeassistant/` and add (receive piVCCU IP via `pivccu-info`):
```yaml
homematic:
  interfaces:
    rf:
      host: <piVCCU IP>
      resolvenames: json
      username: <piVCCU USER>
      password: <piVCCU PASSWORD>
    wired:
      host: <piVCCU IP>
      port: 2000
      resolvenames: json
      username: <piVCCU USER>
      password: <piVCCU PASSWORD>
    ip:
      host: <piVCCU IP>
      port: 2010
  hosts:
    ccu3:
      host: <piVCCU IP>
      port: 2001
      username: <piVCCU USER>
      password: <piVCCU PASSWORD>
```
