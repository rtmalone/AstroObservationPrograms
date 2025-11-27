# Hugo Astronomy Site - Complete Setup Guide

## 1. Create the site structure

```bash
hugo new site astronomy-site
cd astronomy-site
mkdir -p layouts/_default layouts/partials static/css static/images content/observations content/programs
```

## 2. Configuration File

**hugo.toml** (in root directory):

```toml
baseURL = 'https://astronomy.rtylermalone.com/'
languageCode = 'en-us'
title = 'Astronomy Observations - R Tyler Malone'

[params]
  description = 'My Astronomical League observation programs and deep sky observations'
  author = 'R Tyler Malone'

[menu]
  [[menu.main]]
    name = 'Home'
    url = '/'
    weight = 1
  [[menu.main]]
    name = 'Observations'
    url = '/observations/'
    weight = 2
  [[menu.main]]
    name = 'Programs'
    url = '/programs/'
    weight = 3
  [[menu.main]]
    name = 'About'
    url = '/about/'
    weight = 4
```

## 3. Layout Files

**layouts/_default/baseof.html** (main template):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ .Title }} - {{ .Site.Title }}</title>
    <meta name="description" content="{{ .Site.Params.description }}">
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    {{ partial "header.html" . }}
    
    <main>
        {{ block "main" . }}{{ end }}
    </main>
    
    {{ partial "footer.html" . }}
</body>
</html>
```

**layouts/_default/single.html** (individual page):

```html
{{ define "main" }}
<article>
    <header>
        <h1>{{ .Title }}</h1>
        {{ if .Params.date }}
        <time datetime="{{ .Date.Format "2006-01-02" }}">{{ .Date.Format "January 2, 2006" }}</time>
        {{ end }}
    </header>
    
    {{ if .Params.image }}
    <div class="featured-image">
        <img src="{{ .Params.image }}" alt="{{ .Title }}">
    </div>
    {{ end }}
    
    <div class="observation-details">
        {{ if .Params.location }}
        <p><strong>Location:</strong> {{ .Params.location }}</p>
        {{ end }}
        {{ if .Params.equipment }}
        <p><strong>Equipment:</strong> {{ .Params.equipment }}</p>
        {{ end }}
        {{ if .Params.conditions }}
        <p><strong>Conditions:</strong> {{ .Params.conditions }}</p>
        {{ end }}
    </div>
    
    <div class="content-body">
        {{ .Content }}
    </div>
</article>
{{ end }}
```

**layouts/_default/list.html** (list pages):

```html
{{ define "main" }}
<div class="content">
    <h1>{{ .Title }}</h1>
    {{ .Content }}
    
    <div class="observation-grid">
        {{ range .Pages }}
        <article class="observation-card">
            {{ if .Params.image }}
            <a href="{{ .Permalink }}">
                <img src="{{ .Params.image }}" alt="{{ .Title }}">
            </a>
            {{ end }}
            <h2><a href="{{ .Permalink }}">{{ .Title }}</a></h2>
            {{ if .Params.date }}
            <time>{{ .Date.Format "January 2, 2006" }}</time>
            {{ end }}
            <p>{{ .Summary }}</p>
        </article>
        {{ end }}
    </div>
</div>
{{ end }}
```

**layouts/index.html** (homepage):

```html
{{ define "main" }}
<div class="content">
    <h1>Welcome to My Astronomy Journey</h1>
    <p>Documenting my observations and progress through Astronomical League programs.</p>
    
    <h2>Recent Observations</h2>
    <div class="observation-grid">
        {{ range first 6 (where .Site.RegularPages "Section" "observations") }}
        <article class="observation-card">
            {{ if .Params.image }}
            <a href="{{ .Permalink }}">
                <img src="{{ .Params.image }}" alt="{{ .Title }}">
            </a>
            {{ end }}
            <h3><a href="{{ .Permalink }}">{{ .Title }}</a></h3>
            <time>{{ .Date.Format "January 2, 2006" }}</time>
        </article>
        {{ end }}
    </div>
    
    <h2>Observation Programs</h2>
    <div class="programs-list">
        {{ range where .Site.RegularPages "Section" "programs" }}
        <article class="program-card">
            <h3><a href="{{ .Permalink }}">{{ .Title }}</a></h3>
            {{ if .Params.progress }}
            <p>Progress: {{ .Params.progress }}</p>
            {{ end }}
        </article>
        {{ end }}
    </div>
