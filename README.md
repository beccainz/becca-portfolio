# Becca Inz — Portfolio Site

A no-build-step portfolio site (Home, Work, Playground, About) built with plain HTML/CSS/JS. Hash-based routing means it works as a static site with zero server configuration, perfect for GitHub Pages.

This download includes `index.html` plus four media files (two videos, two poster images) that sit right next to it, at the same level, not inside a subfolder. GitHub's drag-and-drop upload doesn't reliably preserve folder structure, so keeping everything flat avoids that entirely.

## Publish it to GitHub Pages

1. **Create a repository on GitHub.**
   Go to [github.com/new](https://github.com/new), name it something like `becca-portfolio`, and create it (public, so Pages can serve it for free).

2. **Add all five files to the repo.**
   Unzip this download, then on the repo's main page click "Add file" → "Upload files," and drag in `index.html` and all four media files together, in one drop (don't drag the folder itself, drag the files inside it). Scroll down and commit.

3. **Turn on GitHub Pages.**
   In the repo, go to **Settings → Pages**. Under "Build and deployment," set **Source** to "Deploy from a branch," pick the **`main`** branch and the **`/ (root)`** folder, then save.

4. **Visit your site.**
   GitHub will give you a URL like `https://<your-username>.github.io/becca-portfolio/`, it usually takes a minute or two to go live after the first push.

That's it, no build tools, no `npm install`, no config files. Any time you want to update the content, re-upload `index.html` (or the specific files that changed) the same way.

## Editing content later

Everything on the site is driven by one JavaScript array near the top of the `<script>` block, called `PROJECTS`, in `index.html`. Each project is one object (title, client, year, tags, and the full case-study fields). To add a new project, copy an existing object in that array and edit the fields, the Work and Playground grids, the filters, and the case-study page template all render from that array automatically, so nothing else needs to change.

To edit any of this on GitHub without installing anything: open the repo, click into `index.html`, then click the pencil ("Edit this file") icon in the top right of the file view. Make your change, scroll down, and click "Commit changes." Pages redeploys automatically within a minute or two.

## Adding more photos and videos

The site ships with placeholder color blocks standing in for real creative on projects that don't have real media yet. To swap one in:

1. **Upload the file to the repo root.** On the repo's main page, click "Add file" → "Upload files," and drag in your image or video directly (no folder needed, keep it flat like the existing media files). Commit.

2. **Point a project at it.** Open `index.html` (pencil icon to edit), find the project in the `PROJECTS` array, search (Ctrl/Cmd+F in your browser) for the project's `id`, e.g. `id:"dna-science-to-so-my-dog"`. Add a `media` line right after it:
   ```js
   media:{type:"image", src:"dna-hero.jpg"},
   ```
   or for video:
   ```js
   media:{type:"video", src:"dna-hero.mp4", poster:"dna-hero-poster.jpg"},
   ```
   (`poster` is optional, a still frame shown before the video plays.) This swaps the placeholder used for that project's card thumbnail and its case-study hero media.

3. **Swap a gallery image.** Inside that same project, find the `gallery: [ ... ]` array further down. Each entry is one placeholder block; add a `media` field to any of them the same way:
   ```js
   {ratio:"16/9", format:"BRAND FILM · 16:9", label:"Hero", hue:"a", caption:"...", media:{type:"image", src:"dna-gallery-1.jpg"}}
   ```

4. **Change your headshot.** Search `index.html` for `const PORTRAIT`, it's currently set to an embedded photo. Replace the whole line with a new photo the same way as above, or with `const PORTRAIT = {type:"image", src:"new-portrait.jpg"};` after uploading that file.

A couple of practical notes: GitHub's web uploader tops out around 25MB per file, so compress video before uploading (most phone-shot clips will need it, a quick pass through HandBrake or a similar free compressor works well; the two videos already in this site were compressed that way). Keep videos reasonably short and compressed for load times, since nothing here streams or lazy-loads video. Leaving `media` off (or set to `null`) keeps the placeholder block, so you can migrate project by project.

A few other things worth knowing before sharing the live link widely:
- **Years** on each project are placeholder estimates, double-check them against your records.
- **LinkedIn link** on the About page is a placeholder, search the file for `id="linkedinLink"` and point it at your real profile URL.
