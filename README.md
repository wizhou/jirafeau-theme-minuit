# Jirafeau Minuit Theme

This is a theme for [Jirafeau](https://gitlab.com/mojo42/Jirafeau), an Open-Source software that allow to easily upload files and share them with a link.

The theme is **dark and minty**, and designed to give the software a *modern look*. It's written in LESS and can be simply modified according to your needs.

![Jirafeau upload page with minuit theme](https://minuit-collectif.com/screenshots/share/upload_finished.png)

## Screenshots

- [Login](https://minuit-collectif.com/screenshots/share/login.png)
- [Admin interface](https://minuit-collectif.com/screenshots/share/admin.png)
- [Admin files list](https://minuit-collectif.com/screenshots/share/list-file.png)
- [Upload](https://minuit-collectif.com/screenshots/share/upload.png)
- [Upload progess](https://minuit-collectif.com/screenshots/share/progress.png)
- [Download file](https://minuit-collectif.com/screenshots/share/download.png)
- [Password download file](https://minuit-collectif.com/screenshots/share/password-protected.png)
- [Delete file](https://minuit-collectif.com/screenshots/share/delete.png)

## Main features

- **Simple** and **modern** look
- Distinctive **colors**
- Is *responsive* and works both on **desktop** and **mobile***
- Can easily be **improved** or **modified**
- Use the beautiful **icons** from [Feather](https://feathericons.com/) to be more friendly and appealing.
- Display text and information with **distinction and readability** thanks to the [IBM Plex Mono](https://github.com/IBM/plex/tree/v4.0.2) font.

\* *Read the [configuration](#enable-mobile-compatibility) section to enable compatibility to mobile.*

## Requirements

You will need a working installation of **Jirafeau** to use the theme. It's quite simple and all is explained in the [Jirafeau documentation](https://gitlab.com/mojo42/Jirafeau#installation).

- **System requirements** are the same as for the Jirafeau software.
- The theme uses **CSS3**.
- The theme uses **web-fonts**
- Work on all modern browsers that support the **CSS Flexible Box Layout Module** — all are listed in the [Can I use](https://caniuse.com/#feat=flexbox) website.

The theme come already built as a CSS file, but you can re-compile it with any LESS compiler. More information about compiling in the [Building](#building) section.

## Installation

You can either **download** and install manually, or **clone** this repository to `media/minuit` of your Jirafeau installation.

````
cd <your jirafeau path>
git clone https://github.com/wizhou/jirafeau-theme-minuit.git media/minuit
````

Once this is done, go to `lib/config.local.php` and change the following lines:

````
$cfg = array (
	// ...
	'style' => 'minuit',
````

Then, **Jirafeau** will automatically link the theme file `style.css.php` as the main stylesheet of your installation.

### For developpement / Configuration

Note that the theme use the slim Less Library [Coeur-de-fer]https://github.com/wizhou/coeur-de-fer) as a **submodule**. It is not needed if you only use the theme as it in Jirafeau, but it will be if you want to configure or modify the theme.

The fastest way to get the library is to tell git to load the submodule when cloning the project.

````
cd <your jirafeau path>
git clone --recurse-submodules https://github.com/wizhou/jirafeau-theme-minuit.git media/minuit
````

If you have already cloned the project and want to load the submodule, you must run two commands:

````
cd <your jirafeau path>/media/minuit
git submodule init
git submodule update
````

This will tell git to initialize your local configuration file, fetch all the data from **Coeur-de-fer** and check out the appropriate commit listed in the project.


## Configuration

The theme can be configured in multiples ways, either to revise it's look or to enable different features.

Most of the theme base elements, **units**, **colors** and **font**, are declared as **LESS variables** inside `src/lib/config.less`. You may modify any of them to make the theme look as you wish, and the file is commented that way.

You will need to compile the **LESS file** `src/style.less` into a **CSS file** to make the changes append. Any LESS compiler can be used to do so, but the end file must be placed and named as follow: `dist/style.css`. You can obtain more informations about compiling in the [Building](#building) section.

### Enable mobile compatibility

The theme uses *responsive web design* and work well in mobile or tablet displays. However, **Jirafeau** is not configured to be usable on phone by default and lack a `viewport` configuration. You must enable it by yourself.

To do so, go to `lib/template/header.php` of your **Jirafeau** installation and add this line just below the `<head>` opening tag.

````
<?php /* Add this line to enable mobile use! */ ?>
<meta name="viewport" content="width=device-width, initial-scale=1">
````

### Hide / Show File max size
If you don't use any **upload size limitations** in your Jirafeau installation, you can hide its text row by setting the following variable to `false` inside `src/lib/config.less`.

````
@show-config-max-upload-size: false;
````

### Change font

**Minuit** theme uses [IBM Plex Mono](https://github.com/IBM/plex/tree/v4.0.2) font in *regular* and *bold* to display texts. The font is installed in `assets` folder and linked inside `style.css.php` file.

There are two ways you can add a new font to the theme:

#### Hosted font

You can import any **hosted font** you like by loading it's stylesheet directly inside the `style.css.php` file.

First, remove the link of the theme font:

````
require_once __DIR__ . '/assets/ibm-plex-mono.css';
````

Then, add this line after the php closings.

````
<?php … ?>
@import url('<my-web-font-url>');
````

After this, go to `src/lib/config.less` and change the value of the following variable to the name of your font.

`````
@font-family: '<My web font>';
`````

Then, re-compile the **LESS** file `src/style.less` into the CSS file `dist/style.css`.

#### Installed font

You can **install** a font on your own installation by following a few extra steps:

- **Download** a font, preferably an open source one, or any you bought and wish to use. You can find some on [Velvetyne](http://www.velvetyne.fr/) website, [Open Font Library](https://fontlibrary.org/en/font/avara), or even [Google Fonts](https://fonts.google.com/).
- Either the font already come with a **bundle** for web use, or you will need to build your own if the fonts allow you to (check its *license* to know). You can use any [Web-font Generator](https://duckduckgo.com/?q=webfont+generator&ia=web) you want.
- Locate the font inside `assets` folder. To keep it simple, you can name the folder containing the font's files with the name of the font, like this: `assets/my-web-font`.
- Your bundle might have come with a **CSS file** linking your font with a `@font-face` declaration, if not, you will need to make your own. Here is an [article from CSS Tricks](https://css-tricks.com/snippets/css/using-font-face/) explaining how. Te be consistent with the font's folder name, you can name this file `my-web-font.css` and locate it in `assets` folder. Inside the `@font-face` declaration, the paths to your font's files will then have to look like this:
````
src: url('assets/<my-web-font>/<my-web-font>.woff'),
````
- Then, go to `style.css.php` and change the **path** of the following line to the **location** of your font CSS file:
````
// From
require_once __DIR__ . '/assets/ibm-plex-mono.css';
// To
require_once __DIR__ . '/assets/<my-web-font>.css';
````
- After this, go to `src/lib/config.less` and change the value of the `@font-family` **variable** to the name of your font.

	`````
	@font-family: '<My web font>';
	`````

- Finally, compile the **LESS** file `src/style.less` into the CSS file `dist/style.css`.

### Change colors

**Minuit** theme uses green and blue colors defined as **LESS variables**. If you wish to change the colors of the theme, you can do so in the file `src/lib/colors.less`

The green colors are defined as `@primary-` variables, and the blue colors are defined as `@secondary-` variables.

The **variables** are organized with like this:

````
@primary-majeure: Strong main color.
@primary-mediante: Regular color
@primary-sensible: Light color, for borders and hover
@primary-mineure: Extra-Light color, for backgrounds
````

You may play with these definitions. Right now there is still a lot of hardcoded base colors. In a future release, there will be more use of LESS color channel functions to allow quicker and smoother modifying of theme colors.

## Building

**Minuit** theme is written in [Less](http://lesscss.org/) in 3.11.1. It uses [Parcel](https://parceljs.org/) as a compiler and a **CSS** minifier, and [npm](https://www.npmjs.com/) to make it run. However, this setup is more a comfort than a need for the project. You can use any LESS compiler you like to build the theme.

The theme also use the slim LESS library [coeur-de-fer](https://github.com/wizhou/coeur-de-fer), with helpers functions and vendors support mixins, as well as a browser reset sheet. It's included as submodule of the project. You will need to load the submodule in order to build the theme. Steps to do so are explained in the [Intstallation](#for-developpement--configuration) section.

### With npm and Parcel

First, install **npm** and **parcel** if you haven't already. To install npm, you first need to install **node** using the node.js [installer](https://nodejs.org/en/), npm is installed as a part of it.

Then, you can make sure you have the most recent version of npm by using npm:
````
npm install npm -g
````

Then, install Parcel with npm:
````
npm install -g parcel-bundler
````

When both are installed, you can go to `minuit` folder and run the following commands to compile the project

Go to the theme in your **jirafeau** installation:
````
cd <path-to-your-jirafeau>/media/minuit
````
If for dev, use this command to ask **Parcel** to `watch` the project.
````
npm run dev
````
Then, to ask **Parcel** to `build` the theme as a minified CSS file, run this command:
````
npm run build
````
**Parcel** will take care to output the complied CSS file to the right place. It will also produce **source maps** by default, allowing an easy debugging and workflow.

By the way, **Parcel** configurations can be found inside `package.json`.

****

### Build with Less.js

You can also build the theme directly with [Less.js](http://lesscss.org/usage/), and do not need anything else.

First install **less.js** with **npm**
````
npm install less -g
````
Then go to the theme folder in you **Jirafeau** installation and run the following command to tell less to build the theme.

````
cd <path-to-your-jirafeau>/media/minuit
lessc src/style.less dist/style.css
````

If you choose this solution, you will need to find a CSS minifier as it don't come natively with less.js.

### Build with a text editor
You can also build the project with any text editor plugin that compile LESS. However, you will be in charge of placing the compiled CSS file inside its folder as follow: `/dist/style.css`.

## Contributing

Contributing is appreciated, and the theme can be improved in many ways. Please refer to `CONTRIBUTING.md` for more details.


### To do:
- The installation wizard is not yet supported.
- Clean the color composition and allow faster color changing.
- Regroup some `media queries` declarations.
- Gather similars declarations into `:extend()` to minify the file size.
- Make a favicon
- Insert the jirafeau logo inside the footer


## Help

This theme has been tested in latest versions of **Chrome**, **Firefox**, **Opera** and **Safari**, and **Chrome Android**, but not in Edge nor Safari iOS, but it should work on them.

If you find any bug, or if something feels quirky, or if you have any question, please **open an issue** on the project.

This theme doesn't change anything to **Jirafeau** software (outside of the mobile configuration explained above), so if you encounter any bug while using the software, please refer to [Jirafeau documentation](https://gitlab.com/mojo42/Jirafeau).

### Known bugs

- The **login page** use `focus` and `z-index` layers to hide the label when the user is typing a password. However, if the text input loose focus, the label re-appear over the input and can be confusing. It's actually quite hard to counter this behavior with only css and because of the way **Jirafeau** is builded.


## Credits

2020 - Wizhou / [Romain Gœtz](https://romaingoetz.fr/).

- [Icomoon](https://icomoon.io/) for handling icons and allowing easy bundling.
- [#COFFEE is the color](https://c0ffee.surge.sh) for color choosing.

## Licenses

- **This project** is licensed under [GNU Affero General Public License](https://www.gnu.org/licenses/).
- **Jirafeau** is licensed under [GNU Affero General Public License](https://www.gnu.org/licenses/).
- **Feather** is licensed under the [MIT License](https://github.com/colebemis/feather/blob/master/LICENSE).
- **IBM Plex** is licensed under the [SIL Open Font License](http://scripts.sil.org/OFL).
