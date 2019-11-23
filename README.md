# Reveal.js setup with menu and toolbar


### Full setup


Step to install reveal js using npm

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

### Now i am going to add reveal.js menu by using npm commands

   1. Download and install the package in your project:
   ```sh
   $ npm install --save reveal.js-menu
   ```
2. Add the plugin to the dependencies in your presentation, as below.
   ```sh
   Reveal.initialize({
			// ...
	
			dependencies: [
			// ... 
	  
				{ src: 'node_modules/reveal.js-menu/menu.js' }
			]
		});
   ```
3. now you have to add theme stylesheet using this id="theme"
   ```sh
   <link rel="stylesheet" href="css/theme/black.css" id="theme">
   ```
4. if you want to change menu title then add below code in your section
   ```sh
   <section data-menu-title="Custom Menu Title"> ...</section>
   ```
### Now i am going to add reveal.js-toolbar using npm

1. Paste below code to your gitbash
   ```sh
   $  npm install --save reveal.js-toolbar
   ```
2. add below code to dependencies
   ```sh
   { src: 'node_modules/reveal.js-toolbar/toolbar.js' }
   ```
   
