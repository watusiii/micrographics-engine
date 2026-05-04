The Micrographic System: Proportion, Constraint, and Visual Harmony

  The Unit System

  At the heart of micrographic design lies a deceptively simple principle: all measurements derive from a single typographic metric—the x-height of the chosen font.

  The x-height (the height of a lowercase 'x') becomes the fundamental unit (1U) upon which the entire system is built. This isn't arbitrary. In typography, x-height represents the most visually stable dimension—it's where our eye naturally settles when reading, and it scales consistently across different font sizes.

  1U = font x-height (extracted via OpenType metrics)
  Grid = 1U
  Gutter = 0.5U
  Icon base = 2U × 2U

  This creates emergent proportion. Because everything shares the same DNA, visual relationships feel inevitable rather than designed. A 3-row data table naturally aligns with icon heights. Text headers span the width in predictable intervals. The grid becomes invisible yet omnipresent.

  Three Element Types

  The system recognizes three primitive forms:

  Type A (Spanners): Full-width headers. Bold, declarative text that breaks the grid horizontally. These establish visual rhythm and hierarchy—"WARNING LABEL", "FRAME 00000000". Font size is measured in units (typically 1.2U), maintaining proportional consistency.

  Type B (Blocks): Square-ish icons with optional labels. These are the visual atoms—logos, symbols, hazard markers. They pack side-by-side like Tetris pieces, wrapping when they hit the canvas edge. Aspect ratio detection allows wide logos (4:1) to claim 4U of horizontal space while tall logos (1:4) stack vertically.

  Type C (Data Streams): Tabular specifications. Label-value pairs that communicate technical information—voltage, frequency, model numbers. Each row is 1.2U tall. These compress information density while maintaining legibility.

  Constraint-Based Layout

  Here's where it gets interesting: you don't position elements. You sequence them.

  The layout engine uses guillotine bin-packing—a horizontal flow algorithm that treats the canvas like a typewriter. Elements enter from a list, pack left-to-right, wrap to new rows when they exceed canvas width, and expand vertically as needed.

  Cursor starts at (GUTTER, GUTTER)
  For each element:
    - Measure bounds
    - Snap to grid (ceil to nearest 1U)
    - Check if it fits on current row
    - If no: wrap to new row
    - If yes: place and advance cursor

  Type A elements force line breaks—they reset the cursor to the left margin regardless of where the previous element ended. This creates visual punctuation.

  The beauty is in what you can't control. You can't manually position an icon at (x: 150, y: 75). You can only reorder the sequence and let the system solve the packing problem. This is liberating—it removes a thousand micro-decisions and replaces them with one macro-decision: what comes next?

  Scale-to-Fit

  Content is measured at the base unit (extracted x-height, typically ~50px for Roboto Mono at 100pt), then the entire composition scales down to fit the canvas bounds:

  1. Render at base UNIT → measure bounds
  2. Calculate scale = min(canvasWidth/contentWidth, canvasHeight/contentHeight, 1.0)
  3. Re-render at UNIT × scale
  4. Center in canvas

  This ensures labels never overflow. A composition designed for 600×400px will gracefully compress to 300×200px, maintaining all proportional relationships. The grid shrinks uniformly.

  Why It Feels Satisfying

  Industrial labels—pharmaceutical boxes, electrical warnings, shipping manifests—share a visual language. They're information-dense yet scannable. They use minimal decoration but achieve maximum clarity.

  This system captures that aesthetic through:

  1. Mathematical consistency: Everything relates through multiplication, not arbitrary pixel pushing
  2. Constraint: Removing positional freedom forces better hierarchy decisions
  3. Rhythm: The grid creates predictable intervals that the eye can anticipate
  4. Modularity: Swap a logo for a data table—the system adapts
  5. Imperfection through perfection: The tetris-like packing creates organic asymmetry within rigid rules

  It's the same satisfaction as watching a perfect Tetris line clear, or seeing shipping containers stack at a port. Constraint yields harmony. The system says "no" to a thousand bad choices, leaving only good ones.

  Technical Implementation

  Built with Paper.js for vector rendering and OpenType.js for real font metrics. The two-pass rendering system (measure, scale, render) ensures pixel-perfect output at any canvas size. SVG logos import with aspect ratio preservation. Drag-and-drop reordering triggers live re-layout.

  The diagnostic panel displays the unit system visually—showing the x-height with guideline overlays, proving the math. It's not decoration; it's verification that the system is working as intended.

  ---
  In Summary: Micrographic design works because it trades positional freedom for proportional consistency. One unit rules them all. Elements flow rather than float. The grid is felt, not seen. And the result looks machine-made in the best possible way—crisp, rational, and oddly human.