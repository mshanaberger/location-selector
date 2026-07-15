# Forecasting Location Selector

## Overview

The Forecasting Location Selector is a single-page HTML tool used to evaluate service-location ZIP Codes and Canadian Forward Sortation Areas and recommend the minimum practical number of forecasting locations needed for adequate geographic coverage.

The tool uses centroid placement, proximity, directional separation, outer geographic extent, and redundancy screening to identify which locations should be retained as forecasting points.

## Supported Location Types

The tool accepts:

- Five-digit U.S. ZIP Codes
- Three-character Canadian Forward Sortation Areas, also called FSAs

Examples:

- `48161`
- `M5V`

A full Canadian postal code such as `M5V 3A8` or `M5V3A8` is automatically reduced to `M5V`.

## How to Use

1. Open the HTML file in a modern browser such as Chrome, Edge, Firefox, or Safari.
2. Enter one ZIP Code or Canadian FSA per line in the Service ZIP / Postal Codes field.
3. Adjust the coverage settings as needed.
4. Add any terrain-, shoreline-, elevation-, or body-of-water-sensitive locations to the sensitive-location field.
5. Select a selection level.
6. Choose the directional weighting.
7. Click **Analyze Locations**.
8. Review the recommended and non-selected locations.
9. Click **Export Proposal PNG** to save the map and recommendation as an image.

## Selection Levels

### Lean

Lean selects the minimum number of forecasting locations needed to satisfy the applicable distance rules.

Use Lean when the primary goal is reducing duplication while maintaining basic geographic coverage.

### Balanced

Balanced applies the distance rules while also preserving locations that provide meaningful north, south, east, west, northeast, northwest, southeast, or southwest coverage.

Use Balanced for most normal forecasting-location evaluations.

### Conservative

Conservative uses tighter working distances and removes fewer outer or geographically distinct locations.

Use Conservative when local weather variability is greater or when maintaining more forecasting points is preferred.

## Coverage Rules

The default working standards are:

- Normal locations: no more than 5 miles from a selected forecasting location
- Terrain-, shoreline-, or body-of-water-sensitive locations: no more than 2.5 miles from a selected forecasting location

Conservative mode may tighten the working standards further.

These distances are based on centroid-to-centroid measurements.

## Directional Weighting

Directional weighting controls how strongly the tool favors locations that add meaningful compass-direction coverage.

The available levels are:

- Low
- Normal
- High

Directional weighting does not simply reward every outer location. It increases the value of locations that are genuinely more north, south, east, west, or diagonal than nearby alternatives.

## Map Symbols

- Green marker: recommended forecasting location
- Gray marker: non-selected location
- Black dashed line: relationship between a non-selected location and the selected location representing it
- Red circle: 2.5-mile radius
- Blue circle: 5-mile radius
- Gray circle: 10-mile radius

The coverage relationship line runs from the outside edge of one marker to the outside edge of the other and redraws when the map is zoomed or moved.

## Recommendation Logic

The tool evaluates each location using:

- Geographic centroid placement
- Distance to nearby locations
- Directional separation
- Outer service-area extent
- Geographic clustering
- Redundancy
- In-between placement
- User-designated sensitive areas
- Coverage-radius requirements

A location may be excluded when it:

- Is too close to a selected location
- Falls between selected locations
- Is adequately represented by surrounding selections
- Does not add meaningful directional coverage
- Does not add distinct forecasting value

A location may be retained when removing it would leave part of the service area without adequate representation.

## Canadian FSA Handling

Canadian entries use the first three characters of the postal code, known as the Forward Sortation Area.

Examples:

- `M5V 3A8` becomes `M5V`
- `M5V3A8` becomes `M5V`
- `M5V` remains `M5V`

Canadian FSA coordinates are retrieved using an online postal-code lookup service.

## U.S. ZIP Code Handling

The tool accepts standard five-digit U.S. ZIP Codes.

U.S. centroid data may come from:

- Bundled sample coordinates
- An online ZIP centroid dataset
- A user-loaded CSV
- Manual latitude and longitude entry

## CSV Upload

The Load Centroid CSV option allows users to provide their own centroid dataset.

The CSV should include columns for:

- ZIP Code, ZCTA, postal code, or location code
- Latitude
- Longitude

Example:

```csv
postal_code,latitude,longitude
48161,41.904793,-83.416690
M5V,43.642600,-79.387100
```

Column names can vary, but they must clearly identify the location code, latitude, and longitude.

## Manual Centroid Entry

If a location cannot be found automatically, use Add Manual Centroid.

Enter:

- ZIP Code or FSA
- Latitude
- Longitude

Then run the analysis again.

## PNG Export

The export process:

1. Waits for the OpenStreetMap tiles to load
2. Flattens the map into a single image
3. Redraws markers, labels, radius circles, relationship lines, and the legend
4. Captures the full proposal layout

For the best result, wait until the map is fully loaded before exporting.

## Internet Requirements

An internet connection is required for:

- OpenStreetMap tiles
- Leaflet libraries
- Online ZIP or FSA lookup
- Export-support libraries

Locations already stored in the file or loaded from CSV can still be analyzed without online lookup, but the map background may not display without internet access.

## Limitations

This tool is a geographic decision-support system. It does not automatically know every local forecasting influence.

Manual review is still recommended for:

- Great Lakes and ocean shoreline effects
- Elevation differences
- Mountain or valley terrain
- Urban heat-island effects
- Rural exposure
- Snowbelt or lake-effect zones
- Coastal wind and precipitation differences
- Known operational or client-specific weather concerns

Centroids represent geographic reference points and may not reflect the exact position of every address within a ZIP Code or FSA.

## Recommended Workflow

1. Run the analysis in Balanced mode.
2. Review the selected locations.
3. Identify any shoreline, terrain, or elevation-sensitive areas.
4. Add those codes to the sensitive-location field.
5. Run the analysis again.
6. Compare Lean, Balanced, and Conservative results.
7. Apply operational forecasting judgment.
8. Export the final proposal PNG.

## File

Main application:

`forecasting_location_selector_us_canada_fsa_v20.html`

## Technology

The application uses:

- HTML
- CSS
- JavaScript
- Leaflet
- OpenStreetMap
- html2canvas
- leaflet-image

## Disclaimer

The recommendations are based primarily on geographic relationships and centroid distance. They should be used as a structured proposal-selection aid and not as a substitute for meteorological expertise or local operational knowledge.
