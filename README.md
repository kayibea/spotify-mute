# Spotify-Mute

A simple script and systemd service to automatically mute Spotify when ads play and unmute it afterward.

## Features

- **Ad Detection**: Detects when Spotify starts playing ads.
- **Automatic Mute/Unmute**: Mutes Spotify during ads and restores volume once music resumes.
- **Service Integration**: Runs automatically on system startup using `systemd`.
- **Crash Recovery**: Automatically restarts if it crashes.

## Installation

### Prerequisites
- **Bash**: Ensure you have a bash shell.
- **PulseAudio**: Required for controlling Spotify's audio.
- **Spotify**: Installed and running.
- **Systemd**: To run the script as a service.

### Steps
1. Clone the repository:
```bash
git clone https://github.com/kayibea/spotify-mute.git
cd spotify-mute
```

2. Copy the spotify-mute script to your local binaries directory:
```bash
cp spotify-mute ~/.local/bin/
chmod +x ~/.local/bin/spotify-mute
```

3. Set up the systemd service:
Open the `spotify-mute.service` file located in `~/.config/systemd/user/spotify-mute.service`:

```bash
nano ~/.config/systemd/user/spotify-mute.service
```

Update the ExecStart path to the correct location of the spotify-mute script. Modify the following line:
```bash
ExecStart=/home/YOUR_USERNAME/.local/bin/spotify-mute
```

4. Install the systemd service:
```bash
mkdir -p ~/.config/systemd/user/
cp spotify-mute.service ~/.config/systemd/user/
```

5. Reload systemd and enable the service:
```bash
systemctl --user daemon-reload
systemctl --user enable spotify-mute.service
systemctl --user start spotify-mute.service
```

## Usage
The script will automatically run on system startup and mute Spotify ads. Logs can be checked for troubleshooting:

```bash
journalctl --user-unit spotify-mute.service
```

To manually start or stop the service:

Start: 
```bash
systemctl --user start spotify-mute.service
```

Stop:
```bash
systemctl --user stop spotify-mute.service
```

## Contributing
Feel free to submit issues or pull requests. Contributions are welcome!

## License
This project is licensed under the MIT License.