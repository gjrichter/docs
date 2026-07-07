# iXMaps Theme Style Properties Documentation

## Overview

Theme styles in iXMaps control how data is visualized on the map. This documentation covers all available style properties and their usage.

## Basic Style Structure

```javascript
.style({
    // Style properties go here
    type: "CHOROPLETH|EQUIDISTANT",
    colorscheme: ["5", "#FFFDD8", "#B5284B"],
    fillopacity: "0.7"
})
```

## Core Style Properties

### `type`
Defines the visualization type and behavior.

**Values:**
- `"CHOROPLETH"` - Color-coded areas
- `"CHART"` - Chart visualization
- `"DOT"` - Point markers
- `"BUBBLE"` - Bubble charts
- `"PIE"` - Pie charts
- `"BAR"` - Bar charts
- `"LINE"` - Line charts
- `"SYMBOL"` - Custom symbols
- `"TEXT"` - Text labels

**Modifiers:**
- `"EQUIDISTANT"` - Equal interval classification
- `"QUANTILE"` - Quantile classification
- `"NATURAL"` - Natural breaks classification
- `"AGGREGATE"` - Aggregate data
- `"ZOOMTO"` - Zoom to feature on click
- `"SIMPLELEGEND"` - Simple legend
- `"CATEGORICAL"` - Categorical data
- `"SORT"` - Sort data
- `"DOWN"` - Sort descending
- `"SYMMETRIC"` - Symmetric layout
- `"SIZEP4"` - Size proportional to value
- `"RECT"` - Rectangular layout
- `"RELOCATE"` - Relocate elements
- `"VALUES"` - Show values
- `"CIRCULARBOX"` - Circular box layout
- `"BOTTOMTITLE"` - Title at bottom

**Example:**
```javascript
.type("CHOROPLETH|EQUIDISTANT|ZOOMTO")
.type("CHART|BUBBLE|SIZEP4|AGGREGATE")
.type("CHART|PIE|CATEGORICAL|SORT|DOWN")
```

### `colorscheme`
Defines the color palette for visualization.

**Format:**
```javascript
colorscheme: [numberOfClasses, startColor, endColor, additionalColors...]
```

**Examples:**
```javascript
// Basic gradient
colorscheme: ["5", "#FFFDD8", "#B5284B"]

// Multiple colors
colorscheme: ["10", "#FFFDD8", "#B5284B", "#FCBA6C"]

// Named color schemes
colorscheme: ["5", "tableau10"]
colorscheme: ["10", "viridis"]
colorscheme: ["7", "plasma"]

// Single color
colorscheme: ["blue"]
colorscheme: ["#FF0000"]
```

### `fillopacity`
Controls the transparency of filled areas.

**Values:** `"0.0"` to `"1.0"`

**Example:**
```javascript
fillopacity: "0.7"
```

### `strokeopacity`
Controls the transparency of stroke/outline.

**Values:** `"0.0"` to `"1.0"`

**Example:**
```javascript
strokeopacity: "1.0"
```

### `stroke`
Defines the stroke color.

**Example:**
```javascript
stroke: "#000000"
stroke: "white"
```

### `strokewidth`
Defines the stroke width.

**Example:**
```javascript
strokewidth: "1"
strokewidth: "2.5"
```

## Chart-Specific Properties

### `symbols`
Defines the symbols used for chart elements.

**Values:**
- `"circle"`
- `"square"`
- `"triangle"`
- `"diamond"`
- `"star"`
- `"cross"`
- `"plus"`

**Example:**
```javascript
symbols: ["circle"]
symbols: ["square", "triangle", "diamond"]
```

### `valuescale`
Scales the size of chart elements.

**Example:**
```javascript
valuescale: "1.5"
valuescale: "0.8"
```

### `textscale`
Scales the size of text elements.

**Example:**
```javascript
textscale: "0.7"
textscale: "1.2"
```

### `units`
Defines the units for value display.

**Example:**
```javascript
units: "€"
units: "km²"
units: "%"
```

### `normalsizevalue`
Defines the reference value for normal size scaling.

**Example:**
```javascript
normalsizevalue: "500000"
normalsizevalue: "1000000"
```

