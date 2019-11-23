# reveal.js [![Build Status](https://travis-ci.org/hakimel/reveal.js.svg?branch=master)](https://travis-ci.org/hakimel/reveal.js) <a href="https://slides.com?ref=github"><img src="https://s3.amazonaws.com/static.slid.es/images/slides-github-banner-320x40.png?1" alt="Slides" width="160" height="20"></a>


### Full setup

Some reveal.js features, like external Markdown and speaker notes, require that presentations run from a local web server. The following instructions will set up such a server as well as all of the development tasks needed to make edits to the reveal.js source code.

1. Install [Node.js](http://nodejs.org/) (4.0.0 or later)

1. Clone the reveal.js repository
   ```sh
   $ git clone https://github.com/hakimel/reveal.js.git
   ```

1. Navigate to the reveal.js folder
   ```sh
   $ cd reveal.js
   ```

1. Install dependencies
   ```sh
   $ npm install
   ```

1. Serve the presentation and monitor source files for changes
   ```sh
   $ npm start
   ```

1. Open <http://localhost:8000> to view your presentation

   You can change the port by using `npm start -- --port=8001`.

### Folder Structure

- **css/** Core styles without which the project does not function
- **js/** Like above but for JavaScript
- **plugin/** Components that have been developed as extensions to reveal.js
- **lib/** All other third party assets (JavaScript, CSS, fonts)


## Instructions

### Markup

Here's a barebones example of a fully working reveal.js presentation:
```html
<html>
	<head>
		<link rel="stylesheet" href="css/reveal.css">
		<link rel="stylesheet" href="css/theme/white.css">
	</head>
	<body>
		<div class="reveal">
			<div class="slides">
				<section>Slide 1</section>
				<section>Slide 2</section>
			</div>
		</div>
		<script src="js/reveal.js"></script>
		<script>
			Reveal.initialize();
		</script>
	</body>
</html>
```

The presentation markup hierarchy needs to be `.reveal > .slides > section` where the `section` represents one slide and can be repeated indefinitely. If you place multiple `section` elements inside of another `section` they will be shown as vertical slides. The first of the vertical slides is the "root" of the others (at the top), and will be included in the horizontal sequence. For example:

```html
<div class="reveal">
	<div class="slides">
		<section>Single Horizontal Slide</section>
		<section>
			<section>Vertical Slide 1</section>
			<section>Vertical Slide 2</section>
		</section>
	</div>
</div>
```


#### Iframe Backgrounds

Embeds a web page as a slide background that covers 100% of the reveal.js width and height. The iframe is in the background layer, behind your slides, and as such it's not possible to interact with it by default. To make your background interactive, you can add the `data-background-interactive` attribute.

```html
<section data-background-iframe="https://slides.com" data-background-interactive>
	<h2>Iframe</h2>
</section>
```

#### Background Transitions

Backgrounds transition using a fade animation by default. This can be changed to a linear sliding transition by passing `backgroundTransition: 'slide'` to the `Reveal.initialize()` call. Alternatively you can set `data-background-transition` on any section with a background to override that specific transition.


### Parallax Background

If you want to use a parallax scrolling background, set the first two properties below when initializing reveal.js (the other two are optional).

```javascript
Reveal.initialize({

	// Parallax background image
	parallaxBackgroundImage: '', // e.g. "https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg"

	// Parallax background size
	parallaxBackgroundSize: '', // CSS syntax, e.g. "2100px 900px" - currently only pixels are supported (don't use % or auto)

	// Number of pixels to move the parallax background per slide
	// - Calculated automatically unless specified
	// - Set to 0 to disable movement along an axis
	parallaxBackgroundHorizontal: 200,
	parallaxBackgroundVertical: 50

});
```

Make sure that the background size is much bigger than screen size to allow for some scrolling. [View example](http://revealjs.com/?parallaxBackgroundImage=https%3A%2F%2Fs3.amazonaws.com%2Fhakim-static%2Freveal-js%2Freveal-parallax-1.jpg&parallaxBackgroundSize=2100px%20900px).

### Slide Transitions

The global presentation transition is set using the `transition` config value. You can override the global transition for a specific slide by using the `data-transition` attribute:

```html
<section data-transition="zoom">
	<h2>This slide will override the presentation transition and zoom!</h2>
</section>

<section data-transition-speed="fast">
	<h2>Choose from three transition speeds: default, fast or slow!</h2>
</section>
```

You can also use different in and out transitions for the same slide:

```html
<section data-transition="slide">
    The train goes on …
</section>
<section data-transition="slide">
    and on …
</section>
<section data-transition="slide-in fade-out">
    and stops.
</section>
<section data-transition="fade-in slide-out">
    (Passengers entering and leaving)
</section>
<section data-transition="slide">
    And it starts again.
</section>
```
You can choose from `none`, `fade`, `slide`, `convex`, `concave` and `zoom`.
### Internal links

It's easy to link between slides. The first example below targets the index of another slide whereas the second targets a slide with an ID attribute (`<section id="some-slide">`):

```html
<a href="#/2/2">Link</a>
<a href="#/some-slide">Link</a>
```

You can also add relative navigation links, similar to the built in reveal.js controls, by appending one of the following classes on any element. Note that each element is automatically given an `enabled` class when it's a valid navigation route based on the current slide.

```html
<a href="#" class="navigate-left">
<a href="#" class="navigate-right">
<a href="#" class="navigate-up">
<a href="#" class="navigate-down">
<a href="#" class="navigate-prev"> <!-- Previous vertical or horizontal slide -->
<a href="#" class="navigate-next"> <!-- Next vertical or horizontal slide -->
```

### Fragments

Fragments are used to highlight individual elements on a slide. Every element with the class `fragment` will be stepped through before moving on to the next slide. Here's an example: http://revealjs.com/#/fragments

The default fragment style is to start out invisible and fade in. This style can be changed by appending a different class to the fragment:

```html
<section>
	<p class="fragment grow">grow</p>
	<p class="fragment shrink">shrink</p>
	<p class="fragment fade-out">fade-out</p>
	<p class="fragment fade-up">fade-up (also down, left and right!)</p>
	<p class="fragment fade-in-then-out">fades in, then out when we move to the next step</p>
	<p class="fragment fade-in-then-semi-out">fades in, then obfuscate when we move to the next step</p>
	<p class="fragment highlight-current-blue">blue only once</p>
	<p class="fragment highlight-red">highlight-red</p>
	<p class="fragment highlight-green">highlight-green</p>
	<p class="fragment highlight-blue">highlight-blue</p>
</section>
```

Multiple fragments can be applied to the same element sequentially by wrapping it, this will fade in the text on the first step and fade it back out on the second.

```html
<section>
	<span class="fragment fade-in">
		<span class="fragment fade-out">I'll fade in, then out</span>
	</span>
</section>
```

The display order of fragments can be controlled using the `data-fragment-index` attribute.

```html
<section>
	<p class="fragment" data-fragment-index="3">Appears last</p>
	<p class="fragment" data-fragment-index="1">Appears first</p>
	<p class="fragment" data-fragment-index="2">Appears second</p>
</section>
```

### Fragment events

When a slide fragment is either shown or hidden reveal.js will dispatch an event.

Some libraries, like MathJax (see #505), get confused by the initially hidden fragment elements. Often times this can be fixed by calling their update or render function from this callback.

```javascript
Reveal.addEventListener( 'fragmentshown', function( event ) {
	// event.fragment = the fragment DOM element
} );
Reveal.addEventListener( 'fragmenthidden', function( event ) {
	// event.fragment = the fragment DOM element
} );
```

### Code Syntax Highlighting

By default, Reveal is configured with [highlight.js](https://highlightjs.org/) for code syntax highlighting. To enable syntax highlighting, you'll have to load the highlight plugin ([plugin/highlight/highlight.js](plugin/highlight/highlight.js)) and a highlight.js CSS theme (Reveal comes packaged with the Monokai themes: [lib/css/monokai.css](lib/css/monokai.css)).

```javascript
Reveal.initialize({
	// More info https://github.com/hakimel/reveal.js#dependencies
	dependencies: [
		{ src: 'plugin/highlight/highlight.js', async: true },
	]
});
```

Below is an example with clojure code that will be syntax highlighted. When the `data-trim` attribute is present, surrounding whitespace is automatically removed.  HTML will be escaped by default. To avoid this, for example if you are using `<mark>` to call out a line of code, add the `data-noescape` attribute to the `<code>` element.

```html
<section>
	<pre><code data-trim data-noescape>
(def lazy-fib
  (concat
   [0 1]
   <mark>((fn rfib [a b]</mark>
        (lazy-cons (+ a b) (rfib b (+ a b)))) 0 1)))
	</code></pre>
</section>
```

#### Line Numbers & Highlights

To enable line numbers, add `data-line-numbers` to your `<code>` tags. If you want to highlight specific lines you can provide a comma separated list of line numbers using the same attribute. For example, in the following example lines 4 and 8-11 are highlighted:

```html
<pre><code class="hljs" data-line-numbers="4,8-11">
import React, { useState } from 'react';
 
function Example() {
  const [count, setCount] = useState(0);
 
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
</code></pre>
```

<img width="300" alt="line-numbers" src="https://user-images.githubusercontent.com/629429/55332077-eb3c4780-5494-11e9-8854-ba33cd0fa740.png">



### Slide number

If you would like to display the page number of the current slide you can do so using the `slideNumber` and `showSlideNumber` configuration values.

```javascript
// Shows the slide number using default formatting
Reveal.configure({ slideNumber: true });

// Slide number formatting can be configured using these variables:
//  "h.v": 	horizontal . vertical slide number (default)
//  "h/v": 	horizontal / vertical slide number
//    "c": 	flattened slide number
//  "c/t": 	flattened slide number / total slides
Reveal.configure({ slideNumber: 'c/t' });

// You can provide a function to fully customize the number:
Reveal.configure({ slideNumber: function() {
    // Ignore numbering of vertical slides
    return [ Reveal.getIndices().h ];
}});

// Control which views the slide number displays on using the "showSlideNumber" value:
//     "all": show on all views (default)
// "speaker": only show slide numbers on speaker notes view
//   "print": only show slide numbers when printing to PDF
Reveal.configure({ showSlideNumber: 'speaker' });
```

## Theming

The framework comes with a few different themes included:

- black: Black background, white text, blue links (default theme)
- white: White background, black text, blue links
- league: Gray background, white text, blue links (default theme for reveal.js < 3.0.0)
- beige: Beige background, dark text, brown links
- sky: Blue background, thin dark text, blue links
- night: Black background, thick white text, orange links
- serif: Cappuccino background, gray text, brown links
- simple: White background, black text, blue links
- solarized: Cream-colored background, dark green text, blue links

Each theme is available as a separate stylesheet. To change theme you will need to replace **black** below with your desired theme name in index.html:

```html
<link rel="stylesheet" href="css/theme/black.css" id="theme">
```

If you want to add a theme of your own see the instructions here: [/css/theme/README.md](https://github.com/hakimel/reveal.js/blob/master/css/theme/README.md).


## Speaker Notes

reveal.js comes with a speaker notes plugin which can be used to present per-slide notes in a separate browser window. The notes window also gives you a preview of the next upcoming slide so it may be helpful even if you haven't written any notes. Press the »S« key on your keyboard to open the notes window.

A speaker timer starts as soon as the speaker view is opened. You can reset it to 00:00:00 at any time by simply clicking/tapping on it.

Notes are defined by appending an `<aside>` element to a slide as seen below. You can add the `data-markdown` attribute to the aside element if you prefer writing notes using Markdown.

Alternatively you can add your notes in a `data-notes` attribute on the slide. Like `<section data-notes="Something important"></section>`.

When used locally, this feature requires that reveal.js [runs from a local web server](#full-setup).

```html
<section>
	<h2>Some Slide</h2>

	<aside class="notes">
		Oh hey, these are some notes. They'll be hidden in your presentation, but you can see them if you open the speaker notes window (hit »S« on your keyboard).
	</aside>
</section>
```

If you're using the external Markdown plugin, you can add notes with the help of a special delimiter:

```html
<section data-markdown="example.md" data-separator="^\n\n\n" data-separator-vertical="^\n\n" data-separator-notes="^Note:"></section>

# Title
## Sub-title

Here is some content...

Note:
This will only display in the notes window.
```

#### Share and Print Speaker Notes

Notes are only visible to the speaker inside of the speaker view. If you wish to share your notes with others you can initialize reveal.js with the `showNotes` configuration value set to `true`. Notes will appear along the bottom of the presentations.

When `showNotes` is enabled notes are also included when you [export to PDF](https://github.com/hakimel/reveal.js#pdf-export). By default, notes are printed in a box on top of the slide. If you'd rather print them on a separate page, after the slide, set `showNotes: "separate-page"`.

#### Speaker notes clock and timers

The speaker notes window will also show:

- Time elapsed since the beginning of the presentation.  If you hover the mouse above this section, a timer reset button will appear.
- Current wall-clock time
- (Optionally) a pacing timer which indicates whether the current pace of the presentation is on track for the right timing (shown in green), and if not, whether the presenter should speed up (shown in red) or has the luxury of slowing down (blue).

The pacing timer can be enabled by configuring by the `defaultTiming` parameter in the `Reveal` configuration block, which specifies the number of seconds per slide.  120 can be a reasonable rule of thumb.  Timings can also be given per slide `<section>` by setting the `data-timing` attribute.  Both values are in numbers of seconds.


## Server Side Speaker Notes

In some cases it can be desirable to run notes on a separate device from the one you're presenting on. The Node.js-based notes plugin lets you do this using the same note definitions as its client side counterpart. Include the required scripts by adding the following dependencies:

```javascript
Reveal.initialize({
	// ...

	dependencies: [
		{ src: 'socket.io/socket.io.js', async: true },
		{ src: 'plugin/notes-server/client.js', async: true }
	]
});
```

Then:

1. Install [Node.js](http://nodejs.org/) (4.0.0 or later)
2. Run `npm install`
3. Run `node plugin/notes-server`


## Plugins

Plugins should register themselves with reveal.js by calling `Reveal.registerPlugin( 'myPluginID', MyPlugin )`. Registered plugin instances can optionally expose an "init" function that reveal.js will call to initialize them.

When reveal.js is booted up via `Reveal.initialize()`, it will go through all registered plugins and invoke their "init" methods. If the "init" method returns a Promise, reveal.js will wait for that promise to be fullfilled before finshing the startup sequence and firing the [ready](#ready-event) event. Here's an example of a plugin that does some asynchronous work before reveal.js can proceed:

```javascript
let MyPlugin = {
	init: () =>  new Promise( resolve => setTimeout( resolve, 3000 ) )
};
Reveal.registerPlugin( 'myPlugin', MyPlugin );
Reveal.addEventListener( 'ready', () => console.log( 'Three seconds later...' ) );
Reveal.initialize();
```

If the init method does _not_ return a Promise, the plugin is considered ready right away and will not hold up the reveal.js startup sequence.

### Retrieving Plugins

If you want to check if a specific plugin is registered you can use the `Reveal.hasPlugin` method and pass in a plugin ID, for example: `Reveal.hasPlugin( 'myPlugin' )`. If you want to retrieve a plugin instance you can use `Reveal.getPlugin( 'myPlugin' )`.


## Multiplexing

The multiplex plugin allows your audience to view the slides of the presentation you are controlling on their own phone, tablet or laptop. As the master presentation navigates the slides, all client presentations will update in real time. See a demo at [https://reveal-js-multiplex-ccjbegmaii.now.sh/](https://reveal-js-multiplex-ccjbegmaii.now.sh/).

The multiplex plugin needs the following 3 things to operate:

1. Master presentation that has control
2. Client presentations that follow the master
3. Socket.io server to broadcast events from the master to the clients


## License

MIT licensed

Copyright (C) 2019 Hakim El Hattab, http://hakim.se
