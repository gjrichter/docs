Absolutely! Here’s a clear explanation of how **user-coded charts** can be included in iXMaps themes, including the workflow, requirements, and a practical example.

---

# Including User-Coded Charts in iXMaps Themes

## 1. **What Are User-Coded Charts?**

User-coded charts in iXMaps are custom JavaScript functions (often using D3.js or SVG) that you write to render map symbols or charts in your own style, beyond the built-in chart types. These functions are then referenced in your theme definition, allowing iXMaps to call your code for each map feature.

---

## 2. **How Does It Work?**

- You write a JavaScript function that draws a chart (e.g., a custom bar, lollipop, or pictogram) using D3 or SVG.
- You register this function in the global `ixmaps` namespace.
- In your theme definition, you set the `type` property to `"CHART|USER"` and specify the function name in the `chartdraw` property.
- iXMaps will call your function for each data item, passing in arguments like the SVG target, data values, and theme options.

---

## 3. **Step-by-Step Example**

### **A. Write Your Chart Function**

Suppose you want to create a custom "pinnacle" chart. You would write a function like this (in a file such as `usercharts/d3/chart.js`):

```javascript
window.ixmaps = window.ixmaps || {};
(function() {
    ixmaps.pinnacleChart = function(SVGDocument, args) {
        // Your D3 or SVG drawing code here
        var svg = d3.select(args.target);
        var nHeight = args.value / 1000 * 50; // Example scaling
        svg.append("rect")
            .attr("x", 0)
            .attr("y", -nHeight)
            .attr("width", 20)
            .attr("height", nHeight)
            .attr("fill", "steelblue");
        // ... more drawing code ...
        return {x:0, y:0}; // Return the offset for the next chart if needed
    };
})();
```

### **B. Load Your Chart Script**

Make sure your custom chart script is loaded **before** the map is initialized. For example, in your HTML:

```html
<script src="https://d3js.org/d3.v5.min.js"></script>
<script src="usercharts/d3/chart.js"></script>
<script src="maps/svg/js/mapapi.js"></script>
<!-- ... other ixmaps scripts ... -->
```

### **C. Reference Your Chart in the Theme**

When defining your theme, set the `type` to `"CHART|USER"` and specify your function name in `chartdraw`:

```javascript
ixmaps.setTheme({
    layer: "MyLayer",
    field: "value",
    style: {
        type: "CHART|USER",
        chartdraw: "pinnacleChart", // Name of your function
        // ... other style properties ...
    }
});
```

Or in JSON:

```json
{
  "type": "CHART|USER",
  "chartdraw": "pinnacleChart",
  "normalsizevalue": "1000",
  "sizepow": "2",
  "scale": "1.0"
}
```

---

## 4. **What Does iXMaps Pass to Your Function?**

Your function receives two arguments:
- `SVGDocument`: The SVG DOM or D3 selection to draw into.
- `args`: An object containing:
  - `target`: The SVG group or element to append to.
  - `value`, `values`: The data value(s) for this feature.
  - `theme`: The theme object (with style, color, etc.).
  - `item`: The data item (feature).
  - `class`: The class index (for color schemes).
  - ...and more, depending on context.

---

## 5. **Tips and Best Practices**

- **Namespace:** Always attach your function to `ixmaps` (e.g., `ixmaps.myChart`).
- **Return Value:** Return an object with `{x, y}` if you want to control the offset for the next chart.
- **D3.js:** You can use D3.js or plain SVG DOM methods.
- **Reusability:** You can create multiple chart functions and select them per theme.
- **Debugging:** Use `console.log(args)` inside your function to inspect what’s available.

---

## 6. **Full Example**

**Custom Chart Function (usercharts/d3/my_custom_chart.js):**
```javascript
window.ixmaps = window.ixmaps || {};
(function() {
    ixmaps.myCustomChart = function(SVGDocument, args) {
        var svg = d3.select(args.target);
        var nHeight = args.value / 1000 * 50;
        svg.append("circle")
            .attr("cx", 10)
            .attr("cy", -nHeight)
            .attr("r", 10)
            .attr("fill", "orange");
        return {x:0, y:0};
    };
})();
```

**Theme Definition:**
```javascript
.style({
    type: "CHART|USER",
    chartdraw: "myCustomChart",
    normalsizevalue: "1000",
    sizepow: "2"
})
```

---

## 7. **Summary Table**

| Property      | Purpose                                      | Example Value      |
|---------------|----------------------------------------------|--------------------|
| `type`        | Chart type, must include `USER`              | `"CHART|USER"`     |
| `chartdraw`   | Name of your chart function                  | `"myCustomChart"`  |
| `normalsizevalue` | Reference value for sizing               | `"1000"`           |
| `sizepow`     | Sizing exponent                             | `"2"`              |
| `scale`       | Overall scale multiplier                    | `"1.0"`            |

---

## 8. **Further Reading**

- [iXMaps Theme Documentation](#)
- [D3.js Documentation](https://d3js.org/)
- [iXMaps Example Gallery](#)

---

**In summary:**  
Write your chart function, load it before the map, and reference it in your theme with `type: "CHART|USER"` and `chartdraw: "yourFunctionName"`. iXMaps will call your function for each feature, letting you fully customize the chart rendering!