### `aggregationscale`
Defines how data aggregates at different zoom levels.

**Format:**
```javascript
aggregationscale: [
    "1:1", "codice_comune",
    "1:1000000", "pr",
    "1:5000000", "regione"
]
```

**Example:**
```javascript
aggregationscale: [
    "1:1", "codice_comune",
    "1:1000000", "provincia",
    "1:5000000", "regione"
]
```

### `boxopacity`
Controls the opacity of aggregation boxes.

**Example:**
```javascript
boxopacity: "0"
boxopacity: "0.3"
```

### `boxupper`
Defines the upper limit for box display.

**Example:**
```javascript
boxupper: "1:200000"
boxupper: "1:500000"
```

### `valueupper`
Defines the upper limit for value display.

**Example:**
```javascript
valueupper: "1:20000"
valueupper: "1:50000"
```

### `showdata`
Controls whether to show data values.

**Values:** `"true"` or `"false"`

**Example:**
```javascript
showdata: "true"
```

### `name`
Defines the name of the chart.

**Example:**
```javascript
name: "chart"
name: "population_chart"
```

## Text and Label Properties

### `label`
Defines the label text.

**Example:**
```javascript
label: "items"
label: "Population"
```

### `title`
Defines the title of the theme.

**Example:**
```javascript
title: "Population by Municipality"
```

### `fontsize`
Defines the font size.

**Example:**
```javascript
fontsize: "12"
fontsize: "14px"
```

### `fontfamily`
Defines the font family.

**Example:**
```javascript
fontfamily: "Arial"
fontfamily: "sans-serif"
```

### `fontweight`
Defines the font weight.

**Values:** `"normal"`, `"bold"`, `"100"`, `"200"`, etc.

**Example:**
```javascript
fontweight: "bold"
fontweight: "normal"
```

### `textcolor`
Defines the text color.

**Example:**
```javascript
textcolor: "#000000"
textcolor: "white"
```

## Advanced Properties

### `shadow`
Controls shadow display.

**Values:** `"true"` or `"false"`

**Example:**
```javascript
shadow: "false"
shadow: "true"
```

### `refreshtimeout`
Defines refresh timeout in milliseconds.

**Example:**
```javascript
refreshtimeout: "0"
refreshtimeout: "5000"
```

### `scale`
Defines the scale factor.

**Example:**
```javascript
scale: "1"
scale: "1.5"
```

### `valuedecimals`
Defines the number of decimal places for values.

**Example:**
```javascript
valuedecimals: "0"
valuedecimals: "2"
```

### `lookupfield`
Defines the field for geographic lookup.

**Example:**
```javascript
lookupfield: "codice_comune"
lookupfield: "geometry"
lookupfield: "Latitudine|Longitudine"
```

### `dbtable`
Defines the data table name.

**Example:**
```javascript
dbtable: "themeDataObj"
dbtable: "population_data"
```

### `dbtableUrl`
Defines the URL for data loading.

**Example:**
```javascript
dbtableUrl: "https://example.com/data.csv"
```

### `dbtableType`
Defines the data type.

**Values:** `"csv"`, `"json"`, `"xml"`

**Example:**
```javascript
dbtableType: "csv"
dbtableType: "json"
```

### `datacache`
Controls data caching.

**Values:** `"true"` or `"false"`

**Example:**
```javascript
datacache: "true"
```

## Complete Style Examples

### Choropleth Map
```javascript
.style({
    type: "CHOROPLETH|EQUIDISTANT",
    colorscheme: ["5", "#FFFDD8", "#B5284B"],
    fillopacity: "0.7",
    stroke: "#FFFFFF",
    strokewidth: "1",
    strokeopacity: "0.8",
    showdata: "true",
    valuedecimals: "0",
    units: "people"
})
```

### Bubble Chart
```javascript
.style({
    type: "CHART|BUBBLE|SIZEP4|AGGREGATE",
    colorscheme: ["blue"],
    fillopacity: "0.6",
    symbols: ["circle"],
    valuescale: "1.5",
    textscale: "0.7",
    units: "€",
    normalsizevalue: "500000",
    aggregationscale: [
        "1:1", "codice_comune",
        "1:1000000", "pr",
        "1:5000000", "regione"
    ],
    boxopacity: "0",
    boxupper: "1:200000",
    showdata: "true",
    name: "chart"
})
```

