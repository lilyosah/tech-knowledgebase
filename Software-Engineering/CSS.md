# CSS
%%
#topic
#concept
**Related:**
-  

%%

Style [[HTML]] with CSS

Link CSS stylesheets to your HTML pages using a link tag.

Ex: `<link rel="stylesheet" href="mystyle.css" type="text/css">`

Cascading order of application of styles:

1. Internal style tag
2. Style tag
3. External stylesheet 

More specific rules apply if there are less specific rules

## CSS syntax
- CSS syntax has a selector and a declaration
- Declarations are made of properties and values

```css
p {
	color: pink;
}
```

### Targeting multiple tags
```css
h1, h2, h3 {
	color: pink;
}
```

### Targeting by ID
You can specify an `id` attribute for HTML elements and then select it by using a hashtag. This ID must be unique on the page

```css
#my-id {
	color: pink;
}
```

### Targeting by class
You can specify a `class` attribute for HTML elements and then select it in CSS by using a period. This class can and probably should be repeated several times in a HTML page
```css
.my-class {
	color: pink;
}
```

To target classes of a certain type
```css
h1.my-class {
	color: pink;
}
```

### Targeting child/descendant tags
To target one type of a HTML tag within another type of HTML tag **anywhere** inside

*Targets h1 tags inside article tags*
```css
article h1 {
	color: pink;
}
```

To target only the **direct** children, use `>`
```css
article>h1 {
	color: pink;
}
```

### Targeting siblings
`~` selector

## Changing the page layout

- ==Content:== The actual content
- ==Padding:== Space between content and border
- ==Border:== Drawn border
- ==Margin:== Space between border and other boxes' margins


### Positioning
==Static:== positioned in normal flow
==Fixed:== measured against the frame of the browser window 
==Relative:== positioned relative to its normal position. Can be used to create overlapping elements
==Absolute:== positioned relative to the first parent element that has a position other than static 

### CSS Grid
Requires using a container element with a `display: grid;` CSS property and `grid-template-columns: ;` and/or `grid-template-rows: ;` and/or the other way of specifying them using a grid looking property. 