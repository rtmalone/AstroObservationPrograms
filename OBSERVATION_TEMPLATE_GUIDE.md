# Observation Template Guide

## Overview
The observation template (`layouts/_default/single.html`) provides a consistent layout for all astronomical observations, regardless of the program they belong to. The template uses the `observation-layout` structure with optional program navigation.

## Template Structure

The template creates a two-column layout:
- **Left Column**: Object title, description, notes, and structured object data
- **Right Column**: Sticky sketch/image box
- **Optional Top**: Program navigation (prev/next, back to program)

## How to Use

### 1. File Location
Observation files live within their program folders:
- `content/programs/double-star/eta-cassiopeiae.md`
- `content/programs/messier/m42.md`
- `content/programs/lunar-i/tycho.md`

### 2. Front Matter Parameters

#### Basic Parameters:
- `title`: The name of the object (required)
- `date`: Date of observation (YYYY-MM-DD format) - shows timestamp when present
- `image`: Path to sketch or photo (defaults to placeholder if omitted)

#### Program Navigation (optional):
Include these to show prev/next navigation at the top of the page:
- `prev_star`: Name of previous object
- `prev_star_link`: Link to previous object
- `next_star`: Name of next object
- `next_star_link`: Link to next object
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

### Lunar Observation (without navigation)
File: `content/programs/lunar-i/tycho.md`

```markdown
---
title: "Crater Tycho"
date: 2024-11-22
object_type: "Lunar Crater"
size: "85 km diameter"
location: "Backyard"
equipment: "8\" Dobsonian, 10mm eyepiece"
---

# Tycho Crater

Spectacular ray system...

---

## Visual Description
The crater walls were sharply defined...
```

## Features

1. **Consistent Layout**: All observations use the same visual structure
2. **Flexible Parameters**: Only displays the object data fields you include
3. **Sticky Sketch Box**: The image stays visible as you scroll the notes
4. **Responsive**: Layout adapts to mobile screens
5. **Smart Defaults**: Uses placeholder images if no image is provided

## Features

- **Flexible Navigation**: Include program navigation parameters to show prev/next links, or omit them for a clean layout
- **Conditional Object Data**: Only the fields you define in front matter are displayed
- **Smart Image Defaults**: Automatically uses appropriate placeholder images based on object type
- **Responsive Design**: Layout adapts for mobile viewing

## Technical Details

- The template splits content on `<hr>` tags (rendered from `---` in markdown)
- The "Object Data" section is automatically inserted between the split sections
- Only parameters that are defined in the front matter are displayed
- The sketch box automatically uses the double-star placeholder if `separation` is defined
- Both templates now support the same object data fields (object_type, size, brightness, etc.)