</div>
{{ end }}
```

## 4. Partial Templates

**layouts/partials/header.html**:

```html
<header>
    <nav>
        <div class="site-title">
            <a href="/">{{ .Site.Title }}</a>
        </div>
        <ul class="nav-menu">
            {{ range .Site.Menus.main }}
            <li><a href="{{ .URL }}">{{ .Name }}</a></li>
            {{ end }}
        </ul>
    </nav>
</header>
```

**layouts/partials/footer.html**:

```html
<footer>
    <p>&copy; {{ now.Year }} {{ .Site.Params.author }}. All observations and images are my own work.</p>
</footer>
```

## 5. CSS Styling

**static/css/style.css**:

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    line-height: 1.6;
    color: #e0e0e0;
    background-color: #0a0e27;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

header {
    background-color: #1a1f3a;
    padding: 1.5rem 0;
    margin-bottom: 2rem;
    border-bottom: 2px solid #2a3f5f;
}

nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.site-title a {
    font-size: 1.5rem;
    font-weight: bold;
    color: #6b9bd1;
    text-decoration: none;
}

.nav-menu {
    list-style: none;
    display: flex;
    gap: 2rem;
}

.nav-menu a {
    color: #b0c4de;
    text-decoration: none;
    transition: color 0.3s;
}

.nav-menu a:hover {
    color: #6b9bd1;
}

main {
    min-height: 70vh;
}

.content {
    padding: 2rem 0;
}

h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    color: #6b9bd1;
}

h2 {
    font-size: 2rem;
    margin: 2rem 0 1rem;
    color: #8bacd6;
}

h3 {
    font-size: 1.5rem;
    margin: 1.5rem 0 0.5rem;
    color: #a0c0e0;
}

.observation-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 2rem;
    margin: 2rem 0;
}

.observation-card {
    background-color: #1a1f3a;
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
    border: 1px solid #2a3f5f;
}

.observation-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 20px rgba(107, 155, 209, 0.3);
}

.observation-card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    display: block;
}

.observation-card h2,
.observation-card h3 {
    padding: 1rem 1rem 0.5rem;
    margin: 0;
    font-size: 1.3rem;
}

.observation-card h2 a,
.observation-card h3 a {
    color: #6b9bd1;
    text-decoration: none;
}

.observation-card time {
    display: block;
    padding: 0 1rem;
    color: #808080;
    font-size: 0.9rem;
}

.observation-card p {
    padding: 0.5rem 1rem 1rem;
    color: #b0c4de;
}

.featured-image {
    margin: 2rem 0;
    text-align: center;
}

.featured-image img {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
    border: 2px solid #2a3f5f;
}

.observation-details {
    background-color: #1a1f3a;
    padding: 1.5rem;
    border-radius: 8px;
    margin: 2rem 0;
    border-left: 4px solid #6b9bd1;
}

.observation-details p {
    margin: 0.5rem 0;
}

.content-body {
    margin-top: 2rem;
    font-size: 1.1rem;
    line-height: 1.8;
}

.content-body p {
    margin-bottom: 1rem;
}

.programs-list {
    display: grid;
    gap: 1rem;
    margin: 2rem 0;
}

.program-card {
    background-color: #1a1f3a;
    padding: 1.5rem;
    border-radius: 8px;
    border-left: 4px solid #6b9bd1;
}

.program-card h3 {
    margin: 0 0 0.5rem 0;
}

.program-card h3 a {
    color: #6b9bd1;
    text-decoration: none;
}

.program-card p {
    color: #b0c4de;
    margin: 0.5rem 0;
}

time {
    color: #808080;
    font-size: 0.95rem;
}

article.content header {
    margin-bottom: 2rem;
}

article.content header h1 {
    margin-bottom: 0.5rem;
}

footer {
    margin-top: 4rem;
    padding: 2rem 0;
    border-top: 2px solid #2a3f5f;
    text-align: center;
    color: #808080;
}

a {
    color: #6b9bd1;
}

a:hover {
    color: #8bacd6;
}

@media (max-width: 768px) {
    nav {
        flex-direction: column;
        gap: 1rem;
    }
    
    .observation-grid {
        grid-template-columns: 1fr;
    }
}
```

