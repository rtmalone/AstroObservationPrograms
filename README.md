# Astronomy Observation Site

A Hugo-based static site for documenting astronomical observations and tracking progress through Astronomical League observing programs.

🌐 **Live Site**: [astronomy.rtylermalone.com](https://astronomy.rtylermalone.com)  
🚀 **Hosted on**: Cloudflare Pages

## Overview

This site provides a structured way to document and track observations across multiple astronomy programs, including:

- **Double Star Program**: 100 double stars for visual observing
- **Lunar Programs**: Systematic observation of lunar features (Lunar I, Lunar II)
- **Messier Objects**: Classic deep-sky catalog observations
- Custom observation programs

## Features

- 📊 **Progress Tracking**: Automatic calculation and visualization of program completion
- 🎯 **Smart Navigation**: Sequential navigation through program objects
- 📝 **Flexible Templates**: Consistent observation layout with program-specific customization
- ✅ **Observation Badges**: Visual indicators for completed observations
- 🖼️ **Sketch Support**: Optional sketch/image display for visual documentation
- 📱 **Responsive Design**: Mobile-friendly layouts

## Quick Start

### Prerequisites

- [Hugo](https://gohugo.io/) (extended version recommended)
- Git

### Local Development

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd AstroObservingSite
   ```

2. **Start the development server**:
   ```bash
   hugo server -D
   ```

3. **View the site**:
   Open your browser to `http://localhost:1313`

### Building for Production

```bash
hugo
```

The static site will be generated in the `public/` directory.

## Project Structure

```
AstroObservingSite/
├── content/              # All content files
│   ├── programs/         # Observing programs
│   │   ├── double-star/  # Double star observations
│   │   ├── lunar-i/      # Lunar I program features
│   │   ├── lunar-ii/     # Lunar II program features
│   │   └── messier/      # Messier object observations
│   ├── observations/     # General observations
│   └── about.md          # About page
├── layouts/              # Hugo templates
│   ├── _default/         # Default templates
│   ├── programs/         # Program-specific templates
│   └── partials/         # Reusable components
├── static/               # Static assets
│   ├── css/              # Stylesheets
│   └── images/           # Images and placeholders
├── hugo.toml             # Hugo configuration
└── OBSERVATION_TEMPLATE_GUIDE.md  # Documentation
```

## Creating Observations

See [OBSERVATION_TEMPLATE_GUIDE.md](OBSERVATION_TEMPLATE_GUIDE.md) for detailed instructions on creating and formatting observations.

### Quick Example

Create a new observation file in the appropriate program folder:

```markdown
---
title: "Object Name"
date: 2024-11-28
observed: true
object_type: "Double Star"
constellation: "Cygnus"
magnitude: "3.1, 5.1"
separation: "34.4"
position_angle: "054°"
location: "Dark Sky Site"
equipment: "8\" Dobsonian"
image: "/images/placeholder-double-star.svg"
prev_star: "Previous Object"
prev_star_link: "../previous-object/"
next_star: "Next Object"
next_star_link: "../next-object/"
program_link: "../"
program_name: "Double Star Program"
---

# Object Name

Brief introduction or summary of the observation.

---

## Visual Description

Detailed description of what you observed...

## Notes

- Additional observations
- Equipment details
- Challenges encountered
```

## Configuration

Key configuration is in `hugo.toml`:

```toml
baseURL = 'https://astronomy.rtylermalone.com/'
title = 'Astronomy'

[params]
  description = 'My Astronomical League observation programs'
  author = 'R Tyler Malone'
  defaultSketchImage = '/images/placeholder-sketch.svg'
  doubleStarPlaceholder = '/images/placeholder-double-star.svg'
```

## Deployment

The site is automatically deployed to Cloudflare Pages when changes are pushed to the main branch.

### Cloudflare Pages Configuration

- **Build command**: `hugo`
- **Build output directory**: `public`
- **Environment variable**: `HUGO_VERSION` (set to your Hugo version)

## Contributing

When adding new observations or programs:

1. Follow the structure outlined in `OBSERVATION_TEMPLATE_GUIDE.md`
2. Use the `observed: true` flag and `date` field for completed observations
3. Enable sketch boxes by setting `hasSketchOrImage: true` in the program's `_index.md`
4. Test locally with `hugo server` before committing

## License

Personal observation site - all observations and content © R Tyler Malone

## Contact

For questions or suggestions, please open an issue in the repository.

