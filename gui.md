Web GUIs
========

GUI: Graphical User Interface
-----------------------------

A GUI or _graphical user interface_ is the main way that most of us
interact with computers most of the time. The standards for graphical
computing are well known: clicking buttons and icons, scrolling windows,
reading images and text, etc. When we created our Turtle programs, we
were programming GUIs.

Most of the examples in this text, however have used _text interfaces_
or Command Line Interfaces (CLI) (or used a special web library I built
to imitate a CLI). With a CLI, the user receives computer
output through text on the screen, and sends input to the program by
entering text. In this chapter, we introduce a Javascript-based library
for creating GUIs web applications.

How the web works (the super brief version)
-------------------------------------------

There are three computer languages that form the base for any web page.
They are HTML, CSS, and Javascript. Hypertext markup language (HTML)
describes the type of content on a web page. HTML describes many different types of content. You are familiar with most of them:
- text: titles, paragraphs, lists, etc
- media: images, videos, audio, animation graphics
- links: that allow navigation to different areas of the web
- form elements: buttons, input boxes, checkboxes, and other elements that users to input information
- tables: that display grids of information

Other HTML elements are more structural, they divide web pages into sections (like headers and footers).

Cascading style sheets (CSS), control the layout of the content described by the
HTML. CSS can be used to change the font or text size, add background images to
elements, space and size different containers, and, generally create useful and
aesthetic interfaces. A single HTML document can work with different CSS styles,
allowing it to adapt to different use cases. One set of styles can control
layout for mobile phones, another for laptops, and yet another for print.

Javascript is the only **programming language** of the three languages discussed
here. It's the only of the group that uses variables and controls the flow of
execution with loops and Boolean conditions. At this point in the book, we are
familiar with many of the programming aspects of Javascript. For the web,
Javascript can interact with user input, and dynamically change the content and
HTML structure on a page. While some, small websites are **static** -- meaning
that all of the content and HTML is written by hand in a text editor -- most websites pull the content from databases or other data
files. We have begun to see how Javascript can interact with larger sets of
data, now we will see how Javascript can be used to display this data on the
web, to create **dynamic** websites that change when the data is changed.

JS Frameworks
------

Web pages *began* with simple *HTML* as a way to display documents; as the web
evolved, CSS and JavaScript were added as ways to *enhance* documents by adding
style (CSS) and interaction (JavaScript). Because of this, original approaches
to JavaScript focused on reaching into an existing webpage (HTML) and making
changes with JavaScript.

As the web has evolved to include web applications, more and more programmers flip 
this logic on its head: thinking of the application (JavaScript) first and using
it to generate HTML. Generating HTML with code is usually done using some form of
*templating language* (a language for mixing variables from your code with JavaScript).

There are *many* languages and they are constantly evolving, but in this
textbook we will use the React framework, which was open-sourced by Facebook in 2014
and has been among the most popular frameworks for nearly a decade as of this writing (2024).


JSX
--------------
The fundamental breakthrough of React is the use of JSX,  which enables programmers to write HTML-like code directly in their JavaScript files. JSX is a syntax extension for JavaScript that looks like HTML. It is used to describe what the UI should look like. JSX may remind you of a template language, but it comes with the full power of JavaScript. The only major difference between JSX and HTML is that JSX can contain JavaScript expressions inside curly braces and that all tags must be closed, which means that for tags like `<img>` and `<input>`, you must include a closing slash and write them as `<img />` and `<input />`.

React allows JavaScript programmers to build webpages out of *components*, which are really just functions that return JSX. Just as we have used functions in the *turtle*
library to produce drawings as output, we can use functions in React to produce HTML as output, resulting in a webpage as a user interface. If you know HTML, you can write React components using any HTML you know. If you don't know HTML, here is a quick reference with some basic elements you might want to create.

- `<div>`: a container for other elements.
- `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`: headers of different sizes.
- `<p>`: a paragraph.
- `<a href="URL">text</a>`: a link
- `<button>text</button>`: a button
- `<input type="text" />`: a text input box
- `<img src="URL" alt="Alternate text"/>`: an image

Note that these are the *open tags* for these elements. Each element must be closed with a corresponding *closing tag*. For example, `<div>` must be closed with `</div>`
and `<p>` must be closed with `</p>`: the text between the tags is the text that will display on the webpage. Tags that don't have text, like `<img>` and `<input>`, are self-closing and in JSX you must write them with a trailing slash like `<img />` and `<input />`.

Here's a sample React component that uses these elements:

```jsx
const HelloWorld = () => {
  return (
    <div>
      <h1>Hello, world!</h1>        
      <input type="text" />
      <button>Click me!</button>
      <p>This is a paragraph.</p>
      <img src="https://upload.wikimedia.org/wikipedia/commons/3/3a/Cat03.jpg
" alt="Cat" width="200"/>
      <a href="https://www.wikipedia.org">This is a link to Wikipedia</a>        
      
    </div>
  );
};
```

