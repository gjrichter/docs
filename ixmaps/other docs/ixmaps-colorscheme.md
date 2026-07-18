# iXMaps colorschemes — draft material for future documentation

Raw draft covering everything now known about how iXMaps creates and modifies colors, to be
distilled into `colors_classification.qmd` (and possibly a dedicated new guide page). Verified
against `maps/svg/js-source/{maptheme,colorscheme}.js` and `ui/js/tools/{colorscheme,colorselect}.js`
— see `ixmaps_colorscheme_reference.md` at the repo root for the full source-level inventory this
draft is distilled from.

---

## Part 1 — Defining a colorscheme

Every `CHOROPLETH` or `CHART` layer that colors by value needs a `colorscheme`. The value you pass
to `.style({ colorscheme: ... })` is a small positional grammar:

```
colorscheme: [ classCount, colorA, colorB, param1, param2 ]
```

You can pass this as a real JS array, or as a string — `"5,#ffffcc,#253494"` (comma-delimited) or
`"5|#ffffcc|#253494"` (pipe-delimited). Strings containing `RGB(...)` must use `|` as the
delimiter, since the color's internal commas would otherwise be mistaken for the grammar's own
delimiters:

```javascript
colorscheme: "7|RGB(74,74,255)|RGB(245,41,38)|dynamic"   // correct — pipe-delimited
colorscheme: "7,RGB(74,74,255),RGB(245,41,38),dynamic"   // wrong — commas inside RGB() corrupt the split
```

### 1.1 Single color

```javascript
colorscheme: ["#0066cc"]
colorscheme: ["blue"]
```

### 1.2 Two-color gradient

```javascript
colorscheme: ["5", "#ffffcc", "#253494"]   // 5 classes, yellow → dark blue
```

By default (`param1` omitted, or `"auto"`/`"dynamic"`), the gradient is **not** a straight linear
interpolation — it expands the low end of the range so early classes are more visually distinct
from each other. Use `"linear"` for a plain straight interpolation instead:

```javascript
colorscheme: ["7", "#ffffcc", "#253494", "linear"]
```

`param1` accepts a shape keyword controlling how the gradient is distributed:

| Keyword | Shape |
|---|---|
| `linear` | Straight interpolation, cc1 → cc2 |
| `dynamic` / `auto` (default) | Expanding sweep — low end compressed, more contrast between low classes |
| `2low` | Sweep with the low end of the range expanded |
| `2high` | Sweep with the high end of the range expanded |
| `2narrow` | Compressed mid-range |
| `2wide` | Expanded mid-range |

::: {.callout-note}
## `2xxx` vs `3xxx` — two colors or three?
The `2low`/`2high`/`2narrow`/`2wide`/`2colors` keywords are for a plain **two-color** sweep, where
the midpoint is derived automatically from `cc1`/`cc2`. The `3low`/`3high`/`3narrow`/`3wide`/`3colors`
keywords signal that you're supplying an explicit **third, middle color** as the next parameter
(`param2`) instead of letting one be computed:

```javascript
colorscheme: ["24", "#c94f35", "#4f9153", "3colors", "#f2d16b"]   // explicit middle: #f2d16b
```

Each pair shares the same split-ratio shape (`low` = 75/25, `high` = 23/77, `narrow`/`wide` as
above) — the `2`/`3` prefix documents whether a middle color follows, it doesn't change the shape
itself.
:::

### 1.3 Explicit multi-stop palette

Pass every color explicitly and skip the generator entirely:

```javascript
colorscheme: ["#ffffcc","#c7e9b4","#41b6c4","#2c7fb8","#253494"]  // 5 explicit colors
```

### 1.4 Explicit middle color (3-stop gradient)

If `param1` isn't one of the shape keywords above, it's read as an explicit **middle color** for
the sweep, and the shape defaults to `auto`:

```javascript
colorscheme: ["24", "#c94f35", "#4f9153", "#f2d16b"]   // sweeps through #f2d16b in the middle
```

`param2` works the same way as a middle-color override, and also accepts `"warm"` (a warm cream
mid-tone) or `"cold"` (white) as shorthand:

```javascript
colorscheme: ["9", "blue", "red", "", "warm"]
```

### 1.5 Color input formats

Any color slot accepts:
- Hex — `"#0066cc"`
- `rgb(...)` / `rgba(...)` — `"rgb(0, 102, 204)"`
- Any of the 147 standard CSS color names — `"cornflowerblue"`

