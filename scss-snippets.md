---
layout: library
title: SCSS Snippets
permalink: /library/scss-snippets/
---

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Mixins

### Breakpoints Media Query

All breakpoints should be defined using a sass map and retrieved using the breakpoint mixin.

```scss
$breakpoints: (
  xl: (min-width: 1600px),
  l: (max-width: 1200px),
  m: (max-width: 880px),
  s: (max-width: 700px),
  xs: (max-width: 420px)
);
@mixin bp($name) {
  $value: map-get($breakpoints, $name);
  @if map-has-key($breakpoints, $name) {
    @media #{inspect(map-get($breakpoints, $name))} {
      @content;
    }
  }
  @else {
    @warn "The '#{$name}' breakpoint is not defined. "
        + "Please make sure it is defined in the global.scss '$breakpoint' map.";
  }
}
```

Source: <http://www.christopherkollars.com/2014/12/05/sass-map-and-my-breakpoints.html/>

### Color Mapping

This mixin retrieves colors from a color map.

```scss
/* Sample color map */
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

/* Color retrieval mixin */
@function color($key) {
  @if map-has-key($colors, $key) {
    @return map-get($colors, $key);
  }
 
  @warn "Unknown `#{$key}` in $colors.";
  @return null;
}
 
/* Mixin usage */
.element {
  background-color: color(primary); // rgb(50, 50, 50)
}
```

Source: <http://www.sitepoint.com/using-sass-maps/>

### CSS3 Vendor Prefix Mixins
For projects that don't use [autoprefixer](https://github.com/postcss/autoprefixer) or a [build process](http://gulpjs.com/), use these mixins to ensure all CSS3 animations are properly prefixed.

#### Transition

```scss
@mixin transition($transition) {
  -moz-transition: unquote($transition);
  -o-transition: unquote($transition);
  -webkit-transition: unquote($transition);
  transition: unquote($transition);
}
```

#### Transform

```scss
@mixin transform($transforms) {
  -moz-transform: unquote($transforms);
  -o-transform: unquote($transforms);
  -ms-transform: unquote($transforms);
  -webkit-transform: unquote($transforms);
  transform: unquote($transforms);
}
```

#### Keyframes

```scss
@mixin keyframes($animation-name) {
  @-webkit-keyframes $animation-name {
    @content;
  }
  @-moz-keyframes $animation-name {
    @content;
  }  
  @-ms-keyframes $animation-name {
    @content;
  }
  @-o-keyframes $animation-name {
    @content;
  }  
  @keyframes $animation-name {
    @content;
  }
}
```

#### Animation

```scss
@mixin animation($str) {
  -webkit-animation: unquote($str};
  -moz-animation: unquote($str};
  -ms-animation: unquote($str};
  -o-animation: unquote($str};
  animation: unquote($str};     
}
```

## Extendable Utility Classes
These [placeholder selectors](http://thesassway.com/intermediate/understanding-placeholder-selectors) can be extended using SASS's `@extend` method.

### No Select
Sometimes it's nice disable selection on an element. I usually use this for buttons and other UI elements. I find it helps create a more native feel.

```scss
%noselect {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
```
Source: <https://developer.mozilla.org/en-US/docs/Web/CSS/user-select?redirectlocale=en-US&redirectslug=CSS/user-select>

### Clear

```scss
%clear {
  &:before,
  &:after {
    content: "";
    display: table;
  }
  &:after {
    clear: both;
  }
}
```
Source: <http://nicolasgallagher.com/micro-clearfix-hack/>

## Other Useful Bits

### Selection Colors
Every site should have customized text selection colors.

```scss
::selection {
  background: rgb(50, 50, 50);
  color: rgb(255, 255, 255);
}
::-moz-selection {
  background: rgb(50, 50, 50);
  color: rgb(255, 255, 255);
}
```