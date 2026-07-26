# openpilot · confidence

A redesign of comma's openpilot UI that communicates the system's driving confidence to the
driver, clearly and without distraction.

**Live demo:** https://iamtemmy.github.io/openpilot-confidence/

## The idea

I put the confidence on the road itself because it is easier on the eye and keeps your focus
centered on the road, instead of making you chase icons in the corners of the screen and look all
over the place. The path openpilot already draws becomes the main signal:

- **Path length** shows how sure openpilot is of the road ahead. A long, smooth green path means it
  is confident driving that stretch; as it gets less sure, the path pulls back and breaks up.
- **Glowing edges** tell you the car is close to a steering limit, so you can be ready to adjust if
  it is about to run out of room to hold a curve.
- **Red braking zone** builds as openpilot brakes harder toward the car ahead, and forward chevrons
  show hard acceleration. You feel the effort before it gets urgent.
- **Sound stays calm and mostly silent by default.** I did not want constant distraction. When
  something actually needs attention, breaking that calm is what triggers a reaction. It is like a
  fire alarm at home: it cannot be going off all the time, because when there is a real fire you
  would not know to react. The quiet is what makes the alert mean something.

## The prototype

Three backdrops: Abstract (clean render), Camera (a more realistic render), and Real drive, which
puts the live overlay on real dashcam footage from comma's MIT-licensed
[video compression challenge](https://github.com/commaai/comma_video_compression_challenge). Try the
scenario buttons (Open highway, Low-sun glare, Lead braking hard, and more) or drag the sliders to
drive the states yourself. There is also an optional nav split and a driver-attention before/after.

## Run it locally

Open `index.html`, or serve it:

```bash
python3 -m http.server 8000
# then http://localhost:8000
```

The Real drive footage loads over http, so it only shows on the live site or a local server, not by
opening the file directly.

## Why I made this

I have been drawn to the autonomy space for about a year, and I am confident in my ability to
improve how these systems work and how they are designed. comma turned out to be a genuinely
interesting company with a product I had not known about before.

## Status

Concept prototype, not affiliated with comma.ai. See [DESIGN.md](DESIGN.md) for the decisions behind
it and what changed after community feedback.
