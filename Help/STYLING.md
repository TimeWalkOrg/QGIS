# Styling and Visualization

## Quick Access
```bash
# Open Style: Right-click layer → Properties → Symbology (F7)
# Style Types: Single Symbol, Categorized, Graduated, Rule-based
```

## Vector Styling

### Basic Polygon Styling
```bash
# Fill Color: Choose color, set transparency (0-100%)
# Outline: Darker color, width 0.5-2.0mm, solid line
# Example: Light blue fill, dark blue outline
```

### Categorized Styling
```bash
# Select "Categorized", Column: property_type, Click "Classify"
# Colors: Residential=Green, Commercial=Orange, Industrial=Gray, Public=Yellow
```

### Graduated Styling
```bash
# Select "Graduated", Column: area_sqft, Method: Natural Breaks
# Classes: 5-7, Color ramp: Blues/Reds/Greens
# Methods: Natural Breaks (uneven data), Equal Interval (even data), Quantile (ranked data)
```

### Rule-Based Styling
```bash
# Select "Rule-based", Click "+" to add rules
# Example Rules:
# - Large parcels (>5000 sqft): Red fill
# - Medium parcels (1000-5000 sqft): Yellow fill  
# - Small parcels (<1000 sqft): Green fill
# - Historical (<1800): Special styling
```

## Labeling

### Basic Labeling
```bash
# Enable: Right-click layer → Properties → Labels → "Single Labels"
# Label with: parcel_id (or any field)
# Style: Arial 10pt, Black color, White buffer 0.5mm
```

### Advanced Labeling
```bash
# Multi-field: "parcel_id" || '\n' || "owner"
# Conditional: CASE WHEN "area_sqft" > 5000 THEN "parcel_id" || ' (Large)' ELSE "parcel_id" || ' (Small)' END
# Placement: Around point, 2-5mm distance, High priority
```

## Raster Styling

### Basic Raster Styling
```bash
# Singleband Gray: Band 1, Stretch to MinMax, Gamma 1.0
# Singleband Pseudocolor: Choose color ramp, set classes
# Multiband Color: RGB bands 1,2,3, Stretch to MinMax
# Adjustments: Brightness/Contrast 0-100, Saturation 0-100
```

## Color Schemes & Transparency

### Color Schemes
```bash
# Historical: Residential=Brown, Commercial=Tan, Public=Blue, Military=Gray
# Modern: Residential=Green, Commercial=Orange, Industrial=Gray, Public=Blue
# Elevation: Water=Blue, Low=Green, Medium=Yellow, High=Orange, Highest=Red
```

### Transparency
```bash
# Layer Transparency: 0-100% (Base=80-90%, Overlay=60-70%, Highlight=100%)
# Blending Modes: Normal, Multiply, Screen, Overlay
```

## Best Practices & Export

### Visual Hierarchy
```bash
# Base Layers: Muted colors, lower opacity
# Data Layers: Distinct colors, higher opacity  
# Highlight Layers: Bright colors, full opacity
# Labels: Contrasting colors with buffers
```

### Export & Sharing
```bash
# Export Map: Project → Import/Export → Export Map to Image
# Resolution: 300 DPI (print), 96 DPI (screen)
# Formats: PNG, JPEG, TIFF, PDF
# Map Composer: Project → New Print Layout
```

### Troubleshooting
```bash
# Labels not showing: Check field exists, placement settings
# Colors not applying: Verify attribute values, classification
# Performance issues: Reduce label density, simplify styles
```

## Related Documentation
- [POLYGONS.md](POLYGONS.md) - For creating and editing the data to style
- [RASTER.md](RASTER.md) - For raster-specific styling techniques
- [WORKFLOWS.md](WORKFLOWS.md) - For styling workflows and best practices
- [TECHNICAL.md](TECHNICAL.md) - For technical styling specifications
