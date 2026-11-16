# Wiskers (web build)

This repo is the Godot Web export of Wiskers, hosted on Vercel.

## What goes in this repo (all in the ROOT, not in a folder)

These files come from Godot's Web export. Godot makes them for you:

- index.html
- index.js
- index.wasm
- index.pck
- index.audio.worklet.js
- index.audio.position.worklet.js
- index.png
- index.icon.png
- index.apple-touch-icon.png
- index.manifest.json (only if "Progressive Web App" is on)

Plus these files from this kit: vercel.json, README.md, .gitignore

## Step 1: Export from Godot

1. Open Wiskers in Godot 4.7.
2. Top menu: Project > Export.
3. Click Add... > Web. If it says templates are missing, click "Manage Export Templates" > Download and Install, then come back.
4. In the Web preset, turn OFF "Thread Support" (so no special server headers are needed).
5. Click "Export Project" (NOT "Export PCK/Zip").
6. Make a new empty folder named wiskers-site. Save as `index.html` inside it. The name must be index.html so every file is named index.*
7. Open the folder. You should see index.html, index.js, index.wasm, index.pck and the others.

## Step 2: Put it on GitHub

The GitHub website only lets you upload files up to 25 MB, and index.wasm is about 39 MB, so use GitHub Desktop:

1. Install GitHub Desktop (desktop.github.com) and sign in.
2. Copy vercel.json, README.md and .gitignore into the wiskers-site folder next to the index.* files.
3. In GitHub Desktop: File > Add Local Repository, pick the wiskers-site folder. If it says it is not a repository, click "create a repository here".
4. Type a summary like "Add Wiskers web build", click "Commit to main".
5. Click "Publish repository" (public or private, either works).

Every single file must be under 100 MB for GitHub.

## Step 3: Deploy on Vercel

1. Go to vercel.com and sign in with GitHub.
2. Click Add New > Project, pick the wiskers-site repo, click Import.
3. Framework Preset: Other. Leave Build Command and Output Directory empty. Root Directory: ./
4. Click Deploy.
5. Open the link Vercel gives you. The first load downloads the big index.wasm, so wait for the loading bar.

## Updating the game later

Re-export from Godot into the same folder (overwrite the index.* files), then in GitHub Desktop commit and Push. Vercel redeploys on its own.

## If something goes wrong

- Black screen or "Error loading": press F12, open Console, and read the red message.
- 404 on index.wasm or index.pck: those files were not committed. Check they show up in GitHub Desktop's changes list.
- Old version showing: hard refresh (Ctrl+Shift+R).
- If you ever turn Thread Support ON in the export, add these two headers to vercel.json under "/(.*)": Cross-Origin-Opener-Policy: same-origin and Cross-Origin-Embedder-Policy: require-corp.
