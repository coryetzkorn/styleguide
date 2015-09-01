---
layout: library
title: SCSS Style
permalink: /library/scss-style/
---

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Naming Conventions

### Classes, not IDs
Never use IDs to style elements. They're completely valid and semantic, but also add unnecessary specificity. These are the reasons I only use classes:

* Classes create a level playing field when debugging CSS. 
* IDs create specificity battles.
* Classes can be reused. It's never safe to assume an element will be used only once.

### Dashes + BEM
Classes and IDs are lowercase with words separated by a dash:

Right:

```scss
.cool-box {}
.amazing-wrapper {}
.rad-button {}
```

Wrong:

```scss
.coolBox {}
.amazingwrapper {}
.rad_button {}
```

Use BEM syntax to extend classes:

```scss
.block {}
.block__element {}
.block--modifier {}
```

* `.block` represents the higher level of an abstraction or component
* `.block__element` represents a descendant of .block that helps form .block as a whole
* `.block--modifier` represents a different state or version of .block

For more about BEM, read [this great explanation](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) by Harry Roberts.

Source: <http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/>, <https://bem.info>

### Functional, not contextual
Class names should never tie an element to a specific location or context.  

Right:

```scss
.sidebar {}
.sidebar--emphasis {}
```

Wrong:

```scss
.right-col {}
.right-col--blue {}
```

The first set of selectors is better because the names describe the *function* of the element they're styling. The function of a sidebar is unlikely to change throughout the life of a project, but it's position or color could change many times.

### Colors
Colors are stored as a SASS map. Always choose names wisely. Use generalized names like "primary" and "accent" instead of "green" or "blue". If "blue" needs to be changed to red later in the project, using generic variable names will help avoid confusion.

```scss
$colors: (
  primary: rgb(50, 50, 50),
  secondary: rgb(50, 50, 50),
  tertiary: rgb(50, 50, 50),
  accent: rgb(50, 50, 50),
  inactive: rgb(50, 50, 50),
  link: rgb(50, 50, 50),
  hover: rgb(50, 50, 50),
  active: rgb(50, 50, 50),
  focus: rgb(50, 50, 50)
);
```
Colors should be defined using RGB or RGBA syntax.

Inspired by: <http://davidwalsh.name/sass-color-variables-dont-suck>

### Fonts
Use mixins to represent font families used throughout the site:

```scss
@mixin sans() {
  font-family: "Helvetica Neue", sans-serif;
  font-weight: 400;
}
@mixin sans-bold() {
  font-family: "Helvetica Neue", sans-serif;
  font-weight: 700;
}
@mixin serif() {
  font-family: "Georgia", serif;
  font-weight: 700;
}
```

These mixins typically include anything related to the styling of the font such as:

* letter-spacing
* line-height
* font-style
* font-weight
* text-decoration
* text-transform

Do not include font-size. Font sizes should be defined in a separate SASS map.

Use generic names such as "sans" of "serif-bold". Avoid naming the mixins "arial" or anything that will tie it to a specific font family.

## Syntax & Spacing

### Spacing
CSS rules should be comma separated but live on new lines:

Right:

```scss
.wrapper,
.wrapper-wide {
  …
}
```

Wrong:

```scss
.wrapper, .wrapper-wide {
  …
}
```

CSS blocks should be separated by a single new line. Not two. Not 0.

Right:

```scss
.wrapper {
  …
}
.wrapper-wide {
  …
}
```

Wrong:

```scss
.wrapper {
  …
}

.wrapper-wide {
  …
}
```

Source: <https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06>

### Indentation & Line Length
Right:

```scss
.lorem {
  color: blue;
  font-size: 2em;
  line-height: 1;
  text-decoration: none;
  font-weight: bold;
  letter-spacing: 0.02em;
}
```

Wrong:

```scss
.lorem { color: blue; font-size: 2em; line-height: 1; text-decoration: none; font-weight: bold; letter-spacing: 0.02em; }
```

### Tabs vs Spaces
TWO SPACES! Use the tab key to indent, but set the code editor to insert two spaces for every tab.

### Comments
Use single-line comments whenever possible because SASS will compile them out.

Right: 

```scss
// Header
// --------------------------------
```
```
// Cool Box
```

Wrong:

```scss
/* Header
---------------------------------*/
```

### Quotes
Quotes are optional in CSS and LESS. However, quotes make it visually clearer that the string is not a selector or a style property.

Right:

```scss
background-image: url("/img/you.jpg");
font-family: "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial;
```

Wrong:

```scss
background-image: url(/img/you.jpg);
font-family: Helvetica Neue Light, Helvetica Neue, Helvetica, Arial;
```

## Performance

### Specificity
Although in the name (cascading style sheets) cascading can introduce unnecessary performance overhead for applying styles. Take the following example:

