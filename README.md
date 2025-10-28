# BitsByMe Hugo Theme

A clean, accessible Hugo theme designed for technical blogs and learning journals. Features a variable-driven color scheme, integrated search, and support for technical content including Mermaid diagrams, Vega charts, and styled callout blocks.

## Features

- **Variable-driven color scheme**: Easy to customize via CSS variables
- **Accessible**: WCAG-compliant with semantic HTML, ARIA labels, and keyboard navigation
- **Responsive**: Mobile-first design using Bootstrap
- **Integrated search**: Client-side search using Fuse.js with mark.js highlighting
- **Technical content support**:
  - Mermaid diagrams
  - Vega/Vega-Lite charts
  - GitHub gist embedding
  - Syntax-highlighted code blocks
- **Styled callouts**: TIP and INFO blockquote styles
- **Content organization**: Support for blog posts, TIL (Today I Learned) notes, series, and tags
- **Related content**: Automatic related posts based on tags
- **Table of contents**: Automatic TOC generation for long posts
- **Customizable fonts**: Use system fonts or easily add your own custom fonts

## Installation

### Quick Start

See [Getting Started Guide](docs/getting-started.md) for detailed installation instructions.

### Hugo Modules (Recommended)

```bash
# Initialize your site as a module
hugo mod init github.com/yourusername/your-site
```

Add to `config.toml`:
```toml
[module]
  [[module.imports]]
    path = "github.com/dvhthomas/blog"
```

Run `hugo server` and the theme will be downloaded automatically.

### Traditional Install

```bash
cd your-hugo-site
git clone https://github.com/dvhthomas/blog.git themes/bitsbyme
```

Add to `config.toml`:
```toml
theme = "bitsbyme"
```

## Configuration

### Minimum Required Configuration

The theme works with just these settings:

```toml
baseURL = "https://example.com/"
languageCode = "en-us"
title = "Your Site Title"
theme = "bitsbyme"

# Required for search functionality
[outputs]
  home = ["HTML", "RSS", "JSON"]
```

Everything else is **optional** and provides sensible defaults or gracefully omits features.

### Complete Configuration (All Optional)

Here's a full example with all optional parameters:

```toml
baseURL = "https://example.com/"
languageCode = "en-us"
title = "Your Site Title"
theme = "bitsbyme"

[pagination]
  pagerSize = 10

[params]
  # Home page text displayed under the title (optional)
  homeText = "your tagline here"

  # Introduction paragraph on home page (optional, supports markdown)
  homeIntro = """
Hi 👋 [I'm Your Name](/about). Most content is in
[blog posts](/blog/) or little notes to my future self called
[Today I Learned...](/til/)
Follow the links up top☝️to explore. Social links are in the footer👇
"""

  # Date format for displaying dates (optional, defaults to "Jan 2, 2006")
  dateFormat = "January 2, 2006"

  # Site description for meta tags (optional, defaults to "Blog")
  description = "Your site description"

  # Default image for social sharing (optional)
  images = ["/path/to/social-image.png"]

  # Link to GitHub repo (optional, enables "View page source" links)
  githubRepo = "https://github.com/username/repo"

  # Search configuration (all optional, have defaults)
  searchPlaceholder = "Search...."
  searchButton = "Search"
  searchLabel = "Search the site"
```

### Footer Links

Configure social and footer links:

```toml
[[params.footerLinks]]
  name = "My Work"
  url = "/work/"
  icon = "briefcase"
  ariaLabel = "My Work"
  external = false

[[params.footerLinks]]
  name = "GitHub"
  url = "https://github.com/yourusername"
  icon = "github"
  ariaLabel = "GitHub profile"
  external = true

[[params.footerLinks]]
  name = "LinkedIn"
  url = "https://www.linkedin.com/in/yourname/"
  icon = "linkedin"
  ariaLabel = "LinkedIn profile"
  external = true

[[params.footerLinks]]
  name = "Bluesky"
  url = "https://bsky.app/profile/yourhandle.bsky.social"
  icon = "bluesky"
  ariaLabel = "Bluesky profile"
  external = true

[[params.footerLinks]]
  name = "Subscribe"
  url = "/index.xml"
  icon = "rss"
  ariaLabel = "Subscribe via RSS"
  external = false
```

Available icons: `briefcase`, `github`, `linkedin`, `bluesky`, `rss`

### Menu Configuration

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
    name = "TIL"
    url = "/til/"
    weight = 3
    [menu.main.params]
      icon = "award"
  [[menu.main]]
    name = "Tags"
    url = "/tags/"
    weight = 4
    [menu.main.params]
      icon = "tag"
  [[menu.main]]
    name = "About"
    url = "/about/"
    weight = 5
    [menu.main.params]
      icon = "user"
```

**Available menu icons**: `home`, `edit`, `award`, `tag`, `book`, `user`

Icons are custom Feather-style SVG symbols defined in `themes/bitsbyme/layouts/partials/nav.html`. The `icon` parameter is optional - if omitted, only the text label will be displayed.

**Note**: For backward compatibility, the theme also supports Hugo's standard `pre` field for icons (e.g., `pre = "home"`), but using the `params.icon` structure is recommended for clarity.

### Permalinks

```toml
[permalinks]
  blog = "/:year/:month/:title"
  til = "/til/:year-:month-:day/"
```

### Taxonomies

```toml
[taxonomies]
  tag = "tags"
  series = "series"
```

### Markup Configuration

```toml
[markup]
  [markup.highlight]
    codeFences = true
    guessSyntax = false
    lineNos = true
    lineNumbersInTable = true
    noClasses = true
    style = "github"
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true  # Required for custom HTML and shortcodes
```

### Search Setup

The theme includes built-in client-side search using Fuse.js. To enable it:

1. Add JSON output format to `config.toml`:

```toml
[outputs]
  home = ["HTML", "RSS", "JSON"]
```

2. Create a search page at `content/search/_index.md`:

```markdown
---
title: "Search"
layout: "search"
---
```

That's it! The theme includes:
- Search JavaScript files (Fuse.js, Mark.js, custom search logic)
- Search index template (`index.json`)
- Search page layout
- Search form in the header

The search page will be available at `/search/` on your site.

## Content

### Front Matter

The theme uses this front matter structure:

```yaml
---
title: "Your Post Title"
date: 2025-01-15
tags: ["tag1", "tag2"]
series: ["series-name"]
summary: "A brief summary of the post"
toc: true  # Enable table of contents
mermaid: false  # Enable Mermaid diagrams
mathjax: false  # Enable MathJax for math equations
draft: false
images: ["/path/to/image.png"]
---
```

### Content Sections

The theme supports these content sections:

- `content/blog/` - Blog posts
- `content/til/` - Today I Learned notes
- `content/about/` - About page
- Any other Hugo content sections

### Callout Blocks

Create styled TIP and INFO blocks using blockquotes:

```markdown
> TIP: This is a helpful tip for readers.

> INFO: This is informational content.
```

### Shortcodes

#### Mermaid Diagrams

```markdown
{{< mermaid >}}
graph TD
    A[Start] --> B[Process]
    B --> C[End]
{{< /mermaid >}}
```

#### Vega Charts

Create data visualizations using [Vega-Lite](https://vega.github.io/vega-lite/).

**Setup:**
1. Add `vega: true` to your page's front matter
2. Create a Vega-Lite JSON spec file in the **same directory** as your `index.md` (page bundle)
3. Reference it using the `vega` shortcode

**Example:**

```
content/blog/my-post/
├── index.md
└── chart.json    ← Vega-Lite spec here
```

In your markdown:
```markdown
{{< vega id="chart1" spec="chart.json" >}}
```

The `id` parameter creates a unique div ID for the chart (useful if you have multiple charts on one page).

**Note:** Chart specs must be in the page bundle (same directory as the markdown file), not in `/static/`. This keeps your content portable and follows Hugo's page resource pattern.

#### GitHub Gist

```markdown
{{< gist username gist-id >}}
```

#### Code Blocks

```markdown
{{< code language="python" >}}
def hello():
    print("Hello, World!")
{{< /code >}}
```

## Customization

### Color Scheme

Edit `assets/css/site.css` to customize colors:

```css
:root {
    --base-hue: 215; /* Change this to adjust the entire color scheme */
    --brand-color: hsl(var(--base-hue), 80%, 65%);
    --action-color: hsl(var(--base-hue), 70%, 45%);
    --highlight-color: hsl(calc(var(--base-hue) + 180), 84%, 40%);
}
```

### Fonts

The theme uses system monospace fonts by default (ui-monospace, Cascadia Code, Source Code Pro, Menlo, Consolas, etc.).

To use a custom monospace font:

1. Add your font files to your site's `static/fonts/` directory

2. Add `@font-face` declarations in your site's `assets/css/custom.css`:

```css
@font-face {
    font-family: "MyCustomFont";
    src: url("/fonts/MyCustomFont.woff2") format("woff2"),
         url("/fonts/MyCustomFont.woff") format("woff");
}

:root {
    --monospace-font: "MyCustomFont", monospace;
}
```

3. Include the custom CSS in your site's `layouts/partials/head.html`:

```html
{{ $customCSS := resources.Get "css/custom.css" | fingerprint }}
<link rel="stylesheet" href="{{ $customCSS.RelPermalink }}" />
```

Popular monospace fonts:
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/) (free)
- [Fira Code](https://github.com/tonsky/FiraCode) (free)
- [Cascadia Code](https://github.com/microsoft/cascadia-code) (free)
- [IBM Plex Mono](https://www.ibm.com/plex/) (free)
- [Berkeley Mono](https://berkeleygraphics.com/typefaces/berkeley-mono/) (commercial)

## License

MIT License - see LICENSE file for details

## Credits

- Built with [Hugo](https://gohugo.io/)
- Uses [Bootstrap](https://getbootstrap.com/) for responsive layout
- Search powered by [Fuse.js](https://fusejs.io/) and [Mark.js](https://markjs.io/)
- Icons from [Feather Icons](https://feathericons.com/)
