# Nevera Realtime Weather & Clock — Overview

A lightweight, **free**, standalone FiveM script that synchronizes **real-world weather and time** in-game using OpenWeatherMap data. Built for roleplay servers that want authentic conditions instead of randomly cycling weather.

Pick a city anywhere on the planet. If it's raining there, it rains on your server. If the sun sets at 20:41, it sets at 20:41 in game.

[Forum thread](https://forum.cfx.re/t/free-nevera-realtime-weather-and-clock-script/5283767) · [GitHub](https://github.com/Nevera-Hard-Rp/Nevera-realtime-weather) · MIT license

## Philosophy

- **Real-world simulation first** — the weather is not random, it is real
- **Zero player intervention** — players cannot change anything
- **Admin control when you need it** — one command for events, then it returns to reality on its own
- **Lightweight** — one API call per server, no per-player polling, no render loop while the panel is hidden

## Features

- **Worldwide** — any city, any timezone, no timezone configuration
- **Automatic DST** — summer and winter time come from the API
- **Drift-free clock** — synchronized every second against real time
- **Detailed weather mapping** — ~40 OpenWeatherMap condition IDs mapped individually (drizzle, moderate rain and a thunderstorm each look different)
- **Smooth transitions** — the sky fades between states over 15 seconds
- **Real wind direction** — wind follows the actual bearing from the API
- **Snow effects** — tyre trails and footprints enable automatically
- **On-screen panel** — time, conditions, temperature and wind, top-left
- **Admin override** — force any weather type for a set duration, with automatic return to real conditions
- **Resilient** — retries on failure, keeps last known data, explains errors clearly
- **No dependencies** — ESX, QBCore, QBox or standalone

## Requirements

- FiveM server artifacts supporting `fx_version 'cerulean'`
- A free [OpenWeatherMap](https://openweathermap.org/) API key
- Outbound HTTPS access from your server

## Performance

| State | Cost |
|---|---|
| Panel hidden | **0.00 ms** |
| Panel visible | ~0.03 ms |

One API call per interval regardless of player count (~4,300/month at the default 10 minutes — inside the free tier).

Continue: [Installation](installation.md) · [Admin commands](admin-commands.md) · [Changelog](changelog.md)
