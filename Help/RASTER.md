# Raster Data Management

## Overview
This guide covers working with raster data in the Timewalk Manhattan QGIS project, including historical maps, Digital Elevation Models (DEMs), and other raster datasets using the Web Mercator coordinate system (EPSG:3857).

## Available Raster Data

### Historical Maps
- **`map_1776_3857_CE.tif`** - 1776 historical map of Manhattan
- **`1844_modified.tif`** - 1844 historical map
- **`1865_2_modified.tif`** - 1865 historical map
- **`map-fire-1776_modified.tif`** - 1776 fire map
- **`18th_cent_elevation.tif`** - 18th century elevation data

### Digital Elevation Models (DEMs)
- **`DEM_12_3857.tif`** - 12-meter resolution DEM
- **`DEM_14_3857.tif`** - 14-meter resolution DEM
- **`DEM_8_3857.tif`** - 8-meter resolution DEM
- **`DEM_8_Underwater_3857.tif`** - Underwater DEM data
- **`DEM_BG_3857.tif`** - Background DEM
- **`DEM_Input_Manhattan_3857.tif`** - Input Manhattan DEM

### Soil and Land Cover Data
- **`soil_color_3857.tif`** - Soil color information
- **`soil_type_32016_var1.tif`** - Soil type classification
- **`ecomm11_types_32016_ref1_modified.tif`** - Land cover types

### NYC-Specific Data
- **`Shoreline_Manhattan_3857.tif`** - Manhattan shoreline data
- **`DEM_Bthymetry_cropped_3857_smoothed.tif`** - Bathymetry data

## Loading Raster Data

### Basic Raster Loading
```bash
# Add raster layer
Layer → Add Layer → Add Raster Layer
# Navigate to appropriate folder (raster/1609/, raster/1776/, etc.)
# Select .tif file
# Click "Add"
```

### Loading Multiple Raster Files
```bash
# For multiple files in same folder
Layer → Add Layer → Add Raster Layer
# Select multiple files (Ctrl+click)
# All selected files will be added as separate layers
```

### Loading Raster with Specific CRS
```bash
# When loading, if CRS dialog appears:
# Select "EPSG:3857 - WGS 84 / Pseudo-Mercator"
# Click "OK"
```

## Raster Data Properties

### Checking Raster Properties
```bash
# Right-click raster layer → Properties
# Information tab shows:
# - File path and size
# - Coordinate Reference System
# - Extent (bounding box)
# - Resolution and dimensions
# - Data type and bands
```

### Understanding Raster Information
- **Resolution**: Pixel size in map units (meters for EPSG:3857)
- **Extent**: Geographic bounds of the raster
- **Bands**: Number of data layers (1=grayscale, 3=RGB, 4=RGBA)
- **Data Type**: Integer or floating-point values
- **No Data Value**: Value representing missing data

## Raster Styling and Visualization

### Basic Raster Styling
```bash
# Right-click layer → Properties → Symbology
# Choose render type:
# - Singleband Gray: For single-band data
# - Singleband Pseudocolor: For elevation data
# - Multiband Color: For RGB imagery
```

### Styling Historical Maps
1. **Singleband Gray**:
   ```bash
   # Render type: Singleband Gray
   # Band: 1 (or appropriate band)
   # Contrast enhancement: Stretch to MinMax
   # Gamma: 1.0 (adjust for brightness)
   ```

2. **Color Adjustments**:
   ```bash
   # Brightness: 0-100 (adjust overall brightness)
   # Contrast: 0-100 (adjust contrast)
   # Saturation: 0-100 (adjust color intensity)
   ```

### Styling DEM Data
1. **Singleband Pseudocolor**:
   ```bash
   # Render type: Singleband Pseudocolor
   # Band: 1
   # Color ramp: Choose elevation-appropriate colors
   # Classification mode: Continuous
   ```

2. **Color Ramps for Elevation**:
   ```bash
   # Low elevation: Blues (water)
   # Medium elevation: Greens (land)
   # High elevation: Browns/Reds (hills)
   ```

### Transparency and Blending
```bash
# Layer properties → Transparency
# Global transparency: 0-100%
# Additional no data value: Set if needed
# Blending mode: Normal, Multiply, Screen, etc.
```

## Raster Analysis and Processing

### Basic Raster Analysis
1. **Raster Calculator**:
   ```bash
   # Processing → Toolbox → Raster Analysis → Raster Calculator
   # Create expressions like:
   # - "DEM_12_3857@1" * 3.28084 (convert meters to feet)
   # - "DEM_12_3857@1" > 10 (elevation above 10 meters)
   ```

2. **Slope Analysis**:
   ```bash
   # Processing → Toolbox → Raster Analysis → Slope
   # Input: DEM layer
   # Output: Slope raster
   # Z factor: 1.0 (for meters)
   ```

