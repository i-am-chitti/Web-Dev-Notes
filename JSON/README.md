---
title: JSON
created: '2021-06-16T15:51:22.887Z'
modified: '2021-06-16T16:28:27.490Z'
---

# JSON

JSON, or JavaScript Object Notation, is a popular, language-independent, standard format for storing and exchanging data.It has become the de facto standard that facilitates storing and sending data between all programming languages.

## JSON syntax

```
{
  "student": {
    "name": "Rumaisa Mahoney",
    "age": 30,
    "fullTime": true,
    "languages": [ "JavaScript", "HTML", "CSS" ],
    "GPA": 3.9,
    "favoriteSubject": null
  }
}
```
Note the following syntax rules for JSON:

* The curly braces, `{..}`, hold objects.
* The square brackets, `[..]`, hold arrays.
* Data is stored in name-value pairs separated by a colon, `:`.
* Every name-value pair is separated from another pair by a comma, `,`. Similarly, every item in an array is delimited by a comma as well. Trailing commas are forbidden.
* JSON property names must be in double-quoted `(" ")` text even though JavaScript names do not hold by this stringency.

## JSON Data Types

A JSON data type must be one of the following:
* string (double-quoted)
* number (integer or floating point)
* object (name-value pair)
* array (comma-delimited)
* boolean (true or false)
* null

### Difference between JSON object and Javascript Object

1. The name portion in each JSON name-value pair and all string values must be enclosed in double-quotes while this is optional in JavaScript.
2. JavaScript accepts string values that are single or double-quoted, however, there exists JavaScript coding guidelines that prefer one style over another.

## Reading a JSON String
Each programming language has its own mechanism to handle this conversion. In JavaScript, for example, we have a built-in JSON class with a method called ```.parse()``` that takes a JSON string as a parameter and returns a JavaScript object.
```
const jsonData = '{ "book": { "name": "JSON Primer", "price": 29.99, "inStock": true, "rating": null } }';
 
const jsObject = JSON.parse(jsonData);
 
console.log(jsObject);
```

Output
```
{
  book: { name: 'JSON Primer', price: 29.99, inStock: true, rating: null }
}
```

## Writing JSON string
In JavaScript, we would use the built-in JSON class method, `.stringify()` to transform our JavaScript object to a JSON string.
```
const jsObject = { book: 'JSON Primer', price: 29.99, inStock: true, rating: null };
const jsonData = JSON.stringify(jsObject);
console.log(jsonData);
```

Output
```
{ "book": "JSON Primer", "price": 29.99, "inStock": true, "rating": null }
```
