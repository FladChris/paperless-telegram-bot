<p align="center">
  <img src="https://raw.githubusercontent.com/GeiserX/paperless-telegram-bot/main/docs/images/banner.svg" alt="paperless-telegram-bot banner" width="900"/>
</p>

<p align="center">
  <strong>Your Paperless-ngx archive, run from Telegram.</strong>
</p>

<p align="center">
  <a href="https://github.com/FladChris/paperless-telegram-bot/actions/workflows/docker-publish.yml"><img src="https://img.shields.io/github/actions/workflow/status/FladChris/paperless-telegram-bot/docker-publish.yml?style=flat-square&logo=github&label=build" alt="Docker Build"></a>
  <a href="https://github.com/FladChris/paperless-telegram-bot/actions/workflows/tests.yml"><img src="https://img.shields.io/github/actions/workflow/status/FladChris/paperless-telegram-bot/tests.yml?style=flat-square&logo=github&label=tests" alt="Tests"></a>
  <a href="https://github.com/FladChris/paperless-telegram-bot/pkgs/container/paperless-telegram-bot"><img src="https://img.shields.io/badge/ghcr.io-container-blue?style=flat-square&logo=docker" alt="GitHub Container Registry"></a>
  <a href="https://github.com/GeiserX/paperless-telegram-bot/blob/main/LICENSE"><img src="https://img.shields.io/github/license/FladChris/paperless-telegram-bot?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/python-3.11%2B-blue?style=flat-square&logo=python&logoColor=white" alt="Python 3.11+">
</p>

---

paperless-telegram-bot is a Telegram bot for [Paperless-ngx](https://docs.paperless-ngx.com/), run in Docker. Send a photo or a file from your phone and it lands in your archive; then tag it, file it, search it and get it back, all from the chat. The bot polls Telegram and talks to Paperless over its API, so it needs no public URL, no open port and no VPN on the phone, and Paperless can stay on your LAN.

> [!IMPORTANT]
> This project is a fork of [GeiserX/paperless-telegram-bot](https://github.com/GeiserX/paperless-telegram-bot).
>
> It is maintained independently and uses its own container image. Changes, releases, and container images in this repository are separate from the upstream project.

## Features

- Send a photo or any file up to 20 MB (Telegram's limit for bots) and it is uploaded to Paperless; the reply changes to the document's title once Paperless has finished processing it.
- Tag it, pick the correspondent, the document type and, optionally, its owner in Paperless from inline keyboards right after the upload, or create a new tag, correspondent or type without leaving the chat.
- A file Paperless already has is not stored twice: the bot names the existing document and offers it for download.
- Type any text to search the archive; results come in pages, each with a Download button. `/search` does the same.
- `/inbox` lists what still carries the inbox tag; Reviewed clears it with one tap, and so does Done after an upload.
- Get the original file back in the chat, up to 50 MB.
- `/recent` shows the latest documents and `/stats` the archive's counts.
- Only the Telegram user ids you list can use the bot; everyone else is refused. It refuses to start with an empty list unless you set `ALLOW_OPEN_ACCESS=true`, which opens it to every Telegram user.
- Works with Paperless-ngx 2.x and 3.x.

## Quick start

```bash
docker run -d --name paperless-telegram-bot --restart unless-stopped \
  -e TELEGRAM_BOT_TOKEN=your_bot_token \
  -e PAPERLESS_URL=http://paperless.home:8000 \
  -e PAPERLESS_TOKEN=your_paperless_api_token \
  -e TELEGRAM_ALLOWED_USERS=123456789 \
  ghcr.io/fladchris/paperless-telegram-bot:latest
```

The image runs on amd64 and arm64. Without Docker, `pip install paperless-telegram-bot` (Python 3.11 or newer) gives you the same `paperless-bot run`; [Getting started](https://geiserx.github.io/paperless-telegram-bot/getting-started/#from-pypi) has the steps.

Get the three values first: the bot token from [@BotFather](https://t.me/BotFather) (`/newbot`), the Paperless API token from your Paperless profile (click your user name, then My Profile, API Auth Token), and your own Telegram user id from [@userinfobot](https://t.me/userinfobot). `PAPERLESS_URL` is the address the bot can reach, which is not always the one in your browser. Use the host's LAN address, or the Paperless container's name when both share a Docker network. When it works the log ends with `Bot commands registered with Telegram`, and sending `/start` to your bot in Telegram gets the command list back; Docker Compose, a run from source and what a working start looks like are in [Getting started](https://geiserx.github.io/paperless-telegram-bot/getting-started/).

## Documentation

Everything below is on the site, https://geiserx.github.io/paperless-telegram-bot/.

- [Getting started](https://geiserx.github.io/paperless-telegram-bot/getting-started/): what you need first, Docker, Docker Compose, from source, and what a working start looks like
- [Configuration](https://geiserx.github.io/paperless-telegram-bot/configuration/): every environment variable and its default, and the security notes
- [Usage](https://geiserx.github.io/paperless-telegram-bot/usage/): a session step by step: upload, tags, search, download, inbox
- [How it works](https://geiserx.github.io/paperless-telegram-bot/how-it-works/): the code layout and the design decisions
- [Troubleshooting](https://geiserx.github.io/paperless-telegram-bot/troubleshooting/): symptom, cause, fix
- [Development](https://geiserx.github.io/paperless-telegram-bot/development/): tests, linting, contributing
- [Related projects](https://geiserx.github.io/paperless-telegram-bot/related/): the other Telegram bots and tools
- [Roadmap](https://github.com/GeiserX/paperless-telegram-bot/blob/main/docs/ROADMAP.md)

## License

[GPL-3.0-or-later](https://github.com/GeiserX/paperless-telegram-bot/blob/main/LICENSE)
