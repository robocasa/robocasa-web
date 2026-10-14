# Subtask Annotations

This pipeline generates per-frame subtask annotations for RoboCasa composite task demos: it decomposes each task into the sequence of subtasks it is composed of and labels every frame with the subtask currently being performed, its stage, and a natural-language instruction. The labels are derived directly from each demo's privileged simulation state, making them precise and fully reproducible, and the code ships with labelers covering all 300 composite tasks.

<div class="admonition warning">
<p class="admonition-title">Not for leaderboard submissions</p>

Do not use these subtask annotations when training models for the <a href="https://robocasa.ai/leaderboard.html" target="_blank" rel="noopener noreferrer">RoboCasa365 leaderboard</a>. Leaderboard entries must train on the standard <code>pretrain_human300</code> dataset without the added subtask labels, so all submissions are compared on equal data.

</div>

<div class="subtask-demo" id="subtask-demo">
<video class="subtask-demo__video" src="../_static/videos/subtask_demo.mp4" muted playsinline preload="auto"></video>
<div class="subtask-demo__track" role="slider" tabindex="0" aria-label="Subtask segments" aria-valuemin="0" aria-valuemax="1111"></div>
<div class="subtask-demo__readout">
<span class="subtask-demo__badge"></span>
<span class="subtask-demo__name"></span>
<span class="subtask-demo__lang"></span>
</div>
</div>

<style>
.subtask-demo { max-width: 560px; margin: 1.5rem auto; }
.subtask-demo__video { display: block; width: 100%; border-radius: 8px; background: #000; cursor: pointer; }
.subtask-demo__track { position: relative; display: flex; gap: 2px; height: 28px; margin-top: 10px; cursor: pointer; user-select: none; touch-action: none; border-radius: 6px; overflow: hidden; }
.subtask-demo__track:focus-visible { outline: 2px solid var(--pst-color-primary, #5b21b6); outline-offset: 2px; }
.subtask-demo__seg { position: relative; display: flex; align-items: center; justify-content: center; font: 600 11px/1 var(--pst-font-family-monospace, ui-monospace, monospace); color: rgba(255,255,255,0.92); opacity: 0.45; transition: opacity 120ms ease; }
.subtask-demo__seg.is-active { opacity: 1; }
.subtask-demo__seg:hover { opacity: 0.8; }
.subtask-demo__seg.is-active:hover { opacity: 1; }
.subtask-demo__seg--pick { background: #3b82f6; }
.subtask-demo__seg--place { background: #22c55e; }
.subtask-demo__seg--navigate { background: #eab308; }
.subtask-demo__seg--done { background: #9ca3af; }
.subtask-demo__head { position: absolute; top: -3px; bottom: -3px; width: 3px; margin-left: -1.5px; background: var(--pst-color-text-base, #111827); border-radius: 2px; pointer-events: none; }
.subtask-demo__readout { display: flex; flex-wrap: wrap; align-items: baseline; gap: 4px 10px; margin-top: 10px; min-height: 2.6em; }
.subtask-demo__badge { font: 600 12px/1 var(--pst-font-family-monospace, ui-monospace, monospace); padding: 4px 7px; border-radius: 4px; color: #fff; }
.subtask-demo__name { font-family: var(--pst-font-family-monospace, ui-monospace, monospace); font-weight: 600; }
.subtask-demo__lang { flex-basis: 100%; color: var(--pst-color-text-muted, #6b7280); }
</style>

<script>
(function () {
  var FPS = 60, FRAMES = 1112;
  var SEGMENTS = [
    { start: 0, end: 174, name: "PickPlaceToasterToCounter", stage: "pick", lang: "pick up a toasted bread slice from the toaster" },
    { start: 175, end: 283, name: "PickPlaceToasterToCounter", stage: "place", lang: "place the bread slice in the bowl" },
    { start: 284, end: 485, name: "PickPlaceToasterToCounter", stage: "pick", lang: "pick up the other toasted bread slice from the toaster" },
    { start: 486, end: 617, name: "PickPlaceToasterToCounter", stage: "place", lang: "place the other bread slice in the bowl" },
    { start: 618, end: 753, name: "PickPlaceCounterToDining", stage: "pick", lang: "pick up the bowl" },
    { start: 754, end: 983, name: "NavigateKitchen", stage: "navigate", lang: "carry the bowl to the peanut butter and jelly on the dining counter" },
    { start: 984, end: 1088, name: "PickPlaceCounterToDining", stage: "place", lang: "place the bowl next to the peanut butter and jelly" },
    { start: 1089, end: 1111, name: "done", stage: "done", lang: "task complete" }
  ];
  var COLORS = { pick: "#3b82f6", place: "#22c55e", navigate: "#eab308", done: "#9ca3af" };

  var root = document.getElementById("subtask-demo");
  if (!root) return;
  var video = root.querySelector(".subtask-demo__video");
  var track = root.querySelector(".subtask-demo__track");
  var badge = root.querySelector(".subtask-demo__badge");
  var nameEl = root.querySelector(".subtask-demo__name");
  var langEl = root.querySelector(".subtask-demo__lang");

  var segEls = SEGMENTS.map(function (s, i) {
    var el = document.createElement("div");
    el.className = "subtask-demo__seg subtask-demo__seg--" + s.stage;
    el.style.flex = String(s.end - s.start + 1);
    el.textContent = String(i);
    el.title = "seg " + i + ": " + s.name + (s.stage !== "done" ? " [" + s.stage + "]" : "");
    track.appendChild(el);
    return el;
  });
  var head = document.createElement("div");
  head.className = "subtask-demo__head";
  track.appendChild(head);

  function frameAt(t) { return Math.min(FRAMES - 1, Math.max(0, Math.floor(t * FPS))); }
  function segIndexAt(frame) {
    for (var i = 0; i < SEGMENTS.length; i++) if (frame <= SEGMENTS[i].end) return i;
    return SEGMENTS.length - 1;
  }

  var shown = -1;
  function render() {
    var frame = frameAt(video.currentTime);
    head.style.left = (frame / (FRAMES - 1)) * 100 + "%";
    track.setAttribute("aria-valuenow", String(frame));
    var i = segIndexAt(frame);
    if (i === shown) return;
    shown = i;
    segEls.forEach(function (el, j) { el.classList.toggle("is-active", j === i); });
    var s = SEGMENTS[i];
    badge.textContent = "seg " + i + " / " + (SEGMENTS.length - 1);
    badge.style.background = COLORS[s.stage];
    nameEl.textContent = s.stage === "done" ? "done" : s.name + " [" + s.stage + "]";
    langEl.textContent = s.lang;
    track.setAttribute("aria-valuetext", "segment " + i + ": " + s.lang);
  }

  function seekToFrame(frame) {
    video.currentTime = (frame + 0.5) / FPS;
    render();
  }
  function frameFromPointer(ev) {
    var r = track.getBoundingClientRect();
    var x = Math.min(Math.max(ev.clientX - r.left, 0), r.width);
    return Math.round((x / r.width) * (FRAMES - 1));
  }

  // A click plays from the start of the clicked segment; a drag scrubs frame by frame.
  var pressed = false, moved = false, downX = 0, wasPlaying = false;
  track.addEventListener("pointerdown", function (ev) {
    pressed = true;
    moved = false;
    downX = ev.clientX;
    wasPlaying = !video.paused;
    video.pause();
    track.setPointerCapture(ev.pointerId);
  });
  track.addEventListener("pointermove", function (ev) {
    if (!pressed) return;
    if (!moved && Math.abs(ev.clientX - downX) < 4) return;
    moved = true;
    seekToFrame(frameFromPointer(ev));
  });
  function release(ev, commit) {
    if (!pressed) return;
    pressed = false;
    if (commit && !moved) {
      seekToFrame(SEGMENTS[segIndexAt(frameFromPointer(ev))].start);
      video.play();
    } else if (wasPlaying) {
      video.play();
    }
  }

  video.addEventListener("click", function () {
    if (video.paused) video.play(); else video.pause();
  });
  track.addEventListener("pointerup", function (ev) { release(ev, true); });
  track.addEventListener("pointercancel", function (ev) { release(ev, false); });

  track.addEventListener("keydown", function (ev) {
    var i = segIndexAt(frameAt(video.currentTime));
    if (ev.key === "ArrowRight") i = Math.min(SEGMENTS.length - 1, i + 1);
    else if (ev.key === "ArrowLeft") i = Math.max(0, i - 1);
    else return;
    ev.preventDefault();
    seekToFrame(SEGMENTS[i].start);
  });

  video.addEventListener("timeupdate", render);
  video.addEventListener("seeked", render);
  video.addEventListener("loadedmetadata", render);
  (function tick() { if (!video.paused) render(); requestAnimationFrame(tick); })();
  render();
})();
</script>

## Fields

| field | type | meaning |
|---|---|---|
| `subtask_idx` | int | 0-based index of the current segment, incrementing at each boundary. The last segment is always `done`. |
| `subtask_name` | str | the atomic skill, e.g. `PickPlaceCabinetToBowl`, `NavigateKitchen` |
| `subtask_stage` | str | the phase, e.g. `navigate`, `pick`, `place`, `press`, `tilt`, `wait`, `done` |
| `subtask_lang` | str | natural-language instruction for the segment, e.g. "carry the eggplant to a bowl next to the sink" |

A "segment" is a maximal run of frames with the same `subtask_idx`; boundaries are where it changes.

## HDF5

Stored per demo at `data/<demo>/{subtask_idx,subtask_name,subtask_stage,subtask_lang}`, frame-aligned with `actions`/`states`.

```python
import h5py
g = h5py.File("demo.hdf5")["data"]["demo_0"]
idx  = g["subtask_idx"][:]                          # (T,) int32
lang = [s.decode() for s in g["subtask_lang"][:]]   # (T,) strings
```

## LeRobot

Per-frame columns in each episode parquet:

- `subtask_idx`: int, identical to the HDF5 value.
- `annotation.human.subtask`, `annotation.human.subtask_name`, `annotation.human.subtask_stage`: integer task indices that resolve to the `subtask_lang` / `subtask_name` / `subtask_stage` strings via `meta/tasks.jsonl`.

<div class="admonition note">
<p class="admonition-title">Note</p>

LeRobot episode order ≠ HDF5 demo order. Pair them by trajectory length if needed.

</div>

## Regenerating

```bash
# HDF5
python robocasa/scripts/dataset_scripts/label_subtasks.py --dataset <demo.hdf5>

# LeRobot
python robocasa/scripts/dataset_scripts/add_subtask_labels_to_lerobot.py \
    --lerobot <lerobot_dir> --from-hdf5 <demo.hdf5>
```

Render a demo with its labels overlaid for inspection:

```bash
python robocasa/scripts/dataset_scripts/visualize_subtask_labels.py \
    --dataset <demo.hdf5> --demo demo_0 --out demo_0.mp4
```
