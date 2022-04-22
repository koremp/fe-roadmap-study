# Getting Started with React

https://nextjs.org/learn/foundations/from-javascript-to-react/getting-started-with-react

To use React in your project, you can load two React scripts from an external website called [unpkg.com](https://unpkg.com/):

* `react` is the core React library.
* `react-dom` provides DOM-specific methods that enable you to use React with the DOM.

Instead of directly manipulating the DOM with plain JavaScript, you can use the `ReactDOM.render()` method from `react-dom` to tell React to render our `<h1>` title inside our `#app` element.

```html
<!-- index.html -->
<html>
  <body>
    <div id="app"></div>

    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>

    <script type="text/javascript">
      const app = document.getElementById('app')
      ReactDOM.render(<h1>Develop. Preview. Ship. 🚀</h1>, app)
    </script>
  </body>
</html>
```

-> Syntax Error cuz `<h1></h1>` is not JSX

## What is JSX?

JSX is a syntax extension for JavaScript that allows you to describe your UI in a familiar HTML-like syntax. The nice thing about JSX is that apart from following [three JSX rules](https://beta.reactjs.org/learn/writing-markup-with-jsx#the-rules-of-jsx), you don’t need to learn any new symbols or syntax outside of HTML and JavaScript.

Note that browsers don’t understand JSX out of the box, so you’ll need a JavaScript compiler, such as a [Babel](https://babeljs.io/), to transform your JSX code into regular JavaScript.

## Adding Babel to your project

To add Babel to your project, copy and paste the following script in your `index.html` file:

```html
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

In addition, you will need to inform Babel what code to transform by changing the script type to `type=text/jsx`.

```html
<html>
  <body>
    <div id="app"></div>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <!-- Babel Script -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/jsx">
      const app = document.getElementById('app');
      ReactDOM.render(<h1>Develop. Preview. Ship. 🚀</h1>, app);
    </script>
  </body>
</html>
```


Comparing the declarative React code you just wrote:

### declarative React code

```html
<script type="text/jsx">
  const app = document.getElementById("app")
  ReactDOM.render(<h1>Develop. Preview. Ship. 🚀</h1>, app)
</script>
```

### Imperative Javascript code

```html
<script type="text/javascript">
  const app = document.getElementById('app')
  const header = document.createElement('h1')
  const headerContent = document.createTextNode('Develop. Preview. Ship. 🚀')
  header.appendChild(headerContent)
  app.appendChild(header)
</script>
```

You can start to see how by using React, you can cut down a lot of repetitive code.

And this is exactly what React does, it’s a library that contains reusable snippets of code that perform tasks on your behalf - in this case, updating the UI.

