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
+ Instead of `spans`, use the `i` elements for icons. It makes it easier to identify the icons location on the page. Still using sprite images instead of SVG icons? Try using FontCustom - it helps generate the complete `.css` and `SVG fonts` for your project. You just need to provide the SVG icons templates.
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

Example a dropdown list.
```html
<div class='dropdown dropdown-list'>
  <div class='list'>
    <div class='list-image'></div>
    <div class='list-detail'></div>
  </div>
</div>
```

```css

/* structure the css based on the html structure 
 * add indentation if the html is nested
**/
.dropdown {}
.dropdown-list{}
  .list {}
    .list-image {}
    .list-detail {}
```

### Layouts design

Problem: Designing a proper css layout can be cumbersome.
Solution: 
1. Separate views and components
2. Separate views for presentation (static, dynamic rendering) and views for actions (button)
3. Views for `presentation` should use BEM naming pattern
4. Views for `actions` should use js-hook naming pattern
5. Use rows and colums naming for designing layouts
6. Layout determine the structure of the page, design it well.
7. Layout might change according to the screen size.
8. Some common layout is the Header-Footer-Layout.

### Components in a View

Always ensure that there is a View (a.k.a container or box) that holds a component. It is easier to compose the layout this way. Another benefit is that rendering on the JavaScript side is simpler - just render the ShareComponent into the ShareView (else you might resort to append the view, which will affects the layout composition).

```html

<div id=ShareView>
  <div id=ShareComponent class=share>
    <div class=share-link>Facebook</div>
    <div class=share-link>Google+</div>
    <div class=share-link>Twitter</div>
  </div>
</div>

```
### Mobile First

To ensure that all UI designs fit nicely on the mobile, follow the `@320px principle`. All UI design (components) should be resizable to 320px, and still retain it's functionality. 

### Naming Repeating Components

If there are multiple similar components on the same page (e.g. modal popup), the naming can be repetitive:

```html
<!--BAD: does not share the same component classes-->
<div class="modal-report">...</div>
<div class="modal-alert">...</div>
<div class="modal-confirm">...</div>
<div class="modal-confirm-delete">...</div>
<div class="modal-confirm-update">...</div>

<!--OK: with BEM modifiers-->
<div class="modal-popup modal--alert">...</div>
<div class="modal-popup modal--confirm">...</div>

<!--OK: with data-attributes-->
<div class="modal-popup" data-role="alert">...</div>
<div class="modal-popup" data-role="confirm">...</div>

<!--OK: with id (but not suitable for lists)-->
<div class="modal-popup" id="modalAlert">...</div>
<div class="modal-popup" id="modalConfirm">...</div>
```
There are three modal confirms markup in the html body. This is bad. One way is to create a single dynamic modal - one whose content can be replaced with a template. That way, we can keep the code DRY. Another possibility is to create one single component in which you can pass in template as options:

```javascript
  var modalAlert = new ModalPopup({
    template: "<div>This is an alert!</div>", // string template for content
    btnConfirm: "OK", // set the text to "OK"
    btnCancel: null // will not show the button
  });
  
  var modalForm = new ModalPopup({
    template: "<div class='report-view'><form>...some form here</form></div>",
    btnConfirm: "SUBMIT", 
    btnCancel: "Cancel",
    onConfirm: function () {
      // do something once the user clicks the confirm button
    },
    onCancel: function () {
      // do something once the user clicks the cancel button
    }
  });

```


### Structuring CSS Components

Each components should be placed in `View`. The `View` is synonymous to `Box` or `Container`. The purpose of the `View` is for managing the positioning of the components. Since the properties for the components are shared through their classes, it is best not to include positional properties in the component's class. The structure is as follow:  

> main > layout > view > components

### Responsive Typography

Typography should be designed to be responsive. Do not use `rem` or `em` to set the responsive fonts - it is not a good idea to scale the font-size linearly. Small fonts will be illegible that way. Instead you can adapt the following pattern: 

```css
  /* .{font-weight}-{font-size}-{color} */
  .medium-36px-silver {
    font-weight: medium;
    font-size: 36px;
    color: #999;
  }
  
  /* another alternative, but probably inefficient */
  [class*="medium"] {
    font-weight: medium;
  }
  [class*="36px"] {
    font-size: 36px;
  }
  [class*="silver"] {
    color: #999;
  }
  
  @media (max-width: 720px) {
  
    /* targets all classes that contains the keyword `36px` */
    [class*="36px"] {
      font-size: 20px;
    }
  }
```


### Debugging Spacing

Do not mix horizontal (left and right) padding/margin with vertical (spacing/break) padding/margin.


```css
.br {
  height: 20px; /* default */
  display: block;
  width: 100%;
}
/* When debugging, just use jquery to select all the .br elements and append the class is debugging. */
.br--20.is-debugging {
  background: rgba(255, 0, 0, 0.5);
}

.br--10.is-debugging {
  background: rgba(0, 255, 0, 0.5);
}

```
### Checklist for UI Designer/Developer

- [ ] section
- [ ] padding/margin
- [ ] responsive
- [ ] media-query
- [x] font-size

## Style vertical and horizontal space differently

- For horizontal spacing, use a custom `<Break height={10}/>` component that accepts a height props. 
- For left/right padding, use css to customize
- If we have multiple columns in a row, use CSS-grid to separate them, rather than using a div with a fix width, or spaces.
- Avoid having borders in a component, this complicates thing when we need to add padding to them. Set the border at the parent component instead.

## Fonts

Create a base font without height and width, but just inherits the font family. Create custom fonts headings from this base font to reuse them.

## Constants

Use css variables for the colors/margin. But if you need them programmatically in JS, you might want to create another file to store these values. This really depends on your use case - if you are exporting them to be used as a package, you might want to make the colors available for both css and js.

### References

1. [CSS Architecture New Best Practices](http://www.sitepoint.com/css-architectures-new-best-practices/)
2. [30 CSS Best Practices for Beginners](http://code.tutsplus.com/tutorials/30-css-best-practices-for-beginners--net-6741)
3. [25 CSS Best Practices We Followed at Innofield](http://www.innofied.com/25-css-best-practices-we-follow-at-innofied/)
4. [CSS Best Practices](http://1stwebdesigner.com/css-best-practices/)
5. [Mozilla Developer Network - Writing Efficient CSS](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
