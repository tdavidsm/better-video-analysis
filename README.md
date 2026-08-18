# 🎬 Better Video Analysis — Motion from Real Video

A browser-based kinematics tool that turns a **real video** into distance–time data. Load a clip of something moving, calibrate the scale, track the object frame-by-frame (by hand or automatically with OpenCV), and read the motion graph. The video-based successor to [Speed Lab](https://tdavidsm.github.io/speed-lab/).

**▶ Use it:** https://tdavidsm.github.io/better-video-analysis/

Everything runs **entirely in the browser** — the video never leaves the device, nothing is uploaded.

## How it works

1. **Load a video** of something moving across the frame (a rolling ball, a walker, a toy car).
2. **Set the fps** to match the clip so times are right (phone video is usually 30 fps; slow-mo 120/240).
3. **Calibrate the scale** — click two points a known real distance apart (a metre stick, a floor tile) and type that distance in metres, so pixels become metres. Optionally set an origin for 0 m.
4. **Track the object:**
   - **✋ Manual tap** — step through frames and tap the object each time; it auto-advances and plots a point. Rock-solid on a touchscreen.
   - **🤖 Auto (OpenCV)** — click the object once to lock on, then **Track to end** and OpenCV template-matching (`cv.matchTemplate`) follows it frame-to-frame.
5. Track several **objects** at once (each its own color), read the **distance–time graph**, add a **best-fit line** (slope = speed), and export **CSV**.

## Notes

- **OpenCV.js is vendored** in the repo (`opencv.js`, ~9.8 MB, v4.9.0) so it loads same-origin from your Pages site rather than a third-party CDN that a school network might block. First load fetches it once, then it's cached. If it can't initialize, Manual tap still works fully.
- **Auto-tracking** uses grayscale template matching within a search window around the last position — fast and reliable for objects with visible contrast/texture. If a fast-moving object outruns the search window, re-click it to re-lock, or use Manual tap.
- Works on Chromebooks, laptops, and tablets (pointer + touch).

## Tech

Self-contained static site: `index.html` + vendored `opencv.js`. HTML5 `<video>` decoded to a native-resolution canvas for frame stepping and pixel access; canvas graph reused from Speed Lab. Deployed via GitHub Pages from `main`.
