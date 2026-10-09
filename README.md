# Web-Power-Switch-Remote-Power-Control-for-Lab-Test-Boards
Built a browser-based power switch on BeagleBone Black so lab engineers can turn test-board power on, off, and cycle it from any PC. Each board runs its own server and starts again after reboot.


**Features**

- Login page before anyone can change power
- Turn each relay ON or OFF from the browser
- 30-second power cycle (OFF, wait, ON)
- Live status from the GPIO pin
- Works for 2 relays and 4 relays
- Saves the last state and restores it after reboot
- Warning when the BeagleBone is offline
- Notes on each relay
- Starts by itself with systemd

**Programs and languages**

| Part | Used |
| --- | --- |
| Web page | HTML, CSS, JavaScript |
| Server | Python, Flask, Gunicorn |
| Settings | YAML |
| Relay control | Bash (GPIO scripts) |
| Auto-start | Linux systemd |
| Board | BeagleBone Black, Ubuntu |

**Main code files**

| File | What it does |
| --- | --- |
| `server.py` | Login, ON/OFF, cycle, health check |
| `templates/index.html` | The web page |
| `relay_controller_local.py` | Calls the relay script |
| `gpio/relay_control.sh` | 2-relay GPIO control |
| `gpio/relay_control_4ch.sh` | 4-relay GPIO control |
| `relay_state_store.py` | Saves ON/OFF |
| `restore-relay-state.sh` | Puts the saved state back at boot |
| `bbb-relay-local.service` | Starts the server on boot |