3. **Aspect Analysis**:
   ```bash
   # Processing → Toolbox → Raster Analysis → Aspect
   # Input: DEM layer
   # Output: Aspect raster (directional slope)
   ```

### Raster Conversion
1. **Reproject Raster**:
   ```bash
   # Processing → Toolbox → Raster Projections → Warp (Reproject)
   # Input: Source raster
   # Target CRS: EPSG:3857
   # Resampling method: Nearest neighbor (for categorical data)
   # Resampling method: Bilinear (for continuous data)
   ```

2. **Raster to Vector**:
   ```bash
   # Processing → Toolbox → Conversion → Raster to Vector
   # Input: Raster layer
   # Field name: Value (or appropriate field)
   # Output: Vector layer
   ```

### Raster Mosaicking
```bash
# Processing → Toolbox → Raster Miscellaneous → Merge
# Input layers: Select multiple raster layers
# Output: Merged raster
# Data type: Match input or specify
```

## Working with Raster Pyramids

### Understanding Pyramids
Raster pyramids are reduced-resolution versions of raster data that improve display performance at smaller scales.

### Building Pyramids
```bash
# Right-click raster layer → Properties → Pyramids
# Click "Build Pyramids"
# Choose resampling method: Nearest neighbor or Average
# Click "OK"
```

### Pyramid Settings
```bash
# In Pyramids tab:
# - Enable pyramids: Check to use pyramids
# - Resampling method: Choose appropriate method
# - Compression: LZW or JPEG for smaller file sizes
```

## Raster Data Quality and Validation

### Checking Data Quality
1. **Visual Inspection**:
   ```bash
   # Zoom to different scales
   # Check for artifacts, missing data, or distortions
   # Verify coordinate system alignment
   ```

2. **Statistics**:
   ```bash
   # Right-click layer → Properties → Histogram
   # Check for reasonable value ranges
   # Look for data gaps or outliers
   ```

### Common Quality Issues
- **Missing Data**: Areas with no data values
- **Coordinate Misalignment**: Incorrect projection or georeferencing
- **Resolution Mismatch**: Different pixel sizes between layers
- **Data Artifacts**: Compression artifacts or processing errors

## Raster Data Management

### File Organization
```
raster/
├── 1609/           # Historical data from 1609
├── 1660/           # Historical data from 1660
├── 1776/           # Historical data from 1776
├── Data_NYC/       # NYC-specific data
├── DEM/            # Digital Elevation Models
├── HistoricalMaps/ # Historical map images
└── maps/           # General map files
```

### Naming Conventions
- **Time-based**: Include year in filename (e.g., `map_1776_3857_CE.tif`)
- **Resolution**: Include resolution in filename (e.g., `DEM_12_3857.tif`)
- **Coordinate System**: Include CRS in filename (e.g., `_3857` for EPSG:3857)
- **Data Type**: Include data type (e.g., `_modified`, `_smoothed`)

### File Formats
- **GeoTIFF (.tif)**: Primary format for raster data
- **Auxiliary Files (.tif.aux.xml)**: Metadata and styling information
- **World Files (.tfw)**: Georeferencing information (if separate)

## Performance Optimization

### Large Raster Files
1. **Pyramid Building**: Always build pyramids for large files
2. **Subsetting**: Extract only needed areas
3. **Compression**: Use LZW or JPEG compression
4. **Resolution**: Use appropriate resolution for analysis needs

### Memory Management
```bash
# Processing → Options → Processing
# Set maximum memory usage
# Enable parallel processing if available
# Close unused layers to free memory
```

## Troubleshooting

### Common Issues
1. **Slow Rendering**:
   - Build pyramids
   - Reduce layer transparency
   - Use appropriate resolution

2. **Missing Data**:
   - Check no data values
   - Verify file integrity
   - Check coordinate system

3. **Poor Quality**:
   - Check original data source
   - Verify processing steps
   - Compare with reference data

### Performance Tips
- Use pyramids for large files
- Enable hardware acceleration
- Close unused layers
- Use appropriate zoom levels
- Consider data subsetting for analysis

## Best Practices

### Data Management
- **Backup**: Keep original files safe
- **Documentation**: Record data sources and processing steps
- **Version Control**: Use Git LFS for large files
- **Metadata**: Maintain data documentation

### Analysis Workflow
1. **Load Data**: Import raster layers
2. **Check Quality**: Verify data integrity
3. **Set CRS**: Ensure correct coordinate system
4. **Build Pyramids**: For performance
5. **Style Appropriately**: For visualization
6. **Analyze**: Perform required analysis
7. **Document**: Record results and methods

## Related Documentation
- [STYLING.md](STYLING.md) - For advanced styling techniques
- [WORKFLOWS.md](WORKFLOWS.md) - For common raster workflows
- [TECHNICAL.md](TECHNICAL.md) - For technical specifications
- [POLYGONS.md](POLYGONS.md) - For combining raster and vector data
