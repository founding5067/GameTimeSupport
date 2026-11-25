# GameTimeSupport

The data file the GameTime app fetches for its game list and its on/off and minimum-version switches. Everything else people pick from (tags, platforms, reactions, quick replies, Free now notes, name words, blocked numbers and avatar emoji) is built into the app. There is no code in this repo, only `gametime.json`.

Raw file:

```
https://raw.githubusercontent.com/founding5067/GameTimeSupport/main/gametime.json
```

The GameTime privacy policy is in [PRIVACY.md](PRIVACY.md), the terms are in [TERMS.md](TERMS.md), and help and contact info is in [SUPPORT.md](SUPPORT.md).

## At a glance

| Key | What it holds | Entries |
| --- | --- | --- |
| `version` | Data version number | n/a |
| `isAppActive` | Whether the app runs at all | n/a |
| `minimumVersion` | Oldest app version allowed to run | n/a |
| `games` | Games people can pick from | 221 |

## Field reference

### `version`

A number, bumped whenever the data changes.

### `isAppActive`

The off switch: `true` or `false`, without quotes. The app asks for this file **every time it opens or comes to the front** (at most once a minute after a good answer), and what it does depends on the answer:

| The file says | The app shows |
| --- | --- |
| `"isAppActive": true`, or no `isAppActive`, or something that isn't `true` or `false` | the app, as normal |
| `"isAppActive": false` | after the age check, a message that GameTime has shut down |
| nothing readable: the file is gone (404), GitHub is down or rate limiting, the phone is offline, or the file isn't valid JSON | the same shutdown message, until a later check works |

So **a broken `gametime.json` shuts the app down for everyone who opens it**, and so does a GitHub outage or an offline phone. A good answer brings the app back by itself. `raw.githubusercontent.com` caches for a few minutes, so a change can take that long to arrive. Builds from before this field existed ignore it. Leave it `true` and set it to `false` only when you mean to shut the app down.

### `minimumVersion`

A dotted version in quotes, such as `"2.0"`, compared part by part (`1.10` is newer than `1.9`). If it is above the installed version, the app shows "Please update" before anything else. With no `minimumVersion`, or something that isn't a version, the app runs as normal. Leave it at `"1.0"` (nobody is blocked) until the build you want to require can be downloaded.

### `games`

The list people pick from when creating a session and when adding to My Games. The search box filters it as they type.

The app cleans, dedupes and sorts the names alphabetically, so the order in the file doesn't affect what users see.

## Editing the data

- Keep `games` alphabetical with no duplicates.
- Keep entries family-friendly, since users see them.
- Only raise `minimumVersion` once the build it names can be downloaded, or people will be told to update to something that isn't there. Set `isAppActive` to `false` only when you mean to shut the app down.
- Check the file parses before every push (`python3 -m json.tool gametime.json > /dev/null`): a file the app can't read shuts it down.
- Bump `version`.

## Requesting changes

Open an [issue](../../issues/new/choose) and pick a form to request a new game or any other change to the data. The other pick lists live in the app, so they aren't changed here.

`.github/CODEOWNERS` makes @founding5067 the owner of every file, so changes need their review.

## Disclaimer

The game titles in `gametime.json` are a plain list of names. I don't own, make or claim any of these games, and this project isn't affiliated with, endorsed by or sponsored by any of their developers or publishers. All game names and trademarks belong to their respective owners.
