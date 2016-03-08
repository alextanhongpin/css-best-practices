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


### References

1. [CSS Architecture New Best Practices](http://www.sitepoint.com/css-architectures-new-best-practices/)
2. [30 CSS Best Practices for Beginners](http://code.tutsplus.com/tutorials/30-css-best-practices-for-beginners--net-6741)
3. [25 CSS Best Practices We Followed at Innofield](http://www.innofied.com/25-css-best-practices-we-follow-at-innofied/)
4. [CSS Best Practices](http://1stwebdesigner.com/css-best-practices/)
5. [Mozilla Developer Network - Writing Efficient CSS](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
