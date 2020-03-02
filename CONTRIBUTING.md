# Contributing

## Project organisation

````
minuit
├── assets // theme fonts
├── dist // compiled css
├── src // Source less files
└── styles.css.php // main css used by jirafeau
````

All the project files are located inside the `src` folder and it is structured as follow.

````
src
├── style.less // main file
├── lib
│   ├── config.less // theme configurations
│   ├── colors.less // theme colors
│   ├── icons.less // theme icons
│   └── animations.less // progess animation
├── components
│   ├── core.less // elements common to all pages
│   └── components.less // button, inputs, error elements.
├── pages
│   ├── admin.less
│   ├── delete.less
│   ├── download.less
│   ├── error.less
│   ├── finished.less
│   ├── login.less
│   ├── progress.less
│   ├── protected-download.less
│   ├── script.less
│   └── upload.less
└── coeur-de-fer // less Framework and mixins.
````

## Icons

The project used [Icomoon](https://icomoon.io/) to gather icons and budle them in a minified font. The icons selections can be re-uploaded to [Icomoon](https://icomoon.io/) using the file `/assets/fonts/selection.json`.
