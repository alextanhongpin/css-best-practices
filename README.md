# CSS Best Practices

/* TODO: Summarize the best practices for CSS with visual examples */


### Reset with Normalize.css
+ There is an option to `reset` or `normalize` the CSS. Read about the differences. [here](http://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css) and [here](https://the-pastry-box-project.net/oli-studholme/2013-june-3)
+ [reset.css](http://meyerweb.com/eric/tools/css/reset/) by Eric Meyer
+ [normalize.css](https://github.com/necolas/normalize.css/blob/master/normalize.css) by Necolas

> Tl;dr: CSS resets aim to remove all built-in browser styling. Normalize CSS aims to make built-in browser styling consistent across browsers.

### Clear Floats
+ [The How and Why of Clearing Floats](https://css-tricks.com/the-how-and-why-of-clearing-floats/)
+ [All About Floats](https://css-tricks.com/all-about-floats/)
+ Use the [Micro Clearfix](http://nicolasgallagher.com/micro-clearfix-hack/) to clear floats.


### Use an Icon Element
+ Instead of `spans`, use the `i` elements for icons. It makes it easier to identify the icons location on the page.
```css 
<p><i class="icon icon-comment"></i>23 comments</p>
...
.icon { background-image: url( sprites.png ); }
.icon-comments { background-position: 0 -30px; }
```

### Reset Box Sizing to Border-Box
+ [Inheriting box-sizing Probably Slightly Better Best-Practice](https://css-tricks.com/inheriting-box-sizing-probably-slightly-better-best-practice/)
```css 
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
// images doesn't work well with border-box
// they still got resized after adding borders
img {
  box-sizing: content-box;
}
```

### Organize the Stylesheet with a Top-down Structure
+ NOTE:Throw some examples here


+ For new rows, add the class .ui-name-row


### References

1. [CSS Architecture New Best Practices](http://www.sitepoint.com/css-architectures-new-best-practices/)
2. [30 CSS Best Practices for Beginners](http://code.tutsplus.com/tutorials/30-css-best-practices-for-beginners--net-6741)
3. [25 CSS Best Practices We Followed at Innofield](http://www.innofied.com/25-css-best-practices-we-follow-at-innofied/)
4. [CSS Best Practices](http://1stwebdesigner.com/css-best-practices/)
5. [Mozilla Developer Network - Writing Efficient CSS](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
