# Design notes

These are the decisions I made and why. I used AI to help write the code, but the design direction,
the choices below, and the responses to feedback are mine. (Remove this line if you'd rather not
mention it.)

## Why the path, not a ring or bars

Most other entries added a confidence ring or a row of limit bars in a corner. I did not want that.
Icons in the corners make your eyes jump around the screen. Confidence is about the road ahead, so I
put it on the road: the path openpilot already draws. Your focus stays centered where you are
already looking.

## The three signals

- Path length and smoothness = confidence in the road ahead.
- Glowing side edge = steering getting close to its limit.
- Red zone and forward chevrons = braking and acceleration effort.

All three sit on the path, in the direction the strain is actually happening, so it reads without
much thinking.

## Why it is mostly silent

Calm and silent is the default so there is no constant distraction. The alert only breaks that calm
when action is needed. Fire-alarm logic: an alarm that is always going off means nothing when there
is a real fire.

## Scenarios

I built scenarios (Open highway, Faded markings, Sharp off-ramp, Crosswind gust, Low-sun glare,
Construction zone, Lead braking hard, Merging on-ramp) so the language can be tested against real
situations, plus manual sliders for confidence, steering, and longitudinal effort.

## What changed after community feedback (v2)

People on the comma Discord tested v1 and pointed out real things:

- The C3 speakers are weak and low-frequency sound distorts or is inaudible, and the cues were too
  slow for warnings. So I made the sounds higher-pitched, shorter, and crisper, and tightened the
  repeat timing for the urgent states.
- The corner icons and status text were too small to read in a peripheral glance. So I scaled them up.
- The edge glow could wash out in bright daylight. So I added a hard, bright edge ring behind the
  soft glow that survives glare.
- The page had too much writing. So I cut it down to the visuals and wrote the descriptions myself.

## Limits

This is a concept. In Real drive the path is a fixed straight overlay on recorded footage; a shipped
version would follow openpilot's real per-frame trajectory, and the clip cannot change to match a
scenario. Still open to feedback.
