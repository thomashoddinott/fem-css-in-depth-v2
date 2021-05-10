My notes from: https://frontendmasters.com/courses/css-in-depth-v2/

Slides: https://estelle.github.io/cssmastery/#slide1

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

```css
F[attr|=val]

html[lang|="en"] /* would match: en, en-us, en-uk, etc. */

p:lang(en)
```

### Link, Locations & User Action

`a` with an `href` attribute

```css
:link
:visited
```

`:any-link` is the same as: `:matches(:link, :visited)`

**User Action Pseudo Classes**

```css
:hover
:active
:focus
```

*always style `:focus`* when you style `:hover` 

```css
:focus-ring
:focus-within
```

```css
:drop
:drop()
```

e.g.

```css
a:visited:hover /* hovering over a visited link can be a different style to a non-visited link - some (most) browsers do this by default? */

button:active:focus
```

**Drag and drop pseudo classes**

https://estelle.github.io/cssmastery/selectors/#slide60

**:target**

```css
:target
```

```html
<!-- myPage.html#anchor e.g. #slide63 = the browser knows we're on slide63 -->

<div id="anchor">abc...</div>
```

```css
div:target::fist-line {
    font-weight: bold;
}
```

e.g.

https://estelle.github.io/cssmastery/selectors/#slide63

<img src="img/image-20210414095952068.png" alt="image-20210414095952068" width=600 />

"Whatever tab is selected, make it white, otherwise make it gray. Whatever tab is selected, bring it to the front of the page (z-index) and push the others back."

**:scope**

