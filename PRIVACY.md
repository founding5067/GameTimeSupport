# GameTime Privacy Policy

Last updated: October 26, 2026

GameTime lets you post when you're playing a game and see when your friends are. This page explains what the app keeps, where it keeps it, and who can see it. It covers the iPhone app listed on the App Store as "GameTime: Game Session Planner" (called GameTime below).

## The short version

- There are no accounts, no ads, no analytics and no tracking.
- Your data lives in your own iCloud. I can't read it.
- Only friends you invite can see your sessions.
- The one thing I can read is a report you send about someone.
- You can erase everything from Settings > Delete my data.

## What is stored in your iCloud

GameTime uses CloudKit, Apple's iCloud storage for apps. Everything below is saved in your private iCloud database, under your Apple Account. I (the developer) have no access to it.

- Your profile: display name, emoji, color, and any ring or effect you picked.
- Sessions you host, who is on each one, and your copies of past sessions.
- Your all-time Hosted and Joined totals.
- Settings that follow your account: Hide my stats, My games, new session defaults, the clock, and your notification switches.
- Your nicknames for friends, and your muted and blocked lists. These are never shared.

## What your friends can see

When you accept someone's invite link, or they accept yours, you each share a read-only copy of your sessions and profile with the other, and a place where friends can add themselves to a session. Friends can see:

- Your profile and your sessions.
- Who is on each session.
- Your Hosted and Joined totals, unless you turn on Hide my stats.

People who aren't your friends can't see your sessions or profile. Anyone with your invite link can become your friend, so share it carefully. You can remove or block a friend from their profile at any time, and that ends their access.

When a friend's session changes, the app leaves a short notice (a title, a message and the session's ID) in the other person's iCloud so their device can show a notification. These notices are deleted after 24 hours.

A friend's app keeps its own copy of a session once it has ended. That copy can include the names of people who were on it, and it stays on their side. If you later remove or block that friend, your name is taken off their kept copies of sessions you shared.

## Reports

If you report a profile or session, the report is saved to a public CloudKit database that only I can read. A report contains:

- The reason you picked and the optional note you wrote.
- Your iCloud user ID and the reported person's iCloud user ID.
- The reported person's display name.
- For a session report: the session's ID and game title.
- The app version.

I use reports only to review and act on what was reported. Delete my data does not remove reports. To have a report removed, email me at the address below.

## The game list (GitHub)

The games, name words and avatar emoji you pick from come from a file in this repository, `gametime.json`. About once a week the app downloads it from `raw.githubusercontent.com`. The request carries nothing about you or your account, but like any web request it reveals your IP address to GitHub. See [GitHub's privacy statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement) for how GitHub handles that. I don't see those requests.

## What stays on your device

Calendar events, reminders, Live Activities and the widget are made on your device from your sessions. They aren't sent anywhere else. Calendar and notification access are optional, and you can turn them off in Settings or in your device's settings.

## Purchases

GameTime Pro and the Supporter Pack are handled by Apple. I never see your payment details.

## Delete my data

Settings > Delete my data erases your profile, sessions, friends and history from iCloud, and the settings and calendar events saved on your device. Upcoming sessions you host are cancelled, and your friends are told. Then the app starts you fresh with a new random profile. Your purchases aren't affected.

It can't remove:

- Your name on past sessions that friends kept their own copies of.
- Reports you sent or that were sent about you (email me to have one removed).

Deleting the app doesn't delete your iCloud data. Use Delete my data first.

## Children

GameTime doesn't ask for your age and isn't built for children under 13.

## Changes

If this policy changes, the date at the top changes with it, and the history is in this repository.

## Contact

Questions, or a request to remove a report: dev@colebraswell.com
