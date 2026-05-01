# Before It Breaks Deploy Reference

This repo deploys by committing the current working tree and pushing `main`.

## Primary Command

Run from the repo root:

```bash
bash sync.sh
```

`sync.sh` runs:

```bash
git add .
git commit -m "BIB_SYNC"
git push -u origin main
```

## Before Sync

Check the working tree:

```bash
git status --short
```

Confirm the changes are meant to go live.

For thumbnail or social preview changes, also check:

- `THUMBNAILS.md`
- `index.html`
- KIND demo page metadata
- referenced image files in the repo root

## What Gets Deployed

The sync command stages everything in the repo, including new files.

This is useful for single-file static updates, but it means unrelated local changes will also be committed if they are present.

## After Sync

After the push completes:

- Confirm the site loads at `https://beforeitbreaks.ca/`.
- Confirm changed pages load directly.
- Confirm new static assets load directly by URL.
- For preview image changes, run an Open Graph preview debugger.

## Preview Debuggers

- https://www.opengraph.xyz/
- https://www.linkedin.com/post-inspector/
- Discord paste test

Use these after deployment when Open Graph or Twitter preview metadata changes.

## Common Problems

No commit created:

- There were no staged changes.
- The working tree was already clean.

Push fails:

- Network or remote auth failed.
- Local `main` is behind `origin/main`.

Preview does not update:

- The social platform cached the old preview.
- Run the preview debugger again to refresh the cache.
