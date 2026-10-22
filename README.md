# Virtual Laboratory (VR prototype)

A workshop-ready **A-Frame** prototype of a simple virtual science lab for the **Meta Quest 3S browser**, with desktop mouse and gaze fallbacks. The whole experience is one self-contained `index.html` (A-Frame 1.7.1 loaded from the official CDN; all geometry, text, textures and sounds are generated in code — no asset files).

> **Simulated educational demonstration.** All chemistry, measurements, reactions and safety behaviour in this prototype are simulated for teaching purposes only. They are **not** real laboratory guidance or scientific measurement.

## Activities

1. **Mixing Liquids (chemistry, simulated)** — put on goggles, pour coloured Solutions A (blue) and B (yellow) into a flask, stir, observe a simulated reaction (colour change, bubbles, small displayed warm-up), then answer a check question.
2. **Simple Circuit (physics, simulated)** — place a battery, bulb and switch on a board, connect three wire gaps, close/open the switch, then answer a check question.

Harmless mistakes are allowed and explained: pouring the decoy Solution C, pouring without goggles, over-filling the flask, putting a part in the wrong slot, closing the switch on an incomplete loop, an optional short-circuit experiment with an extra wire, and wrong quiz answers. Each activity ends with a completion screen that lists learning notes for any mistakes made.

## Run locally

WebXR needs a secure context (`https://` or `http://localhost`). From the folder containing `index.html`:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening the file directly (`file://`) shows the desktop view but VR entry may not be offered.

## Open on Meta Quest 3S

The headset cannot reach your computer's `localhost`, so serve the file over HTTPS:

- **Easiest:** enable GitHub Pages for this repository (Settings → Pages → deploy from `main`, root) and open the Pages URL in Quest Browser; or
- use any HTTPS static host or tunnel (e.g. a service that gives your local server an `https://` URL); or
- with the Quest connected by USB and developer mode on, run `adb reverse tcp:8000 tcp:8000` and open `http://localhost:8000` in Quest Browser.

Then press the **VR** button at the bottom-right of the page and allow the immersive session.

## Interact

| Input | How |
|---|---|
| Quest controllers | Point the laser (turns yellow over selectable things) and pull the trigger. |
| No controllers / hands | Gaze select turns on automatically in VR when no controllers are detected: look at a button for ~1.5 s until the ring shrinks. Toggle with **Gaze select** (Auto → On → Off). |
| Desktop | Drag to look around, click to select. Keys: **1**/**2** start an activity, **H** hint, **R** reset, **M** menu. |

General flow: click an object to pick it up (it lifts), then click where it should go. The main panel shows the steps (current step highlighted, done steps ticked) and a feedback box (blue = guide, green = well done, amber = harmless mistake explained).

No locomotion is needed; everything is reachable by pointing from where you stand or sit. **Seated mode** lowers the whole lab by about 22 cm.

## Reset / retry

- **Reset activity** (right-hand controls panel, or **R**) restarts the current activity.
- **Waste beaker** empties the flask so you can retry the mix without a full reset.
- After completion: **Retry**, switch to the other activity, or return to the **Menu**.

## Known limitations

- Tested only in desktop headless Chromium (software WebGL). **Not yet verified on a Quest 3S**, in a live WebXR session, with physical controllers, haptics, or for headset frame rate.
- Hand-tracking pinch is not supported; with hands only, use gaze select.
- Interactions are point-and-select, not physical grabbing or pouring.
- Chemistry is a colour lookup and the circuit is a rule check — illustrative only, not physical simulations.
- Requires internet access to load A-Frame from `aframe.io`.
- Text is drawn to canvas textures; very long feedback is auto-shrunk to fit the panel.
- Sound is synthesised with Web Audio and may stay silent until the first interaction (browser autoplay rules).
