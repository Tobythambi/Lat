# AR Wall — New Project

Multi-target WebAR page. Scan a printed picture, matching video plays over it.
Built the same way as the Perak Museum wall (MindAR + A-Frame, GitHub Pages),
in a brand-new repo.

## Folder layout

```
/
├── index.html            # the AR page (already built, 20 targets wired up)
├── compile-targets.html  # open this in a browser to generate targets.mind
├── targets.mind          # ← you generate this via compile-targets.html
├── targets/              # your 20 source photos (already included: 01.jpg...20.jpg)
├── media/                # put your 20 videos here, named to match target index
│   └── target-0.mp4 ... target-19.mp4
└── README.md
```

## Step 1 — Compile targets.mind from your 20 photos

Open `compile-targets.html` directly in a browser (double-click it, or drag it
into a Chrome/Firefox tab — no server needed, it runs entirely client-side).

1. Click the drop zone, select all 20 photos in `targets/` (01.jpg…20.jpg) at once
2. They're auto-sorted by filename, so 01.jpg → index 0, 02.jpg → index 1, … 20.jpg → index 19
3. A preview grid shows each photo with its index — **check this matches what you expect**
4. Click "Compile targets.mind" (takes ~30–60s for 20 targets)
5. Click "Download targets.mind" and put the file in the root of this project (next to `index.html`)

The tool also prints the final index → filename mapping in the status box —
keep that, you'll need it for Step 2.

**Important — the lesson from the museum project:** once compiled you can't
just "rename" a target's meaning. The index order it compiled to is final —
match your video filenames to it exactly, not to your intended order.

## Step 2 — Name and place your videos

Rename your 20 videos to `target-0.mp4`, `target-1.mp4`, ... `target-19.mp4`,
matching the **actual compiled index** from Step 1 (not upload order), and
drop them in `media/`.

## Step 3 — Push to a new GitHub repo

```bash
cd ar-new-project
git init
git add .
git commit -m "Initial AR wall — 20 targets"
git branch -M main
git remote add origin https://github.com/Tobythambi/<NEW-REPO-NAME>.git
git push -u origin main
```

Then enable GitHub Pages: repo Settings → Pages → Source: `main` branch, `/root`.

## Step 4 — Known pitfalls (from the last project, already handled here)

- **Camera feed invisible even though it's working**: `#ar-container` needs an
  explicit `z-index`, or in some browsers MindAR's camera `<video>`
  (`z-index: -2`) gets buried behind the page background. Already fixed in
  this `index.html`.
- **Never rename a `.mind` file after uploading to GitHub via the web editor** —
  it routes through GitHub's text editor and silently corrupts the binary
  file. Always type the correct filename before uploading, or point the code
  at whatever name the working upload actually has.
- **Index mismatch = wrong video plays**: always verify the compiler's index
  order against your intended photo order before wiring up `media/target-N.mp4`
  filenames. This bit the museum project (picture 8 ended up missing, others
  shuffled).

## Testing

Serve locally over HTTPS (camera access requires it) or just push to GitHub
Pages and test on the live URL. Point the camera at each printed photo and
confirm the correct video plays — check all 20 before printing/deploying.
