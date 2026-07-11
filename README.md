# portfolio-data

Content for [aravindkumar.tech](https://aravindkumar.tech) — this repo **is the CMS**.
The live site fetches `data.json` at runtime, so anything edited here appears
on the site in **~1–5 minutes, no redeploy needed**. If a fetch ever fails or
the JSON is broken, the site silently falls back to its built-in content — an
edit here can never take the site down.

## How to update things

| To change… | Edit… |
|---|---|
| Projects | `projects` array in `data.json` |
| Certificates | `certificates` array in `data.json` |
| Skills / planet colors | `skillCategories` in `data.json` |
| Client & peer reviews | `reviews` array in `data.json` (see below) |
| Hero name / roles / tagline / availability badge | `hero` in `data.json` |
| Social + resume links | `links` in `data.json` |
| Section titles & subtitles | `sections` in `data.json` |
| Resume file | upload the new PDF over `resume/` (keep the same filename) |
| Certificate images | upload to `images/certs/` |

Edit straight on github.com or in the GitHub mobile app → commit to `main`.

## Adding a review

The Reviews section is hidden until this array has at least one entry.
Copy this into the `reviews` array:

```json
{
  "name": "Client Name",
  "role": "Owner",
  "company": "Cherries Cafe",
  "message": "What they said about working with you…",
  "rating": 5,
  "avatarUrl": ""
}
```

- `rating`: 1–5 stars, or `0` to hide the stars.
- `avatarUrl`: leave `""` to show gradient initials, or upload a photo to
  `images/avatars/` and use its jsDelivr URL (pattern below).

## File URLs (jsDelivr CDN)

Every file in this repo is served free by jsDelivr:

```
https://cdn.jsdelivr.net/gh/aravindpunyamantula/portfolio-data@main/<path>
```

e.g. `…@main/images/certs/mongodb-associate.png`

⚠️ jsDelivr caches files for up to 12 hours. `data.json` is fetched from
`raw.githubusercontent.com` instead (updates in ~1–5 min). For **images** you
replace, prefer a *new filename* (e.g. `resume-2026.pdf`) if you need the
change visible immediately.

## TODO

- [ ] `images/certs/oracle-database.png` — missing, upload the badge/certificate
      image (the old LinkedIn URL expired).
- [ ] `images/certs/java-programming.png` — missing, upload the certificate
      image (the old LinkedIn URL expired).
- [ ] `resume/` — upload your resume PDF, then point `links.resume` in
      `data.json` at its jsDelivr URL (currently still Google Drive).