## 6. Sample Content Files

**content/_index.md** (homepage):

```markdown
---
title: "Home"
---
```

**content/about.md**:

```markdown
---
title: "About"
---

I'm an amateur astronomer working through various Astronomical League observation programs. This site documents my observations, equipment, and astrophotography journey.

## Equipment

- Telescope: [Your telescope]
- Mount: [Your mount]
- Camera: [Your camera]
- Other accessories...

## Observation Programs

I'm currently working on the following Astronomical League programs:

- Messier Program
- [Other programs...]
```

**content/observations/_index.md**:

```markdown
---
title: "Observations"
---

A collection of my astronomical observations and astrophotography.
```

**content/observations/m42-orion-nebula.md** (sample observation):

```markdown
---
title: "M42 - Orion Nebula"
date: 2024-11-20
image: "/images/m42.jpg"
location: "Backyard, Austin, TX"
equipment: "8\" Dobsonian, 25mm eyepiece"
conditions: "Clear, Bortle 6, seeing 3/5"
---

My first successful observation of the Great Orion Nebula. Even in light-polluted skies, the nebulosity was clearly visible surrounding the Trapezium cluster.

## Visual Description

The nebula appeared as a bright, diffuse cloud with the four stars of the Trapezium easily resolved at 80x magnification. Averted vision revealed more extensive nebulosity extending to the north and south.

## Notes

- Used OIII filter to enhance contrast
- The "wings" of the nebula were faintly visible
- Temperature: 45°F, light wind
```

**content/programs/_index.md**:

```markdown
---
title: "Observation Programs"
---

My progress through various Astronomical League observation programs.
```

**content/programs/messier.md** (sample program):

```markdown
---
title: "Messier Program"
progress: "42/110 objects observed"
---

The Messier Catalog contains 110 of the brightest deep-sky objects visible from mid-northern latitudes. This was my first observation program and continues to be a favorite on clear nights.

## Progress

Currently observed: 42/110 objects (38%)

### Completed Objects

- M1 - Crab Nebula ✓
- M13 - Great Hercules Cluster ✓
- M31 - Andromeda Galaxy ✓
- M42 - Orion Nebula ✓
- [Continue listing...]

### Remaining Objects

Working on the summer objects, particularly those in Sagittarius and Scorpius.
```

## 7. Running Your Site

```bash
# Start local server (with drafts visible)
hugo server -D

# Build for production
hugo

# The built site will be in the 'public' folder
```

## 8. Adding New Observations

To add a new observation, just create a new markdown file:

```bash
hugo new observations/m31-andromeda.md
```

Then edit the file and add your content, images, and observation details.

## 9. Deploying

Once you run `hugo`, the entire site is built into the `public` folder. You can:

- Upload the `public` folder contents to any web host
- Use GitHub Pages, Netlify, or Vercel for free hosting
- Point your `astronomy.rtylermalone.com` subdomain to wherever you host

## Tips

- Store images in `static/images/` - they'll be accessible at `/images/filename.jpg`
- Keep observation file names simple: `m42-orion.md`, `ngc7000-north-america.md`
- Use consistent formatting in your front matter for easier maintenance
- Consider adding tags/categories if you want to organize by object type or program