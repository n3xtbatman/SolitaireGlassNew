# Solitaire

To play the games, visit the [live version](https://oddstream.games/Solitaire).

For user-oriented information, please see the [FAQ](https://oddstream.droppages.com/faq.html).

## Implementation

Written in [vanilla ES2017 Javascript](http://vanilla-js.com/),
formatted as per the [Google style rules](https://google.github.io/styleguide/jsguide.html)
with [JSDoc](http://usejsdoc.org/) annotations to try to keep the Visual Studio Code type checker quiet.
 
Implemented as a small hierarchy of classes;
a Card class and a Card Container class, with classes derived from that for Stock, Waste, Foundation, Tableau &c.
Some specialized containers, for example a Freecell tableau, get derived

Each variant has it's own html file which contains layout information for each container and
gameplay rules for that variant. The html file consists of boilerplate header and footers,
wrapped at build time around a central guts file and some SVG symbols. The build script (bake.tcl)
requires Tcl to be installed and is hardwired to my folder configuration.

At run time, the layout information in the html is linked to the Javascript card container classes.

The graphics are implemented in SVG, so they scale smoothly.

Time has been spent making it compatible with both mobile and desktop versions of Chrome, Firefox and Edge. I think it runs *The Best* on a touchscreen Chromebook.

## Philosophy

Keep it simple and facilitate the player's flow. So: no distracting graphics or animations, make the cards easy to scan visually, and no unnecessary features.

Also, make the games authentic, by taking the rules from reputable sources and implementing them exactly.

## Known problems

- Redeals and scorpion/spider symbols not displaying on a Chromebook. There's an open issue on the chromium tracker that relates: https://bugs.chromium.org/p/chromium/issues/detail?id=914919

- Cards sometimes don't animate, so the card is displayed where it started, but the software thinks it's somewhere else. Can be cleared by reloading the page. May be linked to grabbing a moving card?

- Dragging cards goes through phases of being unreliable, as browsers get updated. It's caused when the user agent sends an unwanted pointercancel event. It's currently fixed by having dummy touch start/move/end listeners so all the touch events get ignored.

## Tcl

Without doubt, the greatest programming language I have encountered in forty+ years of doing this nonsense.
I could either reimplement the whole thing in Tcl/Tk (which would make it very non-deployable)
or keep just using Tcl for prototyping stuff and build scripts.

## Forth

An idea I keep kicking around is to implement a small Forth engine, with small scripts for each variant.
Solitaire is all about managing stacks of cards, so the stack-metaphor or Forth ought to
work well.
