# Timewalk Manhattan QGIS Project

## Overview
Historical geospatial data for Manhattan (1609, 1660, 1776) with building parcel polygons using EPSG:3857 coordinate system.

## What is QGIS?
**QGIS** is free, open-source GIS software for creating, editing, and analyzing geospatial data.

## What is a Shapefile?
**ESRI Shapefile** stores geometric and attribute data in multiple files:
- **`.shp`** - Geometry data
- **`.dbf`** - Attribute data  
- **`.prj`** - Coordinate system
- **`.shx`** - Index file
- **`.cpg`** - Character encoding

## Project Structure
```
QGIS/
├── raster/          # Raster data (.tif files)
│   ├── 1609/       # 1609 historical data
│   ├── 1660/       # 1660 historical data  
│   ├── 1776/       # 1776 historical data
│   ├── DEM/        # Digital Elevation Models
│   └── HistoricalMaps/ # Historical map images
├── vector/         # Vector data (.shp files)
│   ├── 1609/       # 1609 vector data
│   ├── 1660/       # 1660 vector data
│   ├── 1776/       # 1776 building parcels
│   └── Masks/      # Boundary files
├── installer/      # QGIS installation files
│   └── QGIS-OSGeo4W-3.34.15-1.msi # QGIS 3.34 installer
├── NYC.qgz        # Main QGIS project
└── .gitattributes # Git LFS configuration
```

## Documentation Guides

### 📋 [POLYGONS.md](Help/POLYGONS.md) - Building Parcels
- Creating/modifying parcel polygons
- Geometry tools & snapping
- Attribute tables & geoprocessing tools

### 🗺️ [RASTER.md](Help/RASTER.md) - Raster Data  
- Historical maps & DEMs
- Loading & styling raster layers
- Analysis & processing

### 🎨 [STYLING.md](Help/STYLING.md) - Visualization
- Polygon styling & labeling
- Color schemes & transparency
- Export & sharing

### 🔄 [WORKFLOWS.md](Help/WORKFLOWS.md) - Workflows
- Step-by-step procedures
- Best practices & quality control
- Data management

### ⚙️ [TECHNICAL.md](Help/TECHNICAL.md) - Technical
- EPSG:3857 coordinate system
- File formats & troubleshooting
- Performance optimization

## Quick Start
1. **Install QGIS**: Use included `installer/QGIS-OSGeo4W-3.34.15-1.msi` or download from [qgis.org](https://qgis.org)
2. **Open Project**: `NYC.qgz` or `NYC_Sunil.qgz`
3. **Explore Data**: Browse raster/vector folders
4. **Choose Guide**: Select documentation for your task

## Key Data Files
- **Parcels**: `vector/1776/parcels_1776_CE_3857.shp`
- **Historical Maps**: `raster/HistoricalMaps/map_1776_3857_CE.tif`
- **DEMs**: `raster/DEM/DEM_12_3857.tif`

## Coordinate System
All data uses **EPSG:3857 (Web Mercator)** for web compatibility.

## Getting Help
- **QGIS Docs**: [docs.qgis.org](https://docs.qgis.org)
- **Project Issues**: Check specific guides
- **Technical**: See [TECHNICAL.md](Help/TECHNICAL.md)