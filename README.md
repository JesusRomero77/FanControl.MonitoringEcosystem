# FanControl.MonitoringEcosystem

An **ecosystem** of tools to **monitor and log** [FanControl](https://github.com/Rem0o/FanControl.Releases) sensors and fan controls, locally and over the network: three FanControl plugins and one portable companion app that ties them together.

> **Monitoring only.** None of these tools sends commands to FanControl or changes any fan speed. Remote sensors must never be used in curves or controls.

This repository contains no code or binaries. Each component has its own repository, with source code, README and release.

## Components

| Component | Type | What it does |
|---|---|---|
| [FanControl.CurveReader](https://github.com/JesusRomero77/FanControl.CurveReader) | Plugin | Logs the sensors and fan controls of the local computer to a file |
| [FanControl.DataServer](https://github.com/JesusRomero77/FanControl.DataServer) | Plugin | Publishes the sensors and controls of the active profile over HTTP, protected by a password. Includes an example HTML client |
| [FanControl.RemoteSensors](https://github.com/JesusRomero77/FanControl.RemoteSensors) | Plugin | Shows the sensors of another computer (running DataServer) inside FanControl. For monitoring only |
| [FanControl.WatchTower](https://github.com/JesusRomero77/FanControl.WatchTower) | Portable app (.exe) | Configures the three plugins from one window and records the data of a remote DataServer into a log |

## How the pieces fit

- **Local log:** CurveReader records the sensors and controls of the computer where FanControl runs.
- **Remote view:** on computer A, DataServer publishes the data. On computer B, RemoteSensors shows it inside FanControl.
- **Remote log:** instead of (or as well as) viewing it, WatchTower on computer B records the data published by DataServer into a local log.
- **Configuration:** WatchTower has one tab for each plugin and one File > Save for all of them.

## Installation

1. Download the DLL of each plugin you want from the Releases page of its repository and install it with FanControl's plugin installer (or copy it to the `Plugins` folder). Restart the FanControl interface.
2. WatchTower is optional and portable: download `WatchTower.exe` from its Releases page and run it from any folder.

## Current versions

| Component | Version |
|---|---|
| FanControl.CurveReader | 2.3 |
| FanControl.DataServer | 2.0 |
| FanControl.RemoteSensors | 2.0 |
| FanControl.WatchTower | 1.0 |

DataServer and RemoteSensors 2.0 work together, and WatchTower 1.0 needs these versions. Tested with FanControl v273 and later.

## Requirements

- Windows and the .NET Framework 4.8 version of FanControl.
- The FanControl interface must be open for the plugins to work.

## Security notes

- DataServer requires a password. Clients prove they know it with a signed challenge (HMAC-SHA256), so the password is never sent over the network.
- The traffic is plain HTTP, not encrypted. Use it only on networks you trust and **never expose the DataServer port to the internet**.
- The default password is public: change it before opening the port to other computers.
- Passwords are stored as plain text in the plugins' configuration files.

See the DataServer README for the full details and limits.

## Disclaimer

This project is not affiliated with FanControl or its author.

## License

Every component is licensed under the [MIT License](LICENSE).
