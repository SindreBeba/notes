# CSS

## Selector specificity

The following selectors are available and increase in specificity:

0. Wildcard selector (`*`)
1. Type selector (e.g., `div` or `p`)
2. Class selector (e.g., `.example`)
3. ID selector (e.g. `#example`)

It's generally a good idea to style by `class` instead of `id`. It's also considered good practice to avoid using `!important`.

## Flexbox layout

Currently, it's advisable to use `display: flex` instead of `display: float` which was used previously. There is also `display: grid`.

[A Complete Guide to Flexbox (CSS-Tricks)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) is a good resource for Flexbox.

## Reset and normalization

A CSS reset removes all default styling, while normalization seeks to keep the rules consistent across all browsers.

I usually have the following code in my projects to include the border and padding in the height and width. It's also one of the few times it's appropriate to use the wildcard selector.

```css
* {
    box-sizing: border-box;
}
```

There is also the [CSS Reset by Eric Meyer](https://meyerweb.com/eric/tools/css/reset/) and [normalize.css](https://necolas.github.io/normalize.css/).