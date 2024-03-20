---
# try also 'default' to start simple
theme: default
title: 'CSS'
titleTemplate: '%s - CPIT-405'
# apply any windi css classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: | 
    CSS: Cascading Style Sheets
# persist drawings in exports and build
drawings:
  persist: false
# page transition
transition: slide-left
# use UnoCSS
css: unocss
# Make monaco available in the exported SPA
monaco: true 
# Make content selectable/copyable
selectable: true
# Make slides downloadable as PDF
download: true
---

# CSS: Cascading Style Sheets
### CPIT-405 Web Applications
#### Khalid Alharbi, PhD


<div class="absolute left-30px bottom-30px">
<p>Last updated: Spring 24</p>
</div>

---
layout: center
---

# Table of Contents
- Introduction
- Brief history
- Basic Structure
- Fundamentals
- Selectors
- Values and units 
- The Box Model: Padding, Borders, Outlines, and Margins
- Floating and Positioning
- Responsive design principles
- Layout: Grid Layout and Flexible Box Layout
- Transitions and animation
- Filters, blending, clipping, and masking
- Best Practices and Accessibility
- CSS Frameworks and Preprocessors
- Conclusion and Resources

---

# Introduction
- **Cascading Style Sheets (CSS)** is a style sheet language used for specifying the presentation and styling of HTML documents.
- CSS is designed to support the principle of separation of content and presentation, including layout, colors, and fonts.
- HTML is utilized for structuring content, while CSS is employed for styling.
  - HTML is primarily dedicated to defining the structure of your document (e.g., headings, paragraphs, lists, links, etc.).
  - CSS is primarily dedicated to defining the visual styling of HTML elements (e.g., colors, fonts, layouts, animations, etc.).
- The cascade is the core of CSS and refers to the algorithm for solving conflicts where multiple CSS rules apply to an HTML element.
- Each web browser uses a layout engine to render web pages, and support for CSS functionality remains inconsistent between browsers.

---

# History
- **1994**: CSS was proposed by Håkon Wium Lie, a Norwegian web pioneer and CTO of Opera Software, the company behind the [Opera browser](https://www.opera.com/).
  - It was proposed as a way to separate content and presentation.
- **1996**: The first version of CSS was invented.
- **1998**: CSS 2 specification was released.
- **1999**: CSS 3 specification was released with the goal to modularize the CSS specification.
  - CSS no longer Instead, it evolves through levels, where each new level builds upon the old one.
- **2006-2009**: CSS preprocessors like `Sass` and `Less` released in response to stylesheets getting larger, more complex, and harder to maintain.
- **2011-Present**:   Modern frameworks like Bootstrap, Foundation (2011), Semantic UI (2013), and Tailwind CSS (2017) received wide adoption.
- **2015-Present**: CSS continues to evolve with new features like animations, flexbox, and grid layout.


---
layout: center
---

# CSS Fundamentals

---

# Basic Structure

<br />

<img src="/images/css-structure.png" alt="CSS structure" ></img>


---

# Adding and Applying CSS to HTML

There are three main ways to apply CSS to an HTML document.

1. External CSS 

```html 
<link rel="stylesheet" href="/path/to/style.css">
```

2. Internal CSS 

```html
<head><style>body{width: 50%;}</style></head>
```

3. Inline CSS

```html
<p style="color:red">foo</p>
```

---

# External CSS

- External styles are defined within the `<link>` element, which is used to link external resource to the current HTML document. 
- The `<link>` element is defined inside the `<head>` section of the HTML page, with an `href` attribute for  the path to the stylesheet, and a `rel` attribute with a value of `stylesheet`:

<iframe class="jsfiddle" width="100%" height="50%" src="//jsfiddle.net/kalharbi/c4jhnw2y/embedded/html,css,result/?menuColor=ccc&accentColor=000" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# External CSS with media queries

- We can also conditionally load an external stylesheet with **media queries**. 
- This works by setting a media type in the `media` attribute. 

- In the following example, the external CSS file _print.css_ will only be loaded if the media condition is true, which is a printer (i.e., for print preview and printing).

```html {
<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" href="main.css">
    <link rel="stylesheet" href="print.css" media="print">
  </head>
    <body>
        <h1>Title...</h1>
        <p>Content...</p>
         <footer>
           <p>Khalid Alharbi</p>
           <p><a href="mailto:someemail@cpit405somedomain">Email</a></p>
         </footer> 
    </body>
</html>
```

_print.css_

```css
/* This hides the footer element when printing the webpage */
footer{
  visibility: hidden;
}

```

---

# Internal CSS
- Internal styles are defined within the `<style>` element, which is defined inside the `<head>` section of the HTML page:

<iframe class="jsfiddle" width="100%" height="80%" src="//jsfiddle.net/kalharbi/45xtpy2h/embedded/html,result/?menuColor=ccc&accentColor=000" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# Inline CSS
- An inline style is defined within a single HTML element using the HTML attribute `style`.

<iframe class="jsfiddle" width="100%" height="80%" src="//jsfiddle.net/kalharbi/xzjvw2dm/embedded/html,result/?menuColor=ccc&accentColor=000" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


---

# Browser Default / User-agent stylesheets
- The web browser may apply a default style when rendering an HTML page.
- Every browser has a set of default styles for HTML elements. These are known as the browser's default styles or user agent styles.
- These default styles can vary from one browser to another. This is why the same webpage can look different when viewed in different browsers.
- Developers can override these default styles by specifying their own styles in CSS.
- It's important to be aware of these default styles as they can affect the layout and appearance of your webpage, especially if you're not explicitly setting all styles yourself. 


---

# User stylesheets

- Although not common, some browsers provide the capability for users to customize styles according to their preferences by using a personalized user stylesheet.
- For example, in FireFox, the configuration editor (`about:config` page) lists some settings known as advanced preferences.
- Changing advanced preferences can affect Browser's stability and security. This is recommended for advanced users only.
- Some browser extensions offer the functionality to modify styles for enhanced accessibility or to create a more personalized user experience.

---

# Cascading Order in CSS
- CSS stands for Cascading Stylesheets. 
- The cascade is the algorithm used to resolve conflicts when multiple CSS rules apply to a single HTML element.
- The following steps apply to the cascading algorithm:
  1. **Relevance:** first the algorithm filters all the rules from the different sources to keep only the rules that apply to a given element and the appropriate `media`.
  2. **Origin and importance:** second the algorithm sorts elements by their importance, whether they have `important` flag.
  3. **Specificity:** the specificity of a rule is considered when choosing one value or another.
  4. **Scoping proximity:** styles defined closer to an element have more influence than those defined farther away.
  5. **Order of appearance:** If you add multiple styles with the same power and location, the last one you write will actually be used.


---


## More on Origin and importance

When there is more than one style defined in an HTML document, the style will be often applied as follows:
1. Inline style will take a higher priority.
2. External and internal style sheets will be applied depending on which one is defined **last** in the head section.
3. Browser default style.

---
layout: two-cols
---

## CSS Selectors

<br>

1. Universal Selector `*`
2. Element selector `element`
3. ID selector `#id`
4. Class Selector `.className`
5. Attribute Selector `element[attribute]`
6. Combinator selectors
    - Descendant `selector1 selector2`
    - Child `element1 > element2`
    - General sibling `selector ~ selector2`
    - Adjacent sibling `selector1 + selector2`
::right::

<br>
<br>

7. CSS Pseudo-classes
    - Visited Links `:visited`
    - Mouse is over elements `:hover`
    - Form input is required `:required`
    - Form input is optional `:optional`
    - First child of an element `:first-child`
    - Last child of an element `:last-child`
    - nth child of an element `:nth-child()`
8. CSS Pseudo-elements 

---

# 1. Universal Selector 
## Syntax: `* { style properties }`
<br>


- The CSS universal selector `*`  matches all HTML elements in the document.


<iframe class="jsfiddle" width="100%" height="60%" src="//jsfiddle.net/kalharbi/rnuL52bg/embedded/css,html,result/?menuColor=ccc&accentColor=000" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# 2. Element selector 
## Syntax: `element { style properties }`
<br>

<iframe class="jsfiddle" width="100%" height="80%" src="//jsfiddle.net/kalharbi/30ysm82a/embedded/css,html,result/?menuColor=ccc&accentColor=000" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# 3. ID selectors 
## Syntax: `#id-value { style properties }`
<br>

- In CSS, an ID selector is a name assigned to a specific style that is used to select an HTML element with the corresponding `id` attribute
- Each ID should be unique within a page and used only once. 
- ID selectors have a higher specificity than class selectors, which means they will override conflicting styles from class selectors.
<iframe class="jsfiddle" width="100%" height="40%" src="//jsfiddle.net/kalharbi/fpqy1d3u/embedded/css,html,result/?menuColor=ccc&accentColor=000" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


---

# 4. Class Selector 
## Syntax: `.className { style properties }`

<br>
<iframe class="jsfiddle" width="100%" height="70%" src="//jsfiddle.net/kalharbi/m4y90ovj/embedded/css,html,result/?menuColor=ccc&accentColor=000" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# 5. Attribute Selector (I)
## Syntax: `{ element[attribute]{ style properties }`

<br>

<iframe class="jsfiddle" width="100%" height="70%" src="//jsfiddle.net/kalharbi/pdjL4yzx/embedded/css,html,result/?menuColor=ccc&accentColor=000" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# 5. Attribute Selectors (II)

|  Selector | Description   |  Example |
|-----------|----------|--------------|
| `[attr]` |  Matches elements that have the attr attribute declared |`input[required]` |
| `[attr=value]`  | Matches elements with an attr attribute whose value is exactly value | `a[href="https://example.com"]` |
| `[attr~=value]` | Matches elements with an attr attribute whose value is exactly value, or contains value in its (space separated) list of values.| `p[class~="special"]` |
| `[attr^=value]`   |  Matches elements with an attr attribute, whose value begins with value. | `li[class^="box-"]` |

---

# 5. Attribute Selectors (III)

|  Selector | Description   |  Example |
|-----------|----------|--------------|
| `[attr$=value]`   | Matches elements with an attr attribute whose value ends with value.  | `li[class$="-box"]` |
| `[attr*=value]`   |  Matches elements with an attr attribute whose value contains value anywhere within the string. | `li[class*="box"]` |
 	 	
 	
---
layout: center
---

# 6. Combinator selectors
<br>

## 6.1 Descendant `selector1 selector2`
<br>

## 6.2 Child `element1 > element2`
<br>

## 6.3 General sibling `selector ~ selector2`
<br>

## 6.4 Adjacent sibling `selector1 + selector2`
<br>

---

# 6.1 Descendant combinator
## Syntax: `element1 element2`

Matches the descendant element(s) of the first element.


**Try it:**
<iframe class="jsfiddle" width="100%" height="60%" src="//jsfiddle.net/kalharbi/5vjo8gqb/embedded/css,html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


---

# 6.2 Child combinator
## Syntax: `element1 > element2`

Matches the direct child or children of the first element.

<iframe class="jsfiddle" width="100%" height="50%" src="//jsfiddle.net/kalharbi/qrnthv0f/embedded/css,html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# 6.3 General sibling combinator
## Syntax: `element1 ~ element2`


Matches all siblings of the first element that are following the first element but not necessarily immediately.

<iframe class="jsfiddle" width="100%" height="60%" src="//jsfiddle.net/kalharbi/ynf26dap/embedded/css,html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


---

# 6.4 Adjacent sibling combinator
## Syntax: `element1 + element2`

Matches the immediate sibiling of the first element that is immediately following the first element.

<iframe class="jsfiddle" width="100%" height="60%" src="//jsfiddle.net/kalharbi/6tz8yq0w/embedded/css,html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


---

# 7. CSS Pseudo-classes (I)
## Syntax: `selector:pseudo-class { style properties }`

- In CSS, a pseudo-class is a keyword added to a selector to indicate a special state of the element (e.g. when the mouse cursor is over the element or the element was clicked on).

- There are several [CSS pseudo-classes &#x2197;](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes). 
- Next are some of the most commonly used pseudo-classes

---

# 7. CSS Pseudo-classes (II)

| Pseudo-class | Description |
| --- | --- |
| `:visited` | Matches links that have been visited. |
| `:hover` | Matches when the mouse pointer is over an element. |
| `:required` | Matches when a form element is required. |
| `:optional` | Matches when a form element is optional. |
| `:first-child` | Matches an element that is the *first* of its siblings. |
| `:last-child` | Matches an element that is the *last* of its siblings. |
| `:nth-child()` | Matches elements based on their position among a group of siblings. |

---

# 7. CSS Pseudo-classes (III): Example 1

<iframe class="jsfiddle" width="100%" height="80%" src="//jsfiddle.net/kalharbi/j5s6rque/embedded/css,html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


---
layout: two-cols-header
---

# 7. CSS Pseudo-classes (IV): Example 2
- Consider the following HTML and CSS code. Where would the border appear?


::left::

```html
    <ul>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>
            Item 3
            <ul>
                <li>Item 3.1</li>
                <li>Item 3.2</li>
                <li>Item 3.3</li>
            </ul>
        </li>
    </ul>
```

```css
ul li:last-child {
  border: 1px solid red
}
```

::right::

<div v-click>

<iframe class="jsfiddle" width="100%" height="300" src="//jsfiddle.net/kalharbi/1byazwgj/embedded/css,html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

</div>

---

# 7. CSS Pseudo-classes (VI): Example 2 (Cont.)
<br>

![](/images/css-pseudo-classes-nth-child.svg)


---

# 8. CSS Pseudo-elements (I)

- In CSS, pseudo-elements are keywords added to element(s) to style a specific part of the element(s). Below are examples of pseudo-elements:
- `::first-line`
  - This can be used to apply styles to the first line of a block-level element. For example, change the font of the first line of a paragraph. 
  - The length of the first line is determined by many factors, including the width of the element, the width of the document or screen and the font size of the text".
- `::after`
  - This can be used to add a psudeo-element that is the last child of the selected element. for example, new content to the end of an element.
- `::before`
  - This can be used to add a psudeo-element that is the first child of the selected element. For example, new content to the beginning of an element.

---

# 8. CSS Pseudo-elements (II)

- `::selection` 
  - This can be used to style an element that has been highlighted by the user (e.g., mouse clicking and dragging the mouse across text).
- For the complete list and description of CSS pseudo-elements, see [MDN - Pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)

---

### CSS Pseudo-elements (II)

**Example:**
The example below shows how to change the font style of the first line and add a [wide-Headed north east arrow &#x2197;](https://unicode-table.com/en/1F865/) after an external link.

<iframe class="jsfiddle" width="100%" height="80%" src="//jsfiddle.net/kalharbi/vch68wk7/embedded/css,html,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# Example: Navigation Bar
Below is the HTML and CSS code for creating a horizontal navigation bar that looks like this:


<iframe class="jsfiddle" width="100%" height="80%" src="//jsfiddle.net/kalharbi/7aw3mr0e/embedded/result,html,css/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

---

# CSS Properties (I)

| CSS Property | Description |
| --- | --- |
| `color` | Sets the color of the text. |
| `background-color` | Sets the background color of an element. |
| `font-size` | Sets the size of the font. |
| `font-family` | Specifies the font face to be used. |
| `text-align` | Aligns the text within an element. |
| `margin` | Specifies the space around an element, outside of any defined borders. |
| `padding` | Specifies the space between the content of an element and its border. |

---

# CSS Properties (II)

| CSS Property | Description |
| --- | --- |
| `border` | Sets the border around an element. |
| `border-radius` | Defines the radius of the element's corners. |
| `width` | Sets the width of an element. |
| `height` | Sets the height of an element. |
| `display` | Specifies how an element should be displayed (block, inline, flex, grid, etc.). |
| `position` | Specifies the type of positioning for an element (static, relative, absolute, fixed, sticky). |
| `opacity` | Sets the opacity level for an element. |

---

# CSS Properties (III)

| CSS Property | Description |
| --- | --- |
| `transition` | Specifies the speed curve of the transition effect. |
| `transform` | Applies a 2D or 3D transformation to an element. |
| `overflow` | Specifies what should happen if content overflows an element's box. |
| `float` | Specifies how an element should float. |
| `clear` | Specifies on which sides of an element floating elements are not allowed to float. |
| `visibility` | Specifies whether or not an element is visible. |
| `line-height` | Sets the height of a line. |

---

# CSS Comments

- Comments in CSS start with `/*` and end with `*/` and can span multiple lines.
- Comments are ignored by the browser, so they don't affect how the CSS is applied.

```css
h1 {font-color: red;} /* This is a CSS comment */
```

---

# The CSS Box Model (II)

## Content, Padding, Border, and Margin

<br>

- The CSS Box Model is a fundamental concept in CSS that defines how elements are rendered on the screen.
- Each element is represented as a rectangular box, with the box's **content**, **padding**, **border**, and **margin**.
- The **content** box contains the actual content of the element, such as text or an image.
- The **padding** box represents the space between the content and the border.
- The **border** box is the line that goes around the element (padding and content).
- The **margin** box is the space around the border. 

---

# The CSS Box Model (II)

<img src="/images/css-box-model.svg" height="100px">


# CSS Units
...

