#Luigi

Luigi is the Scss library developed by the developers at Bozboz and the rest of the world. It takes influence from the most popular of libraries and includes most of the popular mixins, plus some extra Bozboz crafted ones.

All mixins are included into the main `_luigi.scss`. This is so in your `app.scss` or `style.scss` you can just include '_luigi.scss' to benefit from the whole shebang.

**When adding mixins to existing or new files, please ensure that they are place in alphabetical order**

**Luigi** is laid out folders categorising the library
- [**helpers**](#helpers)
- [**mixins**](#mixins)
- [**predefined**](#predefined).

##Helpers

The helpers folder includes:

###Base Vars

This lays out all the vairables that are overwriteable throughout Luigi. Defaults are set here.

###Debug

This file outlines any basic problems you might have in your html. Using some advanced selectors it outlines elements with things such as alt tags missing or direct decendants of `ul`s whoch are not `li`s.

This can be enabled by:

	$debug-mode: true;

{This originates from [inuit.css](https://github.com/csswizardry/inuit.css)}

###Normalize

This is a slightly modified version of [normalize.css]{http://necolas.github.io/normalize.css/} from necolas. It has `$basefont` and `$basegutter` scattered throughout.

###Print

This is a basic print stylesheet - taken from Stu Robson's [Sassifaction](https://github.com/sturobson/Sassifaction). It applies some very basic layout modifications when printing

##Mixins

###CSS3

This file contains many mixins that require vendor prefixes to achieve what have been dubbed as **css3**.

####bg-size

For specifying the background size.

Mixin:

	bg-size($size)

Usage:

	.class {
		@include bg-size(100%);
	}

Output:

	.class {
		-webkit-background-size: 100%; // Safari 3-4
		background-size: 100%; // Chrome, Firefox 4+, IE 9+, Opera, Safari 5+
	}

####border-radius-noclip && border-radius

The `noclip` mixin works the same as `border-radius` but without the background-clip declarations.

Mixin:

	border-radius($radius)
	border-radius-noclip($radius)

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

####gradient

Allows creation of background gradients without endless amounts of vendor prefixing. Can cater for horizontal, vertical or diagonal gradients. Radial gradients will need to be [manually generated](http://www.colorzilla.com/gradient-editor/)

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

Omitting output due to large amounts of code.

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

####transition-property && transition

This handles transitions and being able to override specific transition properties

Mixins:

	transition-property($attr, $value)
	transition($time: 0.5s, $attr: all, $effect: ease)

**$time**: How long the animation lasts

**$attr**: The attribute to affect (e.g. all, opacity, width)

**$effect**: What transition effect should be used. See the [W3C Working Draft](http://www.w3.org/TR/css3-transitions/#transition-timing-function-property) for all options.


Usage:

	.class {
		@include transition();
	}

	.context .class {
		@include transition-property(duration, 0.8s);
	}

Output:

	.class {
		-webkit-transition: 0.5s all ease;
		-moz-transition: 0.5s all ease;
		-o-transition: 0.5s all ease;
		transition: 0.5s all ease
	}

	.context .class {
		-webkit-transition-duration:0.8s;
		-moz-transition-duration:0.8s;
		-o-transition-duration:0.8s;
		transition-duration:0.8s
	}

####transform

Allowing transformations to be used easily

Mixin:

	transform($trans)

Usage:

	.class {
		@include transform(skew(35deg));
	}

Output:

	.class {
	  	-webkit-transform: skew(35deg);
		-moz-transform: skew(35deg);
		-ms-transform: skew(35deg);
		-o-transform: skew(35deg);
		transform: skew(35deg);
	}

##Predefined

Coming Soon