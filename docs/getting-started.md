# Getting Started with BitsByMe Theme

Get up and running with the BitsByMe Hugo theme in minutes!

## Prerequisites

- Hugo Extended v0.110.0 or later
- Go 1.18+ (for Hugo Modules)
- Git

## Installation

### Option 1: Hugo Modules (Recommended)

Hugo Modules is the modern way to manage themes. It's cleaner and easier to update.

```bash
# 1. Initialize your site as a Hugo Module
cd your-hugo-site
hugo mod init github.com/yourusername/your-site

# 2. Add theme to your config.toml
```

Add to `config.toml`:
```toml
[module]
  [[module.imports]]
    path = "github.com/dvhthomas/blog"
```

**Note**: Replace the theme repository URL with the actual published theme repository once it's published separately.

```bash
# 3. Hugo will download the theme automatically
hugo server
```

Benefits:
- ✅ Automatic updates with `hugo mod get -u`
- ✅ Version pinning
- ✅ No git submodule complexity

### Option 2: Copy to themes/ (Simple)

For quick testing or if you don't want modules:

```bash
cd your-hugo-site
git clone https://github.com/dvhthomas/blog.git themes/bitsbyme
```

Then in `config.toml`:
```toml
theme = "bitsbyme"
```

### Option 3: Git Submodule (Legacy)

If your workflow requires submodules:

```bash
cd your-hugo-site
git submodule add https://github.com/dvhthomas/blog.git themes/bitsbyme
```

Then in `config.toml`:
```toml
theme = "bitsbyme"
```

## Configuration

### 1. Basic Config

Update your `config.toml`:

```toml
baseURL = "https://yoursite.com/"
languageCode = "en-us"
title = "Your Site Title"
theme = "bitsbyme"

[outputs]
  home = ["HTML", "RSS", "JSON"]  # Required for search

[params]
  homeText = "your tagline"
  homeIntro = "Your intro paragraph with [links](/about)"
  dateFormat = "January 2, 2006"
  description = "Your site description"
```

### 2. Enable Search

Create `content/search/_index.md`:

```markdown
---
title: "Search"
layout: "search"
---
```

### 3. Add Footer Links

Add to `config.toml`:

```toml
[[params.footerLinks]]
  name = "GitHub"
  url = "https://github.com/yourusername"
  icon = "github"
  ariaLabel = "GitHub profile"
  external = true

[[params.footerLinks]]
  name = "Subscribe"
  url = "/index.xml"
  icon = "rss"
  ariaLabel = "Subscribe via RSS"
  external = false
```

Available icons: `briefcase`, `github`, `linkedin`, `bluesky`, `rss`

### 4. Configure Menu

Add to `config.toml`:

```toml
[menu]
  [[menu.main]]
    name = "Home"
    url = "/"
    weight = 1
    [menu.main.params]
      icon = "home"
  [[menu.main]]
    name = "Blog"
    url = "/blog/"
    weight = 2
    [menu.main.params]
      icon = "edit"
  [[menu.main]]
    name = "About"
    url = "/about/"
    weight = 3
    [menu.main.params]
      icon = "user"
```

**Available menu icons**: `home`, `edit`, `award`, `tag`, `book`, `user`

Icons are custom Feather-style SVG symbols. The `icon` parameter is optional - if omitted, only the text label will be displayed.

## Create Content

### Blog Post

```bash
hugo new blog/my-first-post.md
```

Edit `content/blog/my-first-post.md`:

```markdown
---
title: "My First Post"
date: 2025-01-15
tags: ["example", "getting-started"]
summary: "A brief summary"
toc: true
draft: false
---

Your content here...
```

### TIL (Today I Learned)

```bash
hugo new til/quick-tip.md
```

### About Page

```bash
hugo new about.md
```

## Test Your Site

```bash
# Development server with drafts
hugo server --buildDrafts

# Production build
hugo
```

Visit http://localhost:1313 to see your site!

## Using Theme Features

### Callout Blocks

```markdown
> TIP: This creates a styled tip box

> INFO: This creates an info callout
```

### Mermaid Diagrams

