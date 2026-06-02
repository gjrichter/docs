# ixMaps Quick Start Guide

## Overview

ixMaps is a JavaScript library for creating interactive SVG-based maps with data visualization. This quick start guide will help you get up and running with ixMaps in minutes.

## Prerequisites

- Modern web browser with SVG support
- Basic knowledge of HTML, CSS, and JavaScript
- Web server (local or remote) for serving files

## Step 1: Basic HTML Setup

Create a new HTML file with the following structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ixMaps Quick Start</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }
        #map-container {
            width: 100%;
            height: 100vh;
        }
    </style>
</head>
<body>
    <!-- Map container -->
    <div id="map-container"></div>

    <!-- Include ixMaps library -->
    <script src="https://gjrichter.github.io/ixmaps/ui/js/htmlgui_flat.js"></script>
    
    <!-- Your map code -->
    <script>
        // Map code will go here
    </script>
</body>
</html>
```

## Step 2: Basic Map Embedding

Add this code inside the `<script>` tag:

```javascript
// Embed a basic map
ixmaps.embed("map-container", {
    name: "quickstart-map",
    mapService: "leaflet",
    mapType: "CartoDB - Positron",
    width: "100%",
    height: "100%",
    legend: "true",
    tools: "true"
}, function(map) {
    // Map is ready!
    console.log("Map loaded successfully");
    
    // Set initial view (Italy)
    map.view([42.7954, 13.2083], 9);
});
```

## Step 3: Add Data Visualization

Enhance your map with data:

```javascript
ixmaps.embed("map-container", {
    name: "quickstart-map",
    mapService: "leaflet",
    mapType: "CartoDB - Positron",
    width: "100%",
    height: "100%",
    legend: "true",
    tools: "true"
}, function(map) {
    // Set initial view
    map.view([42.7954, 13.2083], 9);
    
    // Configure map options
    map.options({
        featurescaling: "true",
        objectscaling: "dynamic",
        basemapopacity: "0.8"
    });
    
    // Add a data layer
    map.layer(ixmaps.layer("ITALIA_Comuni_2022")
        .data({
            url: "https://s3.eu-west-1.amazonaws.com/data.ixmaps.com/sample/population.csv",
            type: "csv"
        })
        .binding({
            value: "population",
            position: "codice_comune",
            title: "nome_comune"
        })
        .type("CHOROPLETH|EQUIDISTANT")
        .style({
            colorscheme: ["5", "#FFFDD8", "#B5284B"],
            fillopacity: "0.7"
        })
        .define()
    );
    
    // Set attribution
    map.attribution("Data source: Sample Data");
});
```

## Step 4: Interactive Features

Add interactive elements:

```javascript
ixmaps.embed("map-container", {
    name: "quickstart-map",
    mapService: "leaflet",
    mapType: "CartoDB - Positron",
    width: "100%",
    height: "100%",
    legend: "true",
    tools: "true"
}, function(map) {
    // Set initial view
    map.view([42.7954, 13.2083], 9);
    
    // Configure map options
    map.options({
        featurescaling: "true",
        objectscaling: "dynamic",
        basemapopacity: "0.8"
    });
    
    // Add data layer
    map.layer(ixmaps.layer("ITALIA_Comuni_2022")
        .data({
            url: "https://s3.eu-west-1.amazonaws.com/data.ixmaps.com/sample/population.csv",
            type: "csv"
        })
        .binding({
            value: "population",
            position: "codice_comune",
            title: "nome_comune"
        })
        .type("CHOROPLETH|EQUIDISTANT")
        .style({
            colorscheme: ["5", "#FFFDD8", "#B5284B"],
            fillopacity: "0.7"
        })
        .define()
    );
    
    // Add interactive features
    map.require("https://gjrichter.github.io/ixmaps/ui/js/tools/tooltip_basic.js");
    
    // Set attribution and legend
    map.attribution("Data source: Sample Data");
    map.legend("<h3>Population by Municipality</h3>");
    
    // Add zoom controls
    map.message("Use mouse wheel to zoom, drag to pan", 3000);
});
```

## Step 5: Custom Data

Use your own data:

```javascript
// Sample data (replace with your own)
var sampleData = [
    { codice_comune: "001001", nome_comune: "Roma", population: 2873000 },
    { codice_comune: "001002", nome_comune: "Milano", population: 1352000 },
    { codice_comune: "001003", nome_comune: "Napoli", population: 967000 }
];

