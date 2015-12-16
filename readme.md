#Luigi (v2.1.0)

*Jump to the [index](#index) to everything that is included.*

Luigi is the Scss library developed by the developers at Bozboz and the rest of the world. It takes influence from the most popular of libraries and includes most of the popular mixins, plus some extra Bozboz crafted ones. A full list of libraries and credits can be found in the [appendix](#appendix)

All mixins are included into the main `_luigi.scss`. This is so in your `app.scss` or `style.scss` you can just include `_luigi.scss` to benefit from the whole shebang.

**When adding mixins to existing or new files, please ensure that they are placed in alphabetical order within the file**

**Luigi** is laid out folders categorising the library:

- [**Helpers**](#helpers)
- [**Layout**](#layout)
- [**Mixins**](#mixins)
- [**Predefined**](#predefined)

Alternatively, see the **[Full Luigi Index](#index)** for everything included.

##Helpers

The helpers folder includes the following files:

- [Base Vars](#base-vars)
- [Debug](#debug)
- [Print](#print)

###Base Vars

*[helpers/_base-vars.scss](scss/helpers/_base-vars.scss)*

This lays out all the variables that can be overwritten throughout Luigi. Defaults are set here:

	$base-font: Arial,sans-serif !default;

This sets the body and all inputs to the declared font

	$base-font-size: 12px !default;

The default font size for the website

	$base-gutter: 15px !default;

or

	$gutter: $base-gutter !default;

The default gutter - this is used as the margin bottom for things such as `<p>` and headings

	$gap: $gutter*2 !default

Generic space for paddings

	$grid-gap: $gutter !default

Used as the margin for grid items

	$debug-mode: false !default;

Whether or not debug mode is enabled (see information about [Debug](#debug)).

	$image-fallback-extension: 'png' !default;

Used with the [background-image](#background-image) and [image-2x](#image-2x) to append the 'png' extension to the filename.

	$image-path: '/images' !default;

This sets the default image folder for the mixins in [mixins/_images.scss](scss/mixins/_images.scss).

	$image-retina-suffix: '@2x' !default;

This is the retina suffix for retina images.

	$global-box-sizing: true !default;

This determines whether the site uses global `border-box` as its box model (see the [Box Sizing](#box-sizing) file).

	$sprite: false !default;

Used with the [sprite](#sprite) mixin to set a base path for the image sprite.

	$sprite-size: 0 0 !default;

Used with the [image-2x](#image-2x) mixing in the image file to set the original sprite-size (at 72ppi).

	$sticky-footer-height: false !default;
	$sticky-footer-margin: $sticky-footer-height !default;

These are for the sticky footer predefined file - read about the [Sticky Footer](#sticky-footer).

This is the default media query breakpoints.

	$breakpoints: (
		small: (0em, 40em),
		medium: (40.063em, 64em),
		large: (64.063em, 90em),
		xlarge: (90.063em, 120em),
		xxlarge: (120.063em)
	) !default;

Used to activate the Flex grid

	$enable-flex: false !default;

Flex alignments for Flex grid

	$flex-alignments: (
		top: flex-start,
		center: center,
		bottom: flex-end,
	) !default;

###Debug

*[helpers/_debug.scss](scss/helpers/_debug.scss)*

This file outlines any basic problems you might have in your html. Using some advanced selectors it outlines elements with things such as alt tags missing or direct descendants of `ul`s which are not `li`s.

This can be enabled by:

	$debug-mode: true;

This originates from Inuit (see [Appendix 2.1](#1-inuit))

###Print

*[helpers/_print.scss](scss/helpers/_print.scss)*

This is a basic print stylesheet - taken from Stu Robson's sassifaction (see [Appendix 2.3](#3-sassifaction)). It applies some very basic layout modifications when printing

##Layout

*[layout/_grid.scss](scss/layout/_grid.scss)*

This will generate the 12 column based grid, using the BEM conventions. Column widths are defined as a percentage of their parent and gutters are fixed at 24px. Use `.grid--no-padding` to remove the gutter.

###Inline Grid

The base grid uses inline-block elements, so you will need to remove he whitespace between the elements. There are different solutions for this. Here at Bozboz, we use HTML Comments as [David Walsh](https://davidwalsh.name/remove-whitespace-inline-block) suggests on the Solution 2.

Usage:

	<div class="grid">
		<div class="grid__item small-6 medium-3 large-8">...</div><!--
	 --><div class="grid__item small-6 medium-9 large-4">...</div>
	</div>

	<div class="grid--no-padding">
		<div class="grid__item small-4 medium-3 large-8">...</div><!--
	 --><div class="grid__item small-4 medium-5 large-2">...</div><!--
	 --><div class="grid__item small-4 medium-4 large-2">...</div>
	</div>

###Flex Grid

Flex Grid extends the inline grid conventions, using `.grid__item` and classes like `.medium-3` or `.large-6`.

Usage:

	<div class="grid-flex">
		<div class="grid__item large-4">...</div>
		<div class="grid__item medium-6 large-4">...</div>
		<div class="grid__item medium-6 large-4">...</div>
	</div>

Use `.grid-flex--{position}` to align boxes. _{position}_ can be either top, center or bottom.

Usage:

	<div class="grid-flex--center">
		<div class="grid__item large-4">...</div>
		<div class="grid__item medium-6 large-4">...</div>
		<div class="grid__item medium-6 large-4">...</div>
	</div>

Use `.grid__item--{position}` to align specific box to top, center or bottom.

Usage:

	<div class="grid-flex">
		<div class="grid__item large-4">...</div>
		<div class="grid__item--bottom medium-6 large-4">...</div>
		<div class="grid__item medium-6 large-4">...</div>
	</div>

##Mixins

The mixins folder comprises of:

- [Grid](#grid)
- [Image](#image)
- [Layout](#layout)
- [Modular](#modular)
- [Pseudo](#pseudo)
- [Responsive](#responsive)
- [Shapes](#shapes)
- [Typography](#typography)

###Grid

*[mixins/_grid.scss](scss/mixins/_grid.scss)*

This creates the classes to use in the markup for both grids.

_See the [mixin](scss/mixins/_grid.scss) for more detail_

###Image

*[mixins/_image.scss](scss/mixins/_image.scss)*

The image mixin file contains:

- [background-image](#background-image)
- [image-2x](#image-2x)
- [sprite](#sprite)

####background-image

Background-image is a mixin which uses SVG background images with PNG and retina fallback. This mixin require Modernizr.

Mixin:

	background-image($name, $size:false)

**$name**: The filename

**$size**: The background size

Usage:

	.class {
		@include background-image(sprite, 50px 100px);
	}

Output:

	.class {
		background-image: url(/images/sprite.svg);
		background-size: 50px 100px;
	}

	.no-svg .class {
		background-image: url(/images/sprite.png);
	}

	@media only screen and (-moz-min-device-pixel-ratio: 1.5), only screen and (-o-min-device-pixel-ratio: 3 / 2), only screen and (-webkit-min-device-pixel-ratio: 1.5), only screen and (min-device-pixel-ratio: 1.5) {
		.no-svg .class {
		background-image: url(/images/sprite@2x.png);
		}
	}

####image-2x

This mixin will get the high resolution image for retina displays. The retina images are twice as big with @2x appended in the name.

Mixin:

	image-2x($name, $image-size: $sprite-size)

**$name**: The filename

**$image-size**: The original sprite size (at 72ppi)

Usage:

	$sprite-size: 50px 100px;

	.class {
		@include image-2x(sprite);
	}

Output:

	@media (-moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3 / 2), (-webkit-min-device-pixel-ratio: 1.5), (min-device-pixel-ratio: 1.5), (min-resolution: 1.5dppx) {
		.class {
			background-image: url(/images/sprite@2x.png);
			background-size: 50px 100px;
		}
	}

####sprite

This makes using a sprite in a project easier and less to code - a sprite path is specified and then the mixing included. Needs to be used with the `$sprite` var.

Mixin:

	sprite($width, $height, $bg-extras)

**$width**: The width of the image

**$height**: The height of the image

**$bg-extras**: The location of the image on the sprite & any other

Usage:

	$sprite: '/images/sprite.png';

	.class {
		@include sprite(25px, 20px, 0 0);
	}

Output:

	.class {
		width: 25px;
		height: 20px;
		background: url("/images/sprite.png") no-repeat 0 0;
	}

###Layout

*[mixins/_layout.scss](scss/mixins/_layout.scss)*

The layout mixin file contains:

- [abs](#abs)
- [columns](#columns)
- [vertical-center](#vertical-center)
- [absolute-middle](#absolute-middle)

####abs

The `abs` mixin has server variants allowing for quick absolute positioning.

Mixin:

	abs-tl($top: $base-gutter, $left: $base-gutter)
	abs-tr($top: $base-gutter, $right: $base-gutter)
	abs-bl($bottom: $base-gutter, $left: $base-gutter)
	abs-br($bottom: $base-gutter, $right: $base-gutter)

**$top/$bottom/$left/$right**: Where you want the element positioned (defaults to `$base-gutter`)

Usage:

	.class {
		@include abs-tl();
	}

	.class-alt {
		@include abs-br(20px, 5%);
	}

Output:

	.class {
		left: 15px;
		position: absolute;
		top: 15px;
	}

	.class-alt {
		bottom: 20px;
		left: 5%;
		position: absolute;
	}

####columns

Columns is a simple mixin which allows the use of css3 columns

Mixin:

	columns($cols: 2, $gap: $base-gutter)

**$cols**: Number of columns you want the text split into

**$gap**: The gap between the columns

Usage:

	.class {
		@include columns(3, 10px);
	}

Output:

	.class {
		column-count: 3;
		column-gap: 10px;
	}

####vertical-center

Align vertically an element to center of a parent element

Mixin:

	vertical-center($position: relative)

Output:

	.class {
		position: relative;
		top: 50%;
		transform: translateY(-50%);
	}

####absolute-middle

Align vertically and horizontally an element to center of a parent element

Mixin:

	absolute-middle()

Output:

	.class {
		left: 50%;
		position: absolute;
		top: 50%;
		transform: translate(-50%, -50%);
	}

###Modular

*[mixins/_modular.scss](scss/mixins/_modular.scss)*

This file contains modular classes which can be used in the SCSS or within your HTML and, as such, do not take parameters. To see what each mixin does - view [modular.scss](scss/mixins/_modular.scss)

- [class](#class)
- [clearfix](#clearfix)
- [reset](#reset)
- [secret-list](#secret-list)
- [unselectable](#unselectable)

####class

This encourages more modular class naming approach and will match class names that are an extension of the base class. You passi in a class name (for example `button`) and will be inherited by variations (e.g. `button-alt` will inherit button class) - [see the example on Codepen](http://codepen.io/anon/pen/zaxej)

Mixin:

	class($class)

Usage:

	@include class(button) {
		font-size: red;
	}

Output:

	[class*="button"] {
		font-size: red;
	}


####clearfix

This adopts the clearfix hack as described by [Chris Coyier](http://css-tricks.com/snippets/css/clear-fix/)

####reset

This completely resets an element and strips it of its margin, padding, border and background.

####secret-list

This allows the semantic use of a `ul` and `li` without the styles.

**Clearfix, reset and secret-list are all placeholder selectors and should be used with an extend. E.g:**

	@extend %clearfix;

####unselectable

Disables users being able to select, helps with stopping clicks autoselecting areas

	@extend %unselectable;

###Pseudo

*[mixins/_pseudo.scss](scss/mixins/_pseudo.scss)*

The pseudo file contains mixins which affect or add a pseudo element(s)


- [placeholder](#placeholder)

####placeholder

For styling the placeholder text in a form field

Mixin:

	placeholder {
		@content
	}

**@content**: The styling for the input

Usage:

	.class {
		@include placeholder {
			color: #666;
		}
	}

Output:

	.class::-webkit-input-placeholder{
		color: #666;
	}
	.class:-moz-input-placeholder{
		color: #666;
	}
	.class::-moz-input-placeholder{
		color: #666;
	}
	.class:-ms-input-placeholder{
		color: #666;
	}

###Responsive

*[mixins/_responsive.scss](scss/mixins/_responsive.scss)*

This contains mixins that will aid with responsive web design

- [img-responsive](#img-responsive)

####img-responsive

Keep an image with same aspect ratio

Mixin:

	img-responsive($display: block)

Output:

	.class {
		display: block;
		max-width: 100%;
		height: auto;
	}

###Shapes

*[mixins/_shapes).scss](scss/mixins/_shapes).scss)*

Defines mixins for making shapes with less code.

- [circle](#circle)
- [square](#square)
- [triangle](#triangle)

####circle

The easiest and quickiest way to do circle. This mixin can be used on slider pagination.

Mixin:

	circle($size)

**$size**: The diameter of the circle

Usage:

	.class {
		@include circle(10px);
	}

Output:

	.class {
		border-radius: 50%;
		width: 10px;
		height: 10px;
	}


####square

This creates a regular quadrilateral (four equal sides and four equal angles - 90&deg;).

Mixin:

	square($size)

**$size**: The size of the square

Usage:

	.class {
		@include square(10px);
	}

Output:

	.class {
		height: 10px;
		width: 10px;
	}

####triangle

This makes the element a css triangle - for use as a pointer with the `:after` or `:before` pseudo element

Mixin:

	triangle($direction: down, $size: 20px, $color: #000)

**$direction**: what direction the arrow points (up/down/left/right)

**$size**: The size of the triangle

**$color**: What colour the triangle is

Usage:

	.class:after {
		@include triangle(up, 10px, #fff);
		content: '';
	}

Output:

	.class:after {
		width: 0;
		height: 0;
		border: 10px solid transparent;
		border-bottom-color: #fff;
		border-top-width: 0;
		content: '';
	}

###Typography

*[mixins/_typography.scss](scss/mixins/_typography.scss)*

Contains mixins which would affect the typography of the website

- [font-face](#font-face)
- [font-optimize](#font-optimize)
- [font-size](#font-size)
- [hide-text](#hide-text)
- [truncate-text](#truncate-text)

####font-face

This is a quicker, nicer way of adding a font face declaration to your styles

Mixin:

	font-face($font-name, $file, $svg-font-name: false, $weight: 100, $style: normal)

**$font-name**: The name of the font

**$file**: The path to the font files without the extension

**$svg-font-name**: The svg ID for the font (e.g. )

**$weight**: The font weight

**$style**: The font-style

Usage:

	@include font-face('Helvetica Neue Roman', fonts/helveticaneueltstd-roman-webfont, helvetica_neue_lt_std55_roman);

Output:

	@font-face{
		font-family:'Helvetica Neue Roman';
		src: url('fonts/helveticaneueltstd-roman-webfont.eot');
		src: url('fonts/helveticaneueltstd-roman-webfont.eot?#iefix') format('embedded-opentype'),
			url('fonts/helveticaneueltstd-roman-webfont.woff') format('woff'),
			url('fonts/helveticaneueltstd-roman-webfont.ttf') format('truetype'),
			url'(fonts/helveticaneueltstd-roman-webfont.svg#helvetica_neue_lt_std55_roman') format('svg');
		font-weight: 400;
		font-style: normal
	}

####font-optimize

Allows optimisation of fonts

Mixin:

	font-optimize($kerning: 0, $rendering: optimizeLegibility)

**$kerning**: The letter kerning - can be px/em/%

**$rendering**: Text rendering value - Read more on the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/CSS/text-rendering)

Usage:

	.class {
		@include font-optimize;
	}

Output:

	.class {
		letter-spacing: 0;
		text-rendering: optimizeLegibility;
	}

####font-size

Allows the use of `rem` for font sizes

Mixin:

	font-size($size)

**$size**: The size of your font in px

Usage:

	$enable-rem: true;
	.class {
		@include font-size(16px);
	}

Output:

	html {
		font-size: 62.5%;
	}

	.class {
		font-size: 16px;
		font-size: 1rem;
	}

####hide-text

An alternative way of hiding text (e.g. if you have an image as a background)

Mixin:

	hide-text

Usage:

	.class {
		@include hide-text;
	}

Output:

	.class {
		font: 0/0 a;
		text-shadow: none;
		color: transparent;
	}

####truncate-text

A simple way of truncating text on one line

Mixin:

	truncate-text($overflow: ellipsis)

**$overflow**: The overflow type. Can be clip, ellipsis, or a string

Usage:

	.class {
		@include truncate-text;
	}

Output:

	.class {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}

##Predefined

The predefined folder contains blocks of CSS which have a function - almost like a library of tricks.

- [Box Sizing](#box-sizing)
- [Sticky Footer](#sticky-footer)

###Box Sizing

*[predefined/_box-sizing.scss](predefined/_box-sizing.scss)*

This is the global box sizing, which gives every element a box model of `border-box`

This is automatically turned on in Luigi, but can be turned off by adding the following to your variables file:

	$global-box-sizing: false;

###Sticky Footer

*[predefined/_sticky-footer.scss](predefined/_sticky-footer.scss)*

This is the code to have a sticky footer (see [Appendix 2.5](#5-sticky-footer)) on your website.

Usage:

	$sticky-footer-height; 100px; // The height of your footer

If the margin on the body needs to be more or less than the height of the footer, a second variable can be declared:

	$sticky-footer-margin: 120px;

##Appendix

###1. Authors

[Luigi's authors and contributors](https://github.com/bozboz/luigi/graphs/contributors)

###2. Other Resources

####1. Inuit
[inuit.css](https://github.com/csswizardry/inuit.css)

####2. Sassifaction
[sassifaction](https://github.com/sturobson/Sassifaction)

####3. Sticky Footer
[Modern Clean CSS "Sticky Footer"](http://mystrd.at/modern-clean-css-sticky-footer/)

####4. UtilityBelt
[UtilityBelt](https://github.com/dmtintner/UtilityBelt)

###5. Inspiration

 - [Boss](https://github.com/bozboz/boss/)
 - [Preboot.less](http://markdotto.com/bootstrap)
 - [Clearless](https://github.com/clearleft/clearless)
 - [Triangle Less](https://github.com/stijnj/less-triangle)
 - [Bootstrap](https://github.com/twbs/bootstrap)

##Index

- [**Helpers**](#helpers)
	- [Base Vars](#base-vars)
	- [Debug](#debug)
	- [Print](#print)
- [**Layout**](#grid)
	- [Inline Grid](#inline-grid)
	- [Flex Grid](#flex-grid)
- [**Mixins**](#mixins)
	- [Grid](#grid)
	- [Image](#image)
		- [background-image](#background-image)
		- [image-2x](#image-2x)
		- [sprite](#sprite)
	- [Layout](#layout)
		- [abs](#abs)
		- [columns](#columns)
		- [Vertical Center](#vertical-center)
		- [Absolute Middle](#absolute-middle)
	- [Modular](#modular)
		- [class](#class)
		- [clearfix](#clearfix)
		- [reset](#reset)
		- [secret-list](#secret-list)
		- [unselectable](#unselectable)
	- [Pseudo](#pseudo)
		- [placeholder](#placeholder)
	- [Responsive](#responsive)
		- [bp](#bp)
	- [Shapes](#shapes)
		- [circle](#circle)
		- [square](#square)
		- [triangle](#triangle)
	- [Typography](#typography)
		- [font-face](#font-face)
		- [font-optimize](#font-optimize)
		- [font-size](#font-size)
		- [hide-text](#hide-text)
		- [truncate-text](#truncate-text)
- [**Predefined**](#predefined)
	- [Box Sizing](#box-sizing)
	- [Sticky Footer](#sticky-footer)
- [**Appendix**](#appendix)
	- [1. Authors](#1-authors)
	- [2. Other Resources](#2-other-resources)
	- [3. Inspiration](#2-inspiration)
