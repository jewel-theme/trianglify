# Trianglify

[![Dependency Status](https://david-dm.org/qrohlf/trianglify.svg)](https://david-dm.org/qrohlf/trianglify) [![Build Status](https://travis-ci.org/qrohlf/trianglify.svg?branch=master)](https://travis-ci.org/qrohlf/trianglify)

Trianglify is a library that I wrote to generate nice SVG background images like this one:

![](examples/example1.jpg)

It was inspired by [btmills/geopattern](https://github.com/btmills/geopattern), and uses [d3.js](http://d3js.org) to build the polygons and SVG and SVG filters for rendering. It also includes the [colorbrewer](http://bl.ocks.org/mbostock/5577023) color palette library to get you up and running quickly. The initial version was written in a single day because I got fed up with Adobe Illustrator.

# Demo

**Official:**
http://qrohlf.com/trianglify

**More:**
- [@nixterrimus](https://github.com/nixterrimus) has a nice demo app that lets you modify the parameters and choose between the built-in color palettes: [link](http://nixterrimus.github.io/Triangle-Play-App/) ([source](https://github.com/nixterrimus/Triangle-Play-App))
- [@alssndro](https://github.com/alssndro) put together a version that lets you choose from the top ColourLovers palettes: [link](http://alssndro.github.io/trianglify-background-generator/) ([source](https://github.com/alssndro/trianglify-background-generator))

# Getting Trianglify
The recommended way to use Trianglify is via Bower:

```bash
bower install trianglify
```

Or if you're using nodejs

```bash
npm install trianglify
```

Alternately, you can load it via [CDNJS](http://cdnjs.com/libraries/trianglify), download the latest version as a [zip archive](https://github.com/qrohlf/trianglify/archive/master.zip), or simply clone this repo.

# Usage

Include d3 and `trianglify.js` or `trianglify.min.js` on your page:

```html
<script src="http://d3js.org/d3.v3.min.js"></script>
<script src="trianglify.js"></script>
```

Create a new Trianglify instance and use it to generate patterns:

```javascript
var t = new Trianglify();
var pattern = t.generate(800, 600); // svg width, height
pattern.svg         // SVG DOM Node object
pattern.svgString   // String representation of the svg element
pattern.base64      // Base64 representation of the svg element
pattern.dataUri     // data-uri string
pattern.dataUrl     // data-uri string wrapped in url() for use in css
pattern.append()    // append pattern to <body>. Useful for testing.
```

For example, to generate a background for `<body>` and apply it with inline CSS:

```javascript
var t = new Trianglify();
var pattern = t.generate(document.body.clientWidth, document.body.clientHeight);
document.body.setAttribute('style', 'background-image: '+pattern.dataUrl);
```

# Colors
a list of all the available colorbrewer palettes available can be found [here](http://bl.ocks.org/mbostock/5577023), or you can [specify your own](#options)

# Contributing

Pull Requests and Issues are welcome! Please make sure to read the [contributing guidelines](CONTRIBUTING.md), though.


# Examples

*you can try out all of the below examples in your dev console on the [demo page](http://qrohlf.com/trianglify/)*

## Basic Usage

```
window.open(new Trianglify({
    x_gradient: Trianglify.colorbrewer.PuOr[9],
    noiseIntensity: 0,
    cellsize: 90}).generate(700, 400).dataUri)
```

![](examples/example1.jpg)


## Differing x and y gradients

```
window.open(new Trianglify({
    x_gradient: Trianglify.colorbrewer.YlGnBu[9],
    y_gradient: Trianglify.colorbrewer.RdPu[9],
    noiseIntensity: 0.1,
    cellpadding: 10,
    cellsize: 100}).generate(700, 400).dataUri);
```

![](examples/example2.jpg)


## Cellpadding Close to cellsize/2

```
window.open(new Trianglify({
    cellpadding: 80,
    cellsize: 200}).generate(700, 400).dataUri)
```

![](examples/example3.jpg)


# Options

The constructor takes an optional options object where you can override the default values for Trianglify like so:

```
var t = new Trianglify({cellsize: 100, bleed: 150, ...});
```

The following configuration options are available:

option | usage | valid | default
--- | --- | --- | ---
cellsize | set how large the generated cells should be | integers > 0 | 150
bleed | set how far outside the visible area of the SVG points should be rendered | integers > 0 | cellsize
cellpadding | set the minimum distance between each point | integers > 0 and < cellsize/2 | cellsize*0.1
noiseIntensity | set the opacity of the noise filter. This has a significant impact on SVG rendering time - set to 0 to disable. | 0 to 1 | 0
x_gradient | an array of colors to use to construct a gradient for the x-axis | array of colors in hexadecimal string format (i.e. `["#961E00", "#FF0000", "#EEEEEE"]`) | random selection from colorbrewer palettes
y_gradient | an array of colors to use to construct a gradient for the y-axis | array of colors in hexadecimal string format (i.e. `["#961E00", "#FF0000", "#EEEEEE"]`) | x_gradient, brightened by a factor of 0.5
fillOpacity | sets the opacity of the inside of the cells | 0 to 1 | 1
strokeOpacity | sets the opacity of the outline of the cells | 0 to 1 | 1

# License

Trianglify is licensed under the GPLv3 License. Happy hacking!

# Credits
- Trianglify makes use of the excellent [d3.js](https://github.com/mbostock/d3) visualization library by Michael Bostock.
- Trianglify includes color specifications and designs developed by Cynthia Brewer (http://colorbrewer.org/).
- Trianglify uses the excellent (and free!) [GitHub Pages](https://pages.github.com) for hosting.
