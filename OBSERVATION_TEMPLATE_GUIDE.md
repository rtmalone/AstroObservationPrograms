# Observation Template Guide

## Overview
The observation template (`layouts/_default/single.html`) provides a consistent layout for all astronomical observations, regardless of the program they belong to. The template uses the `observation-layout` structure with optional program navigation and conditional sketch/image display.

## Template Structure

The template creates a flexible layout:
- **Top Navigation** (optional): Program navigation with prev/next links
- **Left Column**: Object title, description, notes, and structured object data
- **Right Column** (conditional): Sticky sketch/image box (only displays if program section has `hasSketchOrImage: true`)
- **Observation Badge** (optional): "Observed" date badge when both `observed: true` and `date` are present

## How to Use

### 1. File Location
Observation files live within their program folders:
- `content/programs/double-star/eta-cassiopeiae.md`
- `content/programs/messier/m42.md`
- `content/programs/lunar-i/tycho.md`

### 2. Front Matter Parameters

#### Basic Parameters:
- `title`: The name of the object (required)
- `date`: Date of observation (YYYY-MM-DD format)
- `observed`: Boolean flag (true/false) to mark if observation is complete
- `image`: Path to sketch or photo (defaults to placeholder if omitted)

**Note**: When both `observed: true` and `date` are present, a formatted "Observed: [date]" badge appears at the top of the content.

#### Program Navigation (optional):
Include these to show prev/next navigation at the top of the page:

**For Double Star Programs:**
- `prev_star`: Name of previous object
- `prev_star_link`: Link to previous object
- `next_star`: Name of next object
- `next_star_link`: Link to next object

**For Lunar Programs:**
- `prev_feature`: Name of previous feature
- `prev_feature_link`: Link to previous feature
- `next_feature`: Name of next feature
- `next_feature_link`: Link to next feature

**Both formats support:**
- `program_link`: Link back to program list
- `program_name`: Display name for the program (defaults to "Program")

#### Object Information (choose relevant ones):
- `object_type`: Type of object (e.g., "Double Star", "Nebula", "Lunar Crater", "Galaxy")
- `constellation`: The constellation containing the object
- `ra`: Right Ascension
- `dec`: Declination
- `magnitude`: Magnitude(s) of the object
- `separation`: For double stars (in arcseconds)
- `position_angle`: For double stars (in degrees)
- `last_measure`: For double stars (WDS measure year)
- `size`: Angular size of the object
- `brightness`: Surface brightness (for nebulae/galaxies)
- `difficulty`: Observing difficulty level

#### Observation Details:
- `location`: Where you observed from
- `equipment`: Telescope/equipment used
- `conditions`: Sky conditions, seeing, transparency, etc.
- `seeing`: Seeing conditions (often rated on a scale or letter grade)
- `transparency`: Sky transparency (limiting magnitude or rating)
- `time`: Time of observation

### 3. Content Structure

Use a horizontal rule (`---`) to separate the header/introduction from the detailed notes:

```markdown
---
title: "Object Name"
date: 2024-11-27
# ... other parameters
---

# Object Name

Brief introduction or summary of the observation.

---

## Visual Description

Detailed description of what you observed...

## Notes

- Additional notes
- Equipment details
- Observing challenges
```

**The `---` separator is important**: It tells the template where to insert the "Object Data" section.

## Examples

### Double Star Observation (with navigation)
File: `content/programs/double-star/albireo.md`

```markdown
---
title: "Beta Cygni (Albireo)"
date: 2024-11-25
observed: true
object_type: "Double Star"
constellation: "Cygnus"
magnitude: "3.1, 5.1"
separation: "34.4"
position_angle: "054°"
location: "Dark Sky Site"
equipment: "8\" Dobsonian, 25mm eyepiece"
conditions: "Excellent, seeing 5/5"
prev_star: "Alpha Herculis"
prev_star_link: "../alpha-herculis/"
next_star: "Zeta Lyrae"
next_star_link: "../zeta-lyrae/"
program_link: "../"
program_name: "Double Star Program"
image: "/images/placeholder-double-star.svg"
---

# Beta Cygni (Albireo)

Beautiful golden-blue double star...

---

## Visual Description
The primary appeared golden...
```

### Nebula Observation (without navigation)
File: `content/programs/messier/m42.md`

```markdown
---
title: "M42 - Orion Nebula"
date: 2024-11-20
object_type: "Emission Nebula"
constellation: "Orion"
magnitude: "4.0"
size: "85' × 60'"
location: "Backyard"
equipment: "8\" Dobsonian"
---

# M42 - Orion Nebula

First observation of this spectacular nebula...

---

## Visual Description
The nebula appeared as...
```

### Lunar Observation (with navigation)
File: `content/programs/lunar-i/tycho-crater.md`

```markdown
---
title: "Tycho Crater"
object_type: "Lunar Impact Crater"
size: "85 km diameter"
date: 2024-02-18
observed: true
time: "5:43 pm EST"
location: "Chattanooga, TN (35.15°N, 85.32°W)"
equipment: "Telescope (750/150mm)"
seeing: "G"
transparency: "4"
image: "/images/placeholder-lunar.png"
prev_feature: "Theophilus"
prev_feature_link: "../theophilus/"
next_feature: "Walther"
next_feature_link: "../walther/"
program_link: "../"
program_name: "Lunar I Program"
---

# Tycho Crater

One of the Moon's most prominent and spectacular craters...

---

## Visual Description
The crater walls were sharply defined...
```

## Features

1. **Consistent Layout**: All observations use the same visual structure
2. **Flexible Parameters**: Only displays the object data fields you include
3. **Conditional Sketch Box**: The image box only appears for programs where the section has `hasSketchOrImage: true` set
4. **Sticky Sketch Box**: When displayed, the image stays visible as you scroll the notes
5. **Responsive**: Layout adapts to mobile screens
6. **Smart Defaults**: Uses placeholder images if no image is provided
7. **Flexible Navigation**: Supports both star-based (prev_star/next_star) and feature-based (prev_feature/next_feature) navigation
8. **Progress Tracking**: Observation badges appear when `observed: true` and `date` are set
9. **Program Progress**: Section pages automatically calculate and display progress (X/Y features observed)

## Technical Details

### Template Logic

- The template splits content on `<hr>` tags (rendered from `---` in markdown)
- The "Object Data" section is automatically inserted between the split sections
- Only parameters that are defined in the front matter are displayed
- The sketch box automatically uses the double-star placeholder if `separation` is defined

### Navigation Flexibility

The template intelligently handles multiple navigation formats:
- Uses `prev_star`/`next_star` for double star programs
- Uses `prev_feature`/`next_feature` for lunar programs
- Falls back gracefully if navigation parameters are omitted

### Section Configuration

To enable the sketch/image box for a program, add this to the program's `_index.md`:

```yaml
---
title: "Program Name"
hasSketchOrImage: true
---
```

### Progress Tracking

The section template (`layouts/programs/section.html`) automatically:
- Counts pages with `observed: true`
- Calculates percentage complete
- Displays a visual progress bar
- Shows "✓ Observed" badges on completed items

