# Setting up your al-folio site (devesh1508.github.io)

## Step 1 — Clear the way
Your current repo `devesh1508.github.io` holds the old single-page site.
Rename it (Settings → General → Repository name) to something like `old-site`
so the name is free. (Or delete it if you don't want to keep it.)

## Step 2 — Create the site from the template
1. Go to https://github.com/alshedivat/al-folio
2. Click the green "Use this template" button → "Create a new repository"
3. Name it exactly: devesh1508.github.io  (Public)

## Step 3 — Enable the build
1. In the new repo: Settings → Pages → under "Build and deployment",
   set Source to "GitHub Actions".
2. Go to the Actions tab. If prompted, click "I understand my workflows,
   go ahead and enable them."

## Step 4 — Upload your content (this package)
Upload the files from this zip into the repo, REPLACING the originals
at the same paths:

    _config.yml                  (replace)
    _data/socials.yml            (replace)
    _pages/about.md              (replace)
    _pages/videos.md             (new)
    _pages/blog.md, cv.md, dropdown.md, profiles.md,
      projects.md, repositories.md, teaching.md   (replace — hides demo pages)
    _bibliography/papers.bib     (replace)
    _news/  (6 files)            (add; delete the 3 announcement_*.md demo files)
    assets/img/prof_pic.jpg      (add)
    assets/pdf/CV_DKJ.pdf        (add)

Easiest way: on the repo page, press "." (period) to open github.dev in the
browser, drag folders in, commit. Or use "Add file → Upload files" folder
by folder.

Optional cleanup (nice, not required): delete the sample content in
_posts/, _projects/, _books/, _teachings/ and _pages/about_einstein.md.

## Step 5 — Wait for the build
Actions tab → the "deploy" workflow runs on every commit (takes ~2-5 min).
Green check = live at https://devesh1508.github.io

## Adding a paper later
Open _bibliography/papers.bib → paste the BibTeX entry (from Google
Scholar's "cite" button) → add `selected = {true}` if you want it on the
homepage → commit. That's it.