An unrecognized color name silently falls back to white — there's no error/warning if you typo a
color name, so double-check spelling if a class renders unexpectedly white.

### 1.6 Diverging scales

Use an even number of colors and set `rangecentervalue` to symmetrize the range around a
meaningful center point (e.g. 0 for a gain/loss map):

```javascript
.style({
    colorscheme:      ["#d73027","#f46d43","#fdae61","#abd9e9","#74add1","#4575b4"],
    rangecentervalue: 0,
    showdata:         "true"
})
```

The range is symmetrized regardless of class-count parity — an odd class count still works fine
(one class straddles the center); using an even count is purely a visual-design choice for a clean
split either side of the center, not a requirement.

### 1.7 Categorical binding

For discrete labels/categories rather than continuous numbers, use `CATEGORICAL` with a `values`
array pinning each category to a color slot by position:

```javascript
.type("CHART|BUBBLE|CATEGORICAL")
.style({
    colorscheme: ["#4fc3f7", "#ffb300", "#ef5350"],
    values:      ["low",     "medium",  "high"],   // strings — not numbers!
    showdata:    "true"
})
```

::: {.callout-tip}
## Sort categories alphabetically instead of by data order
Add `ORDER` to the type string (`CATEGORICAL|ORDER`) to assign colors to alphabetically-sorted
category values, instead of the order they happen to appear in the data.
:::

**A second, independent binding mechanism** exists for cases where the color category should come
from a *different* field than the one driving the display/label:

```javascript
.style({
    colorfield:   "region_type",                    // raw data field driving color
    colorvalues:  ["urban", "rural", "coastal"],     // fixes color-slot order, like `values` does
    colorscheme:  ["#4fc3f7", "#ffb300", "#ef5350"]
})
```

`colorfield` also accepts the special value `"$index$"`, which colors each row by its row index
rather than any field value — useful for arbitrary per-row color assignment unrelated to any real
data column.

### 1.8 Function-based colorschemes

For a palette that depends on the layer's own resolved classes (not knowable until the data
loads), pass a function reference instead of a color array:

```javascript
.style({ colorscheme: "ixmaps.colorScheme_speedmap" })
```

```javascript
ixmaps.colorScheme_speedmap = function (theme) {
    // theme.szLabelA     — one label per class, in class order
    // theme.colorScheme  — mutate in place: one hex string per class
    for (var i = 0; i < theme.szLabelA.length; i++) {
        if (theme.szLabelA[i].match(/^(45|50|55|60|65|70|75) mph/i)) {
            theme.colorScheme[i] = "#CE517F";
        }
        // ...
    }
};
```

::: {.callout-warning}
## Where the function must live
A **dotted** reference (`"ixmaps.colorScheme_speedmap"`) is resolved against iXMaps' own internal
namespace. A **bare, undotted** function name is instead resolved against the *outer embedding
page's* `window` — so if you define your callback as a plain global function (not namespaced under
`ixmaps.`), reference it by its bare name.
:::

### 1.9 `nodatacolor`

Fallback fill for any item with no matching class or value:

```javascript
.style({ nodatacolor: "#eeeeee" })
```

### 1.10 Changing a colorscheme at runtime

`map.Api.changeThemeStyle(...)` recognizes a few additional properties not available at initial
`.style()` definition time — useful for building interactive controls (dropdowns, sliders) that
change an existing theme's coloring live:

```javascript
map.Api.changeThemeStyle("colorscheme:spectrum,pastel;classes:10");
```

| Property | Effect |
|---|---|
| `colorscheme` | Replace the gradient/palette (class count carries over from the current theme) |
| `classes` | Change the number of classes, keeping the same colors/generator |
| `colorstyle` | Change the style preset of a `spectrum` colorscheme (see Part 2) without touching anything else |
| `colordef` | Set the fully-resolved color array directly, bypassing all gradient/palette generation |
| `colorschemegeneration` | Live-update just the gradient's mid-color (`warm`/`cold`/an explicit color) |

---

## Part 2 — Predefined colorschemes

### 2.1 Named categorical palettes

Instead of generating a gradient, name a built-in qualitative palette. Optionally add a class
count and a starting offset (colors wrap around cyclically if you ask for more than the palette
has):

