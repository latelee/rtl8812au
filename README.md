# RTL8812AU/21AU and RTL8814AU linux driver with monitor mode and frame injection
The master branch is based on https://github.com/ulli-kroll/rtl8821au branch v4.3.22-beta/rework.
According to rtw_version.c the real driver version is 4.3.20.

The branch v4.3.21 may be built for RTL8814AU or RTL8812AU/RTL8821AU chipset. 

Known Supported Devices:

```
* NETCORE NW392 WLAN Adapter RTL8812AU 802.11a/b/g/n/ac(900 AC)
  ID 0bda:8812 test under ubuntu16.04 kernel: 4.8.0&4.10.0
```
```
$ lsusb | grep 8812
Bus 001 Device 002: ID 0bda:8812 Realtek Semiconductor Corp. 
```

for building RTL8812AU/RTL8821AU driver type(default: i386):

`$ make`

for building RTL8812AU/RTL8821AU driver for s3c2440 type:

`$ mv Makefile_s3c2440 Makefile`

`$ make`

for building RTL8814 driver type:

`$ make RTL8814=1`


for building driver with debug output type:

`$ make DEBUG=1`

or

`$ make RTL8814=1 DEBUG=1`

for install the driver type:

`$ sudo insmod 8812au.ko`

for uninstall the driver type:

`$ sudo rmmod 8812au`

(tocheck: put ko into /lib/...)

for setting monitor mode

1. Set interface down

  `$ sudo ip link set wlan0 down`

2. Set monitor mode

  `$ sudo iwconfig wlan0 mode monitor`

3. Set interface up

  `$ sudo ip link set wlan0 up`

for switching channels (interface must be up)

Set channel 6, width 40 MHz:
```
$ sudo iw wlan0 set channel 6 HT40-
```

Set channel 149, width 80 MHz:
```
$ sudo iw wlan0 set freq 5745 80 5775
```

for setting TX power (v4.3.21 branch only):
```
$ sudo iwconfig wlan0 txpower 30
```
or
```
$ sudo iw wlan0 set txpower fixed 3000
```

to inject frames with b/g rates use the Rate field in the radiotap header

to inject frames with n rates use the MCS field in the radiotap header

to inject frames with ac rates use the VHT field in the radiotap header 