```css
ul.user-list li span a:hover { color: red; }
```

Styles are resolved during the renderer's layout pass. The selectors are resolved right to left, exiting when it has been detected the selector does not match. Therefore, in this example every a tag has to be inspected to see if it resides inside a span and a list. As you can imagine this requires a lot of DOM walking and and for large documents can cause a significant increase in the layout time.

If we know we want to give all `a` elements inside the `.user-list` red on hover we can simplify this style to:

```css
.user-list a:hover { color: red; }
```

If we want to only style specific `a` elements inside `.user-list` we can give them a specific class:

```css
.user-list .link-primary:hover { color: red; }
```
Source: <https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06>

### Nesting
* Avoid nesting whenever possible.
* Never go more than four levels deep. 
* Nested selectors should NOT match nesting of corresponding HTML elements 1-for-1.

Right:

```scss
.container {
  ul {
    color: red;
  }
  li {
    padding: 0;
  }
  a {
    color: blue;
  }
}
```

Wrong:

```scss
.container {
  ul {
    color: red;
    li {
      padding: 0;
      a {
        color: blue;
      }
    }
  }
}
```

Source: <http://thesassway.com/beginner/the-inception-rule>

## Componentizing
A name like `.homepage-nav` limits its use. Instead think about writing styles in such a way that they can be reused in other parts of the app. Instead of .homepage-nav, try instead `.nav` or `.nav-bar`. Ask yourself if this component could be reused in another context (chances are it could!).

Here are some sample modules and their corresponding CSS:

```html
<!-- This is a cool box module -->
<div class="superbox">
  <div class="superbox__label">This is the label</div>
  <div class="superbox__content">
    <p>This is the content</p>
  </div>
</div>

<!-- This is a cool box module, extended with the "grow" class -->
<div class="superbox superbox--grow">
  <div class="superbox__label">This is the label</div>
  <div class="superbox__content">
    <p>This is the content</p>
  </div>
</div>

<!-- This is a cool text area module -->
<div class="cool-text">
  <p>Super awesome text!</p>
  <ul>
    <li>List item</li>
    <li>List item</li>
    <li>List item</li>
  </ul>
</div>
```

```scss
.superbox {
  height: 100px;
  width: 100px;
  background: red;
  &__label {
    color: white;
  }
  &__content {
    color: blue;
  }
  &--grow {
    width: 200px;
  }
}

.cool-text {
  color: black;
  p {
    margin: 1em 0;
  }
  li {
    list-style: none;
  }
}
```

## Reset vs Normalize
Every project should include either a reset or normalize stylesheet.  
[Eric Meyer's reset](http://meyerweb.com/eric/tools/css/reset/)  
[Nicolas Gallagher's normalize](http://necolas.github.io/normalize.css/)

Unless these is a compelling reason to reset all default styles (maybe if you're building an HTML5 game), use normalize. This [Stack Overflow answer](http://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css) outlines the reasons why normalize is usually more appropriate:

* Normalize.css preserves useful defaults rather than "unstyling" everything.
* Normalize.css corrects some common bugs that are out of scope for reset.css.
* Normalize.css doesn't clutter dev tools.

## Architecture

### Modules
Styles should always be grouped into reusable, modular chunks.
Never organize styles alphabetically by name. It makes sense in theory, but is horribly confusing in practice.

### File division
I typically start projects with seven stylesheets (compiled in this specific order). I've found this division works nicely:

* normalize.scss
* global.scss
* typography.scss
* layout.scss
* modules.scss
* pages.scss
* zindex.scss
* retina.scss

Here's what each file is for:

#### normalize.scss

* [Nicolas Gallagher's normalize](http://necolas.github.io/normalize.css/)

#### global.scss
* Global variables. Colors etc.
* Global mixins. 
* Utility classes such as clearfix, noselect, etc. I define these as extendable classes instead of mixins.
* Box model mode (usually set to border-box gloablly).

#### typography.scss
* Type sizes defined as variables.
* Font mixins.

#### layout.scss
* Responsive grid system.
* Container classes.
* Layout-related helper classes (such as add-margin or pad-all).

#### modules.scss
* Any code that is used more than once throughout the site that can be abstracted into a reusable modules.
* Header styles (the header counts as a module).
* Footer styles.

#### pages.scss
* Any unique code that only applies to certain pages that cannot be abstracted to a module.
* Styles scoped only to a specific page. For example, styles that are only used on the "about" page.
* Page-specific module overrides. For example, the `.cool-box` module might create a blue box by default (as defined in modules.scss). To make it red on a specific page, you could override the default using `.page-id-123 .cool-box`.

#### zindex.scss
* All z-indeces should be defined in this single file.
Here's a nice example: <https://gist.github.com/fat/1f6da6b3bd0311a1f8a0>

#### retina.scss
* Media query to replace background images for hi-dpi screens.
