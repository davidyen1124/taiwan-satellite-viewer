# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-page web application that displays satellite imagery of Taiwan. The application fetches real-time satellite data from Taiwan's Central Weather Administration (CWA) and provides an interactive interface for viewing different satellite image types, coverage areas, and timestamps.

## Architecture

- **Single HTML file application**: The entire application is contained in `index.html` with embedded CSS and JavaScript
- **External dependencies**:
  - Tailwind CSS (via CDN)
  - CWA Satellite Data API (`https://www.cwa.gov.tw/Data/js/obs_img/Observe_sat.js`)
- **No build system**: This is a static HTML file that can be opened directly in a browser

## Key Components

### State Management

- Global `currentState` object manages:
  - `type`: Satellite image type (Tab0-Tab4 for different visualization modes)
  - `area`: Coverage area (Area0=全景, Area1=東亞, Area2=臺灣)
  - `timeIndex`: Selected timestamp index
  - `useBandwidthSaving`: Boolean for image size optimization

### Core Functions

- `generateImageUrl()`: Constructs satellite image URLs from CWA data
- `updateImage()`: Handles image loading with loading states and error handling
- `initializeTimeSelect()`: Populates time dropdown based on current satellite data
- `getCurrentSatelliteData()`: Gets satellite data for current type/area/size combination

### UI Interactions

- Satellite type buttons (可見光, 彩色, 色調強化, 黑白, 真實色)
- Coverage area buttons (全景, 東亞, 臺灣)
- Time selection dropdown
- Bandwidth saving toggle
- Retry functionality for failed image loads

## Development Commands

Since this is a static HTML application, there are no build, test, or lint commands. To develop:

1. Open `index.html` directly in a web browser
2. Use browser developer tools for debugging
3. Test across different browsers for compatibility

## Data Source

The application relies on Taiwan's Central Weather Administration satellite data API. The `SatImg` object is loaded from their JavaScript file and contains structured satellite image metadata organized by:

- Image type (Tab0-Tab4)
- Coverage area (Area0-Area2)
- Image size (size0=full, size1=compressed)
- Color mode ('C' for color)

## Technical Notes

- Images are loaded dynamically from `https://www.cwa.gov.tw/Data/satellite/`
- The application handles loading states and error recovery
- Responsive design works on both desktop and mobile
- No authentication required - uses public CWA data
