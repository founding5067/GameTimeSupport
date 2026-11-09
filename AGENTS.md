# GameTimeSupport

## Git

**Never commit or push without the user's explicit approval.** Approval for one commit or push doesn't carry over to the next.

## What this is

The public support repo for the GameTime app. There is no code here. It holds:

- `gametime.json`, the data file the app downloads about once a week for its game list, username words, avatar emoji, reactions and quick replies. The app reads it from `raw.githubusercontent.com/founding5067/GameTimeSupport/main/gametime.json`, so only what's on `main` reaches users.
- `PRIVACY.md` and `TERMS.md`, the Privacy Policy and Terms of Use, linked from the app's Settings. The app links to the `main` branch.
- `README.md`, the field reference for `gametime.json`.
- `.github/`, with `CODEOWNERS` and the issue forms for requesting new games, emoji and username words.

## Editing `gametime.json`

The rules are in `README.md` under "Editing the data". The short version:

- Keep `games`, `prefixes` and `suffixes` alphabetical with no duplicates. Leave `avatar.emoji` in display order.
- A new suffix needs a `suffixEmoji` entry, and that emoji must be in `avatar.emoji`.
- Prefixes and suffixes are letters only, at most 13 characters. Each avatar emoji is exactly one emoji.
- `username.blockedNumbers` replaces the app's built-in list when present, so include every number to block.
- Keep entries family-friendly.
- Raise `minimumVersion` only once the build it names is live on the App Store. `"isAppActive": false` shuts the app down after the age check, and so does a file the app can't fetch or read, so never push a `gametime.json` that doesn't parse. Bump `version` whenever the data changes.
- Check it still parses: `python3 -m json.tool gametime.json > /dev/null`
- `reactions` entries are `{ emoji, name }` with exactly one emoji, at most 8. `quickReplies` entries are `{ id, text, retired? }`: ids are letters, digits, `-` and `_` (at most 32), text is at most 30 characters. Never rename or reuse an id or emoji (records and settings store them); retire a reply with `"retired": true` instead of deleting it. Keep at least 10 replies not retired. `freeNotes` entries use the same `{ id, text, retired? }` shape and rules (at most 20); keep at least one not retired.
- Update the entry counts in the `README.md` table when they change.

## Policy documents

- Write `PRIVACY.md` and `TERMS.md` in plain first person, in short sections, and change "Last updated" when they change.
- Don't promise what the developer can't do. People's content lives in their own iCloud, so the developer can't remove it or ban anyone. The only things readable are `Report` records in the public CloudKit database.
- Keep the two documents consistent with each other and with how the app behaves.

## Other

- Game titles are only a plain list of names. Keep the disclaimer in `README.md`.
- `.github/CODEOWNERS` makes `@founding5067` the owner of every file.
