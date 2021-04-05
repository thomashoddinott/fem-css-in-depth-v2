### Intro

https://estelle.github.io/cssmastery/intro/index.html#slide1

^ In the example on slide 1, the following CSS3 features are present:

- css3 selectors
- linear gradients
- opacity
- rgba colours
- border-radius
- transforms
- transitions
- animations
- text-shadow
- fonts

### CSS Intro

**C**ascading **S**tyle **S**heets — the presentation layer of the web

Content (HTML) --- Presentation (CSS) --- Behaviour (JS)

Several ways to include CSS:

1. external style sheet

   ```html
   <link href="stylesheet" href="path/file.css" />
   ```

   best for websites - heavy download, but only once as we can cache it

2. embedded styles 

   ```html
   <style>
       body {}
   </style>
   ```

   good if we have a single page website - not for a whole site as we'd be downloading styles every page load

3. inline styles

   ```html
   <p style="color: black">Lorem ipsum</p>
   ```

   quick and dirty - test something out, then put into one of the above

:heavy_check_mark: Why use external stylesheets?

- reusability
- maintainable
- changes are sitewide
- changes are instantaneous
- interchangeable presentation layer

most importantly: **it decouples content from presentation**

### Basic Selectors & CSS Levels

https://estelle.github.io/cssmastery/selectors/index.html#slide1

**Basic Selectors**

```html
<ul>
    <li id="myID" class="myClass">item 1</li>
    <li class="myClass">item 2</li>
    <li>item 3</li>
</ul>
```

3 ways to target:

- target `#myID` - ID

- target `.myClass` - class

- target the `li` - html tag name - **preferable**

There are many kinds of selector: https://css4-selectors.com/selectors/

### Specificity Introduction

<img src="img/spec-01.svg" alt="specificity score of 0000" width=600 />

### Relational Selectors & Combinators

https://www.w3schools.com/css/css_combinators.asp

<img src="img/image-20210405205657585.png" alt="image-20210405205657585" width=600 />

Targeting with **querySelector** natively:

```javascript
var el = document.querySelector('#bar');
var chil = el.querySelectorAll('.foo');
```

And we can remove and add classes with **classList.add** and **classList.remove**

### Attribute Selectors

**element[attribute]** - Select elements containing the named attribute with any value

```css
img[alt] {}
	<img src="image.jpg" alt="accessible">
	/* <img src="image.jpg" alt="inaccessible"> */ 
form [type] {}
	<input type=date>
	/* <select> */
```

In addition:

**element[attritube = "val"]** - matches the exact value

**element[attribute |=  "val"]** - matches value + anything after it

^ useful for languages

```css
p[lang|="en"]{/* <p lang="en-us">  <p lang="en-uk"> */ }
```

... and more:

**element[attr ^= val]** - element whose attribute starts with val - useful for matching links

```css
a[href^=mailto] {background-image: url(emailicon.gif);}
a[href^=http]:after {content: " (" attr(href) ")";}
```

**element[attr $= val]** - element whose attribute ends in val - e.g. tell me a link downloads a PDF by appending that info:

```css
a[href$=pdf] {background-image: url(pdficon.gif);}
a[href$=pdf]:after {content: " (PDF)";}
```

**element[attr *= val]** - match attribute anywhere 

Case insensitivity, add `i` - only relevant if attr val is case sensitive

```css
E[foo="bar" i]
```

```css
input[type="checkbox" i]
```

https://codepen.io/estelle/pen/lEGev

### Attribute Selectors Recap

https://frontendmasters.com/courses/css-in-depth-v2/attribute-selectors-recap/



