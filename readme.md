# CSS Coding Standards

I have decided to put together a CSS coding standard to help keep projects consistent and maintainable. By using a standard, we can become familiarized with one process and make it easier for everyone to work on. There are several coding standard projects, such as [Making WordPress CSS Coding Standards](http://make.wordpress.org/core/handbook/coding-standards/css/) and [Idiomatic CSS](https://github.com/necolas/idiomatic-css) by Nicolas Gallagher, the creator of Normalize. This will be pretty similar to both of those with a few minor differences.

## Table of contents

1. [Formatting](#formatting)
2. [Ordering](#ordering)
3. [Comments](#comments)
4. [Best Practices](#best-practices)


<a name="formatting"></a>
## 1. Formatting

Since css doesn't force any strict formatting, there tends to be several different styles to how the code is formatted. There is single line formatting, multi-line formatting, and everything in-between. We will be using multi-line formatting because it is much easier to maintain and edit.

### White-space
- Indentation should use tabs, not spaces
- If you hate tabs, use spaces, but **keep consistent**. Should **never** see both tabs and spaces combined
- There should be no extra tabs or spaces at the end of lines. Most text editors have an option to show invisible white-space, selecting text usually shows extra spaces as well

### Selectors
- Use lowercase with hyphens to separate multiple words ``.my-selector`` (unless there is no control over the html markup)
- Each selector should be on it's own line for a comma-separated list
- There should be one space between the selector and the opening curly brace ``.selector {``
- Declarations inside the curly braces should be indented
- Properties should be followed by a colon and one space ``display: block;``
- Last declaration line should always have a semi-colon even though it's not required
- Closing curly brace should be on it's own line below all the declarations and in the same column as the selector(s)
- Each Property should be separated by one line space

```css
/* correct */
.selector-1,
.selector-2 {
	margin: 20px 0;
	padding: 5px;
	font-weight: bold;
}

.selector-3 {
	padding: 10px;
}

/* incorrect - selectors on one line - closing bracket not on its own line */
.selector-1, .selector-2 {
	margin: 20px 0;
	padding: 5px;
	font-weight: bold;}

/* incorrect - single line */
.selector-1, .selector-2 { margin: 20px 0; padding: 5px; font-weight: bold; }

/* incorrect - closing bracket not lined up */
.selector-1,
.selector-2 {
	margin: 20px 0;
	padding: 5px;
	font-weight: bold;
	}

/* incorrect - no spacing between colon */
.selector-1,
.selector-2 {
	margin:20px 0;
	padding:5px;
	font-weight:bold;
}
```


<a name="ordering"></a>
## 2. Ordering

- Properties should maintain a consistent order
- Group css properties by type, such as positioning, box model and font
- [CSScomb](http://csscomb.com/) is a great tool that will do this for you automatically. There is a plugin for many different text editors. If you don't have one of those, I highly suggest giving [Sublime Text 2](http://www.sublimetext.com/2) a try, it's a great text editor.

```css
/* comments are just for demonstration, not needed in actual code */
.selector {
	/* positioning */
	position: absolute;
	top: 0;
	left: 0;
	z-index: 10;

	/* display / box-model */
	display: inline-block;
	float: left;
	clear: both;
	overflow: hidden;
	margin: 10px 0;
	padding-top: 5px;
	padding-right: 10px;
	padding-bottom: 5px;
	padding-left: 10px;
	width: 200px;
	height: 100px;
	border: 1px solid #ccc;
	border-radius: 4px;
	background: url(images/sprite.png) no-repeat right top;
	box-shadow: rgba(0, 0, 0, 0.25);

	/* text / fonts */
	color: #333;
	text-align: center;
	text-decoration: none;
	text-transform: uppercase;
	text-shadow: 0 1px 1px rgba(255, 255, 255, 0.75);
	font-weight: bold;
	font-size: 14px;
	font-family: "helvetica neue", helvetica, arial, sans-serif;
	line-height: 1.6;

	/* other */
	opacity: 0.9;
	cursor: pointer;
	transition: all 0.3s ease-out;
}
```


<a name="comments"></a>
## 3. Comments

- Section comments should have one blank line above
- I suggest that section comments should be 70 columns wide (including the closing */), prepend the section name with an equal sign (search for =layout to find section faster)
- Sub-sections should be 50 columns wide and prepend the main section title ``/*=Layout / Header``
- If you have a preferred method of commenting, just make sure that it stays consistent
- Inline comments should go above the selector, or to the right of a property that needs to be described

```css
.last-selector {
	clear: both;
}

/*=Layout
-------------------------------------------------------------------*/
.new-section {
	display: block;
	width: 100%;
}

/* inline comment about selector */
.inner {
	margin-right: auto;
	margin-left: auto;
	max-width: 1140px;
}

/*=Layout / Header
-----------------------------------------------*/
.header {
	padding: 0 20px;
	width: 1100px; /* 1140px */
}

```


<a name="best-practices"></a>
## 4. Best Practices

- Avoid [over-qualified selectors](#over-qualified)
- Avoid [over specific class names](#class-names)
- Avoid using ["magic" numbers](#magic-numbers), magic numbers are numbers that are used because they just work at the moment, but can be very fragile
- Avoid using the font-shorthand property. This shorthand font property can become overly complicated and cause inheritance issues. The font-family must be declared every time too which isn't always necessary to declare.


<h3 id="over-qualified">Over Qualified Selectors</h3>

Over-qualifying selectors are unnecessary such as ``div.container``. This will limit the selector to only div's with a class of container, which most of the time isn't necessary. They can also cause specificity issues and lead to long messy selectors.

```css
/*=Over-qualified
-------------------------------------------------------------------*/
body#home {
	color: #1a1a1a;
}

div.container {
	color: #1a1a1a;
}

ul.nav-main li a {
	display: block;
}

/*=Better options
-------------------------------------------------------------------*/
#home {
	color: #1a1a1a;
}

.container {
	color: #1a1a1a;
}

.nav-main a {
	display: block;
}

```


<h3 id="class-names">Over Specific Class Names</h3>

Overly specific class names like ``.button-red`` tend to describe the visual appearance of the element making it unflexible and tied down to the name of the class.

```css
/* no bueno */
.button-red {
	background: red;
}

.col-220 {
	width: 220px;
}

/* bueno */
.button-primary {
	background: red;
}

.col-1-4 {
	width: 220px;
}

```

If we had to make a change to the color of the button, then the class name wouldn't make sense anymore. Same for the width of the columns, if we decide to change the width or make the site responsive then the static 220 reference wouldn't make sense anymore.

```css
/* no bueno */
.button-red {
	background: orange;
}

.col-220 {
	width: 25%;
}

/* bueno */
.button-primary {
	background: orange;
}

.col-1-4 {
	width: 25%;
}

```


<h3 id="magic-numbers">Magic Numbers</h3>

The ``.nav-main`` height could differ in browsers depending on font rendering or if someone increases the font-size. Using a static number can easily brake the layout.

```css
/* magic number */
.nav-main .sub-menu {
	top: 47px; /* .nav-main is currently 47px tall */
}

/* more bulletproof solution */
.nav-main .sub-menu {
	top: 100%; /* all the way from the top */
}
```


## References
- [idiomatic CSS](https://github.com/necolas/idiomatic-css)
- [Making WordPress CSS Coding Standards](http://make.wordpress.org/core/handbook/coding-standards/css/)
- [CSS-Tricks](http://css-tricks.com/)
- [CSS Wizardry](http://csswizardry.com/)
- My Head

## Links
- [CSScomb](http://csscomb.com/)
- [Sublime Text 2](http://www.sublimetext.com/2)
