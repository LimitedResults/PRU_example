# PRU_example
simplest example for programming PRU on PocketBeagle (Linux beaglebone 4.19.94-ti-r42 #1buster)

## Installation
https://software-dl.ti.com/codegen/esd/cgt_public_sw/PRU/2.3.3/ti_cgt_pru_2.3.3_armlinuxa8hf_busybox_installer.sh
or
https://www.ti.com/tool/PRU-CGT


## Usage

verify the ip address of your board (by default it is 192.168.6.2

```bash
## copy into the Beagle
scp -r PRU_gpioToggle debian@192.168.6.2:
scp ti_cgt_pru_2.3.3_armlinuxa8hf_busybox_installer.sh debian@192.168.6.2:

## install ti_cgt_pru to your PB
chmod a+x ti_cgt_pru_2.3.3_armlinuxa8hf_busybox_installer.sh
sudo ./ti_cgt_pru_2.3.3_armlinuxa8hf_busybox_installer.sh

## compile
cd PRU_gpioToggle/
make

## config the pin as PRU output
config-pin P1_36 pruout

## load
cp gen/PRU_gpioToggle.out /lib/firmware
echo "PRU_gpioToggle.out" > /sys/class/remoteproc/remoteproc1/firmware
echo "start" > /sys/class/remoteproc/remoteproc1/state
echo "stop" > /sys/class/remoteproc/remoteproc1/state

## check
dmesg
...
[  timestamp] remoteproc remoteproc1: powering up 4a334000.pru
[  timestamp] remoteproc remoteproc1: Booting fw image PRU_gpioToggle.out, size 31364
[  timestamp] remoteproc remoteproc1: remote processor 4a334000.pru is now up
```
