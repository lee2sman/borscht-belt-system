# Borscht Belt System - exhibition version

This is the project repo for Borscht Belt System, an artwork exhibited as part of "Spiritual Machines" at Flux Factory, August 15 - September 22, 2024 at Flux Factory, Building 404, Governor's Island. The program runs in a web browser, and needs to be as easy as possible to turn on and run each day in fullscreen. One complication is that the program runs in a web browser, and because of browser security settings it requires a mouse click at start to turn on sound. 

Governor's Island wifi is iffy. Assuming no wifi, this system sets up a local server that runs on startup, then launches firefox in kiosk mode (fullscreen, no tabs or right clicking). Uses caffeine to turn off energy saver/screensaver.

System: Void Linux with i3 window manager.

## Prerequisites

* cronie (or other cron daemon)
* i3 window manager
* caffeine-ng
* live-server (npm package. if not using npm/node, use the python simpleHTTPServer)

### Setup

1 Install cronie (or other cron daemon), caffeine, and the live-server.

```
sudo xbps-install -S cronie
sudo xbps-install -S caffeine-ng
sudo npm install -g live-server
```

2 Set up the crontab.

```
crontab -e
```

3 Set the startup script to run on startup.

```
@reboot sh /home/lettuce/startup.sh
```

Replace "lettuce" with your username. The path to startup.sh must reflect the location. This script starts the local server.

5 Use the window manager to launch firefox in kiosk mode on startup of X windows. Add this line:

```
exec --no-startup-id firefox --kiosk http://localhost:8000
```

Replace with whatever is path to the URL serving.

6 Run caffeine on start as well. Add to the i3 config. 

```
exec --no-startup-id caffeine start
```

7 Ok, all should be ready to go. On computer start, the computer should turn on, start a local server, launch the windowing system, and run the firefox kiosk mode with the website. A single mouse click is required to start unfortunately, so a mouse is hidden behind the computer.
