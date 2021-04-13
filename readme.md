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

play around with the examples: https://estelle.github.io/cssmastery/selectors/#slide28

e.g.

<img src="img/image-20210408092821725.png" alt="image-20210408092821725" width=600 />

### User Interface Selectors

e.g. if there's a *checked* checkbox, make it red.

```css
input[type=checkbox]:checked + label {
    color: red;
}
```

https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes

```css
:default
:valid
:invalid

:required
:optional

:in-range
:out-of-range

:read-only
:read-write

:placeholder-shown

:user-error
/* or */
:user-invalid
```

e.g.

<img src="img/image-20210408093552449.png" alt="image-20210408093552449" width=600/>

If you know your HTML attributes CSS can become very powerful and take up a lot of the work you had JS doing before.

### Structural Selectors

```css
:root
:empty
:blank
:nth-child()
:nth-last-child()
:first-child*
:last-child
:only-child
:nth-of-type()
:nth-last-of-type()
:first-of-type
:last-of-type
:only-of-type
```

- Target elements on the page based on their relationships to other elements int the DOM
- Updates dynamically if page updates
- Reduced need for extra markup, classes and IDs

e.g. https://estelle.github.io/cssmastery/selectors/files/04_firstlastonly.html try these out:

```css
body div:first-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```

```css
body :last-child { color: hsl(205, 87%, 50%); text-decoration: underline;}
```

```css
body :last-of-type { color: hsl(205, 87%, 50%); text-decoration: underline;}
```

^ the prepended `body` is a bug in these examples

### nth-of-type Structural Selectors

e.g.

```css
:nth-child(3n)
:nth-last-child(odd)
:nth-of-type(5)
:nth-last-of-type(3n+1) 
```

`nth-of-type`

```css
:nth-of-type(even)
:nth-of-type(odd)
:nth-of-type(an+b)
```

https://estelle.github.io/selectors/#slide33 (older slides - not broken)

<img src="img/image-20210413084830640.png" alt="image-20210413084830640" width=600 />

### Structural Selectors Demo

https://estelle.github.io/cssmastery/selectors/#slide43

### Root, Empty & Blank

```css
:root	
```

Selects the document root, which is `<html>`

```css
E:empty
```

```css
<E/>
<E></E>
<E><!-- this is a comment --></E>
<E title="this is an empty element"/>
```

```css
E:blank
```

```css
<E>   <!-- has white space -->   </E>
```

^ but not supported yet?

but you can use `:-moz-whitespace-only` in firefox...

https://developer.mozilla.org/en-US/docs/Web/CSS/:-moz-only-whitespace

### Negation, Matching & Parent

```css
E:not(s1) /* matches any element that is not also matched by s1*/
```

```css
div:not(.excludeMe) /* matches any div except for ones with class .excludeMe */
```

Safari Only:

```css
E:not(s1, s2)
```

```css
div:not(.excludeMe, .excuseYou)
```

e.g.

```css
li:first-child {
  color: blue;
  font-weight: normal;
  }
li:not(:first-child) {
  color: red;
  font-weight:bold;
  }
```

<img src="img/image-20210413091007149.png" alt="image-20210413091007149" width=600 />

---

(talking about `:matches`, `:any`, :`has` which are still experimental)

https://caniuse.com/

e.g. 

`:has` - not supported - https://caniuse.com/?search=%3Ahas

`:matches` - kind of supported - https://caniuse.com/?search=%3Amatches

---

### Linguistic Pseudo Classes

https://frontendmasters.com/courses/css-in-depth-v2/linguistic-pseudo-classes/

