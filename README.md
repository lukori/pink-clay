# Pink Clay

Shape a block of pink clay with your hands through the camera. Single file: `index.html` (three.js + MediaPipe Hand Landmarker from CDN).

- Starts as a tall, rounded block, like clay out of the pack, already a little handled: slight lean and taper, lumps, a few old thumb marks. **New clay** makes a different one each time.
- The hand skeleton is drawn over the scene. Each finger is **red**, and turns **green** while its fingertip touches the clay. A ring around the tip closes in as the finger gets near the clay.
- **Depth = how close your hand is to the camera.** Hand far away = fingers float in front of the clay. Bring it closer and the fingers press in.
- **Dents are soft and deep:** the clay around a fingertip goes along with it, and the pushed clay bulges out nearby (the amount of clay stays the same). Dents and folds get darker inside, and the lump casts shadows on itself.
- **The whole lump rounds off while you work it**, a little with every touch, the way real clay loses its corners.
- **It moves in 3D:** a push from one side slides and turns the lump, and it drifts on a bit after you let go. Squeezing from both sides shapes it without moving it. Pressing toward the screen mostly dents. It slowly floats back to the middle.
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
| resist | 0.5 | 0 = clay gives way instantly, 0.95 = very stiff |
| soft | 0.55 | how much clay around the fingertip goes along with it |
| spread | 0.32 | how wide that soft area is |
| rounding | 0.012 | how fast the whole lump rounds off while touched |
| volKeep | 0.5 | how fast pushed clay bulges back out |
| bulge | 0.5 | how wide the bulge around the fingers is |
| smooth | 0.2 | smoothing where fingers rub |
| mobility | 0.8 | how much a one-sided push moves the lump instead of denting it (was 0.45: carved grooves instead of moving) |
| turn | 1.0 | how easily off-centre pushes turn it (was 0.7) |
| drag | 2.5 | how fast it stops drifting/spinning after you let go |
| home | 0.8 | pull back to the middle of the screen |
| cavity | 0.05 | darkening inside dents and folds |
| grain | 0.003 | fine surface grain (0.02 looked like a towel) |
| wheel | 0.6 | wheel speed |
| mouseRate | 1.5 | how fast a held mouse/touch presses in |

Note: the debug panel must not have the id `dbg`. Element ids become globals, and MediaPipe calls a global `dbg()`, which crashes the hand model.

Not yet verified with a real camera: the hand-distance values (sFar/sNear) are estimates for a laptop webcam at arm's length.
