# XBMC360

![xbmclive_homelogo](https://github.com/Fabxx/Xbox-360-Blades-to-PC/assets/30447649/585efb68-ec02-43cd-8541-7dbe5fd7d583)


this is for XBMC 9.11 on Desktop, Linux (wine) and Windows

Skin was made by: Team BlackBolt


https://github.com/Fabxx/Xbox-360-Blades-to-PC/assets/30447649/db256de7-5565-4747-bdf8-3d0a4b062d38


# Details

Changes from vanilla MC360:
```
corrected these sounds with the ones from blades dashboard:

back.wav

exit.wav

select.wav

based off MC360 2.1, which fixes some paths detections to add sources.

```

# Installation

1) run the XBMC9.11 installer and install XBMC where you want.

  -You can also choose to make it a portable installation, so settings will be saved in the install same folder.

  -If installing on default path under "Program Files (x86)", when you want to create scripts you'll need to give admin permissions
   to modify the folder. If you want to avoid this, simply install under C:\ or any other path.

2) Drag & drop MC360 2.1 Folder into skins folder of XBMC, then select it from system settings of XBMC

3) To enable login screen go into Profiles and enable the tick of the login screen.

4) Linux users should install `dxvk` in their prefix through: `winetricks dxvk`  

# Customization - Profile Picture

Drag & drop the `GamerPics` folder into `XBMC` folder. then from the dashboard click on your gamertag and click "change gamer picture"

go into `Q: Drive`, which is the main XBMC folder then select your pic from there.

# Boot Animation

```
Linux (Debian/Ubuntu): sudo apt install mpv

Linux (Arch): 	       sudo pacman -S mpv

Windows: extract the provided MPV folder where you want
```

now just edit the script `XBMC 9.11.bat` if on windows, or `XBMC 9.11.sh` if on linux

the file is self-explanatory, just change the paths with the stuff you need to point to.

when you're gonna run the script it will play the xbox 360 boot screen, then run XBMC

# App Launcher [Windows - manual]

XBMC Supports python, so you can create game/emulator runners with python scripts.

Install lastes python version on windows/linux, then go into "scripts" folder of XBMC

make a subfolder if you want so you can create script categories, create a .py file and add this

```
import os

command="cd 'DiscIndex:\\Path\\to\\executable\\" & .\\your.exe"

os.system(command)
```
# App Launcher [Linux - Manual]

```
linux:

import os

command="cd \"/path/to/exe\"" & your.exe"

os.system(command)
```

NOTES: 
	
 -Paths should NOT HAVE special characters like ' for example.
	
 -If on linux there is a space in the name, add a double backslash like this:

```
command="cd \"/path/to\\ my/exe\""
```

-When launching apps, do NOT reduce XBMC to icon, or else the window tries to take priority and makes the system lag.


then you can go into "System" blade > Memory > File Explorer

Q: Drive > scripts. You can also add a shortcut to the folder you need with "add sources"

# App Launcher [Linux - Automatic]

First, use this program to generate `sh` scripts:

https://github.com/Fabxx/LinuxGSG

then use `pygen.sh` to generate python scripts that will run the `sh` scripts



https://github.com/Fabxx/Xbox-360-Blades-to-PC/assets/30447649/13c7ee34-70fd-40c2-840c-8a68d859125e



https://github.com/Fabxx/Xbox-360-Blades-to-PC/assets/30447649/1c55ba55-25d1-423b-8d3b-c725c419a1ee


# Controller Mappings

enable debugging under System > System settings > Debugging in XBMC

now when you press a button on your controller in the XBMC.log file, located in C:\User\AppData\Roaming\XBMC, you will notice these log messages:
```
02:09:05 T:8784 M:4294967295   DEBUG: Joystick 0 button 1 Down
02:09:05 T:8784 M:4294967295   DEBUG: Joystick 0 button 1 Up
```

gather all button IDs by pressing all buttons on controllers, then in the log file check the name of the detected controller, example in my case:

