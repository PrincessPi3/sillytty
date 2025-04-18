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
4. `curl -s https://raw.githubusercontent.com/PrincessPi3/sillytty/refs/heads/master/install-sillytty | bash`
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
    * `picosilly` picocom terminal: 
    * `$SILLYTTY` virtual tty device 
    * `stop-sillytty`

Others:
* `VARDUMP-SILLYTTY` Sanity checks debugging and info 
* `UNINSTALL-SILLYTTY` Uninstall 
* `NC-SILLYTTY` Standard nc terminal  
* `SOCAT-SILLYTTY` stdio socat terminal 
* `PROBESILLYDEV` get info on private dev pipes ttys links etc 
* `KILLSILLYSOCAT` kill socat, nc, delete pipes 
* `PICOSILLY` picocom on the defaualt baud on the default link 
* `TTYSILLYTTY` alias of `socat -d pty,link=$SILLYPTY,b$SILLYBAUD,raw,echo=0,nonblock $SILLYPROTO:$SILLYHOST:$SILLYPORT &`
* `NEWPTY` development/debug spare function

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