---
title: "Hyprland: Color picker"
date: 2026-05-04T22:30:00Z
categories: [linux, hyprland, hyprpicker]
---

One tool I like to have accessible quickly is a color picker. On keypress, I want to be able to pick a color anywhere on my screen and have it copied to my clipboard.
I am using `hyprpicker` for this. 

To install:
`sudo dnf install hyprpicker wl-clipboard`

I am using the following command:
`hyprpicker --autocopy`

The `--autocopy` places the output to clipboard

For instant access, I added this to my hyprland bindings:
`bind = $mainMod, C, exec, hyprpicker --autocopy`
