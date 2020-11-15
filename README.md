# Tabpanelwidget

This module contains the [standalone (vanilla) script](#vanilla), a [Vue component](#vue), and a [React component](#react).

## TODO

- [ ] use storybook instead of index.html (and vite)...? (would make playing with components better)
- [ ] for "old school" aka tabpanelwidget.min.js -- we should set window.tpw
--[ ] rewrite in typescript

- test page goals:
  - run locally, pug for partials
  - deploy to github pages
  - semi-DRY for vanilla, vue, react
  - same pattern with stylesheets, etc.

## TOC

* [Vanilla](#vanilla)
* [Vue](#vue)
* [React](#react)
* [ ] [Angular](#angular)
* [ ] [Ember](#ember)
* ["Old School"](#old-school)
* [Usage](#usage)
* [Development](#development)

### Vanilla

```js
import * as Tabpanelwidget from "@tabpanelwidget/tabpanelwidget"

const el = document.querySelector('#my-element')
let uninstall; Tabpanelwidget.install(el, _uninstall => (uninstall = _uninstall))
// or Tabpanelwidget.autoinstall()

// later...
if (uninstall) uninstall()
```

### Vue

```js
<script>
import VueTabpanelwidget from "tabpanelwidget/vue"
import "tabpanelwidget/dist/tabpanelwidget.min.css"

Vue.use(VueTabpanelwidget)
// or Vue.component("Tabpanelwidget", VueTabpanelwidget)
// or in component, components: { VueTabpanelwidget, ... }
```

```html
<Tabpanelwidget prop1={} prop2={}>
	<!-- TODO -->
</Tabpanelwidget>
```

### React

```jsx
import ReactTabpanelwidget from "tabpanelwidget/react"
import "tabpanelwidget/dist/tabpanelwidget.min.css"

<ReactTabpanelwidget prop1={} prop2={}>
	<!-- TODO -->
</ReactTabpanelwidget>
```

### Angular

Coming soon!

### Ember

Coming soon!

### Old School

Download the [latest release](https://github.com/tabpanelwidget/tabpanelwidget/releases) of **tabpanelwidget-x.x.x.zip** which includes:

  * The minified Script
  * The minified Polyfill
  * A stylesheet (.scss) that contains "*variables*"
  * A minified stylesheet that is the *output* of the above file

#### Setup

Wrap your headings and their relevant content inside a `div` (or else) to which you apply the class `tpw-widget`.

<small>**Note:** If you are using a Definition List, then simply apply that class to the `dl` itself.</small>

```html
<!-- .tpw-widget -->
<!-- This wrapper can be anything (article/div/dl/whatever) -->
<div class="tpw-widget">
    <!--
    You CAN use any (and as many) headings (h2/h3/h4/h5/h6)
    You MUST use the SAME heading level throughout a Widget
    You CAN use a <dl> but it has to be made of dt/dd pairs
    -->
    <h3 class="tpw-selected">Lorem</h3>
    <!--
    There is no wrapper requirement. Anything may go in between
    the headings. The script wraps that content inside two divs
    The class (optional) dictates which panel should be visible
    -->
    <h3>Ipsum</h3>
    ...
    <h3>Dolor</h3>
    ...
    <h3>Sit Amet</h3>
    ...
</div>
<!-- /.tpw-widget -->
```

Include the stylesheet in the `<head>` of your document:

```html
<link href="/PATH_TO_FILE/tabpanelwidget.min.css" rel="stylesheet" />
```

Include this before `</body>`:

```html
<script src="/PATH_TO_FILE/tabpanelwidget.min.js"></script>
<script>
  // remove this if you do not want to serve the polyfill
  if (!window.ResizeObserver) {
    const script = document.createElement("script")
    script.src = "/PATH_TO_FILE/tabpanelwidget-polyfill.min.js"
    document.head.appendChild(src)
  }
  // Instantiate TabPanelWidget
  Tabpanelwidget.autoinstall();
</script>
```

Or you may choose to load all files from CDN:

```html
<link href="//cdn.jsdelivr.net/npm/tabpanelwidget@1.0.0/dist/tabpanelwidget.min.css" rel="stylesheet" />
```

```html
<script src="//cdn.jsdelivr.net/npm/tabpanelwidget@1.0.0/dist/tabpanelwidget.min.js"></script>
<script>
  // remove this if you do not want to serve the polyfill
  if (!window.ResizeObserver) {
    const script = document.createElement("script")
    script.src = "//cdn.jsdelivr.net/npm/tabpanelwidget@1.0.0/dist/tabpanelwidget-polyfill.min.js"
    document.head.appendChild(src)
  }
  // Instantiate TabPanelWidget
  Tabpanelwidget.autoinstall();
</script>
```

The above will attach the script to all containers with the class `tpw-widget`.

<small>**Note**: The above examples use version `1.0.0` but you should link to the latest version on CDN</small>

## Usage

### Classes

"*Out-of-the-box*", the Widget will appear as shown in the [Demo section](https://tabpanelwidget.com/#demos) of TabPanelWidget.com but a few classes gives you different options. Check the SCSS file or the classes associated to the "demo Widget" at the top of [that section](https://tabpanelwidget.com/#demos).

All classes are meant to be applied to the Widget (the wrapper) with the exception of `tpw-selected` which, applied to a "heading" (or multiple headings in the case of an Accordion), will let you arbitrary choose which panel(s) to open by default (the one(s) associated with that/those heading(s)).

### "Variables"

**tabpanelwidget.min.css** is the *output* of **tabpanelwidget.scss**. The latter contains variables that will let you customize the Widget's tabs, its headers, and its panels (their color, background, border, border-radius, padding, margin, etc.).

The comments in the [SCSS file](https://github.com/tabpanelwidget/tabpanelwidget/blob/master/src/tabpanelwidget.scss) contain a great deal of information, make sure to check them out!.

## Development

Install dependencies and then opens index.html with vite (hot reload, etc.)

```bash
% npm install
% npm run dev
```

Various build scripts, for example:

```bash
% npm run build:css
% npm run build:js
```

To release new version of npm package:

```bash
% npx release-it
```

To check things post release (open index.html without vite),

```bash
% open index.html
```
