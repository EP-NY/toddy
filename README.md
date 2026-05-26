# Toddy
##### a fork of [Neat](http://neat.bourbon.io/) (from ThoughtBot) put together by [Extended Play](http://www.ep-ny.com)
---
###### Installation

via npm:
```sh
$ npm install toddy
```

via Yarn:
```sh
$ yarn add toddy
```

via Bower:
```sh
$ bower install toddy
```

After installing via npm/Yarn, import Toddy into your Sass:
```scss
@import "toddy/core/toddy";
```

Most Sass build tools (Webpack `sass-loader`, Dart Sass, `node-sass`, Vite, etc.) will resolve this path automatically from `node_modules`. If your toolchain doesn't search `node_modules` by default, add it to your Sass `includePaths`/`loadPaths` (e.g. `['node_modules']`) and the import above will work.

---
###### Dependencies

As this is a fork of Bourbon Neat, ~~it is dependent on [Bourbon](http://www.bourbon.io). Include it in your main stylesheet before including Toddy.~~ **Toddy is no longer dependent on Bourbon and can be used easily without it.**

---
###### Custom Settings
To change how Toddy works out of the box,  you can create a .scss file with your settings and import it before Toddy. We'll call this your `grid-settings.scss`.

###### Breakpoints
Toddy comes packaged with a series of breakpoints:

Name | Width Range
---- | -----------
small | 0-767px
medium-only | 768px-1023px
medium-up | 768px-
large-only | 1024px-1279px
large-up | 1024px-
xlarge-only | 1280px-1799px
xlarge-up | 1280px-
xxlarge-up | 1800px-

Breakpoint bounds can be overridden by defining `$width-{breakpointName}-min` and `$width-{breakpointName}-max` variables in your `grid-settings.scss` file.

Example:
```scss
// _grid-settings.scss
// Breakpoint Definitions for Toddy
$width-small-max: 45em;

$width-medium-min: 45.063em;
$width-medium-max: 58em;

$width-large-min: 58.063em;
$width-large-max: 89em;

$width-xlarge-min: 89.063em;
$width-xlarge-max: 120em;

$width-xxlarge-min: 120.063em;
```
---
###### Fixed Gutters
Fixed gutters are enabled by default. To go back to Neat's normal flexible gutters functionality, simply set `$fixed-gutter: false;` in your `grid-settings.scss`.

By default, only `$fixed-gutter-width` is defined, which will apply to all breakpoints without explicity defined gutter sizes. If you wish to change gutter sizes for larger breakpoints (except for `small`, which defaults to `$fixed-gutter-width`), do so by setting `$fixed-gutter-{breakpointName}` in `grid-settings.scss`.

Example:
```scss
// Fixed gutter sizes (only functional if $fixed-gutter is set to true)
$fixed-gutter-width: 1.875rem !global;
$fixed-gutter-medium: 2rem !global;
$fixed-gutter-large: 3rem !global;
$fixed-gutter-xlarge: null !global;
$fixed-gutter-xxlarge: null !global;
```
---
###### Classes
A la Foundation, Toddy comes packaged with classes for you to use when constructing your templates so that not all of your layout has to be written in CSS. Grid size declarations are prefixed with the breakpoint at which they should begin, followed by the number of columns the item should fill. A `div` element that should be full size on the `small` breakpoint but half-size on the `large` breakpoint is written as `<div class="small-12 large-6 columns"></div>`. Rows of grid items should be nested within `.row` elements, and grid items should be given the class of `.columns` after grid size declarations. An example is as follows:
```html
<div class="row">
  <div class="small-12 columns"></div>
  <div class="small-12 medium-6 large-3 xlarge-2 xxlarge-1 columns"></div>
</div>
```

Neat's contextual `span-columns` function works, as well. When in the context of an existing grid column, sub-columns can be created as follows:
```html
<div class="row">
  <div class="small-12 medium-6 columns">
    <div class="row">
      <div class="small-12of12 medium-4of6 columns"></div>
      <div class="small-12of12 medium-2of6 columns"></div>
    </div>
  </div>
</div>
```

You can use Neat's `@include shift()` function using classes.
```html
<div class="row">
  <div class="small-12 medium-6 medium-offset-6 columns">
    <div class="row">
      <div class="small-12of12 medium-2of6 columns"></div>
      <div class="small-12of12 medium-2of6 medium-offset-2of6 columns"></div>
    </div>
  </div>
</div>
```

---
###### Flexbox
Flexbox grids work just like the aforementioned grid classes. However, instead of wrapping grid items in a `div` with a class of `.row`, just give it a class of `.flex-row`. Replace `.columns` with `.flex-columns`. Boom. It works.

```html
<div class="flex-row">
  <div class="small-12 medium-9 large-6 flex-columns"></div>
  <div class="small-12 medium-3 large-6 flex-columns"></div>
</div>
```
