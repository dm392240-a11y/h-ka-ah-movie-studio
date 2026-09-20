# AH! KA AH! Movie Studio

Railway-ready controller for the Roy / Kristy / Sophi animated short.

## Important
Railway does not supply the GPU needed for Wan-class video models. This project therefore uses a **$0-first manual/free-GPU workflow**: the dashboard gives you each shot prompt/reference; generate that short clip in a currently available free image-to-video service/Space; save the resulting MP4 into `clips/`; then the app uses FFmpeg to concatenate approved clips.

Free cloud GPU quotas and public Spaces change frequently, so this package deliberately does not pretend there is an unlimited free API endpoint.

## 1. Add character reference images
Put your approved PNGs in `characters/` using these names:
- `roy.png`
- `kristy-sophi.png`
- `group.png`

Use the same reference designs for every generation to improve consistency.

## 2. Run locally
```bash
npm install
npm start
```
Open http://localhost:3000

## 3. Push to GitHub
Upload all project files to your `ah-ka-ah-movie-studio` repository.

## 4. Deploy on Railway
1. Railway → New Project.
2. Deploy from GitHub Repo.
3. Choose `ah-ka-ah-movie-studio`.
4. Railway detects the Dockerfile and builds it.
5. Generate a public domain in Railway Settings/Networking.

No HF token is required for the manual/free workflow. If a stable API is added later, store its token in Railway Variables, never in GitHub.

## 5. Generate each shot
Open the dashboard and copy the prompt for a shot. Use its listed character reference image in an image-to-video generator. Target the duration shown (typically 7–10 seconds), 16:9, consistent cinematic 3D animation. Download the resulting MP4 and rename it to the shot ID, e.g. `s1a.mp4`.

## 6. Put clips into `clips/`
For a local build, copy the MP4 files directly into `clips/`.

For Railway, ephemeral filesystem storage is not a good long-term upload store. For the first version, build locally after downloading clips, or attach a Railway Volume and extend the app with uploads.

## 7. Build the film
Enter clip filenames in story order in the dashboard and press **BUILD FINAL MOVIE**. The output is `output/AH_KA_AH_FINAL.mp4`.

All input clips should have matching codecs/resolution/frame rate for stream-copy concatenation. If a build fails, normalize clips first (recommended: H.264/AAC, 1920x1080, 30fps).

## Suggested production order
1. Generate/lock Roy reference.
2. Generate/lock Kristy + Sophi reference.
3. Generate shots s1a → s9a.
4. Review each shot; regenerate weak ones.
5. Record narration/dialogue separately.
6. Add licensed/royalty-free ambience/music in an editor, or extend the FFmpeg pipeline.
7. Export the final master.

## Next upgrades
- Browser clip upload + Railway Volume
- Stable video API adapter
- TTS narration
- Music/SFX tracks
- Subtitle generation
- FFmpeg normalization and crossfades
- Job status/history
