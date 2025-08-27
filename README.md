# CloudLab

This repo contains all the files I use to run my personal
infrastructure. If I owned and operated the hardware, it would be a
homelab, but I do not so it is the _CloudLab_. Humorous.

The system is designed with the **explicit goals** of being **elegant,
declarative, and robust.**

## List of Services
1. Ingress → [Caddy]
2. Automatic updates → [Watchtower]
3. Backups → [Tarsnap]
4. Email → [Maddy] and [rspamd]
5. Calendar and contacts → [Radicale]
6. Passwords → [Vaultwarden]
7. Websites
    1. [figbert.com]
    2. [blinddateabook.com]
    3. [systemcolors.xyz]
8. RSS Reader → [Miniflux]
9. Bookmarks → [Linkding]
10. Livestreams → [Owncast]
11. File sync → [Syncthing]

## Architecture
**All programs are run in a single logical Docker Compose instance,
without exception.** The configuration is split throughout several,
domain-oriented files in `definitions/` imported from the primary
`compose.yml` at root.

Individual services store their settings (version-controlled) and data
in the `services/` folder. This entire folder is included in backups.
Secrets are committed directly to the repository using [SOPS].

Container images are not built anywhere on the server, as that would
violate the directive above concerning _activity happening outside of
Compose_. Instead, third-party containers are pulled from various online
registries and bespoke images pushed to the server via the [unregistry].

Concision in this repository is a virtue. It indicates a delegation of
concerns—leaving the aspects of running infrastructure best managed by
experts, or reliant on consistent updates, to be managed elsewhere.

[Caddy]: https://caddyserver.com
[Watchtower]: https://containrrr.dev/watchtower/
[Tarsnap]: https://github.com/FIGBERT/acts-docker
[Maddy]: https://maddy.email/
[rspamd]: https://rspamd.com/
[Radicale]: https://radicale.org/v3.html
[Vaultwarden]: https://github.com/dani-garcia/vaultwarden
[figbert.com]: https://figbert.com
[blinddateabook.com]: https://blinddateabook.com
[systemcolors.xyz]: https://systemcolors.xyz
[Miniflux]: https://miniflux.app/
[Linkding]: https://linkding.link/
[Owncast]: https://owncast.online/
[Syncthing]: https://syncthing.net/
[SOPS]: https://getsops.io/
[unregistry]: https://github.com/psviderski/unregistry
