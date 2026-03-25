# Audio Setup Guide – Leipzig Sound Walk

## Overview

The sound walk plays location-specific audio when users are within proximity of each point on the map. For this to work, each database location needs an `audioUrl` pointing to a real audio file.

---

## Step 1: Add Your Audio Files

Place your MP3 files in the `public/audio/` directory with these exact filenames:

| # | Location | Filename |
|---|----------|----------|
| 1 | Thomaskirche | `thomaskirche.mp3` |
| 2 | Marktplatz | `marktplatz.mp3` |
| 3 | Nikolaikirche | `nikolaikirche.mp3` |
| 4 | Mädler-Passage | `maedler-passage.mp3` |
| 5 | Augustusplatz | `augustusplatz.mp3` |
| 6 | Gewandhaus Forecourt | `gewandhaus-forecourt.mp3` |
| 7 | Johannapark | `johannapark.mp3` |
| 8 | Karl-Liebknecht-Straße | `karli.mp3` |
| 9 | Clara-Zetkin-Park Entrance | `clara-zetkin-park.mp3` |
| 10 | Baumwollspinnerei Gate | `baumwollspinnerei.mp3` |
| 11 | Plagwitz Canal | `plagwitz-canal.mp3` |
| 12 | Hauptbahnhof Main Hall | `hauptbahnhof.mp3` |
| 13 | Völkerschlachtdenkmal | `voelkerschlachtdenkmal.mp3` |
| 14 | Schiller Park | `schiller-park.mp3` |
| 15 | Connewitz Kreuz | `connewitz-kreuz.mp3` |

### Recommended Audio Format
- **Format:** MP3
- **Bitrate:** 128–192 kbps
- **Size:** ≤ 5 MB per file (for fast mobile loading)
- **Duration:** 1–5 minutes per location

---

## Step 2: Update the Database with Audio URLs

The seed script (`scripts/seed.ts`) already includes `audioUrl` values for all 15 locations. Run it to populate or update your database:

```bash
# Locally (requires DATABASE_URL in .env)
npx tsx --require dotenv/config scripts/seed.ts

# Or via Prisma
npx prisma db seed
```

If locations already exist in the database, the script will **update** them to set `audioUrl` only if it's currently `null` – it won't overwrite custom URLs you've set via the admin panel.

---

## Step 3: Commit & Deploy

```bash
# Add your audio files to the repo
git add public/audio/*.mp3
git commit -m "Add audio files for sound walk locations"
git push
```

Then redeploy. The files in `public/audio/` are served directly by Next.js as static assets – fast, no external service needed.

---

## Alternative: Upload via Admin Panel

You can also upload audio files through the admin panel at `/admin`. This uploads to cloud storage (S3), which works but may be slightly slower than local files. Use this for adding new locations or replacing individual files without redeploying.

---

## Troubleshooting

- **No sound?** Check that the file exists at the exact path (e.g., `/audio/thomaskirche.mp3`)
- **Slow loading?** Compress files to 128kbps MP3, keep under 5MB
- **Google Drive links?** The app auto-converts sharing links, but direct files are faster
