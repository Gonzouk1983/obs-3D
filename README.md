# OBS 3D Item (Web Hosted)

This is a tiny, static, web-hosted 3D viewer you can add to OBS as a **Browser Source**.

## Files
- `viewer.html` — the OBS-ready 3D viewer (transparent background).
- `chooser.html` — a helper page that builds the OBS URL for you.

## Quick start (GitHub Pages)
1. Create a new repo and upload these files.
2. Enable **Settings → Pages → Deploy from branch** (root or `/docs`).
3. Visit your Pages URL.
4. Open `chooser.html`, paste your public model URL, tweak settings, copy the generated `viewer.html?...` URL.
5. Paste that URL into an OBS **Browser Source**.

## Netlify / Vercel
- Drag-and-drop the folder to Netlify or `vercel deploy` a static project.
- Use the generated site URL with `viewer.html?...` in OBS.

## Your own VPS (Nginx)
Example server block:
```
server {
  listen 80;
  server_name your.domain;
  root /var/www/obs-3d-viewer;
  index viewer.html;
  add_header Cache-Control "no-cache";
}
```
Copy the files to `/var/www/obs-3d-viewer` and visit `http://your.domain/viewer.html?...`.

## Model hosting tips
- Prefer `.glb` (binary glTF). Keep files small (use Draco + KTX2).
- Host models on the same domain as the viewer to avoid CORS, or ensure your host sets `Access-Control-Allow-Origin: *` for public assets.
- Test with the sample Duck model if your model doesn’t show.

## Query parameters
- `model` — URL to GLB/GLTF (required unless you want the sample Duck)
- `scale` — number (e.g. `1.2`)
- `rx`, `ry`, `rz` — rotation in degrees
- `ao` — ambient light intensity (`0–1`)
- `shadow` — `1` or `0`
- `bg` — `transparent` (default) or hex like `%23000000`
- `cam` — camera distance (e.g. `2.5`)
- `spin` — degrees/second to auto-rotate

## OBS notes
- Add **Browser Source** → paste URL.
- Set width/height (e.g. 1920×1080, or smaller if just a corner element).
- If it doesn’t refresh after changing params, toggle the source’s visibility or add `&nonce=<random>` to the URL.
