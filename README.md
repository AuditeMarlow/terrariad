# Terrariad

`terrariad` is a Terraria daemon script to help in basic administration in
running a Terraria dedicated server.

## Prerequisites

`terrariad` depends on [Tmux][tmux] to run the Terraria dedicated server in the
background. Make sure you have Tmux installed.

Additionally if you want to run the Terraria dedicated server on a Raspberry Pi
or some other ARM or ARM64 device you may want to use [mono][mono] as described
[here][how-to-rpi].

## Installation

You may install `terrariad` to a location in your path and make it executable.

```bash
wget -O- https://raw.githubusercontent.com/AuditeMarlow/terrariad/main/terrariad | sudo tee /usr/local/bin/terrariad
sudo chmod +x /usr/local/bin/terrariad
```

### Systemd Service

If you want to run a Terraria dedicated server on boot, the systemd service
might be helpful for you.

```bash
wget -O- https://raw.githubusercontent.com/AuditeMarlow/terrariad/main/terraria.service | sudo tee /etc/systemd/system/terraria.service
```

Modify the `User=` parameter of the `terraria.service` file to the user you
want to run the Terraria dedicated server as. Then you may start and/or enable
the service.

```bash
sudo systemctl enable --now terraria
```

## Usage

Start the Terraria dedicated server.

```bash
terrariad start
```

Stop the Terraria dedicated server.

```bash
terrariad stop
```

Attach to the Terraria dedicated server console.

```bash
terrariad attach
```

## Configuration

`terrariad` is configured using environment variables. The following
environment variables are supported.

* **TERRARIA_PATH** - The path where your server executable and configuration
  lives.
* **TERRARIA_SERVER** - The server executable file.
* **TERRARIA_CONFIG** - The server configuration file.
* **TERRARIA_CMD** - What command to execute to start the server.
* **TERRARIA_LOG** - Where to output the server logs to.
* **TERRARIA_TMUX_SESSION** - The name of the Terraria tmux session.

You may apply these environment variables to `terrariad` as follows.

```bash
TERRARIA_PATH=/path/to/terraria/server terrariad
```

### Configuring The Systemd Service

You may edit the `terraria.service` systemd service file to configure
`terrariad` using the `Environment=` or `EnvironmentFile=` parameters.

```text
...
[Service]
Environment="TERRARIA_CONFIG=config.txt"
EnvironmentFile=/path/to/terrariad/config
...
```

[tmux]: https://github.com/tmux/tmux/wiki
[mono]: https://www.mono-project.com/
[how-to-rpi]: https://terraria.fandom.com/wiki/Server#How_to_(RPI_/_Others_OSes)
