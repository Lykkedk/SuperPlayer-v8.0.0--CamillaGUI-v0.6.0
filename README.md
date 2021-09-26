# SuperPlayer-v8.0.0 --- CamillaGUI-v0.6.0 .tcz extensions
**SuperPlayer-v8.0.0 is an sort of extension for the piCorePlayer v8 https://www.picoreplayer.org/**

**CamillaGUI .tcz extensions the right way of doing it for TinyCore/PiCore Linux**\
*Instead of pip3 install everything to be able to run the nice CamillaDSP-GUI i created a lot*\
*of .tcz extensions, with help from the nice guy's over at TinyCore Linux RPI Forum*\
*Something i wanted for a long time, and as said the right way of doing it the Tiny/Picore Linux way*\
*Thread and help here :: https://www.diyaudio.com/forums/pc-based/361429-superplayer-dsp_engine-camilladsp-samplerate-switching-esp32-remote-control.html*

*For some insight's of howto ssh into piCorePlayer and edit stuff etc.., take a look at my other repos, where it's explained*

**Here we go ::**

Follow Henrik's instructions https://github.com/HEnquist/camillagui-backend and install the Backend Server for CamillaGUI in this location ::
**/mnt/mmcblk0p2/tce/Camilla_Extensions/camillagui <----- The location is very important** 

This is what have to be done (Snip from GitHub)::
```
Go to "Releases": https://github.com/HEnquist/camillagui-backend/releases 
Download the zip-file ("camillagui.zip") for the latest release. This includes both the backend and the frontend.
Unzip the file, and edit config/camillagui.yml if needed.

```

It should look like this when done ::
```
tc@SuperPlayer:~$ ls -all /mnt/mmcblk0p2/tce/Camilla_Extensions/camillagui
total 68
drwxrwxr-x    5 tc       staff         4096 Sep 23 17:06 ./
drwxrwxr-x    3 tc       staff         4096 Sep 25 10:26 ../
-rw-rw-r--    1 tc       staff        35149 Sep 23 17:06 LICENSE.txt
-rw-rw-r--    1 tc       staff         7057 Sep 23 17:06 README.md
drwxrwxr-x    3 tc       staff         4096 Sep 23 17:40 backend/
drwxrwxr-x    3 tc       staff         4096 Sep 23 17:06 build/
drwxrwxr-x    2 tc       staff         4096 Sep 23 17:06 config/
-rw-rw-r--    1 tc       staff         1198 Sep 23 17:06 main.py
```

Now grab all the .tcz extensions and copy them to right location ::
```
tce-load -w git
tce-load -i git
git clone https://github.com/Lykkedk/SuperPlayer-v8.0.0--CamillaGUI-v0.6.0.git
cd SuperPlayer-v8.0.0--CamillaGUI-v0.6.0
cp *.tcz /mnt/mmcblk0p2/tce/optional
cp *.tcz.dep /mnt/mmcblk0p2/tce/optional
```
When done, the folder ```SuperPlayer-v8.0.0--CamillaGUI-v0.6.0``` can be deleted... Be carefull ;-) ```rm -fr SuperPlayer-v8.0.0--CamillaGUI-v0.6.0```

Go and paste the lines in ```/opt/bootlocal.sh``` so it looks like this (The three lines at the bottom) ::
```
#!/bin/sh
# put other system startup commands here

GREEN="$(echo -e '\033[1;32m')"

echo
echo "${GREEN}Running bootlocal.sh..."
#pCPstart------
/usr/local/etc/init.d/pcp_startup.sh 2>&1 | tee -a /var/log/pcp_boot.log
#pCPstop------

# SuperPlayer ------
camillagui  > /dev/null 2>&1 &
# SuperPlayer ------
```
When we are at it, paste the lines ```camillagui-v0.6.0.tcz & camilladsp-0.6.3.tcz``` in  ```/mnt/mmcblk0p2/tce/onboot.lst```\
*If you somewhat use another camilladsp binary, just delete the ```camilladsp-0.6.3.tcz``` extension.*
```
tc@SuperPlayer:~$ cat /mnt/mmcblk0p2/tce/onboot.lst
pcp.tcz
pcp-8.0.0-www.tcz
nano.tcz
python3.8.tcz
camilladsp-0.6.3.tcz
camillagui-v0.6.0.tcz

```
If you not allready have python3.8 installed, then do ```tce-load -wi python3.8```\
Then the line ```python3.8.tcz``` will be added automaticly...

**Remember to do ```sudo filetool.sh -b``` or the pCP way ```pcp bu``` (pcp = piCorePlayer / bu = Backup)**

When the camillagui-v0.6.0.tcz is loaded/extracted at boot, it will look for the folder's ```/home/tc/camilladsp/configs & coeffs```\
if they are missing **(and only then)** they will be created, but please don't blame me if my .tcz's corrupt anything ;-)

The structure of the .tcz package ::
```
camillagui
├── home
│   └── tc
└── usr
    └── local
        ├── bin
        │   └── camillagui
        └── tce.installed
            └── camillagui-v0.6.0
```
I did test this over and over, and everything seem's to work flawlessly.

Jesper (lykkedk over at diyaudio.com)\

