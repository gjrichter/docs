I need to search for the `themeStyleTranslateA` array in the iXMaps codebase to find all the style properties it contains.

Ran tool
Now let me read the `themeStyleTranslateA` array definition to see all the style properties:

Read file: maps/svg/js/maptheme.js
Let me continue reading to see if there are more properties in the array:

Read file: maps/svg/js/maptheme.js
Now I have the complete `themeStyleTranslateA` array. Let me create a comprehensive table of all the style properties:

# iXMaps Theme Style Properties Reference Table

Based on the `themeStyleTranslateA` array in the iXMaps codebase, here are all the available style properties:

| Style Property | Object Property | Type | Description | Example |
|----------------|-----------------|------|-------------|---------|
| `opacity` | `nOpacity` | Number | Overall opacity | `"0.8"` |
| `fillopacity` | `fillOpacity` | Number | Fill opacity | `"0.7"` |
| `autoopacity` | `autoOpacity` | Boolean | Auto opacity | `"true"` |
| `shadow` | `fOrigShadow` | Boolean | Shadow display | `"false"` |
| `blur` | `nBlur` | Number | Blur effect | `"2"` |
| `filter` | `szFilter` | String | CSS filter | `"blur(2px)"` |
| `dfilter` | `nDeltaFilter` | Number | Delta filter | `"1"` |
| `filterfield` | `szFilterField` | String | Filter field | `"category"` |
| `visible` | `fVisible` | Boolean | Visibility | `"true"` |
| `dbtable` | `coTable` | String | Data table name | `"themeDataObj"` |
| `dbtableUrl` | `coTableUrl` | String | Data table URL | `"data.csv"` |
| `dbtableType` | `coTableType` | String | Data table type | `"csv"` |
| `dbtableExt` | `coTableExt` | String | Data table extension | `".csv"` |
| `dbtableProcess` | `coTableProcess` | String | Data processing function | `"processData"` |
| `dbtableQuery` | `coTableQuery` | String | Data query | `"SELECT * FROM data"` |
| `datacache` | `fDataCache` | Boolean | Data caching | `"true"` |
| `itemfield` | `szItemField` | String | Item field | `"id"` |
| `lookupfield` | `szSelectionField` | String | Geographic lookup field | `"codice_comune"` |
| `lookuptoupper` | `fSelectionFieldToUpper` | Boolean | Convert lookup to uppercase | `"true"` |
| `lookupsuffix` | `szSelectionFieldSuffix` | String | Lookup field suffix | `"_code"` |
| `lookupdigits` | `nSelectionFieldDigits` | Number | Lookup field digits | `"6"` |
| `lookuptonumber` | `fSelectionFieldToNumber` | Boolean | Convert lookup to number | `"true"` |
| `lookupfield2` | `szSelectionField2` | String | Secondary lookup field | `"codice_provincia"` |
| `showdata` | `fShowData` | Boolean | Show data values | `"true"` |
| `datafields` | `szDataFieldsA` | Array | Data fields to display | `["field1", "field2"]` |
| `userdraw` | `userDraw` | Function | Custom drawing function | `"customDraw"` |
| `child` | `fChild` | Boolean | Child theme flag | `"false"` |
| `crsdatum` | `szCRSDatum` | String | Coordinate reference system datum | `"WGS84"` |
| `crsutmzone` | `szCRSUTMZone` | String | UTM zone | `"32N"` |
| `server` | `szServer` | String | Server URL | `"https://api.example.com"` |
| `ranges` | `szRangesA` | Array | Value ranges | `["0-100", "101-200"]` |
| `rangecentervalue` | `nRangeCenterValue` | Number | Range center value | `"100"` |
| `symbols` | `szSymbolsA` | Array | Chart symbols | `["circle", "square"]` |
| `values` | `szValuesA` | Array | Values array | `["val1", "val2"]` |
| `colorvalues` | `szColorValuesA` | Array | Color values | `["red", "blue"]` |
| `symbolvalues` | `szSymbolValuesA` | Array | Symbol values | `["circle", "square"]` |
| `label` | `szOrigLabelA` | Array | Labels | `["Label 1", "Label 2"]` |
| `valuemap` | `valueMap` | Object | Value mapping object | `{"key1": "value1"}` |
| `xaxis` | `szXaxisA` | Array | X-axis values | `["cat1", "cat2"]` |
| `units` | `szUnits` | String | Value units | `"€"` |
| `labelunits` | `szLabelUnits` | String | Label units | `"people"` |
| `titleunits` | `szTitleUnits` | String | Title units | `"Population"` |
| `units100` | `szUnits100` | String | Units for 100% values | `"%"` |
| `sizevalueunits` | `szSizeValueUnits` | String | Size value units | `"km²"` |
| `alphavalueunits` | `szAlphaValueUnits` | String | Alpha value units | `"%"` |
| `legendunits` | `szLegendUnits` | String | Legend units | `"units"` |
| `weights` | `szWeights` | String | Weight values | `"1,2,3"` |
| `align` | `szAlign` | String | Alignment | `"center"` |
| `offsetx` | `nOffsetX` | Number | X offset | `"10"` |
| `offsety` | `nOffsetY` | Number | Y offset | `"5"` |
| `rotation` | `nRotation` | Number | Rotation angle | `"45"` |
| `refreshtimeout` | `nRefreshTimeout` | Number | Refresh timeout | `"5000"` |
| `normalsizevalue` | `nNormalSizeValue` | Number | Normal size reference value | `"500000"` |
| `normalsizescale` | `szNormalSizeScale` | String | Normal size scale | `"1.0"` |
| `scale` | `nScale` | Number | Scale factor | `"1.5"` |
| `rangescale` | `nRangeScale` | Number | Range scale | `"2.0"` |
| `sizepow` | `nSizePow` | Number | Size power | `"3"` |
| `outlierscale` | `nOutlierScale` | Number | Outlier scale | `"1.2"` |
| `colorfield` | `szColorField` | String | Color field | `"category"` |
| `symbolfield` | `szSymbolField` | String | Symbol field | `"type"` |
| `valuefield` | `szValueField` | String | Value field | `"population"` |
| `labelfield` | `szLabelField` | String | Label field | `"name"` |
| `sizefield` | `szSizeField` | String | Size field | `"area"` |
| `timefield` | `szTimeField` | String | Time field | `"date"` |
| `alphafield` | `szAlphaField` | String | Alpha field | `"opacity"` |
| `alphafield100` | `szAlphaField100` | String | Alpha field for 100% | `"opacity100"` |
| `xfield` | `szXField` | String | X coordinate field | `"longitude"` |
| `yfield` | `szYField` | String | Y coordinate field | `"latitude"` |
| `dopacitypow` | `nDopacityPow` | Number | Dynamic opacity power | `"2"` |
| `dopacityramp` | `szDopacityRamp` | String | Dynamic opacity ramp | `"linear"` |
| `dopacityscale` | `nDopacityScale` | Number | Dynamic opacity scale | `"1.0"` |
| `brightness` | `nBrightness` | Number | Brightness adjustment | `"1.2"` |
| `buffersize` | `nBufferSize` | Number | Buffer size | `"100"` |
| `bufferstep` | `nBufferSizeStep` | Number | Buffer step size | `"10"` |
| `field100min` | `nField100Min` | Number | Field 100 minimum | `"0"` |
| `fractionscale` | `nFractionScale` | Number | Fraction scale | `"1.0"` |
| `minvalue` | `nMinValue` | Number | Minimum value | `"0"` |
| `maxvalue` | `nMaxValue` | Number | Maximum value | `"1000000"` |
| `lowvalue` | `nLowValue` | Number | Low value threshold | `"100"` |
| `highvalue` | `nHighValue` | Number | High value threshold | `"10000"` |
| `textfont` | `szTextFont` | String | Text font | `"Arial"` |
| `textcolor` | `szTextColor` | String | Text color | `"#000000"` |
| `textscale` | `nTextScale` | Number | Text scale | `"0.7"` |
| `linecolor` | `szLineColor` | String | Line color | `"#FF0000"` |
| `linewidth` | `nLineWidth` | Number | Line width | `"2"` |
| `markersize` | `nMarkerSize` | Number | Marker size | `"10"` |
| `gapsize` | `nGapSize` | Number | Gap size | `"5"` |
| `bordercolor` | `szBorderColor` | String | Border color | `"#000000"` |
| `borderstyle` | `szBorderStyle` | String | Border style | `"solid"` |
| `borderwidth` | `szBorderWidth` | Number | Border width | `"1"` |
| `borderradius` | `nBorderRadius` | Number | Border radius | `"5"` |
| `boxcolor` | `szBoxColor` | String | Box color | `"#FFFFFF"` |
| `boxopacity` | `nBoxOpacity` | Number | Box opacity | `"0.8"` |
| `boxmargin` | `nBoxMargin` | Number | Box margin | `"10"` |
| `textplacement` | `szTextPlacement` | String | Text placement | `"center"` |
| `infotitle` | `szInfoTitle` | String | Info title | `"Information"` |
| `titlefield` | `szTitleField` | String | Title field | `"name"` |
| `snippetfield` | `szSnippetField` | String | Snippet field | `"description"` |
| `exclude` | `szExcludeA` | Array | Excluded values | `["excluded1", "excluded2"]` |
| `nodatacolor` | `szNoDataColor` | String | No data color | `"#CCCCCC"` |
| `titleupper` | `szTitleUpper` | String | Title upper limit | `"1:1000000"` |
| `titlelower` | `szTitleLower` | String | Title lower limit | `"1:100000"` |
| `labelupper` | `szLabelUpper` | String | Label upper limit | `"1:500000"` |
| `labellower` | `szLabelLower` | String | Label lower limit | `"1:50000"` |
| `valueupper` | `szValueUpper` | String | Value upper limit | `"1:20000"` |
| `valuelower` | `szValueLower` | String | Value lower limit | `"1:2000"` |
| `glowupper` | `szGlowUpper` | String | Glow upper limit | `"1:100000"` |
| `glowlower` | `szGlowLower` | String | Glow lower limit | `"1:10000"` |
| `chartupper` | `szChartUpper` | String | Chart upper limit | `"1:500000"` |
| `chartlower` | `szChartLower` | String | Chart lower limit | `"1:50000"` |
| `layerupper` | `szLayerUpper` | String | Layer upper limit | `"1:1000000"` |
| `layerlower` | `szLayerLower` | String | Layer lower limit | `"1:100000"` |
| `featureupper` | `szFeatureUpper` | String | Feature upper limit | `"1:200000"` |
| `featurelower` | `szFeatureLower` | String | Feature lower limit | `"1:20000"` |
| `boxupper` | `szBoxUpper` | String | Box upper limit | `"1:200000"` |
| `boxlower` | `szBoxLower` | String | Box lower limit | `"1:20000"` |
| `shadowupper` | `szShadowUpper` | String | Shadow upper limit | `"1:100000"` |
| `shadowlower` | `szShadowLower` | String | Shadow lower limit | `"1:10000"` |
| `declutterupper` | `szDeclutterUpper` | String | Declutter upper limit | `"1:50000"` |
| `valuescale` | `nValueScale` | Number | Value scale | `"1.5"` |
| `valuecolor` | `szValueColor` | String | Value color | `"#000000"` |
| `minvaluesize` | `nValueSizeMin` | Number | Minimum value size | `"5"` |
| `minvaluevalue` | `nValueValueMin` | Number | Minimum value value | `"100"` |
| `valuedecimals` | `nValueDecimals` | Number | Value decimal places | `"0"` |
| `fadevaluepow` | `szFadeValuePow` | String | Fade value power | `"2"` |
| `fadenegative` | `nFadeNegative` | Number | Fade negative values | `"1"` |
| `centerpart` | `szCenterPart` | String | Center part | `"true"` |
| `clipframes` | `nClipFrames` | Number | Clip frames | `"10"` |
| `clipframerate` | `nClipFrameRate` | Number | Clip frame rate | `"30"` |
| `cliplegend` | `nClipColorLegend` | Number | Clip color legend | `"1"` |
| `clipparts` | `nClipParts` | Number | Clip parts | `"5"` |
| `minchartsize` | `nChartSizeMin` | Number | Minimum chart size | `"10"` |
| `maxcharts` | `nMaxCharts` | Number | Maximum charts | `"1000"` |
| `showparts` | `szShowParts` | String | Show parts | `"all"` |
| `gridx` | `nGridX` | Number | Grid X spacing | `"100"` |
| `gridwidth` | `nGridWidth` | Number | Grid width | `"50"` |
| `gridmatrix` | `nGridMatrix` | Number | Grid matrix | `"1"` |
| `gridwidthpx` | `nGridWidthPx` | Number | Grid width in pixels | `"100"` |
| `gridoffsetx` | `nGridOffsetX` | Number | Grid X offset | `"0"` |
| `gridoffsety` | `nGridOffsetY` | Number | Grid Y offset | `"0"` |
| `aggregationfield` | `szAggregationField` | String | Aggregation field | `"region"` |
| `aggregationscale` | `szAggregationFieldA` | Array | Aggregation scale | `["1:1", "codice_comune"]` |
| `aggregation` | `szAggregation` | String | Aggregation method | `"sum"` |
| `minaggregation` | `szMinAggregation` | String | Minimum aggregation | `"1:1000000"` |
| `aggregationupper` | `szAggregationUpper` | String | Aggregation upper limit | `"1:5000000"` |
| `aggregationlower` | `szAggregationLower` | String | Aggregation lower limit | `"1:1000000"` |
| `clipupper` | `szClipUpper` | String | Clip upper limit | `"1:200000"` |
| `cliplower` | `szClipLower` | String | Clip lower limit | `"1:20000"` |
| `dominantfilter` | `szDominantFilter` | String | Dominant filter | `"category='A'"` |
| `dominantdfilter` | `nDominantDFilter` | Number | Dominant delta filter | `"1"` |
| `overviewchart` | `szOverviewChart` | String | Overview chart | `"true"` |
| `evidence` | `evidenceMode` | String | Evidence mode | `"true"` |
| `markclass` | `markedClass` | Number | Marked class | `"1"` |
| `markclasses` | `markedClassesA` | Array | Marked classes | `[1, 2, 3]` |
| `name` | `szName` | String | Theme name | `"population_theme"` |
| `title` | `szTitle` | String | Theme title | `"Population by Municipality"` |
| `snippet` | `szSnippet` | String | Theme snippet | `"Population data"` |
| `splash` | `szSplash` | String | Theme splash | `"Welcome"` |
| `description` | `szDescription` | String | Theme description | `"Detailed description"` |
| `tooltip` | `szTooltip` | String | Theme tooltip | `"Hover tooltip"` |

