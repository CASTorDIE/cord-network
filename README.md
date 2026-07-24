# CORD Network Static Site

Clean first-pass static site for the community homepage.

## Files

- `index.html` renders the site.
- `data/site-feed.json` is the only public data file the page reads.
- `data/live.json` is the clean public Who's Live feed.
- `data/schedule.json` is the clean public Scheduler feed.

## Work PC Contract

The hosted site is static. Its public JSON feed is published separately at `CASTorDIE/cord-network-feed`, so routine updates do not trigger GitHub Pages builds.

For this first pass, the feed contains:

- `live.streamers[]`
- or the dedicated `data/live.json`
- `schedule.entries[]` or the dedicated `data/schedule.json`
- `events.items[]`
- `blog.items[]`
- `sources` metadata for freshness/status display

Live and schedule can be generated from existing local data. Events and Blog are manually curated entries for now.

Publish the current public JSON snapshot after local builders update it:

```powershell
node ..\..\scripts\publishCordNetworkFeed.js
```

`scripts\runFetchTwitchData.cmd` runs the Twitch fetch and then publishes the clean feed. The public page rechecks the feed every five minutes.

Build the clean Who's Live feed from the local Twitch snapshot:

```powershell
node ..\..\scripts\buildLevelTogetherLive.js
```

The normal Twitch fetch script also writes it automatically:

```powershell
node ..\..\scripts\fetchTwitchData.js
```

Build the clean Scheduler feed from the local Scheduler store:

```powershell
node ..\..\scripts\buildLevelTogetherSchedule.js
```

## Local Preview

From this folder:

```powershell
python -m http.server 8080
```

Then open `http://127.0.0.1:8080/`.
