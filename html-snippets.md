---
layout: library
title: HTML Snippets
permalink: /library/html-snippets/
---

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Meta Tags

### Description
Every page should have a meta description.

```html
<meta name="description" content="xxx xxx xxxx" />
```

### Favicon

```html
<link rel="shortcut icon" href="xxxxxxx.ico"/>
```

### Viewport
Locks the viewport for responsive sites.

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1"/>
```

### Facebook
Standard open graph meta tags should be included on every page to support rich social sharing.

```html
<meta property="og:title" content="Cory Etzkorn | Blog" />
<meta property="og:name" content="Cory Etzkorn" />
<meta property="og:description" content="Designer and developer at Fuzzco. Currently living in Charleston, SC." />
<meta property="og:url" content="http://coryetzkorn.com" />
<!-- Recommended image size is 1200 x 630px -->
<meta property="og:image" content="http://coryetzkorn.com/logo.png" />
```

Facebook meta tags can be debugged here:
<https://developers.facebook.com/tools/debug/>

### Twitter
Every page should include twitter meta tags to support [twitter cards](https://dev.twitter.com/cards/types/summary).

```html
<meta name="twitter:card" content="summary" />
<meta name="twitter:site" content="Cory Etzkorn" />
<meta name="twitter:title" content="Cory Etzkorn | Blog" />
<meta name="twitter:description" content="Designer and developer at Fuzzco. Currently living in Charleston, SC." />
<meta name="twitter:image" content="http://coryetzkorn.com/logo.png" />
<meta name="twitter:url" content="http://coryetzkorn.com" />
```

Twitter cards can be validated here:
<https://cards-dev.twitter.com/validator>