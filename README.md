playbook language
Finding your way around. The row of tabs under the title chooses a workspace, and the rendering is in all of them. make is the playbook beside the picture; render & save is the size, frame rate, palette and every export; bench is the workbench (blocks, syntax diagrams, whole posts, delivery to a platform, what a frame costs, and the libraries); lab is mutation, breeding, the arena, the thread and the token; share & files is the gallery, the proof codec and the trace; and everything puts every pane on screen at once. The choice is remembered, and a link that addresses a pane (#el=pane.lab) opens the workspace that holds it. The two saves people want most — the animated GIF and the current frame as a PNG — sit directly under the picture, in every workspace.#

Starting out. demo in the top bar replays the two-minute guided tour: each step loads a playbook that plays while it is explained, rings the control it names and opens the workspace that holds it. The arrow keys step it and Esc ends it. my Wikipedia is the other way in: give it your name and the handle you edit under and it asks the public Wikipedia API — anonymously, read-only — what you have edited, reads those articles for numbers, and offers each as a rendering: the tables as curves or bars, the infobox figures as a card, the article's own growth in bytes, and your edits month by month. draw it writes the playbook, provenance and all, and it is then an ordinary playbook. Your name and handle stay in this browser; forget me removes them, and nothing is ever uploaded.#

One statement per line; # starts a comment. The first equation is the formula the rest of the playbook stages.#

f(x, t) = …	definition; the first one is the formula. a = 3 defines a constant.
scene 960x540 fps 30 duration 6	canvas size, frame rate, clip length (seconds)
background #0b1020	backdrop colour
view x -6..6 y -2..2	the window of the plane that fills the canvas
title "…" subtitle "…" from 0 to 2.5	title card, fading in and out
param a from 0 to 1 over 0..4 ease inOut	animate a parameter between two times
key 3 a 1.4 zoom 1.6 ease inOut	keyframe: set channels at a time (key 3 { a: 1.4 } also works)
plot a*f(x,t) color #7ad7ff width 3	curve of an expression in x (and t)
parametric cos(u), sin(u) u 0..tau	parametric curve in u
heat f(x,y,t) palette viridis res 200	shaded 2-D field
complex on	read the maths over ℂ: 0.345+0.515i is a literal, and conj z, abs z, arg z, re z, im z join + - * / ^
heat mandelbrot(x+iy) iter 200 escape 4 res 400	escape time as an ordinary field: mandelbrot(c) and julia(z, c) are builtins, so palettes and res mean what they always did
fractal julia c = -0.4+0.6i iter 200 palette viridis res 400	the same picture, spelled as one statement (fractal mandelbrot … too)
ifs { map w0 z -> 0.5z+0.5
map w1 z -> 0.5conj(z)-0.4 } points 30000 burn 20 seed 12345 color by map palette aurora	the chaos game: named complex contractions, hesper does the random selection, burn-in and plotting; points is an expression, so a param grows the attractor
lsystem koch axiom "F" rule F -> "F+F--F+F" angle 60 depth 5 color #7ad7ff	string rewriting plus a turtle, drawn as paths; depth is an expression too. Presets: koch snowflake dragon sierpinski tree plant levy hilbert
replicate 3 1 4 at 2 size 64 gens 4	a self-replicator on a fixed instruction set: an organism whose first cell is its own length, copied into the space after it, generation by generation
view3d x 0..4 y 0..3 z 0..16	the 3-D box the picture lives in — declaring it makes the frame spatial
camera3d eye 2.5 -3 1.3 target 0 0 0 up 0 0 1 fov 45	where the box is looked at from (coordinates in the normalised cube)
plot3d point a, b, z size 0.05 label "…"	a node in space; its coordinates are expressions, so a parameter moves it
plot3d line x,y,z to x,y,z width 2	a segment in space
plot3d surface f(x, y) res 26	a wireframe surface z = f(x, y) over the box
parametric3d X(u), Y(u), Z(u) u 0..tau	a curve in space
label3d "…" at x, y, z size 15	text anchored at a point of the box
axes on / grid on	axes and grid — in a 3-D playbook, the box with its ticks and its floor
label "a = {a}" at 0.04 0.9	text; {…} holes are evaluated per frame
svg { <circle …/> } at 0.7 0.9 size 0.2 0.2	your own SVG markup, drawn with the frame and kept vector in SVG exports; {…} holes work inside it
link "https://…" label "read more" at 0.04 0.06	a hyperlink: clickable in the studio, a real <a> in the exported SVG
script { … }	your own JavaScript, run per frame in a sandbox; it returns drawing commands, so it is recorded in every export
script { … } mode live at 0.62 0.95 size 0.34 0.34	an interactive panel (a game, a widget): your HTML and JS in a sandboxed frame over the rendering
slideshow transition fade 0.4 default 5	make the playbook a deck: the clip is the slides, one after another
slide "Heading" for 6 background #07101f	start a slide; everything after it lives in that slide's time window
columns 2 gap 0.04 margin 0.05 / rows 2	split the frame into cells (reading order, left to right)
column 2 / column all	put the following layers in that cell (or back on the whole frame)
palette aurora #071022 #2f6fb2 #8be9d8 #ffd479	define a colour ramp; palette viridis just selects one. Heat layers and new curves follow it.
function g(x) = sin(x)/x	a named function (let and def work too); plain g(x) = … still works
table rows x -2..2 step 1 at 0.62 0.9 { x | f(x)
{x} | {f(x,t)} }	a table: first block line is the header, the next is repeated once per row value; {…} holes are live
caption "…" from 2 to 5 say	a caption band at the foot of the frame; say also speaks it
tts "…" at 3 rate 1.1 show	narration: spoken during playback and exported as a subtitle track (show also draws it)
shader { o = vec3(f(q.x*3.+t), l(q), .5); } res 160	a shader-golf fragment: run per pixel, on the CPU, in every export
shader s(l(q)*8.-t) palette inferno res 200	one-liner form; a float result is shaded through the palette, a vec3/vec4 is used as the colour
Shader golf. A shader block is a tiny GLSL-like dialect evaluated per pixel by hesper itself — never by eval, so a shader survives a share link safely. Each fragment sees p (the plane point), uv (0…1), q (centred and aspect-corrected), FC (the fragment coordinate, y upwards), R and r (resolution), t (time), and every animated param. Write the result to o (or just end with an expression). Floats and vec2/3/4 broadcast, swizzles (.xyzw .rgba .stpq) and indexing work, and for/if/else/break/continue/return are available. Golf aliases: s c f a l n m h k d e g for sin cos fract abs length normalize mix hash clamp dot exp smoothstep. Every fragment runs on a fuel budget (fuel N), so a runaway loop stops instead of hanging the tab.#

Marches and matrices. The dialect takes what shader golf is written in: mat2/mat3/mat4 (by columns, as in GLSL), transpose, rotate2D(a) and rotate3D(a, axis), with v * M the row-vector product — so p *= rotate3D(…) turns a point and p.zy *= rotate2D(…) turns two of its lanes. One declaration may name several variables (float i,e,g;, each starting at zero), ++/-- work inside an expression, and the comma operator sequences statements. An o that is only ever added to starts at vec4(0), so an accumulating march (o += exp(-e*2e3)/4e1;) reads as written. The kaleidoscopic fold example is one such march.#

Slides, cells and narration. A slide gives every layer written under it its own time window, so a deck needs no from … to bookkeeping. A column re-reads the fractional coordinates of the layers that follow inside that cell and clips their drawing to it — in the preview and in every export. Narration is spoken by the browser while the clip plays (tick speak); since GIF and MPEG-1 carry no audio, the cues are also exported as a WebVTT subtitle file.#

meta-hesper. A playbook can read and rewrite itself. defmacro f(a, b) { … } runs one phase earlier, over this playbook's own statements (syntax), and emits ordinary hesper; the macro is gone by the time anything is drawn. The builtin autoseek(field, halfwidth, steps, dur) samples a field, scores each pixel by the variance of its neighbourhood and walks towards the structure, so a camera path can be discovered rather than typed. A meta { … } block may also watch the render: inside after frame N { … } or every Ns { … } it can read trace (what the frames cost) and output (the field just drawn) and rewrite append key … — only ever after the current frame, so the clip already shown never changes. Blocks are stratified: meta { } is level 1 and writes level 0, meta level 2 { } writes level-1 blocks, and nothing may emit at its own level. meta strict on makes a lint finding stop the render. Try the meta-zoom, meta-lint and meta-tower examples.#

Import SVG. The import SVG button in the playbook pane turns a file into a playbook: the picture becomes one svg { … } layer, and every SMIL animation in it (animate, animateTransform, set) is lifted into a formula — a param, or a run of key statements — with the animated attribute rewritten as a {hole} that reads it back. Retime it, ease it, drive it from your own expressions, export it. The markup is whitelisted like any other, and the only holes that survive are the ones the import wrote.#

The lab. mutate varies the numbers, colours and choice words of this playbook — never its skeleton, and never the scene format — and offers three mutants, each already parsed and drawn so that nothing on offer is blank. breed crosses it with another rendering gene for gene, and sometimes grafts a whole drawing statement across. predict learns from every rendering this browser holds — a chain over statement heads, the statements themselves, and the range of every number — and writes a playbook nobody has written, using only statements it has seen. In the arena two renderings battle for your vote: the winner takes 3 points and the Elo rating moves from one to the other, and a battle link carries both contenders and the ballots so far, so a friend can vote and send them back. Threads put the comments in the link too, and a token is a signature chain over this exact playbook that any reader can check for themselves. Nothing is uploaded anywhere.#

The library. The library tab of the bench holds named objects brought in from the LMFDB, the OEIS and Wikidata — curves, newforms, number fields, sequences and the items they are. They ship with the page; nothing is fetched to show them. draw it writes the playbook that draws the object, provenance and all, and it is then an ordinary playbook. check it recomputes what the record claims in this browser: the discriminant and j-invariant of a curve in exact integer arithmetic, every ap by counting points over 𝔽p, the Hasse bound, the Hecke relations and the Deligne bound of a form, a form against the point counts of its own curve, a field's discriminant by a resultant, and every published term of a sequence from scratch. certified .svg and file page… prepare a Wikimedia Commons upload carrying that whole record — sources, dates, licences, seals and every check — and upload to Commons… opens the upload form with it filled in; the upload itself is yours to make, under your own account. article…, re-sync… and check Commons… are the only buttons here that touch the network, and each says so when it cannot.#

Share targets. Pick a share target in the export panel and the settings above it are planned for you: the studio walks a ladder of frame sizes, frame rates and palettes — heaviest first — and takes the first rung whose estimated file fits that place's size limit, keeping the scene's aspect ratio and trimming an over-long clip. The line under the menu says what will be written, and says so when nothing fits (the lightest rung is still offered). Leave it on custom to use the manual settings.#

User code. A script block may define draw(hs) or simply run statements. hs carries t, width, height, env (the animated parameters), pointer, a persistent state, the projection px(x) py(y) ux(px) uy(py), and the commands line rect circle poly path text. It runs in an iframe sandbox="allow-scripts": no access to this page, and whatever it returns is re-validated before anything is drawn. Markup in an svg block is whitelisted — scripts, event handlers and unsafe URLs are dropped, and the studio tells you what it dropped.#

Channels usable in key: any parameter name, plus zoom, camx, camy, and in a 3-D playbook camz (the eye) and camtx, camty, camtz (the target). Easings: linear, in, out, inOut, smooth, smoother, cubicIn, cubicOut, sine, step, bounce.#

Maths: + - * / ^ %, comparisons, && ||, if(c, a, b), and sin cos tan asin acos atan atan2 sinh cosh tanh exp log ln log2 log10 sqrt cbrt abs sign floor ceil round min max clamp step smoothstep lerp hypot mod fract saw tri square gauss, with pi, tau, e. Implicit products such as 2x and 3sin(t) are understood
