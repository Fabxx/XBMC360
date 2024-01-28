# Xbox-360-Blades-to-PC
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

1) run the XBMC9.11 installer, it is recommended to install it in default path or `C:\` folder.

  -You can also choose to make it a portable installation in the same C: path, so settings will be saved on the same folder.

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

# Making application launchers

XBMC Supports python, so you can create game/emulator runners with python scripts.

Install lastes python version on windows/linux, then go into "scripts" folder of XBMC

make a subfolder if you want so you can create script categories, create a .py file and add this

on windows:
```
import os

command="cd \"DiscIndex:\\\Path\\to\\.exe\\\" & .\\your.exe"

os.system(command)
```
```
linux:

import os

command="cd \"/path/to/exe\"" & your.exe"

os.system(command)
```

NOTE: Paths should NOT HAVE special characters like ' for example.

NOTE 2: If on linux there is a space in the name, add a double backslash like this:

```
command="cd \"/path/to\\ my/exe\""
```

NOTE 3: For linux users i've made a python script generator that can run .sh files directly to make things easier.
        you can geenerate sh files using LinuxGSG in my repo, then run the generator to recursively parse the sh files
        and write python files automatically.

then you can go into "System" blade > Memory > File Explorer

Q: Drive > scripts. You can also add a shortcut to the folder you need with "add sources"


# Animation Loop Fix

ANIMATION LOOP FIX

As you can see in media i've provided the "bkgd_frames" folder. This should already fix the animation loop but if it doesn't
do these steps:

1) Check the "skin.xml" file in MC360 2.1 folder, specifically these two parameters:
```
	<defaultresolution>pal</defaultresolution>
 	 <defaultresolutionwide>pal16x9</defaultresolutionwide>
```
 	 
 	you can keep them as default or change them based on the region folder you want to use inside MC360 2.1 folder.
 	i recommend to leave it to default unless you have refresh rate issues.

2) Get in the folder you've chosen in those settings, based on your aspect ratio.
   
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

`Z:\\\\media\\username\\mydisc\\XBMC\\MC360\\media\\\\bkgd_frames`


# Controller Support

Controllers need to be manually mapped. Sources to do this are under `XBMC/system/keymaps`

it provides documentation on how to map controllers. If you want to provide xml that map controllers feel free to submit one.
