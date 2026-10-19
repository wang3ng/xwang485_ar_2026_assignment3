# EN.601.654 / EN.601.454 Assignment 3

**Author:** William Wang (`wang3ng`)

Programming code for Introduction to Augmented Reality, Assignment 3. The written answers are in the Gradescope PDF. This repository holds the three programming parts: a WebXR scene that spawns a model from a controller hit test (Q2), an OpenGL projection that maps a camera-space point to a pixel (Q3e), and a Phong fragment shader with one and two point lights (Q4).

Q1 and Q3a–d are written work and are not in this repo. Q5 is the Assignment 2 repository transfer and is not in this repo.

## Layout

| Path | Contents |
|---|---|
| `Q2/index.html` | Babylon.js WebXR scene. Hit-tests with the right controller ray and spawns, moves, rotates, scales, and resets a fish. |
| `Q2/Q2a/fish.glb` | Model loaded by Q2. |
| `Q3/Q3e/index.html` | Projection matrix, NDC, and pixel mapping, drawn on an image plane. |
| `Q4/4a.js` | `shadePointLight` with one point light. |
| `Q4/4c.js` | Same shader plus a second point light. |
| `Q4/index.html` | Page that imports `4c.js`. |

## How to run

Babylon loads scripts and `fish.glb` over HTTP. Opening the HTML files with `file://` will fail. From this directory:

```bash
npx serve .
```

`serve` prints a local URL, usually `http://localhost:3000`. Use the paths below on that origin.

### Q2

Open `http://localhost:3000/Q2/` in a browser that supports WebXR (a Quest browser, or Chrome on Android with ARCore). Desktop Chrome can show the loaded fish, but spawning needs an AR session.

1. Wait until the status line says the fish has loaded.
2. Enter AR.
3. Aim the right controller. A cyan ring marks a hit on a real surface.
4. Pull the right trigger to spawn a fish at that hit.

Further input changes only the newest fish. Older fish stay where they are. Pressing the buttons before any fish exists does nothing.

| Input | Action |
|---|---|
| Right trigger | Spawn a fish at the current hit |
| Right thumbstick | Move the newest fish on the horizontal plane |
| Left thumbstick, horizontal axis | Yaw the newest fish about world Y |
| A | Scale the newest fish up |
| B | Scale the newest fish down |
| X | Put the newest fish back at its spawn position, orientation, and scale |

### Q3e

Open `http://localhost:3000/Q3/Q3e/`. No headset is required.

The script builds the OpenGL projection from width, height, near, far, and the intrinsics `fx`, `fy`, `ox`, `oy`. It multiplies that matrix by a camera-space point, divides by clip `w`, and converts NDC to pixels with the assignment formulas. The result is drawn on an 800×600 image plane, with the principal point in gray and the projected point in cyan. Clip coordinates, NDC, and the pixel are also printed on the image and in the browser console as `Q3`.

The values checked against the hand solution are `W = 800`, `H = 600`, `n = 0.2`, `f = 20`, `fx = fy = 800`, `ox = oy = 400`, and `P = (0.3, -0.15, -6, 1)`. That case reports pixel `(440, 380)`. Edit `intrinsics` and `Pc` near the top of the script to try another camera or point, then reload.

### Q4

Open `http://localhost:3000/Q4/`. The page imports `4c.js`, so you see the cylinder and sphere lit by two point lights: the original light, and a light-blue light at `(-2.5, 3, 2)`. Drag to orbit the camera. The shader updates `uCameraPos` each frame, so the specular highlight follows the view.

`4a.js` is the same scene with only the first light. To view it, change the import in `Q4/index.html` from `./4c.js` to `./4a.js` and reload. Both files export `createScene` and can also be pasted into the Babylon playground if the `export` keyword is removed.
