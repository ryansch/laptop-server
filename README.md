# Laptop Server

This repo is a collection of notes from setting up ubuntu server on a 2017 Macbook Pro.

## Installation

- Install latest supported macOS first.
- Resize macOS partition to make room for Ubuntu.
- Install ubuntu server (reuse the EFI partition).

## Screen blanking

`/opt/console-blanking/console-blanking.service`:
```
[Unit]
Description=Enable virtual console blanking

[Service]
Type=oneshot
Environment=TERM=linux
StandardOutput=tty
TTYPath=/dev/console
ExecStart=/usr/bin/setterm --blank 1 --powerdown 2

[Install]
WantedBy=multi-user.target
```

- `sudo systemctl enable --now /opt/console-blanking/console-blanking.service`

## Ignore lid close
`/etc/systemd/logind.conf`:
```
HandleLidSwitch=ignore
LidSwitchIgnoreInhibited=no
```

- `sudo systemctl restart systemd-logind`
