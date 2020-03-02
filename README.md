# Jirafeau Minuit Theme

This is a theme for [Jirafeau](https://gitlab.com/mojo42/Jirafeau), an Open-Source software that allow to easely upload files and share them with a link.

The theme is **dark and minty**, and designed to give the software a *modern look*. It's written in LESS and can be simply modified according to your needs.

## Screenshots

## Main features

- **Simple** and **modern** look
- Distincive **colors**
- Is *responsive* and works both on **desktop** and **mobile***
- Can easely be **improved** or **modified**
- Use the beautifull **icons** from [Feather](https://feathericons.com/) to be more friendly and appealling.
- Display texts and informations with **distinction and readabillity** thanks to the [IBM Plex Mono](https://github.com/IBM/plex/tree/v4.0.2) font.

** Read the [configuration](#configuration) section to enable compatibility to mobile.*

## Requirements

You will need a working installation of **Jirafeau** to use the theme. It's quite simple and all is explained in the [Jirafeau documentation](https://gitlab.com/mojo42/Jirafeau#installation).

- **System requirements** are the same as for the Jirafeau software.
- The theme use **CSS3**.
- The theme use **webfonts**
- Work on all modern browsers that support the **CSS Flexible Box Layout Module** — all are listed in the [Can I use](https://caniuse.com/#feat=flexbox) website.

The theme come already builded as a CSS file, but you can re-compile it with any LESS compiler. More information about building in the [Contributing](#contributing) section.

## Installation

You can either **download** and install manually, or **clone** this repository to `media/minuit` of your Jirafeau installation.

````
cd <your jirafeau path>
git clone https://github.com/wizhou/jirafeau-theme-minuit.git media/minuit
````

Once this is done, go to `lib/config.local.php` and change the following lines :

````
$cfg = array (
	// ...
	'style' => 'minuit',
````

Then, **Jirafeau** will automatically link the theme file `style.css.php` as the main stylesheet of your installation.


## Configuration

The theme can be configured in multiples ways, either to change it's look or to enable differents features.

Most of the theme base elements, as **units**, **colors** and **font** are declared as **LESS variables** inside `src/lib/config.less`. You may modify any of them to make the theme look as you wish, and the file is commented with this idea.

You will need to re-compile the **LESS file** `src/style.less` into a **CSS file** to make the changes append. Any less compiler can be used to do so, but the end file must be placed and named as follow : `dist/style.css`. You can find more informations about building in the [Contributing](#contributing) section.

### Enable mobile compatibility

The theme use *responsive web design* and work well in mobile or tablet displays. However, **Jirafeau** is not configurated to be usable on phone by default and lack a `viewport`configuration. You must enable it by yourself.

To do so, go to `lib/template/header.php` of your **Jirafeau** installation, and add this line just below the `<head>` opening tag.

````
<?php /* Add this line to enable mobile use ! */ ?>
<meta name="viewport" content="width=device-width, initial-scale=1">
````

### Hide / Show File max size
If you don't use any **upload size limitiation** in your Jirafeau installation, you can hide its text row by setting the following variable to `false` inside `src/lib/config.less`.

````
@show-config-max-upload-size: false;
````

### Change font

**Minuit** theme use the [IBM Plex Mono](https://github.com/IBM/plex/tree/v4.0.2) font in *regular* and *bold* to display texts. The font is installed inside the theme `assets/fonts` and linked inside the `style.css.php` file.

There is two ways you can add a new font to the theme :

#### Hosted font

You can import any **hosted font** you like by loading it's stylesheet directly inside the `style.css.php` file.

First, remove the link of the theme font :

````
require_once __DIR__ . '/assets/fonts/ibm-plex-mono.css';
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

You can **install** a font on your own installation by following a few extra steps :

- **Download** a font, preferably an open source one, or any you bought and wishe to use. You can find some on [Velvetyne](http://www.velvetyne.fr/) website, [Open Font Library](https://fontlibrary.org/en/font/avara), or even [Google Fonts](https://fonts.google.com/).
- Either the font already come with a **bundle** for web use, or you will need to build your own if the fonts allows you to (check its *license* to know). You can use any [Webfont Generator](https://duckduckgo.com/?q=webfont+generator&ia=web) you want, and there is plenty of them over the internet.
- Locate the font insde the `assets/fonts` folder. To keep it simple, you can name the folder containing the font's files with the name of the font, like this : `assets/fonts/my-web-font`.
- Your bundle might have come with a **CSS file** linking your font with a `@font-face` declaration, if not, you will need to make your own. Here is an [article from CSS Tricks](https://css-tricks.com/snippets/css/using-font-face/) explaining how. Te be consitent with the font's folder name, you can name this file `my-web-font.css` and locate it at the root of `/assets/fonts`. Inside the `@font-face` declaration, the paths to your font's file will then have to look like this :
````
src: url('<my-web-font>/<my-web-font>.woff'),
````
- Then, go to `style.css.php` and change the **path** of the following line to location of your font CSS file :
````
// From
require_once __DIR__ . '/assets/fonts/ibm-plex-mono.css';
// To
require_once __DIR__ . '/assets/fonts/<my-web-font>.css';
````
- After this, go to `src/lib/config.less` and change the value of this **variable** to the name of your font.

	`````
	@font-family: '<My web font>';
	`````

- Finally, re-compile the **LESS** file `src/style.less` into the CSS file `dist/style.css`.

### Change colors

**Minuit** theme use green and blue colors defined in **LESS variables**. If you wish to change the colors of the theme, you can do so in the file `src/lib/colors.less`

The green colors are defined with the `@primary-` variables, and the blue colors are definied with the `@secondary-` variables.

The **variables** are organised with like this :

````
@primary-majeure: Strong main color.
@primary-mediante: Regular color
@primary-sensible: Ligth color, for borders and hover
@primary-mineure: Extra-Ligth color, for backgrounds
````

You might play as you like with these definition. Right now there is still a lot of hard coded base colors. In a future release, there will be more use of LESS color channel functions to allow quicker and smoother changings of the theme colors.

## Building

**Minuit** theme is written in [Less](http://lesscss.org/) in 3.11.1. It use [Parcel](https://parceljs.org/) as a compiler and a **CSS** minifier, and [npm](https://www.npmjs.com/) to make it run. However, this setup is more a comfort than a need for the project. You can use any LESS compiler you like to build the theme.

#### With npm and Parcel

First, install **npm** and **parcel** if you haven't already. To install npm, you first need to install **node** using the node.js [installer](https://nodejs.org/en/), npm is installed as a part of it.

Then, you can make sure you have the most recent version of npm by using npm :
````
npm install npm -g
````

Then, install Parcel with npm :
````
npm install -g parcel-bundler
````

When both are installed, you can go to the **minuit theme** folder and run the following commands to compile the project

Go to your jirafeau installation
````
cd <path-to-your-jirafeau>/media/minuit
````
If for dev, use this command to ask **Parcel** to `watch` the project.
````
npm run dev
````
Then, to ask **Parcel** to `build` the theme as a minified CSS file, run this command :
````
npm run build
````
**Parcel** will take care to output the complied CSS file to the right place. It will aslo produce **source maps** by default, allowing an easy debugging and workflow.

Also, the **Parcel** configurations can be found inside `package.json`.

#### Build with Less.js

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

#### Build with text editor
You can also build the project with any text editor plugin that compile LESS. However, you will be in charge of placing the compiled CSS file inside its folder as follow : `/dist/style.css`.

## Contributing

Contributing is appreciated, and the theme can be improved in many ways. Please refer to `CONTRIBUTING.md` for more details.


### To dos
- Clean the color compositon and allow faster color changing.
- Regroup some `media queries` declarations.
- Gather similars declarations into `extends` to minify the file size.
- Make a favicon
- Insert the jirafeau logo inside the footer


## Help

This theme has been tested in latest version of **Chrome**, **Firefox**, **Opera** and **Safari**, and **Chrome Android**, but not in Edge nor Safari iOS, but it should work on them.

If you find any bug, or if something feels quirky, please **open an issue** on the project.

This theme doesn't change anything to **Jirafeau** software (outside of the mobile configuration explained above), so if you encounter any bug while using the software, please refer to [Jirafeau documentation](https://gitlab.com/mojo42/Jirafeau).

### Known bugs

- The **login page** use `focus` and `z-index` layers to hide the label when the user is typing password. However, if the text input loose focus, the label re-appear over the input and can be confusing. It's actually quite hard to conter this behavior with only css and because of the way **Jirafeau** is builded.


## Credits

2020 - Wizhou / [Romain Gœtz](https://romaingoetz.fr/).

- [Icomoon](https://icomoon.io/) for handling icons and allowing easy bundling.
- [#COFFEE is the color](https://c0ffee.surge.sh) for color choosing.

## Licenses

- **This project** is licensed under [GNU Affero General Public License](https://www.gnu.org/licenses/).
- **Jirafeau** is licensed under [GNU Affero General Public License](https://www.gnu.org/licenses/).
- **Feather** is licensed under the [MIT License](https://github.com/colebemis/feather/blob/master/LICENSE).
- **IBM Plex** is licensed uneder the [SIL Open Font License](http://scripts.sil.org/OFL).
