# Departure Confirmation Screen

## Overview
This implements the departure confirmation screen that appears when:
1. The departure marker is placed in a time-restricted zone (orange zone)
2. The user moves to the arrival confirmation screen
3. The user attempts to call by clicking "도착지 확인"

## Files Modified
- `index_0425.html` - Main application file with the new functionality

## Files Created
- `test_departure_confirm.html` - Standalone test file demonstrating the screen design

## How It Works

### User Flow
1. User places departure marker in a time-restricted (orange) zone
2. User clicks "도착지 검색" to enter destination mode
3. User selects arrival location
4. User clicks "도착지 확인" button
5. **NEW**: Instead of proceeding normally, the system detects that the departure was in an orange zone
6. System shows the "출발지를 확인해 주세요" (Confirm departure location) screen
7. Screen displays:
   - Center marker (blue) showing "출발" at the departure location
   - User can drag the map to adjust departure location
   - Bottom sheet with departure location information (updates as map moves)
   - "출발지 확인" confirmation button
8. User can confirm departure or go back to previous screen

### Technical Implementation

#### CSS Classes Added
- `.departure-confirm-content` - Main container for departure confirmation screen
- `.departure-confirm-title` - Title text styling
- `.departure-location-card` - Card containing location information
- `.departure-location-row` - Row layout for icon and text
- `.departure-location-icon` - Icon container (with home icon)
- `.departure-location-info` - Text information container
- `.departure-location-name` - Location name text
- `.departure-location-sub` - Location address text
- `.departure-confirm-btn` - Confirmation button

#### JavaScript Functions Added
- `enterDepartureConfirmMode()` - Enters departure confirmation mode
  - Changes center marker to blue "출발" marker
  - Shows departure confirmation bottom sheet
  - Updates address for current position
- `exitDepartureConfirmMode()` - Exits departure confirmation mode
  - Restores normal home screen
  - Resets zone state
- `updateDepartureAddress()` - Updates departure location info as map moves
  - Fetches address from OpenStreetMap Nominatim API
  - Updates location name and address in the UI

#### Variables Added
- `isDepartureConfirmMode` - Boolean flag for departure confirmation mode
- `departureZone` - Tracks whether departure is in blue, orange, or out of zone

#### Event Handlers Added
- Map `moveend` event - Updates departure address when map moves in departure confirm mode

## Testing

### Option 1: Use the Standalone Test File
Open `test_departure_confirm.html` in a browser to see the screen design without the full application.

### Option 2: Test in Main Application
1. Open `index_0425.html` in a browser
2. Move the center marker to an orange (time-restricted) polygon area
3. Click "도착지 검색"
4. Move the map to select an arrival location (should be in a blue zone)
5. Click "도착지 확인"
6. The departure confirmation screen should appear

### Option 3: Manual Trigger via Console
Open the browser console and run:
```javascript
enterDepartureConfirmMode();
```
The screen will show with the current map center as the departure location.

## Design Details

### Screen Elements
1. **Back Button** (top-left)
   - Circular white button with drop shadow
   - Back arrow icon
   - Returns to previous screen

2. **Location Button** (bottom-left)
   - Circular white button with drop shadow
   - GPS crosshair icon
   - Centers map on user location

3. **Center Marker**
   - **Departure Marker** (Blue, centered)
     - Label: "출발"
     - Blue pin color (#0C39A5)
     - Positioned at screen center
     - User drags map to adjust location

4. **Bottom Sheet**
   - Title: "출발지를 확인해 주세요"
   - **Location Card**
     - Gray background (#F7F7FA)
     - Home icon (red/pink circle with house symbol)
     - Location name (updates as map moves)
     - Address (updates as map moves)
   - **Confirm Button**
     - Blue background (#2462F7)
     - White text
     - Label: "출발지 확인"

## Color Scheme
- Background: #FAFAFA
- Blue (Primary): #2462F7
- Pin Blue: #0C39A5
- Pin Green: #008026
- Text Primary: #121212
- Text Secondary: #909199
- Border: #DFDFE5
- Card Background: #F7F7FA

## Font
- Family: Pretendard Variable
- Title: 18px, Bold (700)
- Location Name: 16px, Regular (400)
- Location Address: 13px, Regular (400)
- Button: 18px, Medium (500)
- Marker Bubble: 15px, Bold (700)
