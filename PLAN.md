# Radiology App Implementation Plan

## Overview
Create a comprehensive radiology protocol app with patient data collection, interactive body model selection, and detailed protocol information for all body parts.

## File Structure
- `index.html` - Main application file (single-page app with multiple screens)
- Image assets: `first.jpg` (body model), `image.png`, `second.jpg`, `third.jpg`, `interface.jpg`

## Implementation Details

### 1. Patient Form Interface (Screen 1)
**Location**: `index.html` section `#scr-form`
- Fields:
  - Patient Name (input)
  - Patient UHID (input)
  - Patient Age (number input)
  - Gender (dropdown: Male, Female, Other)
  - Department (dropdown)
  - Comments: H/O (textarea)
- Submit button that validates all required fields
- No data persistence (interface only)
- Styling: Dark theme with orange accent, matching UI design

### 2. Body Model Interface (Screen 2)
**Location**: `index.html` section `#scr-body`
- Display human body model image (`first.jpg`)
- Add clickable hotspots for ALL body parts:
  - **Head/Neck** (top 18% of body, center)
  - **Chest/Thorax** (upper chest area, 20-35% from top)
  - **Abdomen** (mid-section, 35-50% from top)
  - **Pelvis** (lower abdomen, 45-55% from top)
  - **Upper Limbs** (left/right arms, 25-45% from top, sides)
  - **Lower Limbs** (legs, 50-100% from top, center)
  - **Spine** (back area, vertical center)

- Visual highlighting on hover/click:
  - Add CSS overlay effect with orange glow
  - Show label box with body part name when selected
  - Animate highlight transition

- Navigation: Clicking a body part navigates to protocol list screen

### 3. Protocol List Screens (Screen 3)
**Multiple sections** for each body part category:

#### 3.1 Brain/Head Protocols (`#scr-protocols-brain`)
- BRAIN section:
  - Without contrast → `#scr-brain-nc`
  - With contrast → `#scr-brain-contrast`
  - Angio CT → `#scr-brain-angio`
- FACIAL SKELETON section:
  - Facial skeleton → `#scr-facial`
  - Sinuses → `#scr-sinuses`
  - Orbits → `#scr-orbits`
- EAR AND PEÑASCO section:
  - Ear and peñasco → `#scr-ear`
- NECK - CERVICAL SPINE section:
  - Neck → `#scr-neck`
  - Angio CT → `#scr-neck-angio`
  - Cervical Spine → `#scr-cspine`

#### 3.2 Chest/Thorax Protocols (`#scr-protocols-chest`)
- Chest CT
- Chest with contrast
- Chest without contrast
- Lung protocol
- Cardiac CT
- etc.

#### 3.3 Abdomen Protocols (`#scr-protocols-abdomen`)
- Abdomen with contrast
- Abdomen without contrast
- Liver protocol
- Kidneys protocol
- Pancreas protocol
- etc.

#### 3.4 Pelvis Protocols (`#scr-protocols-pelvis`)
- Pelvis → `#scr-pelvis` (already exists)
- Pelvis with contrast
- Bladder protocol
- etc.

#### 3.5 Upper Limbs Protocols (`#scr-protocols-upper-limbs`)
- Shoulder
- Elbow
- Wrist
- Hand
- etc.

#### 3.6 Lower Limbs Protocols (`#scr-protocols-limbs`)
- Pelvis → `#scr-pelvis`
- Hip
- Knee → `#scr-knee`
- Ankle → `#scr-ankle`
- Foot → `#scr-foot`

#### 3.7 Spine Protocols (`#scr-protocols-spine`)
- Cervical Spine → `#scr-cspine`
- Thoracic Spine
- Lumbar Spine
- Whole Spine

**Protocol List Styling**:
- Orange horizontal dividers between sections
- Dark grey buttons with orange bullet points
- Orange chevron arrows (›) on right
- Scrollable list

### 4. Detailed Protocol Pages (Screen 4)
**Structure for each protocol** (e.g., `#scr-brain-nc`, `#scr-brain-contrast`, etc.):

Each protocol detail page includes:
- Back button (orange left arrow)
- Protocol title (e.g., "WITHOUT CONTRAST")
- Hero image area (protocol-specific image)
- Information cards:
  - **Indications** card: Medical reasons for the study
  - **Previous preparation** card: Pre-procedure requirements
  - **Patient position** card: Positioning instructions
  - **Anatomical reference** card (if applicable): Scan range/details
  - **Technical parameters** card (if applicable): CT settings

