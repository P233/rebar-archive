
# Rebar-Grid

Rebar-Grid is an easy-to-use, flexible, and lightweight grid stystem. It is aimed to make responsive web development more efficient and keep CSS organised.

Current version: 0.1.0

Live demo on SassMeister: [http://sassmeister.com/gist/879b15f69ce08c3d126d](http://sassmeister.com/gist/879b15f69ce08c3d126d)

Rebar-Grid is currently under developing, if you have any feedback please feel free to [open an issue](https://github.com/P233/Rebar-Grid/issues), [send me an email](mailto:hi@peiwen.lu), or [tweet me](https://twitter.com/PeiwenLu), thanks.


## Requirement

Rebar-Grid is based on [Sass maps](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#maps), it requires Sass 3.3.x and is incompatible with Sass 3.2.x and the current version of Libsass.


## Get Started

The idea of Rebar-Grid is to create/organise your own grid system with the powerful Sass map feature. Set properties value for each responsive slice into a list like `width: 30% 50% 100%`, that list means in responsive slice 1 `width: 30%`, in breakpint slice 2 `width: 50%`, etc. Grids work like [Bootstrap 3](http://getbootstrap.com/css/#grid), but container don't have padding.

You can follow these three steps to set up Rebar-Grid:

### 1. Reset `box-sizing: border-box`.

```css
*, *:before, *:after {
  box-sizing: border-box;
}
```

### 2. Add `$container` and `$grid` maps and modify the options to customise your own grids.

```scss
$container: (
  ".container": ()
);

$grid: (
  ".third": (
    width: 1 1/2 1/3
  ),
  ".two-thirds": (
    width: 1 1/2 2/3
  )
);
```


### 3. Import `rebar-grid.scss` after the two maps.

```scss
@import 'path/to/rebar-grid.scss';
```

### The above two maps will be compiled to:

```css
.container {
  margin-left: auto;
  margin-right: auto;
  max-width: 1170px; }

.container:after {
  content: "";
  display: table;
  clear: both; }

.third {
  float: left;
  width: 100%; }

.two-thirds {
  float: left;
  width: 100%; }

.third, .two-thirds {
  padding-left: 5px;
  padding-right: 5px; }

@media screen and (min-width: 480px) {
  .third {
    width: 50%; }

  .two-thirds {
    width: 50%; }

  .third, .two-thirds {
    padding-left: 9px;
    padding-right: 9px; } }
@media screen and (min-width: 768px) {
  .third {
    width: 33.33333%; }

  .two-thirds {
    width: 66.66667%; }

  .third, .two-thirds {
    padding-left: 12px;
    padding-right: 12px; } }
@media screen and (min-width: 960px) {
  .third, .two-thirds {
    padding-left: 15px;
    padding-right: 15px; } }
```



## Documentation

### Max Width

`$max-width` set max width for containers, the default value is `1170px`.


### Mobile First

`$mobile-first` set media queries order, it is enabled by default and the order is:

```scss
@media screen (min-width: nth($breakpoints, 1) ) {}
@media screen (min-width: nth($breakpoints, 2) ) {}
@media screen (min-width: nth($breakpoints, 3) ) {}
```

Set `$mobile-first: false`, media queries order will be:

```scss
@media screen (max-width: nth($breakpoints, 1) ) {}
@media screen (max-width: nth($breakpoints, 2) ) {}
@media screen (max-width: nth($breakpoints, 3) ) {}
```


### Breakpoints

`$breakpoints` contains a list of media query breakpoints, it is possiable to add as many breakpionts as you need. The default breakpoints list is `480px 768px 992px` and it represents four slices: `no media query`, `min-width: 480px`, `min-width: 768px`, and `min-width: 992px`.

If set `$mobile-first: false`, the `$breakpoints` list need to be reversed. For example:

```scss
$mobile-first: false;
$breakpoints: 992px 768px 480px;
```

This represents `no media query`, `max-width: 992px`, `max-width: 768px`, and `max-width: 480px` four slices.


### Gutters

`$gutters` contains a list of grid gutter width, it is also possiable to add as many gutters as you need, but it should always has one more value than `$breakpoints` because of the `no media query` slice. The default gutters list is `10px 18px 24px 30px`.

If set `$mobile-first: false`, the `$gutters` list need to be reversed.


### Container map options

* The length of option value list should be *less or equal* to the length of `$gutters`, each value correspond to a responsive slice. Set a value to `false` will compile nothing to CSS at this responsive slice, and the last `false` values can be omitted.
* `1/2` will be converted to `50%`.

```
nested
Set minus margin (gutter) for container, like the .row class of Bootstrap 3.
Type:    boolean
Default: false
Length:  single value
```

```
width
Set fixed width for container at each responsive slice.
Type:    number (50% | 1/2 | 600px | 40em)
Default: null
Length:  a space separated list
```

```
padding
Set padding (gutter) for container.
Type:    boolean
Default: false
Length:  single value
```


### Grid map options

```
float
Set float direction for grid at each responsive slice.
Type:    string (left | right | none)
Default: left
Length:  a space separated list
```

```
offset-left
Set margin-left for grid at each responsive slice.
Type:    number (10% | 1/12 | 100px | 5em)
Default: null
Length:  a space separated list
```

```
offset-right
Set margin-right for grid at each responsive slice.
Type:    number (10% | 1/12 | 100px | 5em)
Default: null
Length:  a space separated list
```

```
width
Set fluid width for grid at each responsive slice.
Type:    number (50% | 1/2 | 600px | 40em)
Default: null
Length:  a space separated list
```

```
max-width
Set max width for gird. $max-width will override $width.
Type:    number (50% | 1/2 | 600px | 40em)
Default: null
Length:  single value
```


## Copyright & License

Copyright (c) 2014 Peiwen Lu - Released under the MIT license.
