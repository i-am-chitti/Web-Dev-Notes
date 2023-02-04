---
title: JS for Web
created: '2021-05-29T09:07:47.873Z'
modified: '2022-03-27T12:25:55.025Z'
---

# JS for Web

## Javascript foundation

1. Execution context
At the start of a js thread, there is one context available i.e global object(also referenced with `this`). In browser global object is `window` and in node, it is `global` itself.

2. Lexical environment
Lexical scope(available data + variables where the function was defined) determines our available variables. Not where the function is called(dynamic scope). Everytime we create a function, a new lexical scope created.

3. Hoisting


### Defer Attribute

  ```
  <script src="example.js" defer></script> 
  ```
  * It specifies that script should be executed after HTML file is completely parsed. So, it delays the execution. It is useful when a script contains functionality that requires interaction with DOM

### Async Attribute

  * It loads and executes the script asynchrously. It means that script will not wait until the entire page is parsed; it will execute immediately after it has been downloaded. 
  * It is useful for scripts that are independent of other scripts. If it doesn't matter exactly at which point script file is executed, then it is the most suitable option.


## DOM

The Document Object Model, abbreviated DOM, is a powerful tree-like structure that allows programmers to conceptualize hierarchy and access the elements on a web page.

The DOM is a logical tree-like Model that organizes a web page’s HTML Document as an Object.

__Note__: There are other types of documents, such as XML and SVG, that are also modeled as DOM structures.

![DOM Strucutre](./dom_structure.png)


#### ```.querySelector()```

  The ```.querySelector()``` method allows us to specify a CSS selector and then returns the first element that matches that selector.
  ```
  document.querySelector('p');
  document.getElementById('bio').innerHTML = 'The description';
  ```

### Styling an element

  ```
  let blueElement = document.querySelector('.blue');
  blueElement.style.backgroundColor = 'blue';
  ```
  __NOTE__ : Unlike CSS, the DOM style property does not implement a hyphen such as background-color, but rather camel case notation backgroundColor

### Create and Insert Elements

  ```
  let paragraph = document.createElement('p'); //creates an empty element
 
  paragraph.id = 'info'; // assigns an id
  
  paragraph.innerHTML = 'The text inside the paragraph'; //sets innerHTML
  
  document.body.appendChild(paragraph); //inserts it at last
  ```

### Remove an element
  ```
  let paragraph = document.querySelector('p');
  document.body.removeChild(paragraph);

  document.getElementById('sign').hidden = true; // just hides it when loaded initially

  let child = document.getElementById('oaxaca');
  let parent = document.getElementById('more-destinations');
  parent.removeChild(child);
  ```

### onclick interactivity to buttons
  ```
  let element = document.querySelector("button");

  function turnButtonRed (){
    element.style.backgroundColor = 'red';
    element.style.color = 'white';
    element.innerHTML = 'Red Button';
  }

  element.onclick = turnButtonRed;
  ```

### Traversing the DOM 
  ```
  let first = document.body.firstChild; //first child of body element
  first.innerHTML = 'I am the child!'; 
  first.parentNode.innerHTML = 'I am the parent and my inner HTML has been replaced!'; //parent node of first i.e, body
  ```

### Event Handler Registration
  ```
  let eventTarget = document.getElementById('targetElement');
 
  eventTarget.addEventListener('click', function() {
    // this block of code will run when click event happens on eventTarget element
  });
  ```
  Event Handlers can also be registered by setting an ```.onevent``` property on a DOM element (event target). 
  ```
  eventTarget.onclick = eventHandlerFunction;
  ```

### Event Bubbling or Event Capturing?

There are two ways of event propagation in the HTML DOM, bubbling and capturing.

Event propagation is a way of defining the element order when an event occurs. If you have a `<p>` element inside a `<div>` element, and the user clicks on the `<p>` element, which element's "click" event should be handled first?

In bubbling the inner most element's event is handled first and then the outer: the `<p>` element's click event is handled first, then the `<div>` element's click event.

In capturing the outer most element's event is handled first and then the inner: the <div> element's click event will be handled first, then the <p> element's click event.

With the `addEventListener()` method you can specify the propagation type by using the "`useCapture`" parameter:

```
addEventListener(event, function, useCapture);
```

The default value is false, which will use the bubbling propagation, when the value is set to true, the event uses the capturing propagation.


For example:
```
document.getElementById("myP").addEventListener("click", myFunction, true);
document.getElementById("myDiv").addEventListener("click", myFunction, true);
```

### Event Handler Removal

  ```
  eventTarget.removeEventListener('click', eventHandlerFunction);
  ```
  Because there can be multiple event handler functions associated with a particular event, ```.removeEventListener()``` needs both the exact event type name and the name of the event handler you want to remove.

  __NOTE__ : If ```.addEventListener()``` was provided an anonymous function, then that event listener cannot be removed.

### Event Object Properties
  Events are stored as objects. When an event is triggered, the event object can be passed as an argument to the event handler function.
  Some of the properties of event objects are:
  1. ```.target``` : it references the element that the event is registered to.
  2. ```.type``` : access the name of event
  3. ```.timestamp``` : no of milliseconds that passed since document loaded and event was triggered.

  ```
  let sharePhoto = function(event) {
    event.target.style.display = 'none';
    text.innerHTML = event.timeStamp;
  }

share.onclick = sharePhoto;
  ```

  
