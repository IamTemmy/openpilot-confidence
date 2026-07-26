# Design notes

I utilized the use of AI to implement my design ideas in this project. The delegation, description,
and discernment of every feature was mine. Several iterations were made throughout the process.

These are the decisions I made and why.

## Why the path, not a ring or bars

Most other entries added a confidence ring or a row of limit bars in a corner. I did not want that.
Icons in the corners make your eyes jump around the screen. Confidence is about the road ahead, so
I put it on the road: the path openpilot already draws. Your focus stays centered where you are
already looking.

## The three signals

- Path length and smoothness = how sure openpilot is of the road ahead. A long, smooth path means
  it is confident driving that stretch; as it gets less sure, the path pulls back and breaks up.
- Glowing side edge = the steering getting close to its limit.
- Red zone and forward chevrons = braking and acceleration effort.

All three sit on the path, in the direction the strain is actually happening, so it reads without
much thinking.

## Why it is mostly silent

Calm and silent is the default so there is no constant distraction. The alert only breaks that calm
when action is needed. It is like a fire alarm at home: it cannot be going off all the time, because
when there is a real fire you would not know to react. The quiet is what makes the alert mean
something.

## Green, amber, red

The colour is driven by what is actually happening, not by a mode name:

- Green = all clear.
- Amber = one soft threshold crossed (confidence under 48%, steering over 80%, or braking over 70%).
  This is a "get ready" warning, like the amber on a traffic light.
- Red = a hard limit (confidence under 24%, steering over 94%, or braking over 90%). This is "act now."

## Scenarios

I built scenarios (Open highway, Faded markings, Sharp off-ramp, Crosswind gust, Low-sun glare,
Construction zone, Lead braking hard, Merging on-ramp) so the language can be tested against real
situations, plus manual sliders for confidence, steering, and longitudinal effort.

## What changed after community feedback

People on the comma Discord tested the first version and gave me real, specific feedback. I went
through all of it:

- **Sound would not be heard on the real device.** The comma 3's speakers are weak and low sounds
  distort or disappear, and my cues were too slow for warnings. So I remade the sounds to be high,
  short, and crisp instead of low and gentle, and tightened the timing so an urgent cue repeats in
  well under a second (road events happen in seconds).
- **The corner icons and status text were too small** to read in a quick, peripheral glance. So I
  scaled them all up.
- **The warning could wash out in bright daylight.** A soft edge glow is easy for the eye to ignore
  outside. So the warning now breathes across the whole screen: red pulses fast and almost fills the
  screen (without ever freezing as a solid panel, so the road stays visible), and amber breathes
  slow and soft and always stays see-through, since amber only means "get ready," not "act now."
- **A better car.** The lead car was a boxy grey shape that blended into the road. I made it a
  rounded, modern silhouette in cool silver so it stands apart from the road and from the white icons,
  with brake lights that glow red when openpilot brakes toward it.
- **How does it work on the much smaller comma four?** Someone asked how the long path and confidence
  translate to the tiny 1.9" comma four screen. So I added a comma four view that reframes the same
  UI for the smaller, rounded, landscape screen. The point is the language is not tied to the big
  screen; it scales down.

## What's in the prototype

Three backdrops: Abstract (clean render), Camera (a more realistic render), and Real drive, which
puts the live overlay on real dashcam footage from comma's MIT-licensed video compression challenge.
A comma four view for the small screen, an optional nav split, reserved sound, and a driver-attention
before/after (the calm nudge idea versus the full-screen "pay attention" shout). It also respects
reduced-motion settings, holding the red steady instead of flashing for anyone who needs that.

## Limits

This is a concept. In Real drive the path is a fixed straight overlay on recorded footage (I picked
the straightest part of the clip); a shipped version would follow the trajectory openpilot computes
each frame, and the clip cannot change to match a scenario. The comma four proportions are matched
from photos, not from a published spec. Still open to feedback.
