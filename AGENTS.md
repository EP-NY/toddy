# AGENTS.md

## Project Overview

**Toddy** is a lightweight, semantic grid framework built with Sass/SCSS. It's a fork of [Neat](http://neat.bourbon.io/) (originally from ThoughtBot) that has been modified by Extended Play to include fixed gutters and flexbox support. Unlike the original Neat, Toddy is **no longer dependent on Bourbon** and can be used standalone.

### Purpose
Toddy provides a semantic, responsive grid system for building layouts. It supports both traditional CSS grid classes and flexbox-based layouts, with fixed gutter widths as the default behavior.

## Architecture

### Entry Point
The main entry point is `core/_toddy.scss`, which imports all necessary components.

### Directory Structure

```
core/
├── _toddy.scss              # Main entry point
├── _toddy-helpers.scss      # Helper utilities
├── functions/               # Sass functions
│   ├── _clearfix.scss
│   ├── _modular-scale.scss
│   ├── _new-breakpoint.scss
│   ├── _private.scss
│   ├── _px-to-em.scss
│   ├── _px-to-rem.scss
│   └── _strip-units.scss
├── grid/                    # Grid system components
│   ├── _box-sizing.scss
│   ├── _collapse.scss
│   ├── _direction-context.scss
│   ├── _display-context.scss
│   ├── _fill-parent.scss
│   ├── _grid-classes.scss   # CSS classes for grid system
│   ├── _media.scss
│   ├── _omega.scss
│   ├── _outer-container.scss
│   ├── _pad.scss
│   ├── _private.scss
│   ├── _row.scss
│   ├── _shift.scss
│   ├── _span-columns.scss
│   ├── _to-deprecate.scss
│   └── _visual-grid.scss
└── settings/                # Configuration files
    ├── _breakpoints.scss    # Breakpoint definitions
    ├── _disable-warnings.scss
    ├── _grid.scss           # Grid settings and variables
    ├── _px-to-em.scss
    └── _visual-grid.scss
```

## Key Concepts

### Breakpoints
Toddy comes with predefined breakpoints:

| Name | Width Range |
|------|-------------|
| `small` | 0-767px |
| `medium-only` | 768px-1023px |
| `medium-up` | 768px+ |
| `large-only` | 1024px-1279px |
| `large-up` | 1024px+ |
| `xlarge-only` | 1280px-1799px |
| `xlarge-up` | 1280px+ |
| `xxlarge-up` | 1800px+ |

Breakpoints can be customized by overriding variables in a settings file imported before Toddy.

### Fixed Gutters
By default, Toddy uses **fixed gutters** (unlike Neat's flexible gutters). This means gutters maintain a consistent width across breakpoints unless explicitly overridden.

### Grid Classes
Toddy provides CSS classes similar to Foundation's grid system:
- `.row` - Container for grid items
- `.columns` - Grid column items
- `.flex-row` - Flexbox container
- `.flex-columns` - Flexbox column items
- Size classes: `small-12`, `medium-6`, `large-3`, etc.
- Offset classes: `medium-offset-6`, etc.

### Semantic Grid Functions
Toddy also supports Neat's semantic grid functions:
- `span-columns()` - Define column spans in Sass
- `shift()` - Offset columns
- `media()` - Media query mixin
- `new-breakpoint()` - Create custom breakpoints

## Usage Patterns

### Installation
Install via Bower:
```bash
bower install toddy
```

### Basic Import
```scss
@import "path/to/toddy/core/toddy";
```

### Custom Settings
Create a `grid-settings.scss` file and import it **before** Toddy:

```scss
// _grid-settings.scss
$width-small-max: 45em;
$width-medium-min: 45.063em;
$fixed-gutter-width: 1.875rem;
$fixed-gutter-medium: 2rem;

@import "toddy/core/toddy";
```

### HTML Class-Based Usage
```html
<div class="row">
  <div class="small-12 medium-6 large-3 columns"></div>
  <div class="small-12 medium-6 large-3 columns"></div>
</div>
```

### Flexbox Usage
```html
<div class="flex-row">
  <div class="small-12 medium-9 large-6 flex-columns"></div>
  <div class="small-12 medium-3 large-6 flex-columns"></div>
</div>
```

### Sass Function Usage
```scss
.my-element {
  @include span-columns(6);
  @include media($medium-up) {
    @include span-columns(3);
  }
}
```

## Configuration Variables

Key variables that can be customized (in `core/settings/_grid.scss`):

- `$grid-columns: 12` - Total number of columns
- `$fixed-gutter: true` - Enable/disable fixed gutters
- `$fixed-gutter-width: 1rem` - Default fixed gutter width
- `$fixed-gutter-{breakpoint}` - Breakpoint-specific gutter widths
- `$max-width: rem(2560)` - Max width for outer container
- `$border-box-sizing: true` - Enable border-box sizing globally
- `$default-layout-direction: LTR` - Layout direction (LTR/RTL)

## Important Notes

1. **No Bourbon Dependency**: Unlike original Neat, Toddy does not require Bourbon
2. **Fixed Gutters Default**: Fixed gutters are enabled by default (`$fixed-gutter: true`)
3. **12-Column Grid**: Default grid uses 12 columns
4. **Semantic First**: The framework encourages semantic HTML with Sass functions, but also provides utility classes
5. **Flexbox Support**: Includes flexbox variants (`.flex-row`, `.flex-columns`)

## Development Guidelines

- All Sass files use the `_` prefix (partials)
- Settings files define variables with `!default` flags for easy overriding
- Grid functions are in `core/grid/` directory
- Helper functions are in `core/functions/` directory
- The main `_toddy.scss` file orchestrates all imports

## Testing

Currently, there are no automated tests specified in the package.json. The framework is tested through real-world usage.

## License

MIT License - See LICENSE.md

## Repository

- GitHub: https://github.com/EP-NY/toddy
- Homepage: http://neat.bourbon.io (original Neat documentation)

