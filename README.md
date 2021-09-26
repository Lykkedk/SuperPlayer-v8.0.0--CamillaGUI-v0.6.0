# SuperPlayer-v8.0.0 --- CamillaGUI-v0.6.0 .tcz extensions
# SuperPlayer-v8.0.0 is an sort of extension for the piCorePlayer v8 https://www.picoreplayer.org/
*CamillaGUI .tcz extensions the right way of doing it for TinyCore/PiCore Linux*
*For some insight's of howto ssh into piCorePlayer and edit stuff etc.., take a look at my other repos, where it's explained*

Follow Henrik's instructions https://github.com/HEnquist/camillagui-backend and install the Backend Server for CamillaGUI in this location ::
#### /mnt/mmcblk0p2/tce/Camilla_Extensions/camillagui <----- The location is very important 

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

Now grab all the .tcz extensions ::
```
tce-load -w git
tce-load -i git
git clone https://github.com/Lykkedk/SuperPlayer-v8.0.0--CamillaGUI-v0.6.0.git
cd SuperPlayer-v8.0.0--CamillaGUI-v0.6.0
cp *.tcz /mnt/mmcblk0p2/tce/optional
cp *.tcz.dep /mnt/mmcblk0p2/tce/optional
```
Now paste the lines in ```/opt/bootlocal.sh``` so it looks like this ::
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

```


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
Bla... Bla...
