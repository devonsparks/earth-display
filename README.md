# Earth Display

## Context
This repository holds my Polymer port and enhancement of the [Stotz-Thornhill-Van Vleck-Eichin Earth Display](http://www.multicians.org/thvv/gcw.html). The Earth Display has a long and colorful history, dating back to a first implementation in [MAD](https://en.wikipedia.org/wiki/MAD_(programming_language)) on the [CTSS](https://en.wikipedia.org/wiki/Compatible_Time-Sharing_System). All of the data used to generate the land boundaries was digitized and entered by hand. Earth Display is a small program capturing powerful ideas in computer graphics. It deserves to be curated.

## Usage
The /src directory contains the reusable Polymer 2.0 element (`src/earth-display.html`) and an example use case (`src/index.html`). To get started quickly, place the /src directory behind a web server and navigate to index.html. If you have Python locally installed, try this from the project root:

```sh
cd src && python -m SimpleHTTPServer
```

The Earth Display element provides a number of useful properties:

| Property     | Description                                                   | Type           | Default         |
| -------------|---------------------------------------------------------------| ---------------|-----------------|
| `size`       | The height/width of the underlying HTML5 canvas in pixels.    | Number         | 500             |
| `lat`        | Starting latitude (degrees). + is North.                      | Number         | 0               |
| `lon`        | Starting longitude (degrees). + is East.                      | Number         | 0               |
| `rot`        | Starting rotation normal to the page (degrees).               | Number         | 0               |
| `background` | The base color behind the globe.                              | String         | 'white'         |
| `fill`       | Ocean and lang color.                                         | String         | 'blue'          |
| `stroke`     | Land mass outline color.                                      | String         | 'white'         |
| `title`      | The title for the underlying HTML5 canvas.                    | String         | 'Pale Blue Dot' |
| `animate`    | The [Δlat, Δlon, Δrot] to transform the globe on each frame.  | 3-length Array | null            |

A number of these are new to this port. Of special interest might be `animate`, which provides a fun but simple-minded extension to the original drawing behavior using `requestAnimationFrame`. There's plenty of room for improvement here.

![Earth Display](docs/globe.gif)

## Notes

In writing this port I've tried to strike a balance between maintaining the integrity of the original Javascript implementation (including general structure, source comments, and naming conventions) and refactoring to ease understanding and use on the modern web. In several cases I've removed unused variables, refactored code sections into functions, and tried to expose a practical WebComponent properties interface so Earth Display might find wider use. There are many more changes that *could* be made, but I've tried to remain faithful to the original as much as possible.

If you end up doing something fun with the Earth Display, drop me a line!

## Ideas for Extension
* The `animate` behavior is primitive. We're blindly recomputing every frame. Consider caching rendered frames by (lat, lon, rot) index or passing off to a WebWorker to generate the pixel array off-screen.
* The most interesting part of the Earth Display is the underlying data set. The digitized coordinates represent three dimensional points, so why not make a three dimensional model? Reuse of this data in a [THREE.js](https://threejs.org/)-based port would be a fun addition to the Earth Display evolutionary tree.
* Right now we're only drawing land boundaries. What if we want to fill them with another color? What will it take to get reasonable performance here?



