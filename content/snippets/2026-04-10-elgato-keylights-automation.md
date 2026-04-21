---
title: "Elgato Keylights: automating shutdown on linux"
date: 2026-04-11T08:30:00Z
categories: ["linux", "elgato"]
---

I have some nice Elgato keylights that I have been using under windows for a long time. The software for windows has a nice feature that I missed when switching to linux: I had the option to automatically shut down the lights when I shut off my pc.

I got pretty used to it and didn't like that I manually had to turn them off, let alone that I forgot it everytime since I was used to the automation and I then had to go find my phone, find the app and turn them off manually.

What I didn't know, is that I could add the light to my home assistant!
I added the lights there and because I wanted to control them from my pc

In `Home assistant`

- Go to `Settings -> Automation & Scenes`
- Create an automation to turn the light off

That exposes an http endpoint, and I created a systemd service around this:

```bash
[Unit]
Description=Shutdown elgato lights on stop

[Service]
# Short-lived service; runs a single command.
Type=oneshot

# Command to run when the service is stopped (during shutdown).
ExecStop=/usr/bin/curl -X POST https://your-home-assistant-endpoint

# Keep the service considered "active" after start so it gets a proper stop phase.
RemainAfterExit=yes

# Maximum time to wait for the HTTP call before continuing shutdown.
TimeoutStopSec=10s

[Install]
# Start this service with the normal multi-user system; it will be stopped on shutdown.
WantedBy=multi-user.target
```

Save this file as `/etc/systemd/system/ha-shutdown.service` and run the following:

```bash
sudo systemctl daemon-reload
sudo systemctl enable ha-shutdown.service
sudo systemctl start ha-shutdown.service
```

I also added scenes in HomeAssistant to create moodlighting. Those I added as aliases in my shell config file and set keybindings in my hyprland config.

Definitely a little fun project with a lot of use!
