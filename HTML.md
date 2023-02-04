---
title: HTML
created: '2021-05-27T12:34:32.922Z'
modified: '2021-06-20T06:59:40.776Z'
---

# HTML

### ```<html>``` tag

```
<!DOCTYPE html>
<html>
 
</html>
```

* The ```<!DOCTYPE html>``` declaration provides the browser with two pieces of information (the type of document and the HTML version to expect), but it doesn’t actually add any HTML structure or content.

* Anything between the opening ```<html>``` and closing ```</html>``` tags will be interpreted as HTML code. Without these tags, it’s possible that browsers could incorrectly interpret your HTML code.


### ```<head>``` tag

* The <head> element contains the metadata for a web page. Metadata is information about the page that isn’t displayed directly on the web page. Unlike the information inside of the <body> tag, the metadata in the head is information about the page itself.


### Semantic HTML

* Semantic = Relating to Meaning
* we select HTML elements based on their meaning, not on how they are presented.
* Elements such as ```<div>``` and ```<span>``` are not semantic elements since they provide no context as to what is inside of those tags.
* WHY Semantic: 
  1. Accessibility: accessible for mobile devices and for people with disabilities as well. This is because screen readers and browsers are able to interpret the code better.
  2. SEO
  3. Easy to understand
* ```<div>``` is not a semantic tag because it doesn't provide any context of what content is inside.

* Semantic HTML Elements
  1. ```<header>``` : Container usually for either navigational links or introductory content containing headings.
  2. ```<main>``` : Main is the container for main content of a website.
  3. ```<section>``` : A webpage is divided into several sections that are independent to each other and share properties in itself.
  4. ```<article>``` : It contains the content that makes sense on its own. e.g articles, blog, comments, etc.
  ```
  <section>
    <h2>Fun Facts About Cricket</h2>
    <article>
      <p>A single match of cricket can last up to 5 days.</p>
    </article>
  </section>
  ```
  5. ```<aside>``` : mark additional information. e.g bibliographies, endnotes, comments, etc
  6. ```<figure>``` and ```<figcaption>``` : Container for image
  7. ```<audio>```
  ```
  <audio>
    <source src="iAmAnAudioFile.mp3" type="audio/mp3">
  </audio>
  ```
  8. ```<video>``` and ```<embed>``` : video can only be used for video while embed can be used for any type of media.

## HTML Forms

  * Range Input
    ```
    <form>
      <label for="volume"> Volume Control</label>
      <input id="volume" name="volume" type="range" min="0" max="100" step="1">   // step is number by which input increases/decreases at a time
    </form>
    ```

  * Checkbox input

    ```
    <form>
      <p>Choose your pizza toppings:</p>
      <label for="cheese">Extra cheese</label>
      <input id="cheese" name="topping" type="checkbox" value="cheese">
      <br>
      <label for="pepperoni">Pepperoni</label>
      <input id="pepperoni" name="topping" type="checkbox" value="pepperoni">
      <br>
      <label for="anchovy">Anchovy</label>
      <input id="anchovy" name="topping" type="checkbox" value="anchovy">
    </form>
    ```

  * Radio Button Input
    we can have multiple checkboxes but only one radio button
    ```
    <form>
      <p>What is sum of 1 + 1?</p>
      <input type="radio" id="two" name="answer" value="2">
      <label for="two">2</label>
      <br>
      <input type="radio" id="eleven" name="answer" value="11">
      <label for="eleven">11</label>
    </form>
    ```
  * Dropdown List
    ```
    <form>
      <label for="lunch">What's for lunch?</label>
      <select id="lunch" name="lunch">
        <option value="pizza">Pizza</option>
        <option value="curry">Curry</option>
        <option value="salad">Salad</option>
        <option value="ramen">Ramen</option>
        <option value="tacos">Tacos</option>
      </select>
    </form>
    ```

  * Datalist Input

      Even if we have an organized dropdown list, if the list has a lot of options, it could be tedious for users to scroll through the entire list to locate one option. That’s where using the ```<datalist>``` element comes in handy.

      ```
      <form>
        <label for="city">Ideal city to visit?</label>
        <input type="text" list="cities" id="city" name="city">
      
        <datalist id="cities">
          <option value="New York City"></option>
          <option value="Tokyo"></option>
          <option value="Barcelona"></option>
          <option value="Mexico City"></option>
          <option value="Melbourne"></option>
          <option value="Other"></option>  
        </datalist>
      </form>
      ```

  * Textarea input
    ```
    <form>
      <label for="blog">New Blog Post: </label>
      <br>
      <textarea id="blog" name="blog" rows="5" cols="30">
        Default Text
      </textarea>
    </form>
    ```

## HTML validation

  1. Using required attribute
      ```
      <form action="/example.html" method="POST">
        <label for="allergies">Do you have any dietary restrictions?</label>
        <br>
        <input id="allergies" name="allergies" type="text" required>
        <br>
        <input type="submit" value="Submit">
      </form>
      ```

  2. Set a minimum and maximum
      ```
      <form action="/example.html" method="POST">
        <label for="guests">Enter # of guests:</label>
        <input id="guests" name="guests" type="number" min="1" max="4">
        <input type="submit" value="Submit">
      </form>
      ```

  3. Checking text length

      ```
      <form action="/example.html" method="POST">
        <label for="summary">Summarize your feelings in less than 250 characters</label>
        <input id="summary" name="summary" type="text" minlength="5" maxlength="250" required>
        <input type="submit" value="Submit">
      </form>
      ```

  4. Matching a pattern

      ```
      <form action="/example.html" method="POST">
        <label for="payment">Credit Card Number (no spaces):</label>
        <br>
        <input id="payment" name="payment" type="text" required pattern="[0-9]{14,16}">
        <input type="submit" value="Submit">
      </form>
      ```
