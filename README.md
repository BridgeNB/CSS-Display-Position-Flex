## Introduction
When I was developping web application, how to display and position element in a webpage is always confusing. So I want to share how to well position elements through css in this blog. Hope it will be helpful!
## Table of Contents
1. Position and z-index
2. Inline and Block display
3. Float
4. Flex Layout
5. Serverval Common Layout
## Content
### 1. Position and z-index
First of all, the browser will render the html elements without css from left to right, top to bottom, which is called the flow of elements in the document. In order to change the position of the elements, we have to use css position property. First key words I am going to talk about is <strong>position</strong>. There are three ways to use position:
- <strong>relative</strong>: Means this element is relative to its position.
- <strong>absolute</strong>: Means this element is pinned to any part of the page, but the element can still move out of view when the page is scrolled.
- <strong>fixed</strong>: Means this element is pinned to any part of the page, but unlike to absolute, it will remain the view no matter how page scrolled.
Normally, header position will be fixed, written like this:
```css
header {
  position: fixed
}
```
Most div or class objects should be relative with valid offset, so the css be like this:
```css
.question {
  position: relative
  top: 32px;
  bottom: 10px;
}
```
<strong>Z-index</strong> will indicate how element should be set along the z-index, given an example:
```css
.box-top {
  positon: relative;
  z-index: 2;
}
.box-bot {
  position: relative;
  left: 20px;
  z-index: 1;
}
```
then brower will render it like
![z-index.png](https://c1.staticflickr.com/5/4702/39574938564_f97ed1decf_o.png)
As you can see, .box-top element is above .box-bot because it has larger z-index value.
### 2. Inline, Block and Inline-Block Display
Inline display:

```html
<strong></strong> <h1>...<h6> <a> <em>
<!--They are all inline display so they can share the same line-->
```

Block display:

```html
<p> <div> <footer> <header>
<!--They are all block display so they cannot share the same line-->
```

Inline-block display:

```html
<div style="display: inline-block;"></div>
<!--Use this display property, element can share both features from inline and block.-->
```

### 3. Flex Layout
However, float, display, and position these features are very confusing. There is another useful css layout called Flex can help you do more.
So in this blog, I will cover flex fundamentals so you can create several useful css layout.
  1. **Basic concept**
  Before learn hwo to layout, we have to know some basic fundemantals about Flex that are shown in below image.
  ![Flex-fundemental.png](https://c1.staticflickr.com/5/4672/39388873395_fb8de41b55_b.jpg)
As we can see, in the flex container, there are **two axis - main axis and cross axis**. Each unit in flex container called **flex item** with their own **main size** and **cross size**
  - **Flex container**
  Before achieve any flex layout, we have to create a **flex container** (In this case, we create a container named container). Anything could be a container and all elements in this container could be layouted by flex. Container defined as follows with six custimized features:

  ```css
  .container {
    display: flex | inline-flex; // 1
    flex-direction: row | row-reverse | column | column-reverse; // 2
    flex-wrap: nowrap | wrap | wrap-reverse; // 3
    flex-flow: nowrap | wrap | wrap-reverse; // 4
    justify-content: flex-start | flex-end | center | space-between | space-around; // 5
    align-items: flex-start | flex-end | center | baseline | stretch; // 6
    align-content: flex-start | flex-end | center | space-between | space-around | stretch; // 7
  }
  ```

  There is two options for display - flex for div elements and incline-flex for inline elements.
  **Watch out: when apply flex layout, all float, clear, vertical-align features will be disabled for all childern elements under this container.**
  1. **display**: create a flex container
  2. **flex-direction**: decide main axis direction
  3. **flex-wrap**: decide if space is not enough, switch lane or not
  4. **flex-flow**: combine with flex-direction and flex-wrap
  5. **justify-content**: define how items align along main axis
  6. **align-items**: define how items align along cross axis
  7. **align-content**: define how items align when there is multiple axis

 - **Flex item**
  Flex item can have six features to well position items

  ```css
  .item {
    order: <integer>; // 1
    flex-basis: <length>; // 2
    flex_grow: <number>; // 3
    flex_shrink: <number>; // 4
    flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]; // 5
    align-self: auto | flex-start | flex-end | center | baseline | stretch; // 6
  }
  ```
  1. **order**: define the order of items arranged in the container, smaller number comes first, default value set to 0 but you can set negative value.
  2. **flex-basis**: set basic space the item took before flex-grow and flex-shrink, default value set to auto;
  3. **flex-grow**: define how item can be zoomed;
  4. **flex-shrink**: define how item can be shrinked;
  5. **flex**: a short-cut to combine flex-grow, flex-shrink and flex-basis
  6. **align-self**: allow a single item with different alignment to others.

After understanding above features, we can create layout with just a couple lines of codes - much easier than the combinition of float and positions.

Here are some examples:

1. **Grid Layout**
![grid-layout.png](https://c1.staticflickr.com/5/4678/39592974324_cc0608ac46_b.jpg)

**Html snippet:**
```html
<div class="first-grid">
  <div class="Grid-cell">1/2</div>
  <div class="Grid-cell">1/2</div>
</div>
<div class="second-grid">
  <div class="Grid-cell">1/3</div>
  <div class="Grid-cell">1/3</div>
  <div class="Grid-cell">1/3</div>  
</div>
<div class="third-grid">
  <div class="Grid-cell">1/4</div>
  <div class="Grid-cell">1/4</div>
  <div class="Grid-cell">1/4</div>
  <div class="Grid-cell">1/4</div>
</div>
<div class="fourth-grid">
  <div class="Grid-cell">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</div>
  <div class="Grid-cell">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</div>
</div>
```

**Css snippet:**
```css
* {
  box-sizing: border-box;
}

html, body {
  height: 100%;
}

body {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-content: center;
  background: linear-gradient(top, #222, #333);
}

[class$='cell'] {
  margin: 16px;
  padding: 4px;
  border-radius: 2%;

  display: flex;
  justify-content: center;
  align-items: center;
}

[class$='grid'] {
  display:flex;
  flex-direction: row;
  justify-content: center;
  align-items: stretch;
}


.first-grid .Grid-cell {
  background: aqua;
  flex: 1;
}

.second-grid .Grid-cell {
  background: orange;
  flex: 1;
}

.third-grid .Grid-cell {
  background: lightgreen;
  flex: 1;
}

.fourth-grid .Grid-cell {
  background: lightgrey;
  flex: 1;
}
```

**You can find source code in grid-layout folder in github repository.**

2. **Percentage layout**
![percentage-layout.png](https://c1.staticflickr.com/5/4713/38495228310_1d0feda364_b.jpg)

**Html snippet**

```html
<div class="First-Grid">
  <div class="Grid-cell u-1of4">1/2</div>
  <div class="Grid-cell">auto</div>
  <div class="Grid-cell u-1of3">auto</div>
</div>
<div class="Second-Grid">
  <div class="Grid-cell">auto</div>
  <div class="Grid-cell u-1of3">1/3</div>
</div>
<div class="Third-Grid">
  <div class="Grid-cell u-1of4">1/4</div>
  <div class="Grid-cell">auto</div>
  <div class="Grid-cell u-1of3">1/3</div>
</div>
```

**Css snippet**

```css
* {
  box-sizing: border-box;
}

html, body {
  height: 100%;
}

body {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-content: center;
  background: linear-gradient(top, #222, #333);
}

[class$='Grid'] {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.Grid-cell {
  display: flex;
  flex: 1;
  margin: 16px;
  padding: 2px;
  boarder: 5px solid black;
  justify-content: center;
}

.Grid-cell.u-full {
  flex: 0 0 100%;
}

.Grid-cell.u-1of2 {
  flex: 0 0 50%;
}

.Grid-cell.u-1of3 {
  flex: 0 0 33.3333%;
}

.Grid-cell.u-1of4 {
  flex: 0 0 25%;
}

.First-Grid .Grid-cell{
  background: aqua;
}

.Second-Grid .Grid-cell{
  background: orange;
}

.Third-Grid .Grid-cell{
  background: lightgreen;
}
```

3. **Holy Grail Layout**
![holy-grail-layout.png](https://c1.staticflickr.com/5/4626/39592974504_19206bdf54_b.jpg)

**Html snippet**

```html
<div class="header">This is a header</div>
<div class="HolyGrail-body">
  <div class="nav">This is Nav</div>
  <div class="content">This is content</div>
  <aside class="aside">This is aside</aside>
</div>
<div class="footer">This is a footer</div>
```

**scss snippet**

```scss

body {
  display: flex;
  flex-direction: column;
  height: 100%;
  min-height: 100vh;

  .header, .footer {
    width: 100%;
    height: 40px;
    background: grey;
    text-align: center;
  }

  .HolyGrail-body {
    flex: 1 0 auto;
    display: flex;
    .content {
      flex: 1;
      background: lavenderBlush;
      text-align: center;
    }
    .nav, .aside {
      flex: 0 0 12em;
    }
    .nav{
      width: 100px;
      order: -1;
      background: lightcyan;
    }
    .aside{
      width: 100px;
      background: lightCoral;
    }
  }
}
```

4. Input layout
![input-layout.png](https://c1.staticflickr.com/5/4664/39592974564_5bcddc93d8_o.png)

**Html snippet**

```html
<div class="InputAddOn">
  <span class="InputAddOn-item">This a hint</span>
  <input class="InputAddOn-field">
  <button class="InputAddOn-item">button</button>
</div>
```

**Css snippet**

```css
.InputAddOn {
  display: flex;
  width: 20%;
}

.InputAddOn-field {
  flex: 1;
}
```

## Conclusion
In this blog, we should how position and float work in layout. Most importantly, we can also display and postion our html elements in a proper way with fewer code by using flex.
## Code Reference
https://github.com/BridgeNB/CSS-Display-Position-Flex.git
