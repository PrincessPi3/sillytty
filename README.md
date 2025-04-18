# sillytty
letting termux use usb serial devices on stock android without root

## installation
Install these apps
1. Install [F-Droid](https://f-droid.org/en/) ([Docs](https://f-droid.org/en/docs/))
2. Install [Termux](https://f-droid.org/en/packages/com.termux/) ([Wiki](https://wiki.termux.com/wiki/Main_Page))
3. Install [TCPUART app](https://play.google.com/store/apps/details?id=com.hardcodedjoy.tcpuart)

In termux
1. `pkg update`
2. `pkg upgrade`
3. `pkg install netcat-openbsd socat picocom wget`
4. `curl https://raw.githubusercontent.com/PrincessPi3/sillytty/refs/heads/master/install-sillytty | bash`
5. `exit`

In TCPUART
* Baud Rate: `115200`  
    * _Connect_  
* TCP:   
    * Mode `Server`  
    * Port: `31337`  
    * _Start_

## usage
1. Plug in USB Serial device
2. Run TCPUART
    * Baud Rate: `115200` 
    * Mode: `Server`
    * Port `31337`
    * _Connect_
    * _Start_
3. Run Termux
    * `start-sillytty`
    * picocom terminal: `picosilly`
    * virtual tty device `$SILLYTTY`
    * `stop-sillytty`

Others:
* Sanity checks debugging and info `vardump-sillytty`
* Uninstall `uninstall-sillytty`

## supprtorted devices
## supported software

# scratch and notes
working terminals
* `nc localhost 31337`
* `socat - tcp:localhost:31337`

in progress:
```
mkfifo $SILLYPIPE
nc $SILLYHOST $SILLYPORT > $SILLYPIPE &
socat -d -d pty,raw,echo=0,link=$SILLYTTY $SILLYPIPE
```

run live dev script: `curl https://raw.githubusercontent.com/PrincessPi3/sillytty/refs/heads/master/live-dev-script | bash`