## Notes

- **Type**: Indicates the data type expected for the property
- **Array properties**: Use comma-separated values or pipe-separated values (depending on delimiter)
- **Object properties**: Use JSON format
- **Boolean properties**: Use `"true"` or `"false"` strings
- **Number properties**: Use string format (e.g., `"1.5"` instead of `1.5`)
- **String properties**: Use quoted strings

## Common Usage Patterns

### Basic Choropleth
```javascript
.style({
    type: "CHOROPLETH|EQUIDISTANT",
    colorscheme: ["5", "#FFFDD8", "#B5284B"],
    fillopacity: "0.7",
    showdata: "true",
    valuedecimals: "0"
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
    normalsizevalue: "500000",
    aggregationscale: ["1:1", "codice_comune", "1:1000000", "pr"]
})
```

### Advanced Theme
```javascript
.style({
    type: "CHOROPLETH|EQUIDISTANT|ZOOMTO",
    colorscheme: ["5", "#FFFDD8", "#B5284B"],
    fillopacity: "0.7",
    stroke: "#FFFFFF",
    strokewidth: "1",
    showdata: "true",
    valuedecimals: "0",
    units: "people",
    titleupper: "1:1000000",
    valueupper: "1:20000",
    boxupper: "1:200000"
})
```

This table provides a comprehensive reference for all available style properties in iXMaps themes.