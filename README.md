# BICHOCO font faces
A Sass module helping you to create easily one or more @font-face rules

This module helps you (and those who work with you) to organize/codify font files and improves the writing of your @font-face rules.
<br>From now, you should consider first your files rather than your (S)CSS syntax.

`font-face()` and `font-faces()` offer you an easy and simple way to enjoy your webdesigner/decorator/painter (as you want) with custom fonts without wanting to kill him.

You can keep up-to-date with upcoming features, suggestions and fixes by looking at the [bichoco-font-faces](https://trello.com/b/1aKrVBmd) Trello board.


## What does it do?

* Organizes font files in a clear and simply tree.
* Normalizes the naming convention of font files.
* Generates more @font-face rules (same variation, different format or vice versa) from a single line.
* Enhances and standardizes the usage of @font-face in writing less.
* Explains what code does using detailed comments.


## How to use it

**Requires Sass 3.2**

Import the partial in your Sass files:

```scss
@import 'font-faces';
```

Configure both variables provided:

```scss
// The full path where font files are stored
$FONTS_URI: '../fonts';

// Default list of font extensions used to construct @font-face rules
$FONT_FACES_EXTENSIONS: ('eot', 'woff', 'ttf');
```

### Naming and organizing font files

Great power means great responsibilities, write less requires more organization.

First, the operation of the module is based on the organization/distribution of the files by directories.
<br>Remember that one font style/variant is 3 or 4 files in fact. Now it's easy to understand why a single directory is a horrendous solution and would be a fucking hell.
<br>Each font family will have to be represented by a directory with a unique name.
<br>The simplest way (and I recommend it to you) would be to assign the font family name to the one it refers to without shortcut or modification (e.g.: `Lato`, `OpenSans`, `"Lobster Two"` or `ptsans`).

In some cases, if the font family is a collection (e.g.: `Droid Sans`, `Droid Sans Mono`, `Droid Serif`), don't hesitate to nested directories in the following way:

```
.
├── fonts
|   ├── Droid
|   |   ├── Sans
|   |   ├── SansMono
|   |   └── Serif
```


Regarding the naming of font files, it refers to a strict convention established by myself, my convictions and my biases (open to reviews as well).
<br>This convention has been established for the following reasons:

1. Standardize the font files naming supplied by websites (Google Web Fonts, Font Squirrel) or the foundries themselves.
   * e.g. 1: `Lato-RegIta.ttf` (latofonts.com) - `Lato-Italic.ttf` (google.com/webfonts) - `Lato-RegIta-webfont.ttf` (fontsquirrel.com/fontface/generator).
   * e.g. 2: `Lato-RegIta.ttf` - `Ubuntu-RI.ttf` - `SourceSansPro-It.ttf` - `Quicksand_Book_Oblique.otf`.
2. Remove font family name which is identified by the name of directory which stores files.
3. Codify font file names to make the writing of mixins easier.

The naming convention to apply  : `[ [ [ <'weight'> || <'style'> ]? || <'weight'> - <'style'> ]? . [ 'eot' || 'woff' || 'ttf' || 'otf' ]? ]`

The construction of the font filenames will be made with the help of the following conversion tables:

 Literal Style                               | Filename Style
:--------------------------------------------|:---------------
 Italic - Oblique                            | italic


 Literal Weight                              | Filename Weight
:--------------------------------------------|:---------------
 Thin                                        | thin
 Extra Light                                 | extralight
 Light                                       | light
 Regular / Normal / Plain / Roman / Standard | regular
 Medium                                      | medium
 Semi-bold / Demi-bold                       | semibold
 Bold                                        | bold
 Extra-bold / Extra                          | extrabold
 Black / Heavy                               | black

Note : Without this preliminary work, the module will not work correctly.


### Basic usage

The `font-face()` mixin is the easiest way provided by the module (but already very useful).

In this example, we will include a webfont named Asap in its bold variant/style and for all browsers:

```scss
@include font-face('Asap', 'asap', normal, 700);
```

Compiles to:

```css
@font-face {
  font-family: "Asap";
  src: url("../fonts/asap/bold.eot");
  src: url("../fonts/asap/bold.eot?#iefix") format("embedded-opentype"),
       url("../fonts/asap/bold.woff") format("woff"),
       url("../fonts/asap/bold.ttf") format("truetype");
  font-style: normal;
  font-weight: 700;
}
```

### The power

That would be very boring to include many times `font-face()` mixin. No problem, I am as lazy as you are and my idea for that was: `font-faces()`.
<br>With it, you can include several @font-face rules from a single line (wonderful, isn't it).

For the second, we want to declare the 10 variants/styles of the Lato webfont but just to WOFF format:

```scss
@include font-faces(
  'Lato',
  null,
  (100, (italic, 100), 300, (italic, 300), 400, (italic, 400), 700, (italic, 700), 900, (italic, 900)),
  'woff'
);
```

Compiles to:

```css
@font-face {
  font-family: "Lato";
  src: url("../fonts/Lato/thin.woff") format("woff");
  font-style: normal;
  font-weight: 100;
}

@font-face {
  font-family: "Lato";
  src: url("../fonts/Lato/thin-italic.woff") format("woff");
  font-style: italic;
  font-weight: 100;
}

/* ... and much more */
```


## Some resources

* [Testing @font-face Support on Mobile and Tablet](http://blog.kaelig.fr/post/33373448491/testing-font-face-support-on-mobile-and-tablet)
* Font formats support : [EOT](http://caniuse.com/#feat=eot), [WOFF](http://caniuse.com/#feat=woff), [TTF/OTF](http://caniuse.com/#feat=ttf), [SVG](http://caniuse.com/#feat=svg-fonts)
* ...