### Pie Chart
```javascript
.style({
    type: "CHART|PIE|CATEGORICAL|SIZEP4|AGGREGATE",
    colorscheme: ["10", "tableau10"],
    fillopacity: "0.8",
    symbols: ["circle"],
    valuefield: "importo_totale_erogabile",
    valuescale: "1.5",
    textscale: "0.7",
    units: "€",
    normalsizevalue: "500000",
    aggregationscale: [
        "1:1", "codice_comune",
        "1:1000000", "pr",
        "1:5000000", "regione"
    ],
    boxopacity: "0",
    boxupper: "1:200000",
    valueupper: "1:20000",
    showdata: "true",
    name: "chart"
})
```

### Dot Map
```javascript
.style({
    type: "CHART|DOT|FAST|MULTIQUAD|ZOOMTO|SIMPLELEGEND",
    colorscheme: ["blue"],
    fillopacity: "0.7",
    shadow: "false",
    symbols: ["circle"],
    label: "items",
    units: "",
    refreshtimeout: "0",
    scale: "1",
    valuescale: "1",
    valuedecimals: "0",
    title: "dataset"
})
```

### Text Labels
```javascript
.style({
    type: "TEXT",
    fontsize: "12",
    fontfamily: "Arial",
    fontweight: "normal",
    textcolor: "#000000",
    fillopacity: "1.0"
})
```

## Style Property Reference Table

| Property | Type | Description | Example |
|----------|------|-------------|---------|
| `type` | String | Visualization type and modifiers | `"CHOROPLETH\|EQUIDISTANT"` |
| `colorscheme` | Array | Color palette definition | `["5", "#FFFDD8", "#B5284B"]` |
| `fillopacity` | String | Fill transparency | `"0.7"` |
| `strokeopacity` | String | Stroke transparency | `"1.0"` |
| `stroke` | String | Stroke color | `"#000000"` |
| `strokewidth` | String | Stroke width | `"1"` |
| `symbols` | Array | Chart symbols | `["circle"]` |
| `valuescale` | String | Value scaling factor | `"1.5"` |
| `textscale` | String | Text scaling factor | `"0.7"` |
| `units` | String | Value units | `"€"` |
| `normalsizevalue` | String | Reference size value | `"500000"` |
| `aggregationscale` | Array | Zoom level aggregation | `["1:1", "codice_comune"]` |
| `boxopacity` | String | Box transparency | `"0"` |
| `boxupper` | String | Box upper limit | `"1:200000"` |
| `valueupper` | String | Value upper limit | `"1:20000"` |
| `showdata` | String | Show data values | `"true"` |
| `name` | String | Chart name | `"chart"` |
| `label` | String | Label text | `"items"` |
| `title` | String | Theme title | `"Population"` |
| `fontsize` | String | Font size | `"12"` |
| `fontfamily` | String | Font family | `"Arial"` |
| `fontweight` | String | Font weight | `"bold"` |
| `textcolor` | String | Text color | `"#000000"` |
| `shadow` | String | Shadow display | `"false"` |
| `refreshtimeout` | String | Refresh timeout | `"0"` |
| `scale` | String | Scale factor | `"1"` |
| `valuedecimals` | String | Decimal places | `"0"` |
| `lookupfield` | String | Geographic lookup field | `"codice_comune"` |
| `dbtable` | String | Data table name | `"themeDataObj"` |
| `dbtableUrl` | String | Data URL | `"data.csv"` |
| `dbtableType` | String | Data type | `"csv"` |
| `datacache` | String | Data caching | `"true"` |

## Best Practices

1. **Use appropriate chart types** for your data
2. **Choose color schemes** that are accessible and meaningful
3. **Set proper opacity** for overlapping elements
4. **Use aggregation scales** for large datasets
5. **Include units** for better data interpretation
6. **Test performance** with large datasets
7. **Consider accessibility** in color choices

This documentation covers all the main theme style properties available in iXMaps. For more advanced usage and examples, refer to the official iXMaps documentation.