Create diagrams using [Mermaid](https://mermaid.js.org/) syntax.

**1. Enable Mermaid in your page:**
```yaml
---
title: "My Post"
mermaid: true
---
```

**2. Use the mermaid shortcode:**
````markdown
{{</* mermaid */>}}
graph TD
    A[Start] --> B[Process]
    B --> C[End]
{{</* /mermaid */>}}
````

Supports all Mermaid diagram types: flowcharts, sequence diagrams, class diagrams, state diagrams, Gantt charts, pie charts, and more.

See [Mermaid documentation](https://mermaid.js.org/intro/) for syntax examples.

### GitHub Gist

Embed GitHub gists in your posts.

```markdown
{{</* gist username gist-id */>}}
```

Example:
```markdown
{{</* gist dvhthomas 239909 */>}}
```

Parameters:
- `username`: Your GitHub username
- `gist-id`: The gist ID (from the gist URL)

### Code Blocks with Syntax Highlighting

**Standard Markdown (Recommended):**

Use standard markdown code blocks with syntax highlighting:

````markdown
```python
def hello():
    print("Hello, World!")
```
````

**Hugo's highlight Shortcode (Advanced):**

For line highlighting and advanced features:

````markdown
{{</* highlight python "linenos=table,hl_lines=2 4-6,linenostart=1" */>}}
def greet(name):
    print(f"Hello, {name}!")  # This line is highlighted

# These lines are highlighted
for i in range(5):
    greet(f"User {i}")
{{</* /highlight */>}}
````

Parameters:
- Language (required): `python`, `go`, `javascript`, `bash`, etc.
- Options (optional):
  - `linenos=table` or `linenos=inline`: Show line numbers
  - `hl_lines=2 4-6`: Highlight specific lines
  - `linenostart=1`: Starting line number

**Code Shortcode (From File):**

Include code from a file in your page bundle:

```markdown
{{%/* code file="hello.py" lang="python" */%}}
```

This reads `hello.py` from the same directory as your markdown file and displays it with syntax highlighting.

Parameters:
- `file`: Filename in page bundle (required)
- `lang`: Language for syntax highlighting (required)

### GitHub Repository Links

Create links to files in your GitHub repository. Requires `params.githubRepo` in `config.toml`.

**Setup in config.toml:**
```toml
[params]
  githubRepo = "https://github.com/username/repo"
```

**Usage:**

Link to a file (defaults to `main` branch):
```markdown
[View source]({{</* github path="blog.go" */>}})
```

Link to a specific branch:
```markdown
[View on develop]({{</* github path="README.md" branch="develop" */>}})
```

Link to content files:
```markdown
[This post's source]({{</* github path="content/blog/my-post/index.md" */>}})
```

Generates URLs like: `https://github.com/username/repo/blob/main/blog.go`

### Vega-Lite Charts

Create interactive data visualizations using [Vega-Lite](https://vega.github.io/vega-lite/).

**1. Enable Vega in your page:**

Add to your page's front matter:
```yaml
---
title: "My Post"
vega: true
---
```

**2. Create a Vega-Lite JSON spec file:**

Place it in the **same directory** as your markdown file (page bundle):

```
content/blog/my-post/
├── index.md
└── sales-chart.json    ← Your Vega-Lite spec here
```

Example `sales-chart.json`:
```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "A simple bar chart",
  "data": {
    "values": [
      {"category": "A", "value": 28},
      {"category": "B", "value": 55},
      {"category": "C", "value": 43}
    ]
  },
  "mark": "bar",
  "encoding": {
    "x": {"field": "category", "type": "nominal"},
    "y": {"field": "value", "type": "quantitative"}
  }
}
```

**3. Add the shortcode to your markdown:**

```markdown
{{</* vega id="sales" spec="sales-chart.json" */>}}
```

Parameters:
- `id`: Unique identifier for the chart (required if you have multiple charts on one page)
- `spec`: Filename of your Vega-Lite JSON spec (must be in the same directory)

**Finding Chart Examples:**

Visit the [Vega-Lite Examples Gallery](https://vega.github.io/vega-lite/examples/) to explore:
- Bar charts, line charts, scatter plots, area charts
- Heatmaps, histograms, box plots
- Interactive charts with tooltips and selections
- Multi-view and layered visualizations

Copy an example spec, modify the data, and save it in your page bundle.

**Important:** Chart specs must be in the page bundle (same directory as your markdown), not in `/static/`. This keeps your content portable and self-contained.

## Customization

### Change Color Scheme

Edit `themes/bitsbyme/assets/css/site.css`:

```css
:root {
    --base-hue: 270; /* Change from 215 (blue) to any 0-360 */
}
```

Popular hues:
- 0 = Red
- 120 = Green
- 180 = Cyan
- 215 = Blue (default)
- 270 = Purple

### Custom Fonts

The theme uses system monospace fonts by default. To use a custom font (like Berkeley Mono, JetBrains Mono, Fira Code, etc.):

#### Step 1: Add Font Files

Place your font files in `static/fonts/`:

```bash
static/
└── fonts/
    ├── YourFont-Regular.woff2
    ├── YourFont-Regular.woff
    ├── YourFont-Bold.woff2
    ├── YourFont-Bold.woff
    ├── YourFont-Italic.woff2
    └── YourFont-Italic.woff
```

#### Step 2: Create Custom Font CSS

Create `assets/css/custom-fonts.css`:

```css
@font-face {
    font-family: "YourFont";
    src:
        url("/fonts/YourFont-Regular.woff2") format("woff2"),
        url("/fonts/YourFont-Regular.woff") format("woff");
}

@font-face {
    font-family: "YourFont";
    src:
        url("/fonts/YourFont-Italic.woff2") format("woff2"),
        url("/fonts/YourFont-Italic.woff") format("woff");
    font-style: italic;
}

@font-face {
    font-family: "YourFont";
    src:
        url("/fonts/YourFont-Bold.woff2") format("woff2"),
        url("/fonts/YourFont-Bold.woff") format("woff");
    font-weight: bold;
}

/* Override the theme's default monospace font stack */
:root {
    --monospace-font: "YourFont", monospace;
}
```

#### Step 3: Override head.html

Copy the theme's head partial and add your custom CSS:

```bash
cp themes/bitsbyme/layouts/partials/head.html layouts/partials/
```

Edit `layouts/partials/head.html` and add this line after the theme CSS links (around line 17):

```html
<head>
    <meta charset="utf-8" />
    <meta
        name="viewport"
        content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <meta
        name="description"
        content="{{ if .Params.summary }}{{ .Params.summary }}{{ else if .Site.Params.Description }}{{ .Site.Params.description }}{{ else }}Blog{{ end }}"
    />
    {{ hugo.Generator }} {{ $title := print .Title " | " .Site.Title }} {{ if
    .IsHome }}{{ $title = .Site.Title }}{{ end }}
    <title>{{ $title }}</title>
    {{ $bootstrap := resources.Get "css/bootstrap.min.css" | fingerprint }}
    {{ $siteCss := resources.Get "css/site.css" | fingerprint }}
    <link rel="stylesheet" href="{{ $bootstrap.RelPermalink }}" />
    <link rel="stylesheet" href="{{ $siteCss.RelPermalink }}" />

    <!-- ADD THIS LINE for custom fonts -->
    {{ $customFonts := resources.Get "css/custom-fonts.css" | fingerprint }}
    <link rel="stylesheet" href="{{ $customFonts.RelPermalink }}" />

    {{ partial "favicon.html" . }}
    {{ template "_internal/opengraph.html" . }} {{ template
    "_internal/twitter_cards.html" . }} {{ partial "script.html" . }}
</head>
```

Rebuild your site and your custom font will be used!

### Custom Favicons

The theme doesn't include default favicons - you should add your own.

#### Generate Favicons

**Recommended:** Use [RealFaviconGenerator.net](https://realfavicongenerator.net/) to generate a complete favicon bundle:

1. Upload your PNG image (minimum 260x260px, square recommended)
2. Customize icons for different platforms if desired
3. Download the generated package
4. The tool generates all formats including modern SVG favicons

**Simple alternative:** [Favicon.io](https://favicon.io/) for quick favicon generation from images, text, or emoji.

#### Add Favicon Files

Place generated files in `static/`:

```bash
static/
├── android-chrome-192x192.png
├── android-chrome-512x512.png
├── apple-touch-icon.png
├── favicon-16x16.png
├── favicon-32x32.png
├── favicon.ico
└── site.webmanifest
```

#### Verify Favicon Partial

The theme already includes `themes/bitsbyme/layouts/partials/favicon.html` which references these standard favicon files. No changes needed unless you want to customize the favicon partial.

The favicon partial is automatically included in the theme's `head.html`.

### Override Theme Files

To customize any theme file without modifying the theme:

1. Copy from `themes/bitsbyme/layouts/...`
2. Paste to your site's `layouts/...`
3. Edit your copy

Hugo will use your version instead of the theme's.

## Complete Example Config

See `themes/bitsbyme/exampleSite/config.toml` for a complete, working configuration.

## Need Help?

- [Full Documentation](README.md)
- [Migration Guide](MIGRATION.md) (for existing sites)
- [GitHub Issues](https://github.com/dvhthomas/blog/issues)

## Next Steps

1. Customize your config.toml
2. Create content in `content/blog/`, `content/til/`, etc.
3. Add an about page at `content/about.md`
4. Create the search page at `content/search/_index.md`
5. Deploy your site!

Happy blogging! 🎉
