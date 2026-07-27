# SYMBIONT
A living generative organism that reacts to your mouse in real time — flares up, calms down, and forgets everything the moment you leave. No save state, no two visits alike.

# Symbiont
### a living specimen that never holds still

## Inspiration

One line from the brief stuck with me: "art that couldn't exist without technology." I kept turning that over. A computer making something faster doesn't count. A filter on a photo doesn't count. It had to be something that only exists because computation exists, period.

Most generative art answers that with one glowing noun — a fractal, a particle system, whatever the shader-of-the-week is. I wanted mine to feel like a creature instead of a picture. Something you'd feel a little bad about closing the tab on.

Getting there took a while. I burned through the first few days sketching ideas that went nowhere — sound-reactive particles, a genetic algorithm evolving on its own, an endless fractal zoom. None of them clicked. What finally did was one word: specimen. Observe a living thing, instead of generate an image. Once that frame was in place, everything else fell out of it pretty naturally.

## What it does

Symbiont is a particle organism flowing through a Perlin noise field, mirrored into a kaleidoscope pattern so it reads as one body instead of scattered dots. It glows — additive blending, bioluminescent color — and it stays in motion on its own, whether or not anyone's watching.

It's alive in a more active sense too. Move your mouse near it and it notices. Fast, jittery movement makes it flare — more turbulent, more saturated, branching sharpens. Slow down and it calms. Click on it and you're feeding it: the population visibly thickens and ripples outward. A live readout in the corner tracks the actual numbers behind all of it — hue, branching, flow, density, symmetry — updating in real time, so you're watching the internal state shift at the same moment you're watching the shape change.

Stop moving and it settles, the way a startled animal settles: gradually, back toward its resting temperament. Each visit exists entirely in its own moment — complete while it's happening, and finished the second you leave.

## How we built it

It's one HTML file. Canvas 2D, vanilla JavaScript, and a Perlin-style noise function I wrote from scratch rather than importing, mostly because I wanted real control over how the turbulence felt at different intensities. Everything runs client-side, straight from the browser.

The genome — hue, hue-spread, branching, flow speed, density, trail decay, saturation, symmetry — gets recomputed every frame from a rolling window of mouse behavior: speed, how erratic the direction is, click count. That blends against a resting baseline so the organism always has somewhere to return to. I spent an embarrassing amount of time just tuning those blend curves. Too fast and it feels twitchy, like a slider you're dragging. Too slow and it feels dead. There's no formula for that — you just sit there moving your mouse around way longer than is reasonable until it feels right.

There was a whole earlier version of this I built and then killed. It saved the organism's state to shared cloud storage — every visitor left a permanent mark, the next person inherited it, there was a running log of every change. I got it fully working. Then I tore it out. It depended on a storage layer that only worked in one specific viewing environment, and it dragged in a pile of UI — an imprint button, a lineage log, save and load calls — that got in the way of the thing I actually cared about: whether this feels alive right now, in this one encounter. Cutting something that already worked turned out to be harder than building it.

## Challenges we ran into

Getting "alive" to read as different from "random" was the first wall. Early versions looked like static noise, or like an obvious sine wave on a loop. What fixed it was layering multiple drift frequencies into the noise field, and giving trails enough decay that motion carried some weight and memory instead of particles just teleporting frame to frame.

Tuning the reaction curve without it feeling gimmicky took longer than anything else. Overreact to every twitch of the mouse and it turns into a control panel instead of a creature. I rewrote that mapping more times than I want to count — mostly by feel, moving my own mouse around, asking myself whether it felt like the thing noticed me or like I was just operating it.

Letting go of the shared, permanent version was the hardest single call in the whole build. It worked. It just wasn't the stronger version of the idea, and admitting that partway through — instead of shipping the more impressive-sounding feature because it already existed — took more discipline than I expected going in.

Keeping it to one dependency-free file meant building without a safety net. Writing my own noise function and particle engine by hand, instead of grabbing something already battle-tested, meant every performance dip and visual glitch was mine alone to chase down.

## Accomplishments that we're proud of

The reaction genuinely reads as alive rather than randomly animated. A few people who tried it used the word "aware," which is exactly the reaction I was chasing from day one.

It's a single file that runs the same everywhere — client-side only, works locally or hosted anywhere, functional the instant you open it.

I'm proud of cutting the shared-storage feature after already building it. Walking away from working code is harder than it sounds.

And honestly, I'm proud of the sheer hours spent nudging constants across multiple days, until the reaction curve stopped feeling like a demo and started feeling like a temperament.

## What we learned

Interactive and reactive turned out to be two different things, and the gap between them lives almost entirely in the tuning, not the architecture. The mouse-to-genome mapping is conceptually simple. What ate the days wasn't building it — it was making the numbers feel right.

I also learned, the slow way, that the more technically impressive version of a project isn't automatically the better one. Build the ambitious thing first if you need to. Live with it a while. Then have the discipline to cut it back down to whatever the piece actually needs.

## What's next for Symbiont

- Sound reactivity, so it responds to ambient audio or a visitor's voice the same way it currently responds to movement.
- A lighter, opt-in sense of shared history — something ambient rather than the heavier save/log system I cut this time around.
- Touch-specific tuning for mobile, since the current reaction curves were tuned mostly against mouse behavior.
- Testing whether the same behavior-to-genome idea holds up on a completely different renderer, to see how far it generalizes past particle flow fields.
