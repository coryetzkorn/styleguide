---
layout: library
title: JS Snippets
permalink: /library/js-snippets/
---

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## jQuery

### DOM Ready

```javascript
$(function(){
  
});
```

## Global Variables

### Breakpoints
Breakpoints should be saved as an object in the global scope. 

```javascript
var bp = {
  xl: 1600,
  l: 1200,
  m: 880,
  s: 700,
  xs: 420
};
```

This approach makes it easy to target certain breakpoints. For example:

```javascript
if( $(window).width() < bp.m ) {
  alert('This is a small screen');
}
```

## Approved Plugins & Libraries

### jQuery
<http://jquery.com/>  
The original workhorse. Use it, but be sure to let google [host it for you](https://developers.google.com/speed/libraries/devguide) to take advantage of their CDN.

### Underscore
<http://underscorejs.org/>  
Excellent choice for data-heavy projects that require a lot of object and array manipulation. Plays nice with jQuery.

### Cycle 2
<http://jquery.malsup.com/cycle2/>  
The best and most versatile slideshow plugin. Simple, powerful, and responsive out-of-the-box. 

### Throttle / Debounce
<http://benalman.com/projects/jquery-throttle-debounce-plugin/>  
Rate-limit your functions in multiple useful ways. Great for limiting calls to functions triggered by resize or scroll events.

### Masonry
<http://masonry.desandro.com/>  
A grid layout library. Be careful! Always try a CSS solution before resorting to this plugin. This should be a last resort.

### MatchHeight
<http://brm.io/jquery-match-height/>  
Matches the height of all selected elements. Fully responsive. Great for vertically centering variable text in grid layouts.

### Modernizr
<http://modernizr.com/>  
Detects HTML5 and CSS3 features in the user’s browser. Avoid using this unless a site relies heavily on newer browser features.

## Utility Functions

### getRandomInt()

```javascript
function getRandomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
```

### getRandomFromArray()

```javascript
function getRandomFromArray(array) {
  return array[Math.floor(Math.random()*array.length)];
}
```

### shuffle()

```javascript
function shuffle(array) {
  var currentIndex = array.length, temporaryValue, randomIndex ;
  // While there remain elements to shuffle...
  while (0 !== currentIndex) {
    // Pick a remaining element...
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex -= 1;
    // And swap it with the current element.
    temporaryValue = array[currentIndex];
    array[currentIndex] = array[randomIndex];
    array[randomIndex] = temporaryValue;
  }
  return array;
}
```