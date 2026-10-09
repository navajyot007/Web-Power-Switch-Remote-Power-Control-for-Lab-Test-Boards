Use this to set up the Web Power Switch at a new lab location.

## Setup flow

1. Put Ubuntu 22.04 on the BeagleBone and give it an IP on the lab network.
2. Wire the relay to the BeagleBone P9 header.
3. Wire only the test-board **DC+** through the relay (COM to NO). Leave DC− direct.
4. Copy the project to the board: web files in `~/bbb_relay_web`, relay script in `~/bbb_relay_test`.
5. Set the new IP and password in `config.bbb1.yaml` (2 relays) or `config.bbb2.yaml` (4 relays).
6. Install and start it:

```bash
cd ~/bbb_relay_web
sudo ./install-on-bbb.sh bbb1
```

Use `bbb2` for 4 relays.

7. Open `http://<new-ip>:8080`, log in, and test ON, OFF, and the 30-second cycle.

**Runtime flow:** browser → port 8080 → Flask → relay script → GPIO → relay → test-board power.

## Hardware

| Item | Need |
| --- | --- |
| BeagleBone Black | 1 per bench |
| 5V power for the BeagleBone | 1 |
| Relay module, SONGLE SRD-05VDC | 2-channel or 4-channel |
| Jumper wires | GND, 5V, and one wire per relay input |
| Ethernet cable | Board must be on the lab network |
| Test board power supply | DC+ goes through the relay |

| BeagleBone P9 | Relay |
| --- | --- |
| Pin 1 GND | GND |
| Pin 7 +5V | VCC |
| Pin 12 (GPIO 60) | IN1 |
| Pin 11 (GPIO 30) | IN2 |
| Pin 13 (GPIO 31) | IN3, 4-channel only |
| Pin 14 (GPIO 50) | IN4, 4-channel only |

GPIO `0` = relay ON. GPIO `1` = relay OFF.

## Software tools

| Tool | Use |
| --- | --- |
| Ubuntu 22.04 on the BeagleBone | Operating system |
| Python 3.10+ | Runs the web server |
| SSH | Copy files and install |
| systemd | Starts the server on boot |
| curl | Health check: `curl http://<ip>:8080/api/health` |

## Libraries

From `requirements.txt`:

| Library | Use |
| --- | --- |
| Flask | Web pages and API |
| PyYAML | Reads the config file |
| Gunicorn | Keeps the server running |

Install command on the board: `pip install flask pyyaml gunicorn`

The install script also uses the system packages `python3-venv`, `python3-pip`, and `curl`.
