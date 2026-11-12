# Kids' Color Vision Test

Two small browser games that screen young children for color blindness without needing them to read numbers. Instead of the digits used in classic Ishihara plates, the child names a familiar person or points to a shape.

Each game is a single HTML file with no dependencies, build step or server. Open it in a browser and it works. Photos never leave the device.

> **This is a home screening game, not a medical test.** Screens show color differently, so a missed plate means "get it checked," not a diagnosis. Talk to a pediatrician or eye doctor about any concerns.

## The games

### `find-the-shape.html`: Find the Shape

A dotted plate hides one of six shapes: circle, square, triangle, star, heart or moon. The same six shapes are shown as plain dark pictures below the plate, and the child taps the one they see.

- **New shape** picks a random shape, never the same one twice in a row.
- Tapping a picture shows a green check for the right answer (with confetti) or a red "Try again."
- **Show answer** highlights the correct shape so a parent can check without tapping.
- **Test** picks the plate type (see below).
- **Color strength** lowers the color difference to make plates harder.
- **Gray background (HRR-style)** draws the shape as a purple tint on neutral gray dots, in the style of the Hardy-Rand-Rittler test.

### `whos-hiding.html`: Who's Hiding?

Upload photos of people the child knows. Each photo is turned into a plate where the face is drawn only with color differences, and the child says who they see.

- Pick several photos at once, or drag them onto the page. Close-up faces on plain backgrounds work best.
- **Drag to frame** and **Zoom** choose which square of the photo becomes the plate.
- **Shape area**, **Face detail** and **Swap shape and background** adjust how the photo becomes a two-tone shape. The **Hidden shape** preview shows the result.
- **Dot size**, **Color strength** and **Plate type** control how the plate is drawn.
- **Full screen** or tapping the plate shows it full screen. **New dots** redraws the dots.

Photo detail is limited by the dot size, so faces come out as bold, poster-like shapes. Find the Shape is the easier game for very young children.

## Plate types

| Type | Who misses it | Default colors |
|---|---|---|
| Practice | Nobody: it uses a brightness difference everyone can see | Dark shape on light dots |
| Deuteranopia | Red-green, green-weak (most common) | Pink on teal |
| Protanopia | Red-green, red-weak | Pink on teal |
| Tritanopia | Blue-yellow | Purple on green |

With **Gray background** turned on, the background is neutral gray and the shape is a lavender purple (tritanopia), magenta (deuteranopia) or pinkish red (protanopia). Each of these colors looks gray to a person with that type of color blindness.

## Running a test

1. Start with Practice plates so the child learns the game: "Something is hiding in the dots. What is it?"
2. Switch to the test types. In Who's Hiding, use a different person for each type so the child can't remember a face from an earlier plate.
3. Use a bright screen in normal room light, with night mode, True Tone and blue-light filters turned off.
4. If the child gets the Practice plates but misses others, have their color vision checked by a professional.

## How the plates work

The eye has three types of color-sensing cones: L (long, reddish), M (medium, greenish) and S (short, bluish). Each common type of color blindness comes from one cone type missing or not working well:

- Protanopia: L cones
- Deuteranopia: M cones
- Tritanopia: S cones

Two colors that differ **only** in the response of the missing cone look identical to someone without that cone. Each plate is built that way:

1. A random base color is picked for every dot, with randomized brightness so lightness can't give the shape away.
2. The base color is converted to cone responses (LMS) using the RGB-to-LMS matrix from Viénot, Brettel & Mollon (1999).
3. Only the tested cone's response is raised for shape dots and lowered for background dots. In gray mode, the background stays gray and only the shape dots are shifted.
4. The result is converted back to screen RGB. A base color is only used if both of its versions fit on screen, so the shape and background dots share the same brightness spread.

The base colors and shift amounts were chosen to give the largest color difference the sRGB screen gamut allows. The plates were checked with the Machado et al. (2009) color-blindness simulation:

- The deuteranopia and protanopia plates disappear completely.
- The tritanopia plates leave a faint trace in that simulation. That simulation is known to be less exact for tritanopia, but turning down Color strength is a reasonable precaution for that test.

Dots are packed with random dart-throwing on a spatial grid, from large to small.

## Saving plates

When the pages are opened directly, the Who's Hiding **Download PNG** button is hidden because it relies on a Claude artifact feature. To save a plate, right-click it (or long-press on mobile) and save the image.

## License

Free to use, share and modify for any **noncommercial** purpose, including personal use, schools, charities, research and hobby projects, under the [PolyForm Noncommercial License 1.0.0](LICENSE.md). Commercial use requires permission from the author.

Copyright 2026 Barry Behrmann