```javascript
colorscheme: ["5", "tableau10"]        // 5 colors from tableau10
colorscheme: ["5", "tableau10", "3"]   // 5 colors starting at index 3
```

| Palette | Character |
|---|---|
| `tableau` / `tableau10` / `tableau20` | Standard Tableau qualitative sets (10 or 20 distinct hues) |
| `office` | MS-Office-style palette |
| `mineral` | Muted earth-tone palette |
| `pastel` | Soft, low-saturation palette |
| `harvest` | Warm autumnal palette |
| `fruit` | Bright, saturated palette |
| `kmeans` / `kmeansp` | High-distinctiveness palettes generated for cluster visualization |
| `pimp` | High-saturation, high-contrast palette |
| `intense` | Deep, saturated palette |
| `fluo` | Bright neon-toned palette |

### 2.2 Sequential (perceptually uniform) colormaps

For continuous data where perceptual uniformity matters (equal steps in value should look like
equal steps in color), use one of the standard sequential colormaps instead of a named qualitative
palette or a hand-picked gradient:

```javascript
colorscheme: ["9", "viridis"]   // dark purple → teal → yellow
colorscheme: ["9", "plasma"]    // indigo → magenta → yellow
colorscheme: ["9", "magma"]     // black → purple/red → pale yellow
```

Each works for any number of classes — colors are resampled evenly across the colormap's full
range rather than sliced from a fixed list, so `["3", "viridis"]` and `["24", "viridis"]` both
produce correctly-spanning results, not a truncated or repeating subset.

::: {.callout-note}
## These are the real matplotlib-derived colormaps
`viridis`, `plasma`, and `magma` here are the same perceptually-uniform, colorblind-friendly
colormaps used across matplotlib, D3, and most modern data-viz tooling — not an approximation.
Created by Nathaniel J. Smith, Stéfan van der Walt, and Eric Firing, and released under CC0
(public domain).
:::

### 2.3 Spectrum (hue-wheel) generator

A continuous rainbow-style generator, distinct from the named palettes above — walks a hue wheel
between two angles instead of picking from a fixed color list:

```javascript
colorscheme: ["24", "spectrum", "pastel", "0", "300"]
//             classCount, "spectrum", style, hueStart, hueEnd
```

- `hueStart`/`hueEnd` default to `270`/`0` if omitted.
- The third slot selects a style preset:

| Preset | Character |
|---|---|
| `default` | Full saturation/value |
| `pastel` | Soft, desaturated |
| `soft` | Gently muted |
| `hard` | High contrast |
| `light` | Light, airy tones |
| `pale` | Very low saturation |

::: {.callout-warning}
## Avoid the `work` preset
A `colorstyle: "work"` preset exists in the code but is currently broken — it produces invalid
colors. Use one of the presets listed above instead.
:::

### 2.4 Ready-made gradient recipes

A curated library of full recipe strings (`color1, color2, shape, mid-color`) ships as a
convenience for hand-picking a starting point — prepend your desired class count to use one:

```javascript
colorscheme: "7," + "#ffeeee,#dd0000,dynamic,cold"   // the "red" recipe, 7 classes
// → colorscheme: "7,#ffeeee,#dd0000,dynamic,cold"
```

A representative sample (see the full list in the source for more):

| Name | Recipe |
|---|---|
| `red` | `#ffeeee,#dd0000,dynamic,cold` |
| `blue` | `#eeeeff,#0000cc,dynamic,cold` |
| `green` | `#eeffee,#00cc00,dynamic,cold` |
| `heatmap` | `blue,#ffcc77,3low,red` |
| `density1`…`density5` | Sequential yellow/orange/red density ramps |
| `blue-red4` | `#3288BD,#D53E4F,3colors,#F7F7F7` (diverging, ColorBrewer-style) |
| `spectral` | `spectrum,default,200,0` |

---

## Part 3 — COMPOSECOLOR (multi-field color blending)

For layers driven by several numeric fields at once, `COMPOSECOLOR` blends each field's own base
color into a single composite, weighted by that field's value — instead of picking one
"dominant" field's color like plain `DOMINANT` does.

```javascript
.type("CHOROPLETH|DOMINANT|COMPOSECOLOR")
.style({
    colorscheme: ["#d73027", "#1a9850", "#4575b4"],   // one base color per field
    brightness:  0.7
})
```

Two blending modes, selected by an additional type flag:

