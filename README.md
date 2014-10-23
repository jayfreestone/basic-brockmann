# The Basic Brockmann
A super basic grid framework based off of [Steve Hickey](http://stevehickeydesign.com/)'s own [flexible grid](http://www.slideshare.net/stevehickeydsgn/forget-frameworks-create-your-own-flexible-grid-system). Personally I love [Susy](http://susy.oddbird.net/), but it’s currently tied to the featureset of SASS 3.3+, which [Libsass](https://github.com/sass/libsass) hasn’t yet caught up to. On a recent project I found compiling all my partial files took upwards of 5 seconds. Not wanting to have to add a bunch of compiled partial CSS files to my development site (and then strip them out for production) I switched compilers.

Unfortunately this necessitated the need for a new (basic) grid system. Unlike Susy it doesn’t (yet?) do the initial math for column and gutter percentages. What it does allow me to do is get up and running with a basic layout quickly and easily, and allow me to make use of Libsass without going back to v1 of [Neat](http://neat.bourbon.io/).

Currently setup involves declaring the following variables ahead of time:

    $max-width: 1360px;
    $column-width: 6.38298%;
    $gutter-width: 2.12766%;
    $maximum-columns: 12;

## Setup

Include `_grid.scss` & `_mixins.scss` in your project, then declare these variables in a preceding file:

	$max-width: 1360px;
	$column-width: 6.38298%;
	$gutter-width: 2.12766%;
	$maximum-columns: 12;

## Usage

Define the main container with the `%container` placeholder:

	.container {
	 @extend %container;
	}

Then define the widths of elements with the `col` mixin:

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

Currently when passing in the `omega` flag the parent needs to be declared, ensuing `omega` is the last option passed into the mixin. This would, for instance, not be valid: `@include col(2, omega)`.