> #### Naming Components
> By convention, React *components* are nouns and start with a capital letter. That is because unlike most functions, which we think of as "actions," React functions really  stand in for an part of a webpage, so we think of them as *things* (or "Objects" to : 
use programming parlance).
> 
> In addition, it's important that React components use capital letters because React uses this convention to distinguish between HTML elements (lowercase) and React components (capitalized). 

Here is a simple example codepen:
{%include codepen.html id="dPbGBpm" height="400" %}

### Errors in React

If you have written HTML before, you may have noticed it is very *error tolerant*, meaning that if you forget to close a tag, or you use a tag that doesn't exist, the browser will usually try to render the page anyway. React is not so forgiving. If you make a mistake in your JSX, React will throw an error and stop rendering the page. This can be frustrating, but it is also a good thing, because it means that React will not render a page that is broken. Every tag that you open must be closed, and every tag must be a real HTML tag.

## Tags for Lists and Tables

In HTML, there are special tags for writing lists and tables. Here are some examples
of what plain JSX (React) code for lists and tables might look like:

### Lists

In lists, we use the outer tag `<ol>` for a numbered list (ordered) 
or `<ul>` for a bulleted list (unordered). Each item in the list is an `<li>` tag.

```jsx
const FruitList = () => (
<ul>
  <li>Apples</li>
  <li>Bananas</li>
  <li>Pears</li>
</ul>);
```

```jsx
const AfcEast = () => (
<ol>
  <li>Buffalo Bills</li>
  <li>Miami Dolphins</li>
  <li>New York Jets</li>
  <li>New England Patriots</li>
</ol>);
```

### Tables

In tables, we use the `<table>` tag to create a table, and then use `<tr>` tags to create rows. Within rows, we create cells using `<td>` tags. For header cells (typically in the first row or the first column) we can use  `<th>` tags

```jsx
const PriceChart = () => (
    <table>
      <tr>
        <th>Item</th>
        <th>Price</th>
      </tr>
      <tr>
        <td>Apples</td>
        <td>$1.00</td>
      </tr>
      <tr>
        <td>Bananas</td>
        <td>$0.50</td>
      </tr>
      <tr>
        <td>Pears</td>
        <td>$1.25</td>
      </tr>
    </table>
);
```

### Generating Lists from JavaScript Arrays

Because it is very common in programming to have a list stored in an array, React provides a special way to render lists of items. You can use the `map` function to create a list of JSX elements from a JavaScript array. Any time you have a list of JSX items, React will render them correctly. Here is an example of how you might use `map` to render the list from above:

```jsx
const FruitList = () => {
  const fruits = ["Apples", "Bananas", "Pears"];
  return (
    <ul>
      {fruits.map(fruit => <li key={fruit}>{fruit}</li>)}
    </ul>
  );
};
```

> #### Keys
> In React, when you render a list of items, you must provide a `key` attribute to each item. This is a unique identifier for each item in the list. React uses these keys to keep track of which items have changed, and to update the list efficiently. If you don't provide a key, React will print an error to the console. The key should be something unique to each item in your list.

You could also write a custom function which returns an array of JSX elements, and then use that function in your JSX. Here is an example of how you might use this to create a multiplication table.

## A Multiplication Table

```jsx
const MultiplicationTable = () => {
  const numbers = [];
  for (let i = 2; i <= 12; i++) {
    numbers.push(i);
  }
  return (
    <div>
      <h1>Multiplication Table</h1>
      <table>
        <tbody>
          {/* Header Row */}
          <tr>
            <th /> {/* Empty cell first */}
            {numbers.map((headerNumber) => (
              <th key={headerNumber}>{headerNumber}</th>
            ))}
          </tr>
          {/* Row per number */}
          {numbers.map((rowNumber) => (
            <tr key={rowNumber}>
              <th>{rowNumber}</th>
              {/* Now multiply by each number */}
              {numbers.map((colNumber) => (
                <td key={rowNumber * colNumber}>
                  {rowNumber}x{colNumber}={rowNumber * colNumber}
                </td>
              ))}
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};
```
{%include codepen.html id="jENWjer" height="400" %}

## Exercises

For the exercises here, you can start by [forking this codepen](https://codepen.io/thinkle-iacs/pen/LEPGwPX?editors=0010).

1. Write a React Component that contains a header that displays your name and a paragraph with a little information about yourself.
2. Write a React component which displays a list of your favorite hobbies.
3. Write a React component which uses an array and math to display a table of squares. The table should have a header row with the numbers 1-12, and then a row for each number from 1-12, with the squares of each number.