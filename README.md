# SVG for Everybody

Use external SVG spritemaps today. **SVG for Everybody** minds the gap between [SVG-capable browsers](http://caniuse.com/svg) and those which do not support [external SVG spritemaps](http://css-tricks.com/svg-sprites-use-better-icon-fonts/##Browser Support).

To use **svg4everybody**, add it in the `<head>` of your document.

```html
<script src="/path/to/svg4everybody.ie8.min.js"></script>
```

Only IE6-8 require the script run this early, in order to shiv the **svg** and **use** elements.

## Usage

**spritemap.svg:**
```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 64 64">
	<g id="codepen"><title>CodePen</title><path etc.../></g>
	<g id="youtube"><title>YouTube</title><path etc.../></g>
	<g id="twitter"><title>Twitter</title><path etc.../></g>
</svg>
```

The preceding spritemap may be referenced without assistance in **Chrome**, **Firefox**, and **Opera**. This script polyfills the experience in **IE9-11**.

```html
<svg role="img" title="CodePen" viewbox="0 0 64 64"><use xlink:href="spritemap.svg#codepen"></use></svg>
<svg role="img" title="YouTube" viewbox="0 0 64 64"><use xlink:href="spritemap.svg#youtube"></use></svg>
<svg role="img" title="Twitter" viewbox="0 0 64 64"><use xlink:href="spritemap.svg#twitter"></use></svg>
```

![3 SVG logos](http://i.imgur.com/87Npdzn.png)

In **IE6-8**, the document markup is modified to fallback to PNG images.

```html
<svg role="img" title="CodePen" viewbox="0 0 64 64"><img src="spritemap.svg.codepen.png"></svg>
<svg role="img" title="YouTube" viewbox="0 0 64 64"><img src="spritemap.svg.youtube.png"></svg>
<svg role="img" title="Twitter" viewbox="0 0 64 64"><img src="spritemap.svg.twitter.png"></svg>
```

Fallback PNGs point to the same location as their corresponding SVGs, only with the `#` hash replaced by a `.` dot, and with an appended `.png` extension.

## Individual labels

Markup SVG sprites with a combination of attributes and elements that best communicate their meaning to a variety of accessibility tools.

Within SVG markup, each sprite may use a `<title>` element to identify itself.

```html
<g id="codepen"><title>CodePen</title><path etc.../></g>
```

This title will be read aloud in JAWS and NVDA.

Then, within document markup, each sprite reference may use a `title` attribute to identify itself.

```html
<svg title="CodePen" viewbox="0 0 64 64"><use xlink:href="spritemap.svg#codepen"></use></svg>
```

This title will be read aloud in VoiceOver and NVDA. At present, the `title` attribute is the only way to properly read aloud an SVG in VoiceOver.

For maximum compatibility, both the `title` attribute in the document and the `title` element in the SVG should be used.

- [Tips for Creating Accessible SVG](https://www.sitepoint.com/tips-accessible-svg/)
- [Using ARIA to enhance SVG accessibility](http://blog.paciellogroup.com/2013/12/using-aria-enhance-svg-accessibility/)

## Smaller SVGs

SVG files, especially exported from various editors, usually contains a lot of redundant and useless information such as editor metadata, comments, hidden elements, default or non-optimal values and other stuff that can be safely removed or converted without affecting SVG rendering result.

Use a tool like [SVGO](https://github.com/svg/svgo) to optimize SVG spritemaps.

```sh
$ [sudo] npm install -g svgo
$ svgo spritemap.svg
```

---

The standard script is 0.9KB or 408B minified + gzipped. The IE6-8 compatible script (which also works for IE9+) is 1.4KB or 534B minified + gzipped.
