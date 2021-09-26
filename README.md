# SuperPlayer-v8.0.0 --- CamillaGUI-v0.6.0 .tcz extensions
*CamillaGUI .tcz extensions the right way of doing it for TinyCore/PiCore Linux*

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
cd 

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
