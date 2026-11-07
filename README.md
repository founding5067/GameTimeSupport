# GameTimeSupport

The data file the GameTime app fetches for its game list, username words, avatar emoji, and the reactions and quick replies friends can leave on a session. There is no code in this repo, only `gametime.json`.

Raw file:

```
https://raw.githubusercontent.com/founding5067/GameTimeSupport/main/gametime.json
```

The GameTime privacy policy is in [PRIVACY.md](PRIVACY.md), the terms are in [TERMS.md](TERMS.md), and help and contact info is in [SUPPORT.md](SUPPORT.md).

## At a glance

| Key | What it holds | Entries |
| --- | --- | --- |
| `version` | Data version number | n/a |
| `minimumVersion` | Oldest app version allowed to run | n/a |
| `games` | Games people can pick from | 129 |
| `username.prefixes` | First word of a display name | 33 |
| `username.suffixes` | Second word of a display name | 33 |
| `username.blockedNumbers` | Digit strings banned from names | 7 |
| `username.suffixEmoji` | Suffix to emoji for the Shuffle button | 33 |
| `avatar.emoji` | Profile picture options | 79 |
| `reactions` | Emoji reactions on a session | 5 |
| `quickReplies` | Canned replies on a session | 20 |
| `freeNotes` | Notes that can go with "Free tonight" | 6 |

## Field reference

### `version`

A number, bumped whenever the data changes.

### `minimumVersion`

The oldest app version that may keep running, such as `"2.0"`: a dotted number, compared part by part, so `1.10` is newer than `1.9`. A build below it shows "Please update" and nothing else. The app checks it with its weekly download and remembers the last answer, so it holds offline. Only builds from the one that introduced this check onward read it; older builds ignore it. Leave it at `"1.0"` (nobody is blocked) until the new build is live on the App Store, then raise it to that build's version. A value that isn't a version is ignored.

### `games`

The list people pick from when creating a session and when adding to My Games. The search box filters it as they type.

The app cleans, dedupes and sorts the names alphabetically, so the order in the file doesn't affect what users see.

### `username.prefixes` and `username.suffixes`

The two words of a display name, such as `Brave` and `Fox`. A name is prefix + suffix + an optional number of up to 3 digits, like `BraveFox42`.

Each entry must be letters only (no spaces, digits or symbols) and at most 13 characters. Entries that fail are dropped silently.

### `username.blockedNumbers`

Digit strings that can't appear in a name's number. Any number that contains one is blocked, so `69` also blocks 169 and 690.

If the file leaves this key out, the app uses its own built-in list. If the key is present, your list replaces the built-in one entirely, so include every number you want blocked.

### `username.suffixEmoji`

Maps a suffix to an emoji for the Shuffle button, e.g. `"Fox": "🦊"`.

An entry only counts if that emoji is also in `avatar.emoji`. A suffix with no entry, or with an emoji the picker doesn't offer, gets a random emoji from the list.

### `avatar.emoji`

The profile picture options. The order in the file is the order in the grid.

Each entry must be exactly one emoji. Letters, digits and two emoji in one entry are dropped.

### `reactions`

The emoji friends can react to a session with, in the order the bar shows them. Each entry is `{ "emoji": "🔥", "name": "Fire" }`. `name` is what VoiceOver reads and may be left out. At most 8 are kept.

The emoji is what gets saved with each reaction, so it is the entry's ID. Each entry must be exactly one emoji. Anything else is dropped.

### `quickReplies`

The canned replies friends can leave on a session, and that people pick from in Settings > Quick replies. Nobody can type their own, so only what's in this list can ever show up. Each entry is `{ "id": "onMyWay", "text": "On my way" }`, in the order the picker shows them.

- `id` is what gets saved with every reply and in people's settings. Letters, digits, dashes and underscores, at most 32 characters.
- `text` is what people read, at most 30 characters.
- `"retired": true` takes a reply out of the picker, but it still shows on the sessions it was already left on. Use it instead of deleting an entry.

An ID the app has never heard of is never shown, even if someone writes one into a session. A friend whose copy of this file is a few days old won't see a newly added reply until their app downloads it, which happens about once a week.

### `freeNotes`

The notes someone can add when they tell friends they're free tonight, such as "Down for anything". Nobody can type their own. It follows the same rules as `quickReplies`: each entry is `{ "id": "downForAnything", "text": "Down for anything" }`, `id` is saved on the person's profile and never changes meaning, `text` is at most 30 characters, and `"retired": true` takes a note out of the menu while friends who already set it still read. At most 20 are kept.

## Editing the data

- Keep `games`, `prefixes` and `suffixes` alphabetical with no duplicates.
- Leave `avatar.emoji` in display order. Don't sort it.
- When you add a suffix, add its `suffixEmoji` entry, and make sure that emoji is in `avatar.emoji`.
- Never change what an `id` or reaction emoji means, and never reuse one. Fix a typo in `text`, but to drop a reply mark it `"retired": true` rather than deleting it.
- Keep at least 10 `quickReplies` that aren't retired, since Pro lets people pick that many.
- `freeNotes` follow the same ID rules as `quickReplies`. Keep at least one that isn't retired.
- Keep entries family-friendly, since users see them.
- Only raise `minimumVersion` once the build it names can be downloaded, or people will be told to update to something that isn't there.
- Bump `version`.
- Check the file still parses: `python3 -m json.tool gametime.json > /dev/null`

## Requesting changes

Open an [issue](../../issues/new/choose) and pick a form to request a new game, avatar emoji, username prefix or suffix, quick reply or reaction (use "other"), or any other change to the data.

`.github/CODEOWNERS` makes @founding5067 the owner of every file, so changes need their review.

## Disclaimer

The game titles in `gametime.json` are a plain list of names. I don't own, make or claim any of these games, and this project isn't affiliated with, endorsed by or sponsored by any of their developers or publishers. All game names and trademarks belong to their respective owners.
