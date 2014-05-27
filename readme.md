#Luigi (v1.4.0)

*Jump to the [index](#index) to everything that is included.*

Luigi is the Scss library developed by the developers at Bozboz and the rest of the world. It takes influence from the most popular of libraries and includes most of the popular mixins, plus some extra Bozboz crafted ones. A full list of libraries and credits can be found in the [appendix](#appendix)

All mixins are included into the main `_luigi.scss`. This is so in your `app.scss` or `style.scss` you can just include `_luigi.scss` to benefit from the whole shebang.

**When adding mixins to existing or new files, please ensure that they are placed in alphabetical order within the file**

**Luigi** is laid out folders categorising the library:

- [**Helpers**](#helpers)
- [**Mixins**](#mixins)
- [**Predefined**](#predefined)

Alternatively, see the **[Full Luigi Index](#index)** for everything included.

##Helpers

The helpers folder includes the following files:

- [Base Vars](#base-vars)
- [Debug](#debug)
- [Normalize](#normalize)
- [Print](#print)

###Base Vars

*[helpers/_base-vars.scss](helpers/_base-vars.scss)*

This lays out all the variables that can be overwritten throughout Luigi. Defaults are set here:

	$base-font: Arial,sans-serif !default;

This sets the body and all inputs to the declared font

	$base-font-size: 12px !default;

The default font size for the website

	$base-gutter: 15px !default;

The default gutter - this is used as the margin bottom for things such as `<p>` and headings

	$breakpoints: (
		'mouse' '(max-width: 480px)',
		'cat' '(min-width: 481px) and (max-width: 1023px)',
		'dog' '(max-width: 1023px)',
		'whale' '(min-width: 1024px)'
	) !default;

This is the default media query breakpoints array for use with the [bp](#bp) mixin. The variables should be animal names.

	$debug-mode: false !default;

Whether or not debug mode is enabled (see information about [Debug](#debug)).

	$image-fallback-extension: 'png' !default;

Used with the [background-image](#background-image) and [image-2x](#image-2x) to append the 'png' extension to the filename.

	$image-path: '/images' !default;

This sets the default image folder for the mixins in [mixins/_images.scss](mixins/_images.scss).

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

	$vendors: '-webkit-' '-moz-' '-ms-' '-o-' '' !default;
	$vendors-no-ms: '-webkit-' '-moz-' '-o-' '' !default;
	$vendors-no-w3c: '-webkit-' '-moz-' '-o-' '-ms-' !default;
	$vendors-placeholder: ':-webkit' '-moz' ':-moz' '-ms' !default;

Vendor arrays used for the [CSS3](#css3) mixins.

###Debug

*[helpers/_debug.scss](helpers/_debug.scss)*

This file outlines any basic problems you might have in your html. Using some advanced selectors it outlines elements with things such as alt tags missing or direct descendants of `ul`s which are not `li`s.

This can be enabled by:

	$debug-mode: true;

This originates from Inuit (see [Appendix 2.1](#1-inuit))

###Normalize

*[helpers/_normalize.scss](helpers/_normalize.scss)*

This is a slightly modified version of normalize from necolas (see [Appendix 2.2](#2-normalize)). It has `$base-font` and `$base-gutter` scattered throughout.

###Print

*[helpers/_print.scss](helpers/_print.scss)*

This is a basic print stylesheet - taken from Stu Robson's sassifaction (see [Appendix 2.3](#3-sassifaction)). It applies some very basic layout modifications when printing

##Mixins

The mixins folder comprises of:

- [CSS3](#css3)
- [Grid](#grid)
- [Image](#image)
- [Layout](#layout)
- [Modular](#modular)
- [Pseudo](#pseudo)
- [Responsive](#responsive)
- [Shapes](#shapes)
- [Typography](#typography)

###CSS3

*[mixins/_css3.scss](mixins/_css3.scss)*

This file contains many mixins that require vendor prefixes to achieve what have been dubbed as **css3**.
- [animation](#animation)
- [bg-size](#bg-size)
- [border-radius-noclip && border-radius](#border-radius-noclip--border-radius)
- [box-shadow](#box-shadow)
- [box-sizing](#box-sizing)
- [color-alpha](#color-alpha)
- [keyframes](#keyframes)
- [gradient](#gradient)
- [gradient-radial](#gradient-radial)
- [opacity](#opacity)
- [transition && transition-property && transition-transform](#transition--transition-property--transition-tranform)
- [transform && transform-property](#transform--transform-property)


####animation

For defining CSS animations

Mixin:

	aniamtion($animation)

**$animation:**	 Parameters for animation declaration

Usage

	.class {
		@include animation(animation-name 1s linear infinite);
	}

Outout

	.class {
		-webkit-animation: animation-name 1s linear infinte;
		-moz-animation: animation-name 1s linear infinte;
		-o-animation: animation-name 1s linear infinte;
		animation: animation-name 1s linear infinte;
	}


####bg-size

For specifying the background size.

Mixin:

	bg-size($size)

**$size**: The size of the background (see [CSS3 Info](http://www.css3.info/preview/background-size/) for details of how to use it)

Usage:

	.class {
		@include bg-size(100%);
	}

Output:

	.class {
		-webkit-background-size: 100%;
		background-size: 100%;
	}

####border-radius-noclip && border-radius

The `noclip` mixin works the same as `border-radius` but without the background-clip declarations.

Mixin:

	border-radius($radius)
	border-radius-noclip($radius)

**$radius**: Parameters of the required border radius

Usage:

	.class {
		@include border-radius(10px);
	}
	.class-alt {
		@include border-radius-noclip(10px 15px 5px 10px);
	}

Output:

	.class {
		-webkit-border-radius: 10px;
		border-radius: 10px;
		-moz-background-clip: padding;
		-webkit-background-clip: padding-box;
		background-clip: padding-box;
	}

	.class-alt {
		-webkit-border-radius: 10px 15px 5px 10px;
		border-radius: 10px 15px 5px 10px;
	}

####box-shadow

Mixin:

	box-shadow($shadow: 0px 5px 5px 2px rgba(0, 0, 0, 0.3))

**$shadow**: Box shadow parameters - [CSS3 Generator](http://css3generator.com/) can be particularly helpful

Usage:

	.class {
		@include box-shadow();
	}

Output:

	.class {
		-webkit-box-shadow: 0px 5px 5px 2px rgba(0, 0, 0, 0.3);
		box-shadow: 0px 5px 5px 2px rgba(0, 0, 0, 0.3);
	}

####box-sizing

Allows redefining the box-model on elements

Mixin:

	box-sizing($box: border-box)

**$box**: The box model you wish the element to adopt

Usage:

	.class {
		@include box-sizing();
	}

Output:

	.class {
		-webkit-box-sizing: border-box;
		-moz-box-sizing: border-box;
		box-sizing: border-box;
	}

####color-alpha

Provides `rgba` with a property fallback

Mixin:

	color-alpha($theme, $alpha: 0.5, $property: 'background-color')

**$theme**: The colour you wish to make transparent (can be hex or rgb)

**$alpha**: The opacity value (from 0 to 1)

**$property**: The property you wish to apply the `rgba` to (defaults to `background-color`)


Usage:

	.class {
		@include color-alpha(#f00, 0.3);
	}

Output:

	.class {
		background-color: #f00;
		background-color: rgba(255, 0, 0, 0.3);
	}



####Keyframes

Adds relevent prefixes to keyframes

Mixin

	keyframes($name) {
		@content;
	}


***$name:***  The name of the keyframes that you can reference in the animation property

***@content:*** The keyframes declreations

Usage
	@include keyframes(color-change) {
		from {
			color: red;
		}
		to {
			color: blue;
		}
	}

*Omitting output due to large amounts of code.- see the [mixin](mixins/_css3.scss) for more detail*

####gradient

Allows creation of background gradients without endless amounts of vendor prefixing. Can cater for horizontal, vertical or diagonal gradients. See also [radial gradients](#gradient-radial) mixin.

Mixin:

	gradient($type, $start, $end, $degrees: false)

**$type**: Can be **h** (horizontal), **v** (vertical) or **d** (diagonal).

**$start**: The gradient start colour

**$end**: The gradient end colour

**$degrees**: If using a **d** type, then what angle should the gradient be

Usage:

	.class {
		@include gradient(h, #f00, #0f0);
	}

*Omitting output due to large amounts of code.- see the [mixin](mixins/_css3.scss) for more detail*

####gradient-radial

This mixin is for creating a radial gradient.

Mixin:

	gradient-radial($size, $shape, $position, $fallback, $colors...)

**$size**: Size describing how big the ending shape must be. The possible options are: **closest-side**, **closest-corner**, **farthest-side**, **farthest-corner**

**$shape**: The gradient's shape. Can be **circle** or **ellipse**

**$position**: The position of the gradient in the element

**$fallback**: Fallback background color for old browsers

**$colors**: The sequence of colors

Usage:

	.class {
		@include gradient-radial(farthest-corner, circle, center center, #f00, rgba(255,0,0,0.5), #333, orange)
	}

Output:

	.class {
		background: #f00;
		background: -webkit-radial-gradient(center center, farthest-corner circle, rgba(255, 0, 0, 0.5), #333333, orange);
		background: -moz-radial-gradient(center center, farthest-corner circle, rgba(255, 0, 0, 0.5), #333333, orange);
		background: -o-radial-gradient(center center, farthest-corner circle, rgba(255, 0, 0, 0.5), #333333, orange);
		background: -ms--radial-gradient(center center, farthest-corner circle, rgba(255, 0, 0, 0.5), #333333, orange);
		background: radial-gradient(farthest-corner circle at center center, rgba(255, 0, 0, 0.5), #333333, orange);
	}

####opacity

Handles all vendors for using opacity.

Mixin:

	opacity($opacity: 50)

**$opacity**: A number between 0 (transparent) and 100 (opaque)

Usage:

	.class {
		@include opacity(85);
	}

Output:

	.class {
		-ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity="85")";
		filter: alpha(opacity=85);
		opacity: 0.85;
		zoom: 1;
	}

####transition && transition-property && transition-tranform

This handles transitions and being able to override specific transition properties.

Mixins:

	transition($time: 0.2s, $attr: all, $effect: ease, $webkit-transform: false)
	transition-property($attr, $value)
	transition-transform($attr)

**$time**: How long the animation lasts

**$attr**: The attribute to affect (e.g. all, opacity, width). *Optional in transition-transform mixin*.

**$effect**: What transition effect should be used. See the [W3C Working Draft](http://www.w3.org/TR/css3-transitions/#transition-timing-function-property) for all options.

**$webkit-transform**: Whether to add `-webkit-backface-visibility: hidden;` to fix opacity and other rendering issues as [described here](http://stackoverflow.com/questions/15051557/very-difficult-to-solve-and-strange-css3-opacity-transition-issue-must-be-a#answer-17353755)

Usage:

	.class {
		@include transition();
	}

	.context .class {
		@include transition-property(duration, 0.8s);
	}

	.another-context .class {
		@include transition-transform(opacity);
	}

Output:

	.class {
		-webkit-transition: 0.5s all ease;
		-moz-transition: 0.5s all ease;
		-o-transition: 0.5s all ease;
		transition: 0.5s all ease
	}

	.context .class {
		-webkit-transition-duration: 0.8s;
		-moz-transition-duration: 0.8s;
		-o-transition-duration: 0.8s;
		transition-duration: 0.8s
	}

	.another-context .class {
		-webkit-transition-property: -webkit-transform, opacity;
		-o-transition-property: -webkit-transform, opacity;
		transition-property: -webkit-transform, opacity;
		transition-property: transform, opacity;
	}

####transform && transform-property

Much like the transition one, this allows transformations to be used easily

Mixin:

	transform($trans)
	transform-property($attr, $value)

**$trans**: The transform value

**$attr**: The transform attribute to specifically target

**$value**: The value for the specific attribute

Usage:

	.class {
		@include transform(skew(35deg));
	}

	.context .class {
		@include transform-property(origin, 25% 75%)
	}

Output:

	.class {
		-webkit-transform: skew(35deg);
		-moz-transform: skew(35deg);
		-ms-transform: skew(35deg);
		-o-transform: skew(35deg);
		transform: skew(35deg);
	}

	.context .class {
		-webkit-transform-origin: 25% 75%;
		-moz-transform-origin: 25% 75%;
		-ms-transform-origin: 25% 75%;
		-o-transform-origin: 25% 75%;
		transform-origin: 25% 75%;
	}

###Grid

*[mixins/_grid.scss](mixins/_grid.scss)*

The grid system is included but not fully developed - documentation can be seen at the top of the [file](mixins/_grid.scss).

Full instructions on use will be written once the grid system has been implemented.

###Image

*[mixins/_image.scss](mixins/_image.scss)*

The image mixin file contains:

- [background-image](#background-image)
- [image-2x](#image-2x)
- [sprite](#sprite)
- [spritesmith](#spritesmith)

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
			-webkit-background-size: 50px 100px;
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

####spritesmith

These mixins are for use with the [gulp.spritesmith](https://github.com/twolfson/gulp.spritesmith) plugin, defining our own so there is no conflict with the original sprite mixin.

###Layout

*[mixins/_layout.scss](mixins/_layout.scss)*

The layout mixin file contains:

- [abs](#abs)
- [columns](#columns)

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
		position: absolute;
		top: 15px;
		left: 15px;
	}

	.class-alt {
		position: absolute;
		bottom: 20px;
		left: 5%;
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
		-webkit-column-count: 3;
		-moz-column-count: 3;
		column-count: 3;
		-webkit-column-gap: 10px;
		-moz-column-gap: 10px;
		column-gap: 10px;
	}

###Modular

*[mixins/_modular.scss](mixins/_modular.scss)*

This file contains modular classes which can be used in the SCSS or within your HTML and, as such, do not take parameters. To see what each mixin does - view [modular.scss](mixins/_modular.scss)

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

*[mixins/_pseudo.scss](mixins/_pseudo.scss)*

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

*[mixins/_responsive.scss](mixins/_responsive.scss)*

This contains several mixins that will aid with responsive web design

- [bp](#bp)
- [img-responsive](#img-responsive)

####bp

This is helpful when using the sass bubbling technique and allows (with the help of the `$breakpoints` variable) a definition of user-friendly sizes

Adapted from CSS Wizarry Grids (see [Appendix 2.4](#4-grids))

Mixin:

	bp($media-query) {
		@content
	}

**$media-query**: User-friendly name or px based (e.g. `palm` or `(max-width: 480px)`)

**@content**: The declarations to affect the element

Usage:

	.class {
		@include bp(desktop) {
			width: 50%;
		}
		width: 25%
	}

Output:

	.class {
		width: 25%;
	}
	@media only screen and (max-width: 1600px){
		.class {
			width:50%;
		}
	}

####img-responsive

This helps make the image responsive

Mixin:

	img-responsive($display: block);

**$display**: What you want the display type to be

Usage:

	.class {
		@include img-responsive();
	}

Output:

	.class {
		display: block;
		max-width: 100%;
		height: auto;
	}

###Shapes

*[mixins/_responsive.scss](mixins/_responsive.scss)*

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
		-webkit-border-radius: 10px;
		border-radius: 10px;
		-moz-background-clip: padding;
		-webkit-background-clip: padding-box;
		background-clip: padding-box;
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
		width: 10px;
		height: 10px;
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

*[mixins/_typography.scss](mixins/_typography.scss)*

Contains mixins which would affect the typography of the website

- [font](#font)
- [font-face](#font-face)
- [font-optimize](#font-optimize)
- [font-size](#font-size)
- [hide-text](#hide-text)
- [truncate-text](#truncate-text)

####font

Allows quick setting of some default font families

Mixin:

	font($type)

**$type**: What font you want. Can be hell (Helvtica Neue), sans (Arial), serif (Georgia) or monospace (Monaco)

Usage:

	.class {
		@include font(monospace)
	}

Output:

	.class {
		font-family: "Monaco", "Courier New", monospace;
	}

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

####2. Normalize
[normalize.css](http://necolas.github.io/normalize.css/)

####3. Sassifaction
[sassifaction](https://github.com/sturobson/Sassifaction)

####4. Grids
[csswizardry-grids](https://github.com/csswizardry/csswizardry-grids)

####5. Sticky Footer
[Modern Clean CSS "Sticky Footer"](http://mystrd.at/modern-clean-css-sticky-footer/)

####5. UtilityBelt
[UtilityBelt](https://github.com/dmtintner/UtilityBelt)

###3. Inspiration

 - [Boss](https://github.com/bozboz/boss/)
 - [Preboot.less](http://markdotto.com/bootstrap)
 - [Clearless](https://github.com/clearleft/clearless)
 - [Triangle Less](https://github.com/stijnj/less-triangle)
 - [Bootstrap](https://github.com/twbs/bootstrap)

##Index

- [**Helpers**](#helpers)
	- [Base Vars](#base-vars)
	- [Debug](#debug)
	- [Normalize](#normalize)
	- [Print](#print)
- [**Mixins**](#mixins)
	- [CSS3](#css3)
		- [animation](#animation)
		- [bg-size](#bg-size)
		- [border-radius-noclip && border-radius](#border-radius-noclip--border-radius)
		- [box-shadow](#box-shadow)
		- [box-sizing](#box-sizing)
		- [color-alpha](#color-alpha)
		- [keyframes](#keyframes)
		- [gradient](#gradient)
		- [gradient-radial](#gradient-radial)
		- [opacity](#opacity)
		- [transition && transition-property && transition-transform](#transition--transition-property--transition-tranform)
		- [transform && transform-property](#transform--transform-property)
	- [Grid](#grid)
	- [Image](#image)
		- [background-image](#background-image)
		- [image-2x](#image-2x)
		- [sprite](#sprite)
		- [spritesmith](#spritesmith)
	- [Layout](#layout)
		- [abs](#abs)
		- [columns](#columns)
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
		- [img-responsive](#img-responsive)
	- [Shapes](#shapes)
		- [circle](#circle)
		- [square](#square)
		- [triangle](#triangle)
	- [Typography](#typography)
		- [font](#font)
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