```
02:08:26 T:8784 M:4294967295  NOTICE: Enabled Joystick: Controller (XBOX 360 For Windows)
```

Now go into XBMC/system/Keymaps, here you need `gamepad.xml`

If you use a logitech controller or similar layouts, you can copy paste the file `joystick.Logitech.RumblePad.2.xml`

rename it into the joystick name you've found in the log. Don't put spaces, use dots like the original file name. Example:

`joystick.Controller.(XBOX.360.For.Windows)`

NOTE: under wine you should have: `Wine joystick driver` as the gamepad name

open `gamepad.xml` and `your controller xml` with notepad++ or anything useful for xml editing.

`gamepad.xml` contains the button definitions for XBMC, for example A is used to "Select" action, B is used to "Previous menu" action, and so on.

You have to compare your button IDs and change the button ID in the action of your copy-pasted xml.

Also, the main section is the `<global>` section that maps the main keys

example:
```
<button id="2">Select</button>
<button id="3">PreviousMenu</button>
```

in gamepad.xml select and previousmenu are:
```
 <A>Select</A>
 <B>ParentDir</B>
```

NOTE: Different menus can use different actions for same buttons.

 in my XBMC.log when i press A and B i have:
 
```
 Joystick 0 button 1 Down for A
 Joystick 0 button 2 Down for B
```

when i press B and X i have
```
 Joystick 0 button 2 Down for A
 Joystick 0 button 3 Down for B
```

 so now the original config uses B and X to select and exit a window, which is wrong. So i replace it with my IDs:
 
```
<button id="1">Select</button>
<button id="2">PreviousMenu</button>
```

you can also add a mapping if it's not available, like if you just want to go up a single folder you need ParentDir mapping:

`<button id="3">ParentDir</button>`

in my case i mapped it to X

NOTE: for d-pads the button is indicated as "hat":

`Joystick 0 hat 1 Down`
 
Also, change all the `name` controller parameters into your game controller name.

Example:

<joystick name="Logitech Logitech Cordless RumblePad 2">

replace ALL of these with your controller name, in my case:

<joystick name="Controller (XBOX 360 For Windows)">


NOTE: I provided a pre-defined controller mapping for generic Xbox 360 controllers for windows and wine

NOTE 2: the controller name must be Exactly the same as shown in the log, there must be no difference
	in terms of Upper/lower case letters.


# Fix Extreme lag (Linux/Wine)

in your wine prefix folder, go into `dosdevices` folder

create a symlink like this:

`ln -s /dev/sr0 e:`

`ln -s /dev/sr0 d:`

apparently this creates a symlink to the fake dvd drive looked by MC360, which then stops lagging, however the DVD button will be stuck on "Reading"



# Fix Animation Loop (if broken)

As you can see in media i've provided the "bkgd_frames" folder. This should already fix the animation loop but if it doesn't
do these steps:

1) Check the "skin.xml" file in MC360 2.1 folder, specifically these two parameters:
```
	<defaultresolution>pal</defaultresolution>
 	 <defaultresolutionwide>pal16x9</defaultresolutionwide>
```

2) Get in the indicated folder based on your aspect ratio.
   
3) Open `includes.xml`, find this section:

```
<include name="Background-animation-commons">
		<description>Background Animation</description>
		<imagepath>BKGD_Frames</imagepath>
		<timeperimage>0</timeperimage>
		<fadetime>70</fadetime>
		<loop>yes</loop>
		<randomize>false</randomize>
```


change `BKGD_Frames` value to the absolute path of the folder, for example:

`C:\Users\Desktop\XBMC\Skins\MC360\media\bkgd_frames`

save the xml, now the animation is fixed.

NOTE FOR LINUX USERS:

If using under wine, instead of `C:\` you have to write the index disc as: `Z\\\\`, then each separator must have a double slash, example:

`Z:\\\\media\\username\\mydisc\\XBMC\\MC360\\media\\bkgd_frames`
