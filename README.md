# svg-scss v1.0.2

A single file, Sass-based (or SCSS-based) import that allows you to define SVGs directly inside/inline your SCSS to be used anywhere that uses the stylesheet without managing external SVG assets or resources. This is useful for adding icons to your web project without all the workflow overhead or end-user bloat of other icon systems.

## Support

Anything that has SVG support, so IE9 and above, if you care about that sort of thing. [Can I use svg?](https://caniuse.com/?search=svg)

## Demo

[Demo Link](http://htmlpreview.github.io/?https://github.com/vaughnroyko/svg-scss/blob/master/demo.html)

## Usage

The first and only necessary step is to import the svg-scss.scss file:

```scss
@import "svg-scss";
```

### Basic Example

A simple SVG icon set inside of a span element:

```scss
.icon-arrow {
	@include svg("#242424", 24px, 39px, '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 57.05 92.89"><polygon fill="currentColor" points="10.61 0 0 10.61 35.84 46.45 0 82.28 10.61 92.89 57.05 46.45 10.61 0"/></svg>');
}
```

```html
<p><span class="icon icon-arrow" role="img" aria-hidden="true"></span></p>
```

Note the usage of `fill="currentColor"` when adding the SVG. This is necessary to assign colors to the SVG through Sass.

### Basic Example with Text

Show an icon inline with text:

```scss
.icon-arrow-small {
	@include svg("#242424", 10px, 16px, '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 57.05 92.89"><polygon fill="currentColor" points="10.61 0 0 10.61 35.84 46.45 0 82.28 10.61 92.89 57.05 46.45 10.61 0"/></svg>');
	margin-right: 5px;
}
```

```html
<p><span class="icon icon-arrow-small" role="img" aria-hidden="true"></span>Test</p>
```

### Hover Example

Change the color of an icon when hovering:

```scss
.icon-arrow-hover {
	@include svg-hover("#242424", "#00a6ff", 24px, 39px, '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 57.05 92.89"><polygon fill="currentColor" points="10.61 0 0 10.61 35.84 46.45 0 82.28 10.61 92.89 57.05 46.45 10.61 0"/></svg>');
}
```

```html
<p><span class="icon icon-arrow-hover" role="img" aria-hidden="true"></span></p>
```

### Animation Example

Animate an icon:

```scss
.icon-circle {
	@include svg("#242424", 32px, 32px, '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 92.99 91.77"><path fill="currentColor" d="M92.99 45.88A46.5 46.5 0 0 0 53.99 0v15.3a31.49 31.49 0 0 1 0 61.17v15.3a46.5 46.5 0 0 0 39-45.89Zm-77.99 0A31.54 31.54 0 0 1 39 15.3V0a46.49 46.49 0 0 0 0 91.77V76.49a31.56 31.56 0 0 1-24-30.61Z"/></svg>');

	&::before {
		animation: spin 1s infinite;
	}
}

@keyframes spin {
	0% {
		transform: rotate(0deg);
	}

	100% {
		transform: rotate(359deg);
	}
}
```

```html
<p><span class="icon icon-circle" role="img" aria-hidden="true"></span></a>
```

### Switch on Hover

Change the color and icon when hovering:

```scss
.icon-menu {
	@include svg-hover("#242424", "#00a6ff", 28px, 28px, '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 92.89 92.99"><path fill="currentColor" d="M0 0h92.89v15H0zm0 38.99h92.89v15H0zm0 39h92.89v15H0z"/></svg>', '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 92.89 92.89"><polygon fill="currentColor" points="92.89 10.61 82.28 0 46.45 35.84 10.61 0 0 10.61 35.84 46.45 0 82.28 10.61 92.89 46.45 57.05 82.28 92.89 92.89 82.28 57.05 46.44 92.89 10.61"/></svg>');
}
```

```html
<p><span class="icon icon-menu" role="img" aria-hidden="true"></span></a>
```

### List Example Without Additional Markup

You can even use it without adding a span or additional markup in the HTML. Here's an example with a standard list:

```scss
ul {
	list-style: none;

	li {
		position: relative;
		margin-bottom: 10px;

		@include svg("#00a6ff", '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 57.05 92.89"><polygon fill="currentColor" points="10.61 0 0 10.61 35.84 46.45 0 82.28 10.61 92.89 57.05 46.45 10.61 0"/></svg>');
		width: auto; // Overwrite what svg() sets
		height: auto; // Overwrite what svg() sets

		&::before {
			width: 10px;
			height: 16px;
			left: -20px;
		}
	}
}
```

```html
<ul>
	<li>Test</li>
	<li>Test</li>
	<li>Test</li>
</ul>
```

### Hover Parent Example

You can make it so hovering over parent elements also triggers the hover state of the SVG. For example, using a link:

```scss
a {
	font-size: 24px;
	border: 2px #242424 solid;
	padding: 12px 12px 16px 12px;
	text-decoration: none;
	color: #242424;
	transition: color 0.25s ease-in-out;

	&:hover {
		color: #00a6ff;
	}
}
```

```html
<p>
	<a href="#" class="icon-hover"><span class="icon icon-arrow-hover" role="img" aria-hidden="true"></span>Test</a>
</p>
```

### Hover Parent Example with Specific Children

Similar to the above, you can also do this just for specific children icons:

```scss
a {
	border: 2px #242424 solid;
	padding: 12px 12px 16px 12px;
}
```

```html
<p>
	<a href="#" class="icon-hover-parent">
		<span class="icon icon-arrow" role="img" aria-hidden="true"></span>
		<span class="icon icon-hover-child icon-arrow-hover" role="img" aria-hidden="true"></span>
		<span class="icon icon-arrow" role="img" aria-hidden="true"></span>
	</a>
</p>
```

### Hover Example with Modified Transition Speed

Change the transition speed of the hover effect:

```scss
.icon-arrow-large-hover {
	@include svg-hover("#242424", "#00a6ff", 48px, 78px, '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 57.05 92.89"><polygon fill="currentColor" points="10.61 0 0 10.61 35.84 46.45 0 82.28 10.61 92.89 57.05 46.45 10.61 0"/></svg>', "", 1s);
}
```

```html
<p><span class="icon icon-arrow-big-hover" role="img" aria-hidden="true"></span></p>
```

## Changelog

**Version: 1.0.2 (February 13th, 2024)**

- Improved color-shifting animations so no in between shade is visible and timing is more consistent when used in conjunction with other transitions/animations.
- Added more encoded character replacements for a wider range of support for SVGs.
- Added a parameter for changing transition/animation timing.
- Moved the $svg parameter to the end of svg() to better match svg-hover().
- The credit comment now uses double slashes so it is removed in minification by default.
- Linted all files.

**Version: 1.0.1 (October 18th, 2021)**

- Changed it so SVGs are now scaled proportionally to set dimensions rather than clipped/cropped.

**Version: 1.0 (October 13th, 2021)**

- Initial release.

## License

svg-scss is licensed under the [MIT License](https://github.com/vaughnroyko/svg-scss/blob/master/LICENSE).
