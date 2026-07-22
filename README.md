# openpilot · confidence

An interactive concept for the [comma.ai design challenge](https://comma.ai/leaderboard):
communicate openpilot's driving confidence — and how close it is to its steering, brake, and
acceleration limits — to the driver, continuously, and without nagging.

**▶ Live demo:** https://iamtemmy.github.io/openpilot-confidence/

---

## The problem

openpilot is a Level 2 system. It doesn't handle every situation, but it *knows* how likely it is
to need a hand-off. Today the driver only learns that at the last moment — an audible alert that
fires *after* the wheel has already run out of torque and the car is drifting off line. By then
it's late, and the alert is more annoying than useful.

The challenge is to convey that confidence *while engaged* — the full spectrum from "reliable" to
"take over within seconds" — clearly and non-intrusively, and to surface how close openpilot is to
its actuator limits *before* it hits them.

## The idea: the path is the instrument

Every other approach reaches for a new widget — a colored ring, a set of bars, a frame around the
screen. This concept instead makes the path openpilot **already draws** carry the meaning, because
confidence *is* about the road ahead.

- **Reach** — high confidence draws a long, solid green ribbon far down the road. As confidence
  falls, the ribbon **retracts toward the car**, so you watch trust shorten *before* anything
  goes wrong.
- **Dissolve** — an uncertain path breaks into a drifting stipple the further ahead it goes: the
  system visibly failing to commit to where the road goes. Analog and glanceable — no reading required.
- **Steering strain** — in a hard curve the strained *side* edge of the path brightens as openpilot
  nears its steering-torque limit. Early, directional, and silent — the fix for "you only find out at the alert."
- **Braking strain + lead** — a chevron marks the car ahead. As openpilot brakes toward its authority
  limit, a tension band grows back from the lead — the fore-aft mirror of steering strain. Hard
  acceleration reads as forward surge chevrons. Together these cover all three actuator limits the
  brief names: steering, brake, and acceleration.
- **Reserved escalation** — only when a hand-off is likely does a calm edge-breath, a plain-language
  prompt, and a soft chime appear. Silence and green mean trust, so the escalation actually means something.

## What's in the prototype

- **Three backdrops** — *Abstract* (clean stylized road), *Camera* (a camera-realistic render), and
  *Real drive*, which composites the live overlay onto real dashcam footage from comma's
  MIT-licensed [video compression challenge](https://github.com/commaai/comma_video_compression_challenge).
- **Scenarios + manual sliders** — drive Open highway, Faded markings, Sharp off-ramp, Low-sun glare,
  Lead braking hard, and more, or steer confidence / steering / longitudinal effort yourself.
- **Reserved sound** — a single onset cue that escalates only as things worsen; on by default, toggleable.
- **Nav split** — an optional map panel matching openpilot's real split-screen.
- **Driver attention, reframed** — a before/after showing openpilot's full-screen "pay attention" shout
  versus a calm, earlier, graduated nudge that grabs attention without ever covering the road.

## Why it stays deployable

- Keeps openpilot's real visual language — dark flat chrome, white type, the openpilot green.
- Doesn't collide with the driver-monitoring icon, which already owns green/amber for driver attention.
- Flat, QT-friendly, glanceable in windshield-mounted peripheral vision.
- Reads as *a better openpilot*, not a redesign — the direction comma's own 0.11.1 release is already heading.

## Run it locally

Open `index.html` in any modern browser, or serve it:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

Note: the *Real drive* footage loads via `fetch`, so it appears only when the page is served over
`http(s)` (the live site, or a local server) — not when opening the file directly via `file://`.
Use the scenario chips or the Confidence / Steering / Longitudinal sliders to drive the states.

## Status

Concept prototype. Stylized road scenes; *Real drive* overlays a fixed path on recorded footage
(the shipped version would follow openpilot's per-frame trajectory). The proposal is the interaction
model — living path, edge strain, reserved escalation. Independent work, not affiliated with comma.ai.
