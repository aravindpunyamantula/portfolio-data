# portfolio-data

Content for [aravindkumar.tech](https://aravindkumar.tech) — **this repo is the CMS**.
The live site fetches `data.json` at runtime, so anything edited here appears
on the site in **~1–5 minutes, no redeploy needed**. If a fetch fails or the
JSON is broken, the site silently falls back to its built-in content — an edit
here can never take the site down.

---

## Quick reference — what to edit

| To change… | Edit… |
|---|---|
| Projects | `projects` array in `data.json` |
| Certificates | `certificates` array in `data.json` |
| Skills / planet colors | `skillCategories` in `data.json` |
| Client & peer reviews | `reviews` array in `data.json` |
| Hero name / roles / tagline / availability badge | `hero` in `data.json` |
| Social + resume links | `links` in `data.json` |
| Section titles & subtitles | `sections` in `data.json` |
| Order things appear in | `order` field on each project / certificate |
| Resume file | upload PDF to `resume/` |
| Certificate images | upload to `images/certs/` (guide below) |

Edit straight on github.com (pencil icon on `data.json`) or in the GitHub
mobile app → commit to `main`. Done.

---

## How images work (read this once)

Every file in this repo automatically gets a **free CDN URL** from jsDelivr:

```
https://cdn.jsdelivr.net/gh/aravindpunyamantula/portfolio-data@main/<path-inside-repo>
```

So a file at `images/certs/mongodb-associate.png` is served at:

```
https://cdn.jsdelivr.net/gh/aravindpunyamantula/portfolio-data@main/images/certs/mongodb-associate.png
```

That URL is what goes into `data.json`.

### Adding a certification image, step by step

1. Get the image: download the badge from Credly/Oracle/Cisco, or screenshot
   your certificate. PNG or JPG, ideally 400–800 px wide, under ~300 KB.
2. Name it simply, lowercase with dashes: `aws-cloud-practitioner.png`.
3. On github.com open this repo → `images/certs/` folder → **Add file →
   Upload files** → drop the image → **Commit changes**.
   (Mobile app: same flow from the folder view.)
4. Build its URL using the pattern above:
   `https://cdn.jsdelivr.net/gh/aravindpunyamantula/portfolio-data@main/images/certs/aws-cloud-practitioner.png`
5. Open `data.json`, add or edit an entry in `certificates` and paste that
   URL into `imageUrl`:

```json
{
  "order": 5,
  "title": "AWS Cloud Practitioner",
  "organisation": "Amazon Web Services",
  "date": "August 2026",
  "link": "https://link-to-verify-page",
  "skills": ["AWS", "Cloud"],
  "imageUrl": "https://cdn.jsdelivr.net/gh/aravindpunyamantula/portfolio-data@main/images/certs/aws-cloud-practitioner.png"
}
```

6. Commit. The site picks it up within minutes.

⚠️ **Cache rule:** jsDelivr caches a URL for up to 12 hours. Uploading a NEW
filename is instant; REPLACING an existing file keeps serving the old one for
a while. So when you update an image, prefer a new name
(`mongodb-associate-v2.png`) and update the URL in `data.json`.

### Avatars for reviews

Same idea, different folder: upload to `images/avatars/`, use
`…@main/images/avatars/<file>` as `avatarUrl`. Leave `""` for gradient
initials (looks fine without a photo).

### Resume

Upload your PDF to `resume/` (e.g. `resume/Aravind_Kumar_Resume.pdf`), then
set in `data.json`:

```json
"resume": "https://cdn.jsdelivr.net/gh/aravindpunyamantula/portfolio-data@main/resume/Aravind_Kumar_Resume.pdf"
```

To update the resume later, upload with a new filename (see cache rule) and
change the link.

---

## Ordering projects & certificates

Every project and certificate has an `"order"` number — **lower shows
first**. Current entries use 10, 20, 30… so you can slot something between
two items without renumbering everything (e.g. `15` goes between 10 and 20,
`5` goes first). Items missing `order` sink to the end.

## Adding a review

The Reviews section is **hidden until this array has at least one entry**
(one dummy entry is in there now — replace it with a real client's words, or
delete it to hide the section):

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

- `rating`: 1–5 stars, or `0` to hide the stars for that review.
- `role` / `company` appear as "Role · Company" under the name; either may
  be `""`.

## Field reference (`data.json`)

- `hero.greeting` — small line above your name ("Hi, I'm")
- `hero.name` / `hero.nameShort` — desktop / mobile headline
- `hero.roles` — the rotating titles under your name
- `hero.tagline` — paragraph under the roles
- `hero.availability` + `hero.showAvailability` — the green-dot badge text
  and whether it shows at all
- `hero.footerTagline` — line under your name in the footer
- `hero.currentlyBuilding` — the "Building: …" live ticker chip in the hero.
  Update it whenever you start something new (great from the GitHub app!);
  set to `""` to hide the chip
- `links.*` — github, linkedin, instagram, email (`mailto:…`), resume
- `sections.<projects|skills|certificates|reviews|contact>` — each section's
  `eyebrow` (small caps label), `title`, `subtitle`
- `projects[]` — `order`, `title`, `description`, plus **one of**:
  `liveUrl` (renders a live iframe preview) or `githubUrl` (renders the
  repo's README). If both are set, `liveUrl` wins.
- `certificates[]` — `order`, `title`, `organisation`, `date`, `link`
  (Verify button; `""` hides it), `skills` (chips), `imageUrl`
- `skillCategories[]` — `title`, `color` (hex like `"#6366F1"`, tints the
  planet and its orbit), `skills` (orbiting chips)
- `reviews[]` — see above

**Rule of thumb:** any field you omit falls back to the site's built-in
value, and if the whole file is unreachable or invalid the site still works.
You cannot break the site from here — worst case your edit is just ignored.

## TODO

- [ ] `images/certs/oracle-database.png` — missing, upload the badge/certificate
      image (the old LinkedIn URL expired). The `data.json` entry already
      points at this exact path, so just uploading the file fixes the card.
- [ ] `images/certs/java-programming.png` — same as above.
- [ ] Upload resume PDF to `resume/` and point `links.resume` at it
      (currently still Google Drive).
- [ ] Replace the dummy entry in `reviews` with a real client review.
