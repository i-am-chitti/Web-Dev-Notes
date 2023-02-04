---
title: Single Page Application
created: '2021-06-19T12:34:45.742Z'
modified: '2021-06-19T12:36:26.615Z'
---

# Single Page Application

Wikipedia defines a single-page application (SPA) as “a web application that interacts with the web browser by dynamically rewriting the current web page with new data from a web server, instead of the default method of the browser loading entire new pages.” The name single-page application generally refers to the application consisting of one page that is constantly updated by JavaScript. Requests to the server are now quicker since they contain just the data needed to update the view. SPAs are full applications, running in the browser yet still connected to a server to update any application data.

### Pros
* SPAs are fast. The main selling point of a SPA is that it feels like a desktop or mobile application. By eliminating requests for new files and only relying on smaller amounts of data from the server, SPAs provide a real-time interface with their users.
* Reuse of code is a big bonus when using SPAs because it saves time within a project and across multiple projects. Many SPA libraries and frameworks advise that components be general enough that they can be reused from project to project.
* SPAs provide an easier path to migrate code to a mobile application. With a SPA, the back-end of the application feeds data to the decoupled front-end interface. This separation of tasks allows the creation of a mobile app UI while maintaining the back-end logic of the application.

### Cons
* SPAs require more files to run at startup so the load time of the application can be longer. This is something to consider if a user will not want to visit a site that takes too long to load. SPA load time can be minimized through strategically loading resources throughout the run of an application.
* Search Engine Optimization (SEO) has some pitfalls when it comes to SPAs. Search engines, like Google or DuckDuckGo, index pages of a website to rank the content. This can be difficult with only one page that may not have content until it is loaded by JavaScript. SEO is an ever-changing world so strategies already exist to mitigate these downsides.
* SPAs may not function as expected within the browser. For example, the back button or browsing history can act differently while using a single-page application. This can be frustrating for users who are expecting certain functionality within their browsers.
