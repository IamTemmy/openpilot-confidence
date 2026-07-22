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
- **Reserved escalation** — only when a hand-off is likely within seconds does a calm edge-breath
  and a plain-language prompt appear. Sound is held back for this moment, so it actually means something.

## Why it stays deployable

- Keeps openpilot's real visual language — dark flat chrome, white type, the openpilot green.
- Doesn't collide with the driver-monitoring icon, which already owns green/amber for driver attention.
- Flat, QT-friendly, glanceable in windshield-mounted peripheral vision.
- Reads as *a better openpilot*, not a redesign of the device.

## Run it locally

Open `index.html` in any modern browser, or serve it:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

Use the scenario chips (Open highway → Faded markings → Sharp off-ramp → Low-sun glare) or the
Confidence / Steering-effort sliders to drive the states.

## Status

v1 concept prototype. The road scene is stylized; the proposal is the interaction model
(living path, edge strain, reserved escalation). Independent work — not affiliated with comma.ai.
