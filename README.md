# The Basic Brockmann
A super basic grid framework based off of [Steve Hickey](http://stevehickeydesign.com/)'s own [flexible grid](http://www.slideshare.net/stevehickeydsgn/forget-frameworks-create-your-own-flexible-grid-system). Personally I love [Susy](http://susy.oddbird.net/), but it’s currently tied to the featureset of SASS 3.3+, which [Libsass](https://github.com/sass/libsass) hasn’t yet caught up to. On a recent project I found compiling all my partial files took upwards of 5 seconds. Not wanting to have to add a bunch of compiled partial CSS files to my development site (and then strip them out for production) I switched compilers.

Unfortunately this necessitated the need for a new (basic) grid system. Unlike Susy it doesn’t (yet?) do the initial math for column and gutter percentages. What it does allow me to do is get up and running with a basic layout quickly and easily, and allow me to make use of Libsass without going back to v1 of [Neat](http://neat.bourbon.io/).

Currently setup involves declaring the following variables ahead of time:

    $max-width: 1360px;
    $column-width: 6.38298%;
    $gutter-width: 2.12766%;
    $maximum-columns: 12;
