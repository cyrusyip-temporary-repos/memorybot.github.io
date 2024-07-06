# Hugo Book Theme

[![Hugo](https://img.shields.io/badge/hugo-0.124-blue.svg)](https://gohugo.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Build with Hugo](https://github.com/alex-shpak/hugo-book/workflows/Build%20with%20Hugo/badge.svg)

### [Hugo](https://gohugo.io) documentation theme as simple as plain book

![Screenshot](https://raw.githubusercontent.com/alex-shpak/hugo-book/master/images/screenshot.png)

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Menu](#menu)
- [Blog](#blog)
- [Configuration](#configuration)
- [Shortcodes](#shortcodes)
- [Versioning](#versioning)
- [Contributing](#contributing)

## Features

- Clean simple design
- Light and Mobile-Friendly
- Multi-language support
- Customisable
- Zero initial configuration
- Handy shortcodes
- Comments support
- Simple blog and taxonomy
- Primary features work without JavaScript
- Dark Mode

## Requirements

- Hugo 0.124 or higher
- Hugo extended version, [Installation Instructions](https://gohugo.io/installation/)

## Installation

### Install as git submodule
Navigate to your hugo project root and run:

```
git submodule add https://github.com/alex-shpak/hugo-book themes/hugo-book
```

Then run hugo (or set `theme = "hugo-book"`/`theme: hugo-book` in configuration file)

```
hugo server --minify --theme hugo-book
```

### Install as hugo module

You can also add this theme as a Hugo module instead of a git submodule.

Start with initializing hugo modules, if not done yet:
```
hugo mod init github.com/repo/path
```

Navigate to your hugo project root and add [module] section to your `hugo.toml`:



### Partials

There are layout partials available for you to easily override components of the theme in `layouts/partials/`.

In addition to this, there are several empty partials you can override to easily add/inject code.

| Empty Partial                                      | Placement                                   |
| -------------------------------------------------- | ------------------------------------------- |
| `layouts/partials/docs/inject/head.html`           | Before closing `<head>` tag                 |
| `layouts/partials/docs/inject/body.html`           | Before closing `<body>` tag                 |
| `layouts/partials/docs/inject/footer.html`         | After page footer content                   |
| `layouts/partials/docs/inject/menu-before.html`    | At the beginning of `<nav>` menu block      |
| `layouts/partials/docs/inject/menu-after.html`     | At the end of `<nav>` menu block            |
| `layouts/partials/docs/inject/content-before.html` | Before page content                         |
| `layouts/partials/docs/inject/content-after.html`  | After page content                          |
| `layouts/partials/docs/inject/toc-before.html`     | At the beginning of table of contents block |
| `layouts/partials/docs/inject/toc-after.html`      | At the end of table of contents block       |

### Extra Customisation

| File                     | Description                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------- |
| `static/favicon.png`     | Override default favicon                                                              |
| `assets/_custom.scss`    | Customise or override scss styles                                                     |
| `assets/_variables.scss` | Override default SCSS variables                                                       |
| `assets/_fonts.scss`     | Replace default font with custom fonts (e.g. local files or remote like google fonts) |
| `assets/mermaid.json`    | Replace Mermaid initialization config                                                 |

### Plugins

There are a few features implemented as pluggable `scss` styles. Usually these are features that don't make it to the core but can still be useful.

| Plugin                            | Description                                                 |
| --------------------------------- | ----------------------------------------------------------- |
| `assets/plugins/_numbered.scss`   | Makes headings in markdown numbered, e.g. `1.1`, `1.2`      |
| `assets/plugins/_scrollbars.scss` | Overrides scrollbar styles to look similar across platforms |

To enable plugins, add `@import "plugins/{name}";` to `assets/_custom.scss` in your website root.

### Hugo Internal Templates

There are a few hugo templates inserted in `<head>`

- [Google Analytics](https://gohugo.io/templates/internal/#google-analytics)
- [Open Graph](https://gohugo.io/templates/internal/#open-graph)

To disable Open Graph inclusion you can create your own empty file `\layouts\_internal\opengraph.html`.
In fact almost empty not quite empty because an empty file looks like absent for HUGO. For example:
```
<!-- -->
```

## Shortcodes

- [Buttons](https://hugo-book-demo.netlify.app/docs/shortcodes/buttons/)
- [Columns](https://hugo-book-demo.netlify.app/docs/shortcodes/columns/)
- [Details](https://hugo-book-demo.netlify.app/docs/shortcodes/details/)
- [Hints](https://hugo-book-demo.netlify.app/docs/shortcodes/hints/)
- [KaTeX](https://hugo-book-demo.netlify.app/docs/shortcodes/katex/)
- [Mermaid](https://hugo-book-demo.netlify.app/docs/shortcodes/mermaid/)
- [Tabs](https://hugo-book-demo.netlify.app/docs/shortcodes/tabs/)

By default, Goldmark trims unsafe outputs which might prevent some shortcodes from rendering. It is recommended to set `markup.goldmark.renderer.unsafe=true` if you encounter problems.

```toml
[markup.goldmark.renderer]
  unsafe = true
```

If you are using `config.yaml` or `config.json`, consult the [configuration markup](https://gohugo.io/getting-started/configuration-markup/)

## Versioning

This theme follows a simple incremental versioning. e.g. `v1`, `v2` and so on. There might be breaking changes between versions.

If you want lower maintenance, use one of the released versions. If you want to live on the bleeding edge of changes, you can use the `master` branch and update your website when needed.

## Contributing

### [Extra credits to contributors](https://github.com/alex-shpak/hugo-book/graphs/contributors)

Contributions are welcome and I will review and consider pull requests.  
Primary goals are:

- Keep it simple.
- Keep minimal (or zero) default configuration.
- Avoid interference with user-defined layouts.
- Avoid using JS if it can be solved by CSS.

Feel free to open issues if you find missing configuration or customisation options.
