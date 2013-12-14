#Luigi

Luigi is the Scss library developed by the developers at Bozboz and the rest of the world. It takes influence from the most popular of libraries and includes most of the popular mixins, plus some extra Bozboz crafted ones.

All mixins are included into the main `_luigi.scss`. This is so in your `app.scss` or `style.scss` you can just include '_luigi.scss' to benefit from the whole shebang.

**Luigi** is laid out in 3 folders - **helpers**, **mixins** and **predefined**.

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
