---
layout: library
title: HTML Style
permalink: /library/html-style/
---

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Validation
All HTML pages should be verified against the [W3C validator](http://validator.w3.org/) to ensure that the markup is well formed. This in and of itself is not directly indicative of good code, but it helps to weed out problems that are able to be tested via automation.

## Self-closing Elements
Most tags should be properly closed. These include:

```
html, head, body, p, dt, dd, li, option, thead, th, tbody, tr, td, tfoot, colgroup
```

These tags do not need to be closed:

```
img, input, br, hr, meta
```

Source: <http://blog.teamtreehouse.com/to-close-or-not-to-close-tags-in-html5>

## Attributes and Tags
All tags and attributes must be written in lowercase:

```html
<a href="http://example.com/" data-color="blue" title="Description Here">Example.com</a>
```

## Quotes
According to the [W3C specifications](http://www.w3.org/TR/xhtml1/#h-4.4) for HTML, all attributes must have a value, and must use double- or single-quotes. The following are examples of proper and improper usage of quotes and attribute/value pairs.

Right:

```html
<input type="text" name="email" disabled="disabled" />
<input type='text' name='email' disabled='disabled' />
```

Wrong:

```html
<input type=text name=email disabled>
```
Source: <https://make.wordpress.org/core/handbook/coding-standards/html/#quotes>

## Indentation
HTML indentation should always reflect logical structure. Use tabs and not spaces.

Right:

```html
<?php if ( ! have_posts() ) : ?>
    <div id="post-1" class="post">
        <h1 class="entry-title">Not Found</h1>
        <div class="entry-content">
            <p>Apologies, but no results were found.</p>
            <?php get_search_form(); ?>
        </div>
    </div>
<?php endif; ?>
```
Source: <https://make.wordpress.org/core/handbook/coding-standards/html/#indentation>

## Body Class
Always use a body class to describe the contents of a page.

```html
<body class="home">
</body>

<body class="blog">
</body>

<body class="page-about page-id-1">
</body>

<body class="page-work page-id-2">
</body>

```
These descriptive classes allow CSS rules to be scoped to specific pages without crowding the global namespace. For example, the above HTML would allow for the following CSS:

```scss
// Cool box module defined in modules.scss
.cool-box {
  width: 200px;
  height: 200px;
  background: red;
}
// Page-specific override defined in pages.scss
.page-about {
  .cool-box {
    background: blue;
  }
}
```

This approach encourages DRY code and is also very semantic. A new developer could easily understand what is happening – even without any comments.

## File Naming
Image file names should be prefixed with their usage.

Right:

```
icon-home.png
bg-container.jpg
bg-home.jpg
sprite-top-navigation.png
```

Wrong:

```
home-icon.png
container-background.jpg
bg.jpg
top-navigation.png
```