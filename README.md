# jetson-watchdog-timer

### check kernel to watchdog is avaliable:

`ls -al /dev/watchdog*`

crw------- 1 root root  10, 130 May 19 07:09 /dev/watchdog

crw------- 1 root root 253,   0 May 19 07:09 /dev/watchdog0

`sudo apt-get install watchdog`

`ls -l /lib/systemd/system/`

watchdog.service
wd_keepalive.service

`ls -al /etc/default/watchdog`

### Start watchdog at boot time? 0 or 1

`run_watchdog=1`

### Start wd_keepalive after stopping watchdog? 0 or 1

`run_wd_keepalive=1`

### Load module before starting watchdog

`watchdog_module="none"`

`sudo vim /etc/watchdog.conf`

### Uncomment the following lines or add them in the bottom of the files if you don’t find these lines in the above file.

ping                    = 8.8.8.8
ping                    = 1.1.1.1

max-load-1 = 24
min-memory = 1

watchdog-device = /dev/watchdog

### There is one more line that I added at the end of the above file is this.

watchdog-timeout=15

`sudo systemctl start watchdog`

`sudo systemctl status watchdog`

`sudo systemctl stop watchdog`

`sudo vim /lib/systemd/system/watchdog.service`

### and add the following lines under the Install section.

[Install]
WantedBy=multi-user.target
save it and run this command:

`sudo systemctl daemon-reload` 
`sudo systemctl enable watchdog`









