
# Node.js #Day4: Introduction to Express.js | Creating a Server | Basic API CALL Methods



Welcome to Day 4 of our Node.js journey, where we’ll introduce you to Express.js, teach you how to create a server, and delve into some basic API call methods.

Learning programming can be daunting, but fear not. We’ll break down these concepts, providing detailed code examples with explanations to make your learning experience smooth and enlightening.

**‼️Prerequest for this tutorial article:**

Must read previous Nodejs Series Articles, Otherwise you won’t understand how thimngs are working

Previous Articles🫰:

**Nodejs Day#1:**
[**Node.js #Day 1: Unraveling File Handling Magic & Basics of Node.js**
*Day#1 Node.js: Basics of Node.js, File handling, Modules, Package.json*sandydev.medium.com](https://sandydev.medium.com/node-js-day-1-unraveling-file-handling-magic-basics-of-node-js-ccbee5e8c70c)

**Nodejs #Day2:**
[**Nodejs Day#2: Building a Basic Backend with Pure Node.js (Without Express.js)**
*Day#2 Node.js: Building Basic Backend with Pure Nodejs*sandydev.medium.com](https://sandydev.medium.com/nodejs-day-2-building-a-basic-backend-with-pure-node-js-without-express-js-8781d177454d)

**Nodejs #Day3:**
[**Nodejs #Day3: Exploring HTTP Methods — GET, POST, DELETE, PATCH, PUT, and More**
*Learn how to handle HTTP methods like GET, POST, DELETE, and PUT in Pure Node.js with practical code examples*sandydev.medium.com](https://sandydev.medium.com/nodejs-day3-exploring-http-methods-get-post-delete-patch-put-and-more-cd71449acaf2)

## Table of Contents

1. What is Express.js?

1. Creating Your First Express Server

1. Routing in Express.js

1. Handling HTTP GET Requests

1. Handling HTTP POST Requests

1. Handling HTTP PUT Requests

1. Handling HTTP DELETE Requests

1. Middleware in Express.js

1. Conclusion

1. FAQs

## What is Express.js?

Express.js, often simply referred to as Express, is a minimal and flexible Node.js web application framework.

It equips you with a robust set of features to develop web and mobile applications with ease.

Express simplifies the process of handling HTTP requests and defining routes, making it an excellent choice for web development.

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/Looa06wacy8" frameborder="0" allowfullscreen></iframe></center>

## Creating Your First Express Server

Let’s roll up our sleeves and create your first server using Express.js. Start by creating a new directory for your project and navigating to it in your terminal:

    mkdir my-express-app
    cd my-express-app

Next, initialize your project with npm:

    npm init -y

This generates a package.json file with default values. Then, install Express:

    npm install express

With Express in your toolkit, create a JavaScript file (let’s name it app.js). In this file, import Express and set up your basic server:

    const express = require('express');
    const app = express();
    const port = 3000;
    
    app.listen(port, () => {
      console.log(`Server is running on port ${port}`);
    });

Explanation:

* const express = require('express');: Here, we import the Express.js framework by requiring the 'express' module. This line ensures that you can use the Express functionalities in your code.

* const app = express();: This line initializes an instance of the Express application. The app object will be used to configure routes, handle HTTP requests, and more.

* const port = 3000;: We define a variable called port and set it to 3000. This is the port number on which your server will listen for incoming requests. You can change this number to any available port you prefer.

* app.listen(port, () => { ... });: This line starts your Express server and makes it listen on the specified port. When a client makes a request to this port, the code inside the arrow function gets executed. In this case, it logs a message to the console indicating that the server is running on the chosen port.

## Routing in Express.js

Now, let’s explain how routing works in Express.js.

    app.get('/hello', (req, res) => {
      res.send('Hello, Express!');
    });

Explanation:

* app.get('/hello', ...: This code defines a route for handling HTTP GET requests to the '/hello' URL. When a client (like a web browser) sends a GET request to your server with '/hello' in the URL, this route will be triggered.

* (req, res) => { ... }: Just like before, this part is a callback function. It takes two parameters: req (the request object) and res (the response object).

* res.send('Hello, Express!');: When this route is triggered, it sends the string 'Hello, Express!' as the response to the client. This could be a web page, an API response, or any other data you want to send.

## Handling HTTP GET Requests

![](https://cdn-images-1.medium.com/max/2560/1*IBeEibVhTBcDqPqO2uwmUA.png)

In this section, we’ll delve into the code that handles HTTP GET requests.

    const items = ['item1', 'item2', 'item3'];
    
    app.get('/items', (req, res) => {
      res.json(items);
    });

Explanation:

* const items = ['item1', 'item2', 'item3'];: At the beginning of this code, an array named items is defined. This array contains some sample items, which you might imagine as data you want to serve via your API.

* app.get('/items', ...: This code defines a new route that listens for HTTP GET requests with the URL path '/items'. When a client sends a GET request to this endpoint, the code inside the callback function is executed.

* (req, res) => { ... }: Just like before, this part is a callback function. It takes two parameters: req (the request object) and res (the response object).

* res.json(items);: When a GET request is made to '/items', this line of code responds to the client by sending the items array as a JSON response. The .json() method serializes the JavaScript array into JSON format, making it suitable for transferring data over the web.

This example demonstrates how to handle GET requests and send JSON data as a response.

## Handling HTTP POST Requests

Next, let’s explain how to handle HTTP POST requests:

    app.post('/items', (req, res) => {
      const newItem = req.body.item;
      items.push(newItem);
      res.json(items);
    });

Explanation:

* app.post('/items', ...: This code defines a route for handling HTTP POST requests to the '/items' URL. It expects clients to send data to this endpoint to create a new item.

* (req, res) => { ... }: The callback function receives the req (request) and res (response) objects.

* const newItem = req.body.item;: In this line, we extract the 'item' property from the request body. When clients send POST requests, they often include data in the request body. Here, we assume that the client sends an object with an 'item' property in the request body.

* items.push(newItem);: The extracted 'newItem' is then pushed into the 'items' array, effectively adding a new item to the collection.

* res.json(items);: Finally, the updated 'items' array is sent back as a JSON response to the client, confirming that the new item has been added.

This code illustrates how to handle POST requests to create new data resources in your API.

## Handling HTTP PUT Requests

Now, let’s explore how to handle HTTP PUT requests:

    app.put('/items/:id', (req, res) => {
      const itemId = req.params.id;
      const updatedItem = req.body.item;
    
      // Update the item with the provided ID
      items[itemId] = updatedItem;
      res.json(items);
    });

Explanation:

* app.put('/items/:id', ...: This code defines a route for handling HTTP PUT requests to '/items/:id'. The ':id' part is a URL parameter, which allows you to specify the ID of the item you want to update.

* (req, res) => { ... }: As usual, this is the callback function that executes when the route is triggered. It takes the req (request) and res (response) objects.

* const itemId = req.params.id;: Here, we retrieve the value of the ':id' parameter from the URL using req.params.id. This value represents the unique identifier of the item you want to update.

* const updatedItem = req.body.item;: Similarly to the POST request example, we extract the 'item' property from the request body. This is assumed to contain the updated data for the item.

* items[itemId] = updatedItem;: The code then updates the item in the 'items' array with the provided ID (itemId) with the new data (updatedItem).

* res.json(items);: Finally, it sends the updated 'items' array as a JSON response to confirm that the item has been successfully updated.

This code illustrates how to handle PUT requests to modify existing data resources.

## Handling HTTP DELETE Requests

Now, let’s dive into the code for handling HTTP DELETE requests:

    app.delete('/items/:id', (req, res) => {
      const itemId = req.params.id;
    
    // Remove the item with the provided ID
      items.splice(itemId, 1);
      res.json(items);
    });

Explanation:

* app.delete('/items/:id', ...: This code defines a route for handling HTTP DELETE requests to '/items/:id'. As before, ':id' represents the unique identifier of the item to delete.

* (req, res) => { ... }: The callback function receives the req (request) and res (response) objects.

* const itemId = req.params.id;: It retrieves the ':id' parameter from the URL, identifying the item to be deleted.

* items.splice(itemId, 1);: The code uses the splice method to remove the item from the 'items' array based on its index (itemId). The second argument '1' specifies that we want to remove one item at that index.

* res.json(items);: Finally, it sends the updated 'items' array as a JSON response to confirm that the item has been successfully deleted.

This code demonstrates how to handle DELETE requests to remove data resources from your API.

## Exploring Middleware in Express.js

Middleware in Express.js is a powerful concept that allows you to perform various tasks within your application’s request-response cycle.

It acts as a bridge between the incoming request and the final response, enabling you to add functionality like authentication, logging, data parsing, and much more.

Let’s take a closer look at how middleware works and provide an example using the JSON parsing middleware.

Middleware functions in Express.js are essentially functions that have access to the request (req) and response (res) objects.

They can execute code, modify request and response objects, end the request-response cycle, or call the next middleware function in the stack. This modular and flexible approach makes Express.js incredibly versatile.

### JSON Parsing Middleware Example

One commonly used middleware is the JSON parsing middleware, which is responsible for parsing JSON data sent in the request body.

Here’s an example of how to use the JSON parsing middleware in Express.js:

    const express = require('express');
    const bodyParser = require('body-parser'); // Middleware for parsing JSON
    
    const app = express();
    const port = 3000;
    // Middleware to parse JSON data
    app.use(bodyParser.json());
    // Route that uses JSON data
    app.post('/api/postData', (req, res) => {
      const data = req.body; // Parsed JSON data
      // Process the data and send a response
      res.json({ message: 'Data received and processed successfully', data });
    });
    app.listen(port, () => {
      console.log(`Server is running on port ${port}`);
    });

In this example, we’ve incorporated the body-parser middleware using app.use(bodyParser.json()). This middleware parses JSON data from the request body and makes it accessible via req.body. We then have a route (/api/postData) that uses this parsed JSON data.

### Going Deeper into Middlewares

This is just a glimpse of what middleware can do in Express.js.

In a dedicated tutorial on middlewares, we will explore this topic in-depth. We’ll cover how to create custom middlewares, delve into advanced use cases, and show you how middleware can enhance the functionality and security of your Express.js applications.

Stay tuned for our upcoming tutorial on Express.js middlewares, where we’ll provide comprehensive insights and practical examples to level up your Express.js development skills.

If you have specific questions or requests regarding middlewares, please feel free to share, and we’ll ensure they are addressed in our upcoming tutorial.

<iframe src="https://medium.com/media/2ef5cb5944bc6e2e3a23fcb9d439a57a" frameborder=0></iframe>

## How to Test APIs?
> **This tutorial video is in Hindi Language, If you want in English just comment down and I will make in English as well😊🧑‍💻**

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/V3qPOs4du6A" frameborder="0" allowfullscreen></iframe></center>

## Stay Connected for Quick Updates!

Thank you for exploring our guide on Node.js and Express.js. To stay updated with the latest developments, tutorials, and insightful content, be sure to follow us on LinkedIn and Twitter.

**LinkedIn:** [Sandeep Singh](https://www.linkedin.com/in/sandeep-singh55/)

**Twitter:** [sandeepdev_me](https://twitter.com/sandeepdev_me)

![](https://cdn-images-1.medium.com/max/2000/1*DQbCtj0VH40Khbk-FI9jRA.jpeg)

By following us on these platforms, you’ll be the first to know about new articles, tutorials, and valuable resources to enhance your skills as a developer. Don’t miss out on the opportunity to stay connected with our community!

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/Looa06wacy8" frameborder="0" allowfullscreen></iframe></center>

## Conclusion

Congratulations! You’ve taken your first steps into the world of Express.js. You’ve learned what Express.js is, how to set up your development environment, create a server, define routes, and handle HTTP requests. You’ve also explored middleware, error handling, and built a basic API. Keep practicing, and soon you’ll be a proficient backend developer with Node.js and Express.js.

## FAQs

### Q1: What is Express.js?

Express.js, often referred to as Express, is a minimal and flexible Node.js web application framework. It provides a robust set of features to develop web and mobile applications. With Express, you can easily build powerful APIs and web applications. It simplifies the process of handling HTTP requests and defining routes, making it an excellent choice for web development.

### Q2: How do I set up my Node.js development environment?

Before diving into Express.js, ensure you have Node.js and npm (Node Package Manager) installed on your system. You can download them from the official Node.js website ([https://nodejs.org/](https://nodejs.org/)). Once installed, you can verify the installation by running the following commands in your terminal:

    node -v
    npm -v

### Q3: How do I create a basic Express server?

To create a basic Express server, you need to import the Express.js framework, initialize an instance of the Express application, and define a port for your server to listen on. Here’s a simplified example:

    const express = require('express');
    const app = express();
    const port = 3000;
    
    app.listen(port, () => {
      console.log(`Server is running on port ${port}`);
    });

### Q4: How do I handle HTTP GET requests in Express.js?

In Express.js, you can handle HTTP GET requests by defining a route using app.get(). For example:

    app.get('/hello', (req, res) => {
      res.send('Hello, Express!');
    });

### Q5: How do I handle HTTP POST requests in Express.js?

To handle HTTP POST requests in Express.js, define a route using app.post() and access the request body to retrieve data sent by the client. Here's a simplified example:

    app.post('/items', (req, res) => {
      const newItem = req.body.item;
      // Process the newItem and respond with updated data
      res.json(updatedData);
    });

### Q6: How do I handle HTTP PUT and DELETE requests in Express.js?

HTTP PUT and DELETE requests can be handled similarly to POST requests. Use app.put() and app.delete() to define routes, access request parameters or body, and update or delete data accordingly.

### Q7: What is middleware in Express.js, and how do I use it?

Middleware functions in Express.js have access to the request and response objects and can modify them. Middleware is useful for tasks like authentication and logging. You can use middleware with the app.use() method to apply it to your routes.

### Q8: How can I test my Express.js API?

To test your Express.js API, you can use tools like Postman. Postman allows you to send various HTTP requests (GET, POST, PUT, DELETE) to your API endpoints and inspect the responses. It’s a valuable tool for API development and testing.
