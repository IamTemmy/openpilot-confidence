# Controls Challenge — probe kit (stage 1)

Fidelity-verified re-implementation of the tinyphysics rollout that exposes the
fixed per-step random draw u_t, plus three planners to A/B test the core idea:
does knowing u_t (quantile pre-compensation) beat mean-aiming?

## Files
- harness.py   : faithful sim (matches real tinyphysics cost exactly, Δ=0)
- planners.py  : PID, MeanAim (u-blind), QuantilePrecomp (u-aware)
- real_test.py : runs all three on real segments, prints total_cost

## Setup (M1, from the controls_challenge repo root)
    uv venv --python 3.11 && source .venv/bin/activate
    uv pip install -r requirements.txt
    # download the 0.6G dataset (first run auto-downloads into ./data):
    python tinyphysics.py --model_path ./models/tinyphysics.onnx --data_path ./data --num_segs 5 --controller pid

## Run the A/B test
    cp /path/to/probe/*.py .          # put harness.py planners.py real_test.py in repo root
    python real_test.py --data ./data --model ./models/tinyphysics.onnx --n 8

Optional: add jerk weighting, e.g. --jerk_w 0.05

## What to look for / report back
- PID mean should land near ~110 (sanity: matches leaderboard baseline)
- The key signal: does Precomp(u-aware) beat MeanAim(u-blind)? by how much?
