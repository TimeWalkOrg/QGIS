# Working with Building Parcel Polygons

## Quick Start
1. **Open Project**: `File → Open Project → NYC.qgz`
2. **Load Parcels**: `Layer → Add Layer → vector/1776/parcels_1776_CE_3857.shp`
3. **Verify CRS**: Right-click layer → Properties → Information (should show EPSG:3857)

## Available Data
- **`parcels_1776_CE_3857.shp`** - Main building parcels dataset
- **`parcels_1776_CE_Sunil_3857.shp`** - Alternative parcels dataset
- **`all_CE_shapes.shp`** - Comprehensive shape collection

## Creating New Parcel Layers

### New Shapefile with Attributes
```bash
# 1. Create Layer
Layer → Create Layer → New Shapefile Layer
# File: new_parcels_1776_3857.shp
# Type: Polygon, CRS: EPSG:3857

# 2. Add Fields
# parcel_id (Integer, 10)
# owner (String, 100) 
# area_sqft (Real, 15, 2)
# property_type (String, 50)
# year_built (Integer, 4)
# source (String, 200)
```

## Geometry Tools

### Basic Editing Tools
```bash
# Enable Editing: Right-click layer → Toggle Editing

# Add Polygon: Click points, right-click to finish
# Move Feature: Select tool, drag to new location  
# Resize Feature: Select corner, drag to resize
# Split Features: Draw line across parcel
# Merge Features: Select multiple (Ctrl+click), merge
# Delete Feature: Select, press Delete key

# Advanced Tools:
# Add Ring: Create holes in polygons
# Delete Ring: Remove holes
# Reshape: Draw new boundary
# Simplify: Reduce vertex count
```

## Snapping Setup
```bash
# Enable: Project → Snapping Options
# Settings: Tolerance 15px, Vertex/Segment/Intersection
# Advanced: Snap to grid, common angles
# Visual: Red=vertex, Blue=segment, Green=intersection
```

## Attribute Tables

### Basic Operations
```bash
# Open Table: Right-click layer → Open Attribute Table (F6)
# Enable Editing: Click pencil icon
# Add Record: Click green plus icon
# Save Changes: Click disk icon

# Edit Values: Double-click cell, type, press Enter
# Bulk Edit: Select multiple (Ctrl+click), right-click → Change Values
```

### Field Calculator
```bash
# Area: $area * 10.764 (m² to ft²)
# Concatenate: "owner" || ' - ' || "property_type"  
# Conditional: CASE WHEN "area_sqft" > 1000 THEN 'Large' ELSE 'Small' END
```

## Vector Geoprocessing Tools for Polygons

### Essential Geoprocessing Tools

#### 1. Buffer
```bash
# Vector → Geoprocessing Tools → Buffer
# Input: Point layer (building locations)
# Distance: Building width/2 (e.g., 10 meters)
# Segments: 8 (for smooth circles)
# Output: Polygon layer with building footprints
```

#### 2. Clip
```bash
# Vector → Geoprocessing Tools → Clip
# Input: Parcel layer
# Overlay: Manhattan boundary (shoreline_manhattan_2020.shp)
# Output: Clipped parcel layer (removes areas outside boundary)
```

#### 3. Intersection
```bash
# Vector → Geoprocessing Tools → Intersection
# Input: Parcel layer
# Overlay: Study area polygon
# Output: Only parcels within study area
```

#### 4. Union
```bash
# Vector → Geoprocessing Tools → Union
# Input: Multiple parcel layers
# Output: Combined parcel layer with all features
```

#### 5. Difference
```bash
# Vector → Geoprocessing Tools → Difference
# Input: Parcel layer
# Overlay: Exclusion area (e.g., water bodies)
# Output: Parcels with excluded areas removed
```

#### 6. Dissolve
```bash
# Vector → Geoprocessing Tools → Dissolve
# Input: Parcel layer
# Dissolve field: property_type
# Output: Merged parcels by property type
```

### Advanced Geoprocessing Tools

#### 7. Convex Hull
```bash
# Vector → Geoprocessing Tools → Convex Hull
# Input: Point layer (building locations)
# Output: Polygon encompassing all points
```

#### 8. Voronoi Polygons
```bash
# Vector → Geoprocessing Tools → Voronoi Polygons
# Input: Point layer (building locations)
# Output: Polygons dividing space around each point
```

#### 9. Minimum Bounding Geometry
```bash
# Vector → Geoprocessing Tools → Minimum Bounding Geometry
# Input: Parcel layer
# Type: Rectangle, Circle, or Convex Hull
# Output: Bounding geometry for each parcel
```

## Creating New Parcels from Existing Data

### Method 1: Digitizing from Historical Maps
```bash
# 1. Load Base Map
Layer → Add Layer → Add Raster Layer
# Select: raster/HistoricalMaps/map_1776_3857_CE.tif

# 2. Start Digitizing
# Enable editing on parcel layer
# Use "Add Polygon Feature" tool
# Follow building outlines on historical map
```

### Method 2: Converting from Other Formats
```bash
# 1. Import Data
Layer → Add Layer → Add Vector Layer
# Select .dxf or .dwg files

# 2. Reproject to EPSG:3857
Vector → Data Management Tools → Reproject Layer
# Target CRS: EPSG:3857
```

### Method 3: Using Geoprocessing Tools
```bash
# 1. Buffer Points to Create Parcels
Vector → Geoprocessing Tools → Buffer
# Input: Point layer, Distance: 10m

# 2. Clip to Study Area
Vector → Geoprocessing Tools → Clip
# Input: Buffered layer, Overlay: Manhattan boundary
```

## Quality Control and Validation

### Topology Checks
```bash
# Check for overlapping parcels
Processing → Toolbox → Vector Geometry → Check Validity
# Fix any topology errors
```

### Attribute Validation
```bash
# Verify required fields are populated
# Check for duplicate parcel IDs
# Validate area calculations
```

### Common Validation Tasks
1. **Check for Gaps**: Ensure no gaps between adjacent parcels
2. **Check for Overlaps**: Verify no overlapping parcel boundaries
3. **Validate Attributes**: Ensure all required fields are populated
4. **Check Coordinate System**: Verify EPSG:3857 is applied correctly

## Best Practices

### Data Standards
- **Consistent Naming**: Use descriptive, standardized names
- **Attribute Schema**: Define consistent field names and types
- **Coordinate Precision**: Maintain appropriate decimal places
- **Topology**: Ensure no gaps or overlaps between parcels

### Historical Accuracy
- **Source Documentation**: Document historical sources used
- **Uncertainty Indicators**: Include confidence levels for historical data
- **Temporal References**: Clearly mark time periods and dates
- **Validation**: Cross-reference with multiple historical sources

### Technical Considerations
- **File Formats**: Use shapefiles for compatibility, GeoPackage for advanced features
- **Coordinate System**: Always use EPSG:3857 for web compatibility
- **File Size**: Consider splitting large datasets into manageable chunks
- **Backup**: Maintain multiple copies of important datasets

## Troubleshooting

### Common Issues
- **Coordinate System Mismatch**: Always verify CRS before starting work
- **Topology Errors**: Use validation tools to identify and fix issues
- **Large File Sizes**: Consider using GeoPackage format for better performance
- **Missing Attributes**: Ensure all required fields are populated

### Performance Optimization
- **Spatial Indexing**: Create spatial indexes for large datasets
- **Layer Filtering**: Use attribute filters to work with subsets
- **Memory Management**: Close unused layers to free memory
- **File Organization**: Keep related files in organized folder structure

## Keyboard Shortcuts

### Editing Shortcuts
- **F6**: Open attribute table
- **Ctrl+T**: Toggle editing mode
- **Ctrl+S**: Save edits
- **Delete**: Delete selected features
- **Ctrl+Z**: Undo last action
- **Ctrl+Y**: Redo last action

### Selection Shortcuts
- **Ctrl+A**: Select all features
- **Ctrl+D**: Deselect all features
- **Ctrl+Click**: Add to selection
- **Shift+Click**: Select range

## Related Documentation
- [STYLING.md](STYLING.md) - For styling and visualizing your polygons
- [WORKFLOWS.md](WORKFLOWS.md) - For common workflows and best practices
- [TECHNICAL.md](TECHNICAL.md) - For technical specifications and troubleshooting