| Mode | Type | Behavior |
|---|---|---|
| Additive (default) | `COMPOSECOLOR` | Light-mixing — colors combine like overlapping light sources (adding channels, brighter where multiple fields are high) |
| Subtractive | `COMPOSECOLOR\|SUBTRACTIVE` | Pigment-mixing — colors combine like overlapping ink/paint (darker where multiple fields are high) |

`brightness` (0–1) tunes the overall intensity of the resulting blend — lower values produce more
muted composites, higher values push toward saturated combined hues.

::: {.callout-tip}
## When to reach for this
`COMPOSECOLOR` is well suited to genuinely multivariate choropleths — e.g. three demographic
shares per polygon — where you want one glance to convey "which mix of factors dominates here"
without needing a legend per field.
:::

---

## Part 4 — Dynamic opacity (`DOPACITY*`)

Independent of `colorscheme`, a layer's fill/stroke opacity can be driven dynamically by data —
letting a map show "how much" alongside "which color class" in the same fill.

### 4.1 Type keys

Add one of these to the `type` string:

| Type key | Opacity driven by |
|---|---|
| `DOPACITY` | Value's position between min and median (single-sided) |
| `DOPACITYMIN` | Distance below the maximum (fades out toward the max) |
| `DOPACITYMAX` | Distance above the minimum (fades in toward the max) |
| `DOPACITYLOG` | Same as `DOPACITY`, on a logarithmic scale — better for skewed distributions |
| `DOPACITYMINMAX` (alias `BIPOLAR`) | Distance from the median, in whichever direction (toward min or max) the value lies — for showing both extremes |
| `DOPACITYMEAN` | Percent deviation from the field's mean |
| `DOPACITYLOGMEAN` | Same as `DOPACITYMEAN`, log-scaled |
| `DOPACITYLOGMAX` | Value-over-max ratio, log-scaled (used with `DOMINANT`-style multi-field themes) |
| `DOPACITYPOWMAX` | Value-over-max ratio, power-curved |

```javascript
.type("CHOROPLETH|QUANTILE|DOPACITYMAX")
```

### 4.2 Style parameters

| Property | Effect |
|---|---|
| `dopacitypow` | Exponent for the power-curve — values `>1` push more contrast toward the high end, `<1` toward the low end |
| `dopacityscale` | Linear multiplier applied to the computed ratio before curving — use to boost or dampen the overall opacity spread |

Resulting opacity is always clamped between ~0 and the layer's own `opacity` setting (default 0.9),
so these parameters shape the curve within that range rather than overriding it.

### 4.3 Value binding — `alphafield`

By default, `DOPACITY*` derives opacity from the same value driving the color class. To drive
opacity from a **different field** entirely, set `alphafield`:

```javascript
.style({
    alphafield: "population_density",
    dopacitypow: 1.5
})
```

When `alphafield` is set, opacity is computed purely from that field's own min/max range across
the layer — completely decoupled from whatever field is driving the color classification.

### 4.4 Special case — density-normalized opacity

Two distinct "density" mechanisms exist, easy to confuse:

**Classification density** — add `DENSITY` to the type string to convert the *classification
value itself* into a per-area density (value ÷ polygon area) before it's classified into color
classes. This changes what the map's colors mean (raw totals vs. density), not just the opacity.

```javascript
.type("CHOROPLETH|QUANTILE|DENSITY")
```

**Opacity density** — a separate, narrower mechanism: set `alphafield100` to the literal string
`"$density$"` alongside `alphafield` on a `CHOROPLETH` (not `CHART`) layer. This normalizes the
*opacity-driving* field by polygon area before computing `DOPACITY*` opacity — so a small dense
polygon and a large sparse polygon with the same raw `alphafield` total get proportionally
different opacity, reflecting true density rather than raw magnitude:

```javascript
.type("CHOROPLETH|QUANTILE|DOPACITYMAX")
.style({
    alphafield:    "incident_count",
    alphafield100: "$density$"
})
```

::: {.callout-note}
## Use this when raw counts would mislead
This is the right tool when comparing polygons of very different sizes — e.g. incident counts
across postal-code zones of wildly different areas — where opacity should reflect concentration,
not just absolute magnitude.
:::

---

*Draft status: raw material for a future revision of `colors_classification.qmd`. Not yet wired
into `_quarto.yml` / the rendered site.*
