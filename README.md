# PRU_example
simplest example for programming PRU on PocketBeagle



Copy to your Pocketbeagle
$ scp -r PRU_gpioToggle debian@192.168.6.2:
$ scp -r ti_cgt_pru_2.3.3_armlinuxa8hf_busybox_installer.sh  debian@192.168.6.2:

install ti_cgt_pru to your PB
chmod a+x ti_cgt_pru_2.3.3_armlinuxa8hf_busybox_installer.sh
sudo ./ti_cgt_pru_2.3.3_armlinuxa8hf_busybox_installer.sh


compile
$ cd PRU_gpioToggle/
$ make
$ cp PRU_gpioToggle.out /lib/firmware

config the pin as output
$ config-pin P1_36 pruout

load
$ echo "PRU_gpioToggle.out" > /sys/class/remoteproc/remoteproc1/firmware
$ echo "start" > /sys/class/remoteproc/remoteproc1/state
$ echo "stop" > /sys/class/remoteproc/remoteproc1/state

check
$ dmesg
...
[  timestamp] remoteproc remoteproc1: powering up 4a334000.pru
[  timestamp] remoteproc remoteproc1: Booting fw image PRU_gpioToggle.out, size 31364
[  timestamp] remoteproc remoteproc1: remote processor 4a334000.pru is now up