**Cards styling**:
- Dark grey background
- White text
- Orange horizontal line under section titles
- Scrollable content

### 5. JavaScript Functionality

#### 5.1 Navigation System
- `show(screenId)` function: Switch between screens
- `goBody()` function: Validate form and navigate to body model
- Back button handlers for each screen

#### 5.2 Body Model Interaction
- Hotspot click handlers for each body part
- Visual feedback on hover/click:
  - Add/remove highlight class
  - Show body part label
- Smooth transitions

#### 5.3 Protocol Data Management
- Create `protocolData` object structure:
```javascript
const protocolData = {
  brain: {
    withoutContrast: {
      title: "WITHOUT CONTRAST",
      image: "image.png",
      indications: "...",
      preparation: "...",
      position: "...",
      anatomicalRef: "..."
    },
    // ... other protocols
  },
  // ... other body parts
}
```

#### 5.4 Dynamic Content Rendering
- Function to render protocol detail pages from data
- Function to generate protocol list items
- Reusable card component rendering

### 6. CSS Enhancements

#### 6.1 Body Model Highlighting
```css
.hotspot {
  position: absolute;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 50%;
}

.hotspot:hover {
  background: rgba(255, 159, 46, 0.2);
  box-shadow: 0 0 20px rgba(255, 159, 46, 0.5);
}

.hotspot.selected {
  background: rgba(255, 159, 46, 0.4);
  box-shadow: 0 0 30px rgba(255, 159, 46, 0.8);
}

.body-part-label {
  position: absolute;
  background: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 8px 12px;
  border-radius: 8px;
  pointer-events: none;
  font-weight: 600;
}
```

#### 6.2 Protocol List Styling
- Match UI design: Orange dividers, dark cards, orange accents
- Smooth scrolling
- Hover effects on protocol items

#### 6.3 Detail Page Styling
- Image carousel support (if multiple images)
- Scrollable content area
- Card animations on load

### 7. Complete Body Parts Coverage

#### Hotspot Coordinates (approximate, to be fine-tuned):
- **Head**: left: 33%, top: 6%, width: 34%, height: 18%
- **Neck**: left: 35%, top: 18%, width: 30%, height: 8%
- **Chest**: left: 25%, top: 26%, width: 50%, height: 15%
- **Abdomen**: left: 25%, top: 41%, width: 50%, height: 12%
- **Pelvis**: left: 25%, top: 48%, width: 50%, height: 10%
- **Left Arm**: left: 5%, top: 28%, width: 18%, height: 25%
- **Right Arm**: left: 77%, top: 28%, width: 18%, height: 25%
- **Left Leg**: left: 30%, top: 58%, width: 20%, height: 35%
- **Right Leg**: left: 50%, top: 58%, width: 20%, height: 35%
- **Spine**: left: 42%, top: 24%, width: 16%, height: 40%

### 8. Medical Content Structure

For each protocol, provide realistic medical content:
- **Indications**: Common clinical scenarios
- **Previous preparation**: Patient preparation steps
- **Patient position**: Positioning instructions
- **Anatomical reference**: Scan boundaries
- **Technical parameters**: CT settings (optional)

### 9. Image Assets
- Body model: `first.jpg`
- Protocol images: `image.png`, `second.jpg`, `third.jpg`
- Placeholder images for protocols without specific images

### 10. Responsive Design
- Mobile-first approach (already implemented)
- Touch-friendly hotspots
- Scrollable lists
- Proper viewport handling

## Implementation Steps

1. **Enhance patient form** - Verify styling matches UI exactly
2. **Expand body model hotspots** - Add all body part regions with proper coordinates
3. **Add highlighting effects** - CSS and JS for visual feedback
4. **Create protocol list screens** - For all body parts (chest, abdomen, upper limbs, spine, etc.)
5. **Build protocol detail pages** - Complete all protocol detail screens with medical content
6. **Implement JavaScript navigation** - Smooth transitions and proper routing
7. **Add protocol data structure** - Organize all medical content
8. **Test all navigation paths** - Ensure all links work correctly
9. **Polish UI/UX** - Match exact design from reference images
10. **Add footer/credits** - "Created by Deepak B.Sc ACS Medical College"

## Technical Notes

- Single-page application (SPA) architecture
- CSS-only animations (no external libraries)
- Vanilla JavaScript (no frameworks)
- All content in one HTML file for simplicity
- Images stored locally
- No backend/database (interface only as specified)