Matches elements that are a reference point for selectors to match against. (Doesn't exist yet...)

**Grid-structural selectors**

Column combinator

```css
E || F
```

```css
col.selected || td {
    /* matches all cells within the column's scope */
}
```

```css
:nth-column(An+B)
:nth-last-column(An+B)
```

**Time dimensional**

```css
:current
:future
:past
```

https://css4-selectors.com/selector/css4/time-dimensional-pseudo-class/ (again, doesn't exist yet... so what's the point putting all this into the presentation???)

### Specificity 

<img src="img/readme.md" alt="specifishity chart" width=600 />

Try to avoid **div**itis and **ID**itis (hence the shark as it isn't as cute as the plankton or fish)

inline styles = BP oil tanker (very bad)

`!important` - never use in production. Acceptable as a debugging tool: "Why isn't my CSS working? OK let's see what it should be like with `!important`, etc."

**Example: Hacking Specificity with IDs**

```css
#TheirWidget {background-color: blue !important;}
#3rdPartyWidget {background-color: white;}
```

```css
#TheirWidget#TheirWidget {background-color: blue ;}
#3rdPartyWidget {background-color: white;}
```

Always comment what you're doing when you play with hacks like this.

**Example: Worst case scenario hack of !important**

```css
li {
    color: white !important;
}
```

can be overridden with an animation!

```css
li {
    animation: color forwards;
	}
@keyframes color {
    100% { color: #f50; }
}
```

### Introduction to Pseudo-Elements

```css
::first-line
::first-letter
::selection (not in spec)
::before
::after
```

**pseudo-classes** select elements that already exist.

**pseudo-elements** create faux elements you can style

Example:

```css
p:first-of-type::first-letter {
	position: relative;
	top: 8px;
	float: left;
	font-size: 3em;
	line-height: 1;
	color: hsl(205, 87%, 50%);
	padding: 0 4px 2px 0;
	font-weight: bold;
}
```

<img src="img/image-20210426111837110.png" alt="image-20210426111837110" width=300 />

### Before, After and Generated Content

e.g.

```css
p:before {
	content: '- before';	
}
p:after {
	content: '- after';	
}
```

```html
<p> the quick brown fox ... </p>
```

--> **- before the quick brown fox ... - after**

---

**additional pseudo-elements**

```css
::selection
::inactive-selection
::spelling-error
::grammar-error
```

**other pseudo-elements**

```css
::marker
::placeholder
::content
```

### Selection & More Pseudo-elements

You might want to disable `::selection` when on mobile (and sometimes desktop) apps when the user clicks over something for too long. The native feature might start to show you a copy/paste dialog, which you want to override. e.g. an app with drag and drop ???

```css
.thisSlide {
    -webkit-tap-highlight-color: #bada55;
    -webkit-user-select: none;
    -webkit-touch-callout: none;
}
```

There are lots of browser-specific elements (differences between browser scroll bars, and so on...)

"Shadow DOM"

e.g.

```css
.scrollbar ::-webkit-scrollbar {
	margin-right: 5px;
    background-color: #f36;
    border-radius: 6px;
    width: 12px;
}
/* etc. */
```

If you want to find out what's going on behind the scenes in your browser, the dev tools (f12) will reveal all.

### Before and After

continued...

before/after are **within** the target:

<img src="img/image-20210427092050272.png" alt="image-20210427092050272" width=600 />

### Counters

```css
body {counter-reset: sections;}
header h1.sectiontitle:before{
		content: "Part " counter(sections) ": ";
    	counter-increment: sections;
}
```

^ Reset the counter (called sections) every time we reach a section. +1 every time we hit a `<h1>`. Saves us having to put everything in an ordered list `<ol>` to count it. Need to explicitly say `counter-increment`. 

### Quotes & Attributes

```css
/* Specify pairs of quotes for two levels in two languages */
:lang(en) > q { quotes: '"' '"' "'" "'" }
:lang(fr) > q { quotes: "«" "»" "’" "’" }

/* Insert quotes before and after Q element content */
q::before { content: open-quote }
q::after  { content: close-quote }
```

example:

<img src="img/image-20210428085740573.png" alt="image-20210428085740573" width=600 />

### Counters Review

[example](https://estelle.github.io/cssmastery/generated/#slide17)

```css
body {counter-reset: invalidCount;}
:invalid {
  background-color: pink;
  counter-increment: invalidCount;
}
p:before {
  content: "You have " 
      counter(invalidCount) " invalid entries";
}
```

<img src="img/image-20210428090627935.png" alt="image-20210428090627935" width=400 />

[another example](https://estelle.github.io/cssmastery/generated/#slide18)

```css
body { counter-reset: pagecount; }
p { 
	counter-increment: pagecount;
}
p:after { color: magenta;
  content: " " counter(pagecount);
}
```

<img src="img/image-20210428090740211.png" alt="image-20210428090740211" width=200 />

### Images

<img src="img/image-20210428091450486.png" alt="image-20210428091450486" width=600 />

### Strings & Special Characters

<img src="img/image-20210428092042461.png" alt="image-20210428092042461" width=600 />

<img src="img/image-20210428092109111.png" alt="image-20210428092109111" width=600 />

<img src="img/image-20210428092449797.png" alt="image-20210428092449797" width=600 />

### Icon Accessibility 

e.g.

```css
[class|='material-icons']:after { 
  content: "\e84e";
  content: "bed";
  color: blue;
}
.material-icons {
  font-size: 3rem;
}
```

```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
<!-- ... -->
<p class="material-icons">accessibility<p>
```

<img src="img/image-20210504095713802.png" alt="image-20210504095713802" width=100 />

needs `-webkit-font-feature-settings: 'liga';`

### Design Elements

Thought bubbles example

<img src="img/image-20210504100358195.png" alt="image-20210504100358195" width=600 />

see this for more: https://css-tricks.com/the-shapes-of-css/

and more ... https://estelle.github.io/cssmastery/generated/#slide38

### Media Type, Screen Size & Resolution

https://estelle.github.io/cssmastery/media/#slide1

We use **media queries** to change the presentation layer depending on what screen (browser, actually -- called the viewport) we're viewing from (size in pixels, orientation, etc.).

e.g.

```css
@media screen and (max-width: 600px) {
  #presentation {
    background: red;
      /* turn the background red when the 			 screen is < 600 px wide */
  }
}
@media screen and (orientation: portrait) {
  #presentation {
    background: yellow;
    /* turn the background yellow when the 		   screen is taller than it is wide   		   (portrait) */
  }
/* 1st query overrides 2nd? */
```

Media Features: https://estelle.github.io/cssmastery/media/#slide9

**Resolution Units**

- dpi: dots per inch
- dpcm: dots per cm (1 dpcm ~ 2.54 dpi)
- dppx: dots per pixel (1 dppx = 96 dpi)

Efficient to serve higher/lower quality images depending on the users' screen resolution. E.g. When a user has a high DPI screen, serve a high resolution image.

e.g.

```css
@media (-webkit-min-device-pixel-ratio: 2), /* Safari */
       (min-resolution: 192dpi) /* Everyone else */ 
		{
    		/* CSS */
		}
```

Images are typically served at 72, maybe 96 dpi. Sometimes we might go up to 300 though. Maybe we're printing an image? Or we're doing something that needs high quality? 

Demo: https://estelle.github.io/cssmastery/media/files/mediaqueries.html

### Syntax & Punctuation

`only` leaves out older browsers

```css
media="only print and (color)"
```

`and` - both parts must be true

```css
media="only screen and (orientation: potrait)"
```

`not` - if untrue

```css
media="not screen and (color)"
```

A `,` separates selectors - any part can be true

```css
media="print, screen and (min-width: 480px)"
```

`<` , `>` , and `>=` are coming soon. Won't have to do `min-width` and `max-width` all the time.

### Browser Capability @supports

`@supports` checks browser can do something before trying it

```css
@supports (display: flex){
	/* ... CSS stuff if the browser can do flex box */
}
```

https://codepen.io/estelle/pen/ihsny

e.g. https://estelle.github.io/cssmastery/media/files/typowidth.html

```css
@media screen and (min-width: 38em){
  #content { padding: 0 21%; }
}
```

|                    small screen (< 38em)                     |                    larger screen (> 38em)                    |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| <img src="img/image-20210506100328120.png" alt="image-20210506100328120" width=600 /> | <img src="img/image-20210506100245052.png" alt="image-20210506100245052" width=600 /> |

^ puts in a margin of 21% when we're on a larger screen.

### Use Cases: Hyphenations

```css
@media screen and (max-width: 38em){
  #content { padding: 0 21%; }
}
 p {
  hyphens: auto;
}
```

^ useful when we're on a small screen and don't long words to break onto a new line.

### Use Cases: Columns

e.g.

```css
column-count: 1;
column-width: 10em;
column-rule: 1px solid #bbb;
column-gap: 2em;
```

Have a play around to learn what this does: https://estelle.github.io/cssmastery/media/#slide26

It's nice to use columns with media queries, and we can do that without using `@media`:

```css
#content {columns: 18em 3;}
h1 {column-span: all;}
```

Each column must be at least 18ems wide. If there is space enough for 3, render 3. If are screen is for example only 40ems wide, for example, then generate just 2 columns. etc.

https://estelle.github.io/cssmastery/media/#slide27

### Use Cases: SVG

With SVGs, the width is the width **of the container** of the SVG.

https://estelle.github.io/cssmastery/media/files/circlesvg.html

### Colours: RGB, HSL & HEX

These are all the same:

```css
  color: white;
  color: #fff;
  color: #FFFFFF;
  color: #FFFFFFFF;
  color: rgb(255,255,255);
  color: rgb(100%,100%,100%);
  color: rgba(255,255,255,1);
  color: rgba(100%,100%,100%, 1);
  color: hsl(0, 100%, 100%);
  color: hsla(0, 100%, 100%, 1);
```

There are lots of colour name keywords: https://estelle.github.io/cssmastery/colors/#slide4 ...

`currentcolor` follows the cascade to apply the color:

e.g. https://estelle.github.io/cssmastery/colors/#slide11

<img src="img/image-20210510110418338.png" alt="image-20210510110418338" width=600 />

### Opacity vs. Alpha Transparency

https://frontendmasters.com/courses/css-in-depth-v2/opacity-vs-alpha-transparency/















 