ixmaps.embed("map-container", {
    name: "quickstart-map",
    mapService: "leaflet",
    mapType: "CartoDB - Positron",
    width: "100%",
    height: "100%",
    legend: "true",
    tools: "true"
}, function(map) {
    // Set initial view
    map.view([42.7954, 13.2083], 9);
    
    // Configure map options
    map.options({
        featurescaling: "true",
        objectscaling: "dynamic"
    });
    
    // Add custom data layer
    map.layer(ixmaps.layer("ITALIA_Comuni_2022")
        .data({
            data: sampleData,
            type: "json"
        })
        .binding({
            value: "population",
            position: "codice_comune",
            title: "nome_comune"
        })
        .type("CHART|BUBBLE")
        .style({
            colorscheme: ["blue"],
            fillopacity: "0.6",
            symbols: ["circle"]
        })
        .define()
    );
    
    map.attribution("Custom Data");
});
```

## Step 6: Multiple Themes

Add multiple data layers:

```javascript
ixmaps.embed("map-container", {
    name: "quickstart-map",
    mapService: "leaflet",
    mapType: "CartoDB - Positron",
    width: "100%",
    height: "100%",
    legend: "true",
    tools: "true"
}, function(map) {
    // Set initial view
    map.view([42.7954, 13.2083], 9);
    
    // Configure map options
    map.options({
        featurescaling: "true",
        objectscaling: "dynamic"
    });
    
    // Theme 1: Choropleth
    map.layer(ixmaps.layer("ITALIA_Comuni_2022")
        .data({
            url: "https://s3.eu-west-1.amazonaws.com/data.ixmaps.com/sample/population.csv",
            type: "csv"
        })
        .binding({
            value: "population",
            position: "codice_comune"
        })
        .type("CHOROPLETH|EQUIDISTANT")
        .style({
            colorscheme: ["5", "#FFFDD8", "#B5284B"],
            fillopacity: "0.7"
        })
        .define()
    );
    
    // Theme 2: Bubble chart
    map.layer(ixmaps.layer("ITALIA_Comuni_2022")
        .data({
            url: "https://s3.eu-west-1.amazonaws.com/data.ixmaps.com/sample/gdp.csv",
            type: "csv"
        })
        .binding({
            value: "gdp",
            size: "gdp",
            position: "codice_comune"
        })
        .type("CHART|BUBBLE")
        .style({
            colorscheme: ["blue"],
            fillopacity: "0.6"
        })
        .define()
    );
    
    map.attribution("Multiple Data Sources");
});
```

## Step 7: Advanced Configuration

Add advanced features:

```javascript
ixmaps.embed("map-container", {
    name: "quickstart-map",
    mapService: "leaflet",
    mapType: "CartoDB - Positron",
    width: "100%",
    height: "100%",
    legend: "true",
    tools: "true",
    search: "Italy"
}, function(map) {
    // Set initial view
    map.view([42.7954, 13.2083], 9);
    
    // Advanced options
    map.options({
        featurescaling: "dynamic",
        objectscaling: "dynamic",
        normalSizeScale: "50000000",
        dynamicScalePow: "3",
        flushChartDraw: "1000000",
        basemapopacity: "0.8",
        hideOnPan: "false",
        freezeOnPan: "false"
    });
    
    // Add data layer
    map.layer(ixmaps.layer("ITALIA_Comuni_2022")
        .data({
            url: "https://s3.eu-west-1.amazonaws.com/data.ixmaps.com/sample/population.csv",
            type: "csv"
        })
        .binding({
            value: "population",
            position: "codice_comune",
            title: "nome_comune"
        })
        .type("CHOROPLETH|EQUIDISTANT|ZOOMTO")
        .style({
            colorscheme: ["5", "#FFFDD8", "#B5284B"],
            fillopacity: "0.7",
            showdata: "true"
        })
        .define()
    );
    
    // Add tooltips
    map.require("https://gjrichter.github.io/ixmaps/ui/js/tools/tooltip_basic.js");
    
    // Set attribution and legend
    map.attribution("Data source: Sample Data");
    map.legend("<h3>Population by Municipality</h3><p>Hover over areas for details</p>");
    
    // Welcome message
    map.message("Welcome to ixMaps! Use mouse wheel to zoom, drag to pan", 5000);
});
```

## Complete Example

Here's a complete working example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ixMaps Quick Start</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }
        #map-container {
            width: 100%;
            height: 100vh;
        }
        .controls {
            position: absolute;
            top: 10px;
            left: 10px;
            z-index: 1000;
            background: white;
            padding: 10px;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }
        .controls button {
            margin: 5px;
            padding: 5px 10px;
            border: none;
            background: #007cba;
            color: white;
            border-radius: 3px;
            cursor: pointer;
        }
        .controls button:hover {
            background: #005a87;
        }
    </style>
</head>
<body>
    <div class="controls">
        <button onclick="zoomIn()">Zoom In</button>
        <button onclick="zoomOut()">Zoom Out</button>
        <button onclick="resetView()">Reset View</button>
    </div>
    
    <div id="map-container"></div>

    <script src="https://gjrichter.github.io/ixmaps/ui/js/htmlgui_flat.js"></script>
    
    <script>
        var mapInstance = null;
        
        // Embed the map
        ixmaps.embed("map-container", {
            name: "quickstart-map",
            mapService: "leaflet",
            mapType: "CartoDB - Positron",
            width: "100%",
            height: "100%",
            legend: "true",
            tools: "true"
        }, function(map) {
            mapInstance = map;
            
            // Set initial view
            map.view([42.7954, 13.2083], 9);
            
            // Configure map options
            map.options({
                featurescaling: "true",
                objectscaling: "dynamic",
                basemapopacity: "0.8"
            });
            
            // Add data layer
            map.layer(ixmaps.layer("ITALIA_Comuni_2022")
                .data({
                    url: "https://s3.eu-west-1.amazonaws.com/data.ixmaps.com/sample/population.csv",
                    type: "csv"
                })
                .binding({
                    value: "population",
                    position: "codice_comune",
                    title: "nome_comune"
                })
                .type("CHOROPLETH|EQUIDISTANT")
                .style({
                    colorscheme: ["5", "#FFFDD8", "#B5284B"],
                    fillopacity: "0.7"
                })
                .define()
            );
            
            // Add tooltips
            map.require("https://gjrichter.github.io/ixmaps/ui/js/tools/tooltip_basic.js");
            
            // Set attribution and legend
            map.attribution("Data source: Sample Data");
            map.legend("<h3>Population by Municipality</h3>");
            
            // Welcome message
            map.message("ixMaps Quick Start - Use mouse wheel to zoom, drag to pan", 5000);
        });
        
        // Control functions
        function zoomIn() {
            if (mapInstance) {
                ixmaps.zoomIn();
            }
        }
        
        function zoomOut() {
            if (mapInstance) {
                ixmaps.zoomOut();
            }
        }
        
        function resetView() {
            if (mapInstance) {
                mapInstance.view([42.7954, 13.2083], 9);
            }
        }
    </script>
</body>
</html>
```

## Next Steps

1. **Customize the map**: Change colors, add more data layers, or modify the base map
2. **Add interactivity**: Implement click handlers, filters, or search functionality
3. **Optimize performance**: Use data filtering and appropriate chart types for large datasets
4. **Deploy**: Host your map on a web server and share it with others

## Troubleshooting

- **Map not loading**: Check browser console for errors and ensure SVG support
- **Data not displaying**: Verify data URLs are accessible and format is correct
- **Performance issues**: Use appropriate options for large datasets and enable feature scaling

## Resources

- [ixMaps Documentation](https://gjrichter.github.io/ixmaps/)
- [API Reference](https://gjrichter.github.io/ixmaps/docs/)
- [Examples Gallery](https://gjrichter.github.io/ixmaps/examples/)

This quick start guide should get you up and running with ixMaps in no time!