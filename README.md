# Easy Node Creator

Hello and welcome to the **Easy Node Creator**! This is a simple set of functions designed to do one thing: Make your Javascipt-generated HTML easier to write. At the very least, there should be quite a few less lines of code! After having to use .appendChild() and .classList.add() far too many times, I decided it was time to write some functions to abstract and clean up the code.

## How to Use

As the code is written, the JS file is accessed via export/import: 

1. The export statement is already present at the end of the **module-node-creator.js** file:
`export {nodePlainCreator, nodeTextCreator, nodeClassCreator, nodeTextClassCreator, nodeLinkClassTextCreator, nodeImgSrcAlt};`
2. You'll need to add an *import* statement at the beginning of any JS file you want to use these functions in:
`import {nodePlainCreator, nodeTextCreator, nodeClassCreator, nodeTextClassCreator, nodeLinkClassTextCreator, nodeImgSrcAlt} from './module-node-creators.js';`
3. The html `<script>` tag that references your JS file will need to have `type="module"` as an attribute:
```
<head>
    <script src="./your-file.js" type="module"></script>
</head>
```

Another way to use the functions is to copy and paste them into your JS file directly. 

## The Functions

The JS file comes with a few functions, which I highly encourage you to modify to your liking. Each function **return**s the created node, which comes in handy for any modifications and event listeners (*more on this in the next README section*).

1. `nodePlainCreator(type, parent)` - Creates an element of the provided type, and appends it to the parent node.
2. `nodeTextCreator(type, parent, text)` - Creates an element of the provided type, appends it to the parent node, and adds text to the new element. The new text is added via `.createTextNode()`, not `.innerHTML`.
3. `nodeClassCreator(type, parent, classes)` - Creates an element of the provided type, adds classes to the new element, and appends it to the parent node.
4. `nodeTextClassCreator(type, parent, text, classes)` - Creates an element of the provided type, adds classes to the new element, inserts a text node into the new element, and appends it to the parent node.
5. `nodeLinkClassTextCreator(parent, text, link, classes)` - Creates an `<a>` element, appends it to the parent, adds text to the link, adds the `href` value, and adds a class. If the class argument is left blank or is an empty string, no class attribute is added to the created `<a>` element;
6. `nodeImgSrcAlt(parent, source, alternate)` - Creates an `<img>` element. The image's `src=""` attribute is filled by the string provided in *source*, and the alt text is populated by the *alternate* argument. The `<img>` element is appended to the parent node. 

For each function, the arguments are formatted as follows:
-**type** - a string representing the element type. For example, `'div'`
-**parent** - a reference to the parent node. This could be written as `document.getElementById('id')`, or can refer to a variable that references the node: 
```
const nodeWithId = document.getElementById('id');
nodePlainCreator('div', nodeWithId);
```
-**text** - a string of text, such as `'hello'`;
-**classes** - a string of classes. These should be written with the same syntax used in an HTML attribute: `'class1 class-two funnyname'`
-**link** - a string containing information on a link/path. Write this string in the same manner you'd write the `href=""` attribute, such as: `'www.google.com'` for external links, or `'#nifty-id'` for internal links.
-**source** - a string containing information on a source path. Write this string in the same manner you'd write the `src=""` attribute in the final HTML document, such as: `'./images/nifty-image.jpg'`.
-**alternate** - a string that will populate the `alt=""` attribute, such as `'A beautiful sunset over the ocean'` 

## A Demonstration

Each function can be called on its own, without assigning it to any variable. It will parse in the same order you'd expect your JS document to parse - so keep that in mind for the order in which children are appended to parents. 

`nodeClassCreator('nav', headerNode, 'site-nav-wide');` - This creates the HTML element `<nav class="site-nav-wide"></nav>` and appends it to `headerNode`.

You can assign the function to a variable. The function returns the newly created node, allowing you to add modifiers as you normally might in JS.

```
let headerNode = document.getElementsByTagName('header')[0];
let containerNav = nodeClassCreator('nav', headerNode, 'site-nav-wide');
containerNav.style.width = '100px';
```

This will create a new `<nav>` element, append it to the `<header>` element, add the 'site-nav-wide' class, and apply an inline-style `width: 100px` to the nav. The new **containerNav** element can be referenced just like after using `let containerNav = document.createElement('nav');`
