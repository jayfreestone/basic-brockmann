# The Basic Brockmann

A super basic grid framework based off of [Steve Hickey](http://stevehickeydesign.com/)'s own [flexible grid](http://www.slideshare.net/stevehickeydsgn/forget-frameworks-create-your-own-flexible-grid-system). Personally I love [Susy](http://susy.oddbird.net/), but it’s currently tied to the featureset of SASS 3.3+, which [Libsass](https://github.com/sass/libsass) hasn’t yet caught up to. On a recent project I found compiling all my partial files took upwards of 5 seconds. Not wanting to have to add a bunch of compiled partial CSS files to my development site (and then strip them out for production) I switched compilers.

Unfortunately this necessitated the need for a new (basic) grid system. Unlike Susy it doesn’t (yet?) do the initial math for column and gutter percentages. What it does allow me to do is get up and running with a basic layout quickly and easily, and allow me to make use of Libsass without going back to v1 of [Neat](http://neat.bourbon.io/).

## Install
You can [download Brockmann here](https://github.com/jayfreestone/basic-brockmann/archive/master.zip), or [clone the repo](https://github.com/jayfreestone/basic-brockmann).
Alternatively you can install it using [Bower](http://bower.io):

	bower install the-basic-brockmann

## Setup
Include `_grid.scss` & `_mixins.scss` in your project, then declare these variables in a preceding file (the values are examples).

	$max-width: 1360px;
	$column-width: 6.38298%;
	$gutter-width: 2.12766%;
	$maximum-columns: 12;

## Usage
Define the main container with the `%container` placeholder.

	.container {
		@extend %container;
	}

Then define the widths of elements with the `col` mixin.

	main {
	 	@include col(8);
	}

By default `col` will assume the parent element contains the maximum number of columns specified in `$maximum-columns` — in this example 12. If you are nesting elements and wish to instead declare how many columns the parent has you may pass in a second number:

	aside {
		@include col(2, 6);
	}

This translates to: ‘span two of six columns’.

The final column in a row must be declared by passing in the `omega` flag, or optionally using the `omega` mixin:

	aside {
		@include col(2, 6, omega);
	}
	
	// Or:
	
	aside {
		@include col(2, 6);
		@include omega;
	}

The first is preferable as it avoids outputting CSS that will be rewritten.

Currently when passing in the `omega` flag the parent needs to be declared, ensuring `omega` is the last option passed into the mixin. This, for instance, would be invalid: `@include col(2, omega)`.

The `omega` syntax can also take a third option: `none`. This outputs the width and margins without the floats (there is 'no' float). This is useful when collapsable margins are desirable, for instance when styling elements within an article body.

You can break the flow with the `push` mixin.

	@include push(left, 1);

The example above will ‘push’ the element one column from the left  to the right, essentially adding a left margin equivalent to one column and gutter.

## FAQ

### How do I work out the % values?
You’re currently on your own here. At the moment Brockmann doesn’t handle the original grid calculations. There are, however, a bunch of grid calculators out there, including [Gridset](https://gridsetapp.com).

### How can I change the grid at various breakpoints?
You can wrap your styles in a simple media query mixin: 

	@mixin breakpoint($breakpoint) {
		@media only screen and (min-width: $breakpoint) { @content; }
	}  

And then just redeclare the `col` mixin when needed:

	.intro{
		@include col(1, 1, omega);
	
 		@include breakpoint(43.750em){
			@include col(1, 2, omega);
  		}
	  
		@include breakpoint(62.500em){
			@include col(2, 4, omega);
	  	}
	}

### Asymmetry?
Not yet, although this is something I’m interested in exploring.

### Why should I use Brockmann?
Because you’re using Libsass, which (at the time of writing) rules out the two well established SASS based grid systems, [Susy](http://susy.oddbird.net) and [Neat](http://neat.bourbon.io). Brockmann is designed to be *super* lightweight and incredibly easy to understand. It’s not a comprehensive system. It’s a set of transparent and reusable mixins that let you built out a pre-conceived grid quickly.