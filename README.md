A simple script for toggleing xinput

First, go to terminal. Type xinput. Output Example:

user@dell ~ $ xinput                                                                                                                                                      [ruby-2.3.1p112]
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ DELL0802:00 06CB:7E92 Touchpad          	id=12	[slave  pointer  (2)]
⎜   ↳ Delux Efficiency  series                	id=19	[slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad              	id=17	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]
    ↳ Video Bus                               	id=8	[slave  keyboard (3)]
    ↳ Power Button                            	id=9	[slave  keyboard (3)]
    ↳ Sleep Button                            	id=10	[slave  keyboard (3)]
    ↳ Integrated_Webcam_HD: Integrate         	id=11	[slave  keyboard (3)]
    ↳ Intel HID 5 button array                	id=13	[slave  keyboard (3)]
    ↳ Intel HID events                        	id=14	[slave  keyboard (3)]
    ↳ Dell WMI hotkeys                        	id=15	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=16	[slave  keyboard (3)]
    ↳ Delux Efficiency  series                	id=18	[slave  keyboard (3)]
    
In this case the touchpad is the device with id=12

Create a the script in ~/toggle_touchpad.sh containing

#!/bin/bash

device=12
state=`xinput list-props "$device" | grep "Device Enabled" | grep -o "[01]$"`

if [ $state == '1' ];then
    xinput --disable $device && notify-send -i emblem-nowrite "Touchpad" "Disabled"
else
    xinput --enable $device && notify-send -i input-touchpad "Touchpad" "Enabled"
fi

Change the permissions of the file to make it executable:

chmod +x ~/toggle_touchpad.sh

And add it to the unity keyboard shortcuts
