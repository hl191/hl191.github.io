---
layout: page
title: Sass
exclude: true
---

[Sass](https://sass-lang.com/) is a CSS extension, which comes in very handy for web applications.

To generate multiple style classes to use for your HTML we can generate them in Sass:

# Generate dynamic style classes

#### color and background-color

```CSS
$gray-scales: (
  gray-900: #2b2b2b,
  gray-700: #595959,
  gray-600: #6a6a6a,
);

@each $class, $value in $gray-scales {
  .color-#{$class} {
    color: $value;
  }
  .bg-color-#{$class} {
    background-color: $value;
  }
}
```

Will produce multiple classes:

```CSS
.color-gray-900 {
  color: #2b2b2b;
}
.bg-color-gray-900 {
  background-color: #2b2b2b;
}

// etc. for all values in the gray-scales list
```

#### font classes

Here I use a `mixin` function to generate multiple lines of predefined CSS styles with variable font size and line height.

```CSS
@mixin regular-font($font-size, $line-height) {
  font-style: normal;
  font-weight: normal;
  font-size: $font-size;
  line-height: $line-height;
}

@mixin bold-font($font-size, $line-height) {
  font-style: normal;
  font-weight: bold;
  font-size: $font-size;
  line-height: $line-height;
}

$font-sizes: (
  xs: (12px, 120%),
  sm: (14px, 125%),
  base: (16px, 150%),
  lg: (18px, 150%),
);

@each $class, $value in $font-sizes {
  .font-regular-#{$class} {
    @include regular-font(#{nth($value, 1)}, #{nth($value, 2)});
  }
  .font-bold-#{$class} {
    @include bold-font(#{nth($value, 1)}, #{nth($value, 2)});
  }
}
```

The result classes will look like this (where `xs` may be replaced with any size, defined in the `font-sizes` map)

```CSS
.font-regular-xs {
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 120%;
}
.font-bold-xs {
  font-style: normal;
  font-weight: bold;
  font-size: 12px;
  line-height: 120%;
}
```
