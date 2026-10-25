# tools

PC-side tools that work with the gateway. Nothing in this directory runs on the microcontroller.

## Planned tools

| Tool | Purpose | Status |
|---|---|---|
| `monitor/` | Reads the serial port and prints decoded values (rpm, speed, coolant temperature) live | planned |
| `logger/` | Records CAN frames with timestamps to a CSV file for offline analysis | planned |
| `decoder/` | Decodes a recorded CSV log offline and can produce test data for `../tests` | planned |
| `scripts/` | Helper scripts, for example flashing the firmware or calculating CAN bit timing | planned |

## Layout

Every tool lives in its own subdirectory with its own `README.md` that explains:

- what the tool does,
- how to install its dependencies,
- how to run it, with an example command and example output.

Python tools list their dependencies in a `requirements.txt` file:

```bash
cd tools/monitor
python -m venv .venv
.venv\Scripts\activate        # Windows
pip install -r requirements.txt
python monitor.py --port COM5 --baud 115200
```

## Compatibility

When the firmware speaks the SLCAN protocol, standard tools work without anything from this directory:

- [SavvyCAN](https://www.savvycan.com/) for viewing and analysing CAN traffic,
- SocketCAN with `slcand` on Linux.

Tools here focus on OBD-II specific tasks that those programs do not cover.

## Rules

- No hard-coded serial port names. The port is always a command line argument.
- Virtual environments (`.venv/`) and generated logs are not committed (see `.gitignore`).