# Hexagon Tessellation Guide

A comprehensive guide to creating proper hexagonal honeycomb patterns that tessellate correctly.

## Table of Contents
- [Understanding Hexagon Geometry](#understanding-hexagon-geometry)
- [The Two Orientations](#the-two-orientations)
- [Critical Spacing Rules](#critical-spacing-rules)
- [Step-by-Step Implementation](#step-by-step-implementation)
- [Common Mistakes](#common-mistakes)
- [Mathematical Formulas](#mathematical-formulas)
- [Code Examples](#code-examples)

---

## Understanding Hexagon Geometry

A regular hexagon has 6 equal sides and 6 equal angles (120° each). The key to proper tessellation lies in understanding how hexagons nest together.

### Key Measurements

For a regular hexagon with side length `s`:

- **Side length**: `s` (given)
- **Apothem** (center to midpoint of side): `s × √3 / 2`
- The `√3` factor (≈ 1.732) is crucial for all hexagon calculations

---

## The Two Orientations

### Flat-Top Hexagons (⬡)
Hexagons with a flat edge on top and bottom.

**Dimensions:**
- Width (point to point): `2s`
- Height (flat to flat): `h = s × √3`

**Vertex positions** (centered at origin):
```
Top-left:     (-0.5s, -0.5h)
Top-right:    (+0.5s, -0.5h)
Right:        (+s,     0   )
Bottom-right: (+0.5s, +0.5h)
Bottom-left:  (-0.5s, +0.5h)
Left:         (-s,     0   )
```

### Pointy-Top Hexagons (⬢)
Hexagons with a point on top and bottom (30° rotation of flat-top).

**Dimensions:**
- Width (flat to flat): `w = s × √3`
- Height (point to point): `2s`

**Vertex positions** (centered at origin):
```
Top:          (0,      -s   )
Top-right:    (+0.5w,  -0.5s)
Bottom-right: (+0.5w,  +0.5s)
Bottom:       (0,      +s   )
Bottom-left:  (-0.5w,  +0.5s)
Top-left:     (-0.5w,  -0.5s)
```

---

## Critical Spacing Rules

### THE GOLDEN RULE: Rows Must Overlap

In a proper hexagon honeycomb, **rows MUST overlap**. The vertical spacing between row centers is not the full height of a hexagon, but only **half the height**.

### Flat-Top Tessellation

For flat-top hexagons with side length `s` and height `h = s × √3`:

1. **Horizontal spacing**: `1.5s` (center to center between adjacent hexagons)
2. **Vertical spacing**: `h/2` (HALF the height - this is critical!)
3. **Row offset**: Alternate rows offset by `1.5s` horizontally

**Pattern repeat dimensions:**
- Width: `3s` (to accommodate the offset pattern)
- Height: `h` (contains 2 rows spaced `h/2` apart)

**Example layout:**
```
Row 0 (y=0):     [Hex at x=1.5s]
Row 1 (y=h/2):   [Hex at x=0] [Hex at x=3s]
Row 2 (y=h):     [Hex at x=1.5s]
Row 3 (y=1.5h):  [Hex at x=0] [Hex at x=3s]
...
```

### Pointy-Top Tessellation

For pointy-top hexagons with side length `s` and width `w = s × √3`:

1. **Horizontal spacing**: `w/2` (HALF the width)
2. **Vertical spacing**: `1.5s` (center to center between adjacent hexagons)
3. **Column offset**: Alternate columns offset by `1.5s` vertically

**Pattern repeat dimensions:**
- Width: `w` (contains 2 columns spaced `w/2` apart)
- Height: `3s` (to accommodate the offset pattern)

---

## Step-by-Step Implementation

### For Flat-Top Hexagons

1. **Define your base unit**: Choose a side length `s` (e.g., 20 pixels)

2. **Calculate height**: `h = s × Math.sqrt(3)` (approximately `s × 1.732`)

3. **Set pattern dimensions**:
   - Pattern width: `3s`
   - Pattern height: `h`

4. **Place your hexagons**:
   - Row 1 at y=0: One hexagon centered at `(1.5s, 0)`
   - Row 2 at y=h/2: Two hexagons at `(0, h/2)` and `(3s, h/2)`

5. **Tile the pattern**: The pattern repeats every `3s` horizontally and every `h` vertically

### For Pointy-Top Hexagons

1. **Define your base unit**: Choose a side length `s`

2. **Calculate width**: `w = s × Math.sqrt(3)`

3. **Set pattern dimensions**:
   - Pattern width: `w`
   - Pattern height: `3s`

4. **Place your hexagons**:
   - Column 1 at x=0: One hexagon centered at `(0, 1.5s)`
   - Column 2 at x=w/2: Two hexagons at `(w/2, 0)` and `(w/2, 3s)`

5. **Tile the pattern**: The pattern repeats every `w` horizontally and every `3s` vertically

---

## Common Mistakes

### ❌ Mistake #1: Using Full Height for Vertical Spacing
```javascript
// WRONG - hexagons won't nest properly
const patternHeight = h * 2;  // Too much space!
placeHex(x, h);  // Row 2 too far down
```

**Fix**: Use `h/2` for vertical spacing between rows
```javascript
// CORRECT - proper nesting
const patternHeight = h;  // Contains 2 rows
placeHex(x, h/2);  // Row 2 at half-height
```

### ❌ Mistake #2: Not Offsetting Alternate Rows
```javascript
// WRONG - creates vertical columns, not honeycomb
for (let row = 0; row < rows; row++) {
    placeHex(0, row * h/2);  // All at same x position
}
```

**Fix**: Offset every other row
```javascript
// CORRECT - creates interlocking pattern
for (let row = 0; row < rows; row++) {
    const xOffset = (row % 2) * 1.5 * s;
    placeHex(xOffset, row * h/2);
}
```

### ❌ Mistake #3: Mixing Orientations Incorrectly
Using both flat-top and pointy-top hexagons in the same grid typically creates visual confusion. **Pick one orientation and stick with it** for the entire pattern.

**Exception**: Some advanced patterns intentionally mix orientations for artistic effect, but this requires careful planning.

### ❌ Mistake #4: Forgetting the √3 Factor
```javascript
// WRONG - treats hexagons like squares
const height = s;  // Missing the √3!
```

**Fix**: Always apply √3 to convert between width and height
```javascript
// CORRECT
const height = s * Math.sqrt(3);
```

---

## Mathematical Formulas

### Flat-Top Hexagons
Given side length `s`:

| Measurement | Formula | Example (s=20) |
|-------------|---------|----------------|
| Width | `2s` | 40 |
| Height | `s × √3` | ≈34.64 |
| Horizontal spacing | `1.5s` | 30 |
| Vertical spacing | `(s × √3) / 2` | ≈17.32 |
| Pattern width | `3s` | 60 |
| Pattern height | `s × √3` | ≈34.64 |

### Pointy-Top Hexagons
Given side length `s`:

| Measurement | Formula | Example (s=20) |
|-------------|---------|----------------|
| Width | `s × √3` | ≈34.64 |
| Height | `2s` | 40 |
| Horizontal spacing | `(s × √3) / 2` | ≈17.32 |
| Vertical spacing | `1.5s` | 30 |
| Pattern width | `s × √3` | ≈34.64 |
| Pattern height | `3s` | 60 |

### Area Formulas
- **Single hexagon**: `(3√3 / 2) × s²` ≈ `2.598 × s²`
- **Hexagons per unit area**: Approximately `1 / (2.598 × s²)`

---

## Code Examples

### SVG Pattern (Flat-Top)

```javascript
function generateFlatTopHexagonPattern(sideLength) {
    const s = sideLength;
    const h = s * Math.sqrt(3);
    const patternWidth = s * 3;
    const patternHeight = h;

    // Helper to create flat-top hexagon centered at (cx, cy)
    const flatTopHex = (cx, cy) => {
        return `${cx - 0.5*s},${cy - 0.5*h} ` +
               `${cx + 0.5*s},${cy - 0.5*h} ` +
               `${cx + s},${cy} ` +
               `${cx + 0.5*s},${cy + 0.5*h} ` +
               `${cx - 0.5*s},${cy + 0.5*h} ` +
               `${cx - s},${cy}`;
    };

    const svg = `
        <svg width="${patternWidth}" height="${patternHeight}"
             xmlns="http://www.w3.org/2000/svg">
            <defs>
                <pattern id="hexagons"
                         width="${patternWidth}"
                         height="${patternHeight}"
                         patternUnits="userSpaceOnUse">
                    <!-- Row 1: Even row -->
                    <polygon points="${flatTopHex(1.5*s, 0)}"
                             fill="none" stroke="black" stroke-width="1"/>

                    <!-- Row 2: Odd row (offset horizontally, h/2 down) -->
                    <polygon points="${flatTopHex(0, h/2)}"
                             fill="none" stroke="black" stroke-width="1"/>
                    <polygon points="${flatTopHex(3*s, h/2)}"
                             fill="none" stroke="black" stroke-width="1"/>
                </pattern>
            </defs>
            <rect width="100%" height="100%" fill="url(#hexagons)"/>
        </svg>
    `;

    return svg;
}
```

### Canvas Drawing (Flat-Top)

```javascript
function drawHexagonGrid(ctx, cols, rows, sideLength) {
    const s = sideLength;
    const h = s * Math.sqrt(3);
    const xSpacing = 1.5 * s;
    const ySpacing = h / 2;

    function drawHexagon(x, y) {
        ctx.beginPath();
        ctx.moveTo(x - 0.5*s, y - 0.5*h);
        ctx.lineTo(x + 0.5*s, y - 0.5*h);
        ctx.lineTo(x + s,     y);
        ctx.lineTo(x + 0.5*s, y + 0.5*h);
        ctx.lineTo(x - 0.5*s, y + 0.5*h);
        ctx.lineTo(x - s,     y);
        ctx.closePath();
        ctx.stroke();
    }

    for (let row = 0; row < rows; row++) {
        for (let col = 0; col < cols; col++) {
            // Offset every other row by half a horizontal spacing
            const xOffset = (row % 2) * xSpacing;
            const x = col * xSpacing * 2 + xOffset;
            const y = row * ySpacing;
            drawHexagon(x, y);
        }
    }
}

// Usage
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');
drawHexagonGrid(ctx, 10, 10, 20);
```

### CSS Grid Approximation

While CSS Grid isn't perfect for hexagons, you can approximate the layout:

```css
.hex-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, 30px); /* 1.5s */
    gap: 17.32px; /* h/2 for s=20 */
}

.hex-grid .hex:nth-child(even) {
    margin-left: 15px; /* 0.5 × 1.5s */
}
```

---

## Visual ASCII Reference

### Flat-Top Honeycomb Pattern
```
    ___         ___         ___
   /   \___    /   \___    /   \
   \___/   \___/   \___/   \___/
   /   \___/   \___/   \___/   \
   \___/   \___/   \___/   \___/
       \___/   \___/   \___/
```

### Key Observations:
1. Each hexagon shares edges with 6 neighbors
2. Rows interlock - points of one row fit into valleys of the next
3. Horizontal rows overlap vertically by exactly 50%
4. The pattern repeats both horizontally and vertically

---

## Advanced Topics

### Hexagonal Coordinates

For game development or complex layouts, consider using **axial** or **cube** coordinate systems designed specifically for hexagons. These make neighbor-finding and pathfinding much easier.

**Resources:**
- [Red Blob Games - Hexagonal Grids](https://www.redblobgames.com/grids/hexagons/)
- Axial coordinates: `(q, r)` where movements are along two axes
- Cube coordinates: `(x, y, z)` where `x + y + z = 0`

### Performance Optimization

For large grids:
1. **Use SVG patterns or CSS background-image** - Browser handles tiling efficiently
2. **Viewport culling** - Only render visible hexagons
3. **Instancing** - For WebGL/Canvas, use geometry instancing
4. **Level of detail** - Reduce detail for distant hexagons

### Responsive Patterns

To make hexagon patterns scale:
```javascript
function getResponsiveSideLength() {
    const screenWidth = window.innerWidth;
    // Adjust formula based on your design
    return Math.max(10, Math.min(30, screenWidth / 50));
}
```

---

## Quick Reference Card

| Need | Flat-Top Formula | Pointy-Top Formula |
|------|------------------|-------------------|
| Height/Width calc | `h = s × √3` | `w = s × √3` |
| Horizontal spacing | `1.5s` | `(s × √3) / 2` |
| Vertical spacing | `(s × √3) / 2` | `1.5s` |
| Offset direction | Horizontal (x-axis) | Vertical (y-axis) |
| Offset amount | `1.5s` | `1.5s` |
| Pattern repeat | `3s × (s√3)` | `(s√3) × 3s` |

---

## Conclusion

The key to proper hexagon tessellation is understanding that **hexagons must nest and overlap**. Whether you choose flat-top or pointy-top orientation:

1. ✅ Use the correct spacing formula (always involves √3)
2. ✅ Rows/columns must be spaced at HALF the hexagon dimension
3. ✅ Alternate rows/columns must be offset
4. ✅ Pattern must repeat at the correct interval

Follow these principles, and your hexagons will tessellate beautifully into a proper honeycomb pattern.

---

## Additional Resources

- [Wikipedia: Hexagonal Tiling](https://en.wikipedia.org/wiki/Hexagonal_tiling)
- [Red Blob Games: Hexagonal Grids](https://www.redblobgames.com/grids/hexagons/)
- [MDN: SVG Patterns](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/pattern)
- [Canvas API Documentation](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)

---

**License**: This guide is released into the public domain. Use it freely in your projects!

**Contribute**: Found an error or have a suggestion? Please open an issue or submit a pull request.
