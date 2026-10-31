# Pink Clay

Shape a block of pink clay with your hands through the camera. Single file: `index.html` (three.js + MediaPipe Hand Landmarker from CDN).

- Starts as a tall, rounded block, like clay out of the pack, already a little handled: slight lean and taper, lumps, a few old thumb marks. **New clay** makes a different one each time.
- The hand skeleton is drawn over the scene. Each finger is **red**, and turns **green** while its fingertip touches the clay. A ring around the tip closes in as the finger gets near the clay.
- **Depth = how close your hand is to the camera.** Hand far away = fingers float in front of the clay. Bring it closer and the fingers press in.
- **Only pressing changes the clay, not time:** clay moves only when a finger moves further into it. Holding a finger still inside changes nothing. The fingertip is a soft round pad (the middle pushes fully, the edge fades), and the clay follows by `give`. Rounding and smoothing also come from pressing, not from time. Hand tracking is smoothed (steady).
- **It behaves as one solid lump:** every push moves the clay like a nearly incompressible solid (a "Kelvinlet": the physics of pushing an elastic block at one point, made permanent). Neighbouring clay moves together, so it dents, smears and bulges but never tears into sheets or strings. Only a small part (direct) presses straight in under the fingertip, along the surface normal, never sideways.
- **Dents go inward, the shape changes overall:** Pushed-in clay mostly flows into the whole lump's shape rather than a rim around the finger (overall). Dents and folds get darker inside, and the lump casts shadows on itself.
- **Both hands on the clay = holding it:** with two fingers of each hand touching (palm lines turn green), turning your hands turns the clay and moving them moves it. Rolling it between the hands rounds it off (by how much the hands move, not by time). Two hands never squeeze or stretch it (`squeeze` 0.5 removed). While held, fingers press in gently.
- **It always turns very slowly** (idleSpin), faster with the wheel.
- **The whole lump rounds off while you work it**, a little with every touch, the way real clay loses its corners.
- **It moves in 3D:** a push from one side slides and turns the lump, and it drifts on a bit after you let go. Squeezing from both sides shapes it without moving it. Pressing toward the screen mostly dents. It slowly floats back to the middle.
- **Background stars:** small, darker pink dots at many depths. Stars at the clay's depth are sharp, nearer and further ones are soft blurred discs (like a camera's depth of field), and the field turns slowly around the clay so near and far stars drift past each other.
- Buttons: **New clay**, **Wheel** (turns it like a potter's wheel). Mouse / touch also works: hold to press in, drag to push.

## Tuning

Add `?debug` for live numbers, +/- buttons per parameter (the address updates so you can copy the tuned link), and Save/Copy log.

| param | default | what it does |
|---|---|---|
| sFar | 0.11 | palm size (share of camera height) where fingers start touching range |
| sNear | 0.20 | palm size where fingers reach full depth |
| pushRange | 2.4 | how deep the hand travels between sFar and sNear |
| fingerDepth | 3.0 | extra depth from a fingertip leaning toward the camera |
| zStart | 1.4 | depth of a far hand (block front is around 0.6) |
| tipR | 0.13 | fingertip size |
| give | 0.25 (more rigid; was 0.4, before that 0.75) | how much the clay follows a finger moving into it (replaced the time-based `pressSpeed` 0.35, which kept pressing while a finger stood still) |
| steady | 0.35 | hand tracking smoothing, lower = steadier |
| grabTurn | 1.0 | two hands: how much turning the hands turns the clay |
| grabMove | 0.8 | two hands: how much moving the hands moves the clay |
| handRound | 0.04 | two hands: how much rolling between the hands rounds the clay (replaced squeeze/stretch) |
| idleSpin | 0.08 | constant slow turn, rad/s (about 4.6° per second) |
| spread | 0.16 | size of the clay region that moves with a push (solid-clay push; was a 0.32 per-point soft spread) |
| direct | 0.3 | share of the push pressed straight into the surface under the fingertip (finger-shaped marks) |
| rounding | 0.006 (firmer clay; was 0.012) | how much pressing rounds off the whole lump |
| volKeep | 0.2 | how fast lost clay volume comes back (was 0.35; the solid push already keeps volume) |
| bulge | 1.0 | how wide the returning clay spreads around the fingers (your tuning, was 0.5) |
| overall | 1.0 | returning volume goes into the whole shape (was 0.7) |
| smooth | 0.1 (firmer clay; was 0.2) | smoothing where fingers rub |
| mobility | 0.8 | how much a one-sided push moves the lump instead of denting it (was 0.45: carved grooves instead of moving) |
| turn | 1.0 | how easily off-centre pushes turn it (was 0.7) |
| drag | 2.5 | how fast it stops drifting/spinning after you let go |
| home | 0.8 | pull back to the middle of the screen |
| cavity | 0.2 (your tuning, was 0.05) | darkening inside dents and folds |
| grain | 0.003 | fine surface grain (0.02 looked like a towel) |
| wheel | 0.6 | wheel speed |
| stars | 260 | number of background stars (reload to apply) |
| starBlur | 0.5 | how out of focus stars away from the clay's depth get |
| starDim | 0.8 | star brightness (kept below the clay; 0.45 was nearly invisible) |
| starSpin | 0.03 | how fast the star field turns around the clay (the 3D drift) |
| mouseRate | 2.9 (your tuning, was 1.5) | how fast a held mouse/touch presses in |

Note: the debug panel must not have the id `dbg`. Element ids become globals, and MediaPipe calls a global `dbg()`, which crashes the hand model.

Not yet verified with a real camera: the hand-distance values (sFar/sNear) are estimates for a laptop webcam at arm's length.
