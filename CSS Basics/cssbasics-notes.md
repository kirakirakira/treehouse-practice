# CSS Basics Notes

**Inline Styles**: For inline styles, the CSS is written in the HTML file, directly inside an element's tag using a style attribute.

Inline styles override internal styles.

```html
<body style="background-color: orange;">
```

**Internal Styles**: Internal styles are embedded in the ```<head>``` section of the HTML document and are defined inside a ```<style>``` tag.

```html
<style>
  p {
    font-size: 20px;
    font-weight: bold;
  }
</style>
```

**External Style Sheets**: Linking to an external style sheet
```html
<link rel="stylesheet" href="css/style.css">
```
The rel attribute specifies the relationship between the HTML document and the linked document.

The href attribute points to the location of the CSS file.

**Importing style sheets with @import**: The @import statement lets us import CSS from other style sheets. It shares some of the same advantages as linking a stylesheet, like browser caching and maintenance efficiency.

Example using @import:
```css
@import 'reset-styles.css';
```

The @import statement must precede all other CSS rules in a style sheet in order for it to work properly. Don't need to include the folder in the file path if the CSS file is in the same folder as the one that you are importing.

Each @import statement requires a call to the server. Can be costly to load time.

## Selectors

**CSS Rule**:
```CSS
selector {
  property: value;
}
```

**Declaration Block**:
```CSS
    {
  property: value;
}
```

Selectors target the content we want to style. When defining a selector in a stylesheet, you're instructing the browser to match every instance of that selector in the HTML.

**Universal Selector**: targets every element on the page at once and applies the styles we set.

```CSS
* {
  margin: 0;
  padding: 0;
}
```
The universal selector will apply the margin and padding styles to every element on the page.

**Type Selector**: target element types on the page. Also called element selectors because we use the element's HTML tag as the selector.

To target the footer element and change its background color:

```CSS
footer {
  background-color: lightblue;
}
```

To target all paragraphs on the page, can use a type selector:

```CSS
p {
  color: slategrey;
  font-size: 18px;
}
```

**ID Selector**: targets a unique ID that was given to an element.

ID selectors are declared using the # symbol followed by the ID name.

```CSS
#primary-content {
  background: grey;
}
```

This selector will match the HTML element that has an ID attribute with the value primary-content.

IDs are unique to the page, so an element can only have one ID and a page can only have one element with the same ID name.

**Class Selector**: target elements based on their class attribute. The main difference between a class and an ID selector is that IDs are unique and they're used to identify one element on the page, whereas a class can target more than one element.

Class selectors are defined with the . character followed by the class name.

```CSS
.primary-content {
  background: grey;
}
```

**Example of reusing classes**: It's best to create classes for the repeated styles.

Space-separate each class name in the class attribute:
```HTML
<div class="primary-content t-border rounded">
```

Then target each class in the style sheet:
```CSS
.primary-content {
  background: grey;
}
.t-border {
  border-top: 1px solid;
}
.rounded {
  border-radius: 10px;
}
```

If an element has both an id and a class, the id CSS will override the class CSS.

**Descendant Selectors**: Can combine selectors to create descendant selectors that target elements that are descendants of an element. This makes selectors more specific.

**Examples of descendant selectors**: To create a descendant selector, use two or more selectors separated by whitespace:

```CSS
.main-header span {
  font-size: 26px;
}

ul li {
  margin-bottom: 12px;
}
```

**Multiple Class ID Selectors**:
https://css-tricks.com/multiple-class-id-selectors/
```CSS
#header.callout {}
#header .callout {}
```

The ```#header .callout``` selects all elements with the class name callout that are descendants of the element with an ID of header.

The ```#header.callout``` selects the element which has an ID of header and also a class name of callout.

**Pseudo-classes**: Pseudo-classes are similar to classes, but they're not explicitly defined in an element's class attribute. Unlike type, ID and class selectors, pseudo-classes can target elements dynamically based on user interaction, an element's state, and more.

Think of a pseudo-class as a keyword we add to a selector to style a special state of an element.

The :link pseudo-class targets links that have not been visited by the user:
```CSS
a:link {
  color: orange;
}
```
Will only apply to a elements with an href attribute.

The :visited pseudo-class targets links that have been visited --or clicked-- by the user:
```CSS
a:visited {
  color: lightblue;
}
```

The :hover pseudo-class targets an element when a user hovers over it:
```CSS
a:hover {
  color: forestgreen;
}
```

The :active pseudo-class gets applied when an element is in an active state:
```CSS
a:active {
  color: lightcoral;
}
```

The :focus pseudo-class is only applied to interactive elements like links, buttons and form elements. The styles are applied as soon as an element receives focus:
```CSS
a:focus {
  color: white;
  background-color: orange;
}
```

**CSS Comments**: Comments in CSS begin with a forward-slash and an asterisk and end with an asterisk and forward-slash. Everything we write between the opening and closing characters is ignored by the browser.

```CSS
/* Class Selectors */

.main-header {
  background: orange; /* Makes the header background orange */
}
```

## Common Data Types

**Pixel Units**: size in pixel will always remain the same and will not scale, regardless of the browser window and size of the screen.

**Percentages**: percentage values in CSS are measured relative to a parent element's length.

**Em Units**: most commonly used relative unit. The em is known as a font-relative unit because it's calculated based on a parent element's font size.

Example:
```CSS
body {
  font-size: 1em;
}
```
This is equivalent to setting the font-size value to:
```CSS
body {
  font-size: 16px;
}
```

Default font size for most browsers is 16px, which would equal 1em.

**Converting pixels to ems**: To convert a px value to its equivalent em value: divide an element's px value by the parent element's font-size value.

Example:
```CSS
.intro {
  font-size: 24px;
}
```
To convert the font-size value of intro to an em value, divide 24 by the parent element's font-size. In this case, the parent element is the body element, which has the font-size set to 1em, or 16px. 24/16 = 1.5 This gives us an em-based font-size value of:
```CSS
.intro {
  font-size: 1.5em;  /* 24px/16px */
}
```

Watch out for this:
If the parent element's font-size is 2em, and a descendant element is 1.5em, then the descendant element is actually 2*1.5em = 3em.

**Rem Units**: Rem stands for "root em". The rem unit is similar to the em unit. The difference is that rem is relative only to the root element of the page (the root element is the html element.)

Example:
```CSS
h1 {
  font-size: 5.625rem;
}
```

Technique for sizing with px, rem, and em: https://css-tricks.com/rems-ems/
px at the Root (document level), rem for Components (modules on the page), em for Text Elements (will be relative to the module)

**Color Values**: colors can be described with a keyword, a hexadecimal value, or an RGB function.

Examples:
Hexadecimal Values
```CSS
.main-header {
  background-color: #ff0033;
}
```

RGB Values
```CSS
a:link {
  color: rgb(255, 169, 73);
}
```

RGBa Values: a is alpha - the opacity of the color
```CSS
a:hover {
  color: rgba(255, 169, 73, .4);
}
```

**Text Styles**:

```text-align```: controls the horizontal alignment of text
```text-transform```: changes the case of text - uppercase, lowercase, or capitalized
```text-decoration```: sets the line decoration of elements; commonly used to remove underlines in links
```font-weight```: sets how thick or thin the characters are displayed
