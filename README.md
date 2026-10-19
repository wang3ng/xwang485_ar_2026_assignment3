# EN.601.654 Assignment 3

Programming submission for Introduction to Augmented Reality. Each question lives in its own folder. Serve the repo over HTTP (Babylon module imports and the glTF loader fail from `file://`). From this directory:

```bash
npx serve .
```

## Q2 — WebXR

`Q2/index.html` loads `Q2/Q2a/fish.glb` and starts an `immersive-ar` session.

Open `http://localhost:3000/Q2/` (port depends on the server) in a WebXR browser, enter AR, and aim the right controller. A hit shows a ring.

| Input | Action |
|---|---|
| Right trigger | Spawn the fish at the hit |
| Right thumbstick | Move the newest fish on the horizontal plane |
| Left thumbstick (x) | Yaw the newest fish about world Y |
| A / B | Scale the newest fish up / down |
| X | Restore the newest fish to its spawn pose |

Only the most recently spawned fish is moved, rotated, scaled, or reset. Buttons do nothing until one exists.

## Q3e — OpenGL projection

`Q3/Q3e/index.html` builds the projection matrix from camera intrinsics, maps a camera-space point to a pixel, and draws that pixel on an image plane.

The checked case is `W = 800`, `H = 600`, `n = 0.2`, `f = 20`, `fx = fy = 800`, `ox = oy = 400`, and `P = (0.3, -0.15, -6, 1)`. The page reports pixel `(440, 380)`. Change the `intrinsics` and `Pc` values in the script to try another camera.

## Q4 — Phong shading

`Q4/4a.js` is one point light. `Q4/4c.js` adds a second light. `Q4/index.html` imports `4c.js`.

To view 4.a instead, change the import in `Q4/index.html` to `./4a.js`, then open `http://localhost:3000/Q4/`.
