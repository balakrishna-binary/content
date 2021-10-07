---
title: Express/Node introduction
slug: Learn/Server-side/Express_Nodejs/Introduction
tags:
  - Beginner
  - CodingScripting
  - Express
  - Learn
  - Node
  - nodejs
  - server-side
---
<div>{{LearnSidebar}}</div>

<div>{{NextMenu("Learn/Server-side/Express_Nodejs/development_environment", "Learn/Server-side/Express_Nodejs")}}</div>

<p>In this first Express article we answer the questions "What is Node?" and "What is Express?", and give you an overview of what makes the Express web framework special. We'll outline the main features, and show you some of the main building blocks of an Express application (although at this point you won't yet have a development environment in which to test it).</p>

<table>
 <tbody>
  <tr>
   <th scope="row">Prerequisites:</th>
   <td>Basic computer literacy. A general understanding of <a href="/en-US/docs/Learn/Server-side/First_steps">server-side website programming</a>, and in particular the mechanics of <a href="/en-US/docs/Learn/Server-side/First_steps/Client-Server_overview">client-server interactions in websites</a>.</td>
  </tr>
  <tr>
   <th scope="row">Objective:</th>
   <td>To gain familiarity with what Express is and how it fits in with Node, what functionality it provides, and the main building blocks of an Express application.</td>
  </tr>
 </tbody>
</table>

<h2 id="Introducing_Node">Introducing Node</h2>

<p><a href="https://nodejs.org/">Node</a> (or more formally <em>Node.js</em>) is an open-source, cross-platform runtime environment that allows developers to create all kinds of server-side tools and applications in <a href="/en-US/docs/Glossary/JavaScript">JavaScript</a>. The runtime is intended for use outside of a browser context (i.e. running directly on a computer or server OS). As such, the environment omits browser-specific JavaScript APIs and adds support for more traditional OS APIs including HTTP and file system libraries.</p>

<p>From a web server development perspective Node has a number of benefits:</p>

<ul>
 <li>Great performance! Node was designed to optimize throughput and scalability in web applications and is a good solution for many common web-development problems (e.g. real-time web applications).</li>
 <li>Code is written in "plain old JavaScript", which means that less time is spent dealing with "context shift" between languages when you're writing both client-side and server-side code.</li>
 <li>JavaScript is a relatively new programming language and benefits from improvements in language design when compared to other traditional web-server languages (e.g. Python, PHP, etc.) Many other new and popular languages compile/convert into JavaScript so you can also use TypeScript, CoffeeScript, ClojureScript, Scala, LiveScript, etc.</li>
 <li>The node package manager (NPM) provides access to hundreds of thousands of reusable packages. It also has best-in-class dependency resolution and can also be used to automate most of the build toolchain.</li>
 <li>Node.js is portable. It is available on Microsoft Windows, macOS, Linux, Solaris, FreeBSD, OpenBSD, WebOS, and NonStop OS. Furthermore, it is well-supported by many web hosting providers, that often provide specific infrastructure and documentation for hosting Node sites.</li>
 <li>It has a very active third party ecosystem and developer community, with lots of people who are willing to help.</li>
</ul>

<p>You can use Node.js to create a simple web server using the Node HTTP package.</p>

<h3 id="Hello_Node.js">Hello Node.js</h3>

<p>The following example creates a web server that listens for any kind of HTTP request on the URL <code>http://127.0.0.1:8000/</code> — when a request is received, the script will respond with the string: "Hello World". If you have already installed node, you can follow these steps to try out the example:</p>

<ol>
 <li>Open Terminal (on Windows, open the command line utility)</li>
 <li>Create the folder where you want to save the program, for example, <code>test-node</code> and then enter it by entering the following command into your terminal:
  <pre class="brush: bash">cd test-node</pre>
 </li>
 <li>Using your favorite text editor, create a file called <code>hello.js</code> and paste the following code into it:<br>

  <pre class="brush: js">// Load HTTP module
const http = require("http");

const hostname = "127.0.0.1";
const port = 8000;

// Create HTTP server
const server = http.createServer((req, res) =&gt; {

   // Set the response HTTP header with HTTP status and Content type
   res.writeHead(200, {'Content-Type': 'text/plain'});

   // Send the response body "Hello World"
   res.end('Hello World\n');
});

// Prints a log once the server starts listening
server.listen(port, hostname, () =&gt; {
   console.log(`Server running at http://${hostname}:${port}/`);
})
</pre>
 </li>
 <li>Save the file in the folder you created above.</li>
 <li>Go back to the terminal and type the following command:
  <pre class="brush: bash">node hello.js</pre>
 </li>
</ol>

<p>Finally, navigate to <code>http://localhost:8000</code> in your web browser; you should see the text "<strong>Hello World</strong>" in the upper left of an otherwise empty web page.</p>

<h2 id="Web_Frameworks">Web Frameworks</h2>

<p>Other common web-development tasks are not directly supported by Node itself. If you want to add specific handling for different HTTP verbs (e.g. <code>GET</code>, <code>POST</code>, <code>DELETE</code>, etc.), separately handle requests at different URL paths ("routes"), serve static files, or use templates to dynamically create the response, Node won't be of much use on its own. You will either need to write the code yourself, or you can avoid reinventing the wheel and use a web framework!</p>

<h2 id="Introducing_Express">Introducing Express</h2>

<p><a href="https://expressjs.com/">Express</a> is the most popular <em>Node</em> web framework, and is the underlying library for a number of other popular <a href="https://expressjs.com/en/resources/frameworks.html">Node web frameworks</a>. It provides mechanisms to:</p>

<ul>
 <li>Write handlers for requests with different HTTP verbs at different URL paths (routes).</li>
 <li>Integrate with "view" rendering engines in order to generate responses by inserting data into templates.</li>
 <li>Set common web application settings like the port to use for connecting, and the location of templates that are used for rendering the response.</li>
 <li>Add additional request processing "middleware" at any point within the request handling pipeline.</li>
</ul>

<p>While <em>Express</em> itself is fairly minimalist, developers have created compatible middleware packages to address almost any web development problem. There are libraries to work with cookies, sessions, user logins, URL parameters, <code>POST</code> data, security headers, and <em>many</em> more. You can find a list of middleware packages maintained by the Express team at <a href="https://expressjs.com/en/resources/middleware.html">Express Middleware</a> (along with a list of some popular 3rd party packages).</p>

<div class="notecard note">
<p><strong>Note:</strong> This flexibility is a double edged sword. There are middleware packages to address almost any problem or requirement, but working out the right packages to use can sometimes be a challenge. There is also no "right way" to structure an application, and many examples you might find on the Internet are not optimal, or only show a small part of what you need to do in order to develop a web application.</p>
</div>

<h2 id="Where_did_Node_and_Express_come_from">Where did Node and Express come from?</h2>

<p>Node was initially released, for Linux only, in 2009. The NPM package manager was released in 2010, and native Windows support was added in 2012. At time of writing the current LTS release is Node v12.18.4 while the latest release is Node 14.13.0. This is a tiny snapshot of a rich history; delve into <a href="https://en.wikipedia.org/wiki/Node.js#History">Wikipedia</a> if you want to know more.</p>

<p>Express was initially released in November 2010 and is currently on version 4.17.1 of the API (with 5.0 in "alpha"). You can check out the <a href="https://expressjs.com/en/changelog/4x.html">changelog</a> for information about changes in the current release, and <a href="https://github.com/expressjs/express/blob/master/History.md">GitHub</a> for more detailed historical release notes.</p>

<h2 id="How_popular_are_Node_and_Express">How popular are Node and Express?</h2>

<p>The popularity of a web framework is important because it is an indicator of whether it will continue to be maintained, and what resources are likely to be available in terms of documentation, add-on libraries, and technical support.</p>

<p>There isn't any readily-available and definitive measure of the popularity of server-side frameworks (although you can estimate popularity using mechanisms like counting the number of GitHub projects and StackOverflow questions for each platform). A better question is whether Node and Express are "popular enough" to avoid the problems of unpopular platforms. Are they continuing to evolve? Can you get help if you need it? Is there an opportunity for you to get paid work if you learn Express?</p>

<p>Based on the number of <a href="https://expressjs.com/en/resources/companies-using-express.html">high profile companies</a> that use Express, the number of people contributing to the codebase, and the number of people providing both free and paid for support, then yes, <em>Express</em> is a popular framework!</p>

<h2 id="Is_Express_opinionated">Is Express opinionated?</h2>

<p>Web frameworks often refer to themselves as "opinionated" or "unopinionated".</p>

<p>Opinionated frameworks are those with opinions about the "right way" to handle any particular task. They often support rapid development <em>in a particular domain </em>(solving problems of a particular type) because the right way to do anything is usually well-understood and well-documented. However they can be less flexible at solving problems outside their main domain, and tend to offer fewer choices for what components and approaches they can use.</p>

<p>Unopinionated frameworks, by contrast, have far fewer restrictions on the best way to glue components together to achieve a goal, or even what components should be used. They make it easier for developers to use the most suitable tools to complete a particular task, albeit at the cost that you need to find those components yourself.<br>
 <br>
 Express is unopinionated. You can insert almost any compatible middleware you like into the request handling chain, in almost any order you like. You can structure the app in one file or multiple files, and using any directory structure. You may sometimes feel that you have too many choices!</p>

<h2 id="What_does_Express_code_look_like">What does Express code look like?</h2>

<p>In a traditional data-driven website, a web application waits for HTTP requests from the web browser (or other client). When a request is received the application works out what action is needed based on the URL pattern and possibly associated information contained in <code>POST</code> data or <code>GET</code> data. Depending on what is required it may then read or write information from a database or perform other tasks required to satisfy the request. The application will then return a response to the web browser, often dynamically creating an HTML page for the browser to display by inserting the retrieved data into placeholders in an HTML template.</p>

<p>Express provides methods to specify what function is called for a particular HTTP verb (<code>GET</code>, <code>POST</code>, <code>SET</code>, etc.) and URL pattern ("Route"), and methods to specify what template ("view") engine is used, where template files are located, and what template to use to render a response. You can use Express middleware to add support for cookies, sessions, and users, getting <code>POST</code>/<code>GET</code> parameters, etc. You can use any database mechanism supported by Node (Express does not define any database-related behavior).</p>

<p>The following sections explain some of the common things you'll see when working with <em>Express</em> and <em>Node</em> code.</p>

<h3 id="Helloworld_Express">Helloworld Express</h3>

<p>First lets consider the standard Express <a href="https://expressjs.com/en/starter/hello-world.html">Hello World</a> example (we discuss each part of this below, and in the following sections).</p>

<div class="notecard note">
<p><strong>Note:</strong> If you have Node and Express already installed (or if you install them as shown in the <a href="/en-US/docs/Learn/Server-side/Express_Nodejs/development_environment">next article</a>), you can save this code in a text file called <strong>app.js</strong> and run it in a bash command prompt by calling:</p>

<p><strong><code>node ./app.js</code></strong></p>
</div>

<pre class="brush: js">const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) =&gt; {
  res.send('Hello World!')
});

app.listen(port, () =&gt; {
  console.log(`Example app listening on port ${port}!`)
});
</pre>

<p>The first two lines <code>require()</code> (import) the express module and create an <a href="https://expressjs.com/en/4x/api.html#app">Express application</a>. This object, which is traditionally named <code>app</code>, has methods for routing HTTP requests, configuring middleware, rendering HTML views, registering a template engine, and modifying <a href="https://expressjs.com/en/4x/api.html#app.settings.table">application settings</a> that control how the application behaves (e.g. the environment mode, whether route definitions are case sensitive, etc.)</p>

<p>The middle part of the code (the three lines starting with <code>app.get</code>) shows a <em>route definition</em>. The <code>app.get()</code> method specifies a callback function that will be invoked whenever there is an HTTP <code>GET</code> request with a path (<code>'/'</code>) relative to the site root. The callback function takes a request and a response object as arguments, and calls <code><a href="https://expressjs.com/en/4x/api.html#res.send">send()</a></code> on the response to return the string "Hello World!"</p>

<p>The final block starts up the server on a specified port ('3000') and prints a log comment to the console. With the server running, you could go to <code>localhost:3000</code> in your browser to see the example response returned.</p>

<h3 id="Importing_and_creating_modules">Importing and creating modules</h3>

<p>A module is a JavaScript library/file that you can import into other code using Node's <code>require()</code> function. <em>Express</em> itself is a module, as are the middleware and database libraries that we use in our <em>Express</em> applications.</p>

<p>The code below shows how we import a module by name, using the <em>Express</em> framework as an example. First we invoke the <code>require()</code> function, specifying the name of the module as a string (<code>'express'</code>), and calling the returned object to create an <a href="https://expressjs.com/en/4x/api.html#app">Express application</a>. We can then access the properties and functions of the application object.</p>

<pre class="brush: js">const express = require('express');
const app = express();
</pre>

<p>You can also create your own modules that can be imported in the same way.</p>

<div class="notecard note">
<p><strong>Note:</strong> You will <em>want</em> to create your own modules, because this allows you to organize your code into manageable parts — a monolithic single-file application is hard to understand and maintain. Using modules also helps you manage your namespace, because only the variables you explicitly export are imported when you use a module.</p>
</div>

<p>To make objects available outside of a module you just need to expose them as additional properties on the <code>exports</code> object. For example, the <strong>square.js</strong> module below is a file that exports <code>area()</code> and <code>perimeter()</code> methods:</p>

<pre class="brush: js">exports.area = function(width) { return width * width; };
exports.perimeter = function(width) { return 4 * width; };
</pre>

<p>We can import this module using <code>require()</code>, and then call the exported method(s) as shown:</p>

<pre class="brush: js">const square = require('./square'); // Here we require() the name of the file without the (optional) .js file extension
console.log('The area of a square with a width of 4 is ' + square.area(4));</pre>

<div class="notecard note">
<p><strong>Note:</strong> You can also specify an absolute path to the module (or a name, as we did initially).</p>
</div>

<p>If you want to export a complete object in one assignment instead of building it one property at a time, assign it to <code>module.exports</code> as shown below (you can also do this to make the root of the exports object a constructor or other function):</p>

<pre class="brush: js">module.exports = {
  area: function(width) {
    return width * width;
  },

  perimeter: function(width) {
    return 4 * width;
  }
};
</pre>

<div class="notecard note">
<p><strong>Note:</strong> You can think of <code>exports</code> as a <a href="https://nodejs.org/api/modules.html#modules_exports_shortcut">shortcut</a> to <code>module.exports</code> within a given module. In fact, <code>exports</code> is just a variable that gets initialized to the value of <code>module.exports</code> before the module is evaluated. That value is a reference to an object (empty object in this case). This means that <code>exports</code> holds a reference to the same object referenced by <code>module.exports</code>. It also means that by assigning another value to <code>exports</code> it's no longer bound to <code>module.exports</code>.</p>
</div>

<p>For a lot more information about modules see <a href="https://nodejs.org/api/modules.html#modules_modules">Modules</a> (Node API docs).</p>

<h3 id="Using_asynchronous_APIs">Using asynchronous APIs</h3>

<p>JavaScript code frequently uses asynchronous rather than synchronous APIs for operations that may take some time to complete. A synchronous API is one in which each operation must complete before the next operation can start. For example, the following log functions are synchronous, and will print the text to the console in order (First, Second).</p>

<pre class="brush: js">console.log('First');
console.log('Second');
</pre>

<p>By contrast, an asynchronous API is one in which the API will start an operation and immediately return (before the operation is complete). Once the operation finishes, the API will use some mechanism to perform additional operations. For example, the code below will print out "Second, First" because even though <code>setTimeout()</code> method is called first, and returns immediately, the operation doesn't complete for several seconds.</p>

<pre class="brush: js">setTimeout(function() {
   console.log('First');
   }, 3000);
console.log('Second');
</pre>

<p>Using non-blocking asynchronous APIs is even more important on Node than in the browser because <em>Node</em> is a single-threaded event-driven execution environment. "Single threaded" means that all requests to the server are run on the same thread (rather than being spawned off into separate processes). This model is extremely efficient in terms of speed and server resources, but it does mean that if any of your functions call synchronous methods that take a long time to complete, they will block not just the current request, but every other request being handled by your web application.</p>

<p>There are a number of ways for an asynchronous API to notify your application that it has completed. The most common way is to register a callback function when you invoke the asynchronous API, that will be called back when the operation completes. This is the approach used above.</p>

<div class="notecard note">
<p><strong>Note:</strong> Using callbacks can be quite "messy" if you have a sequence of dependent asynchronous operations that must be performed in order because this results in multiple levels of nested callbacks. This problem is commonly known as "callback hell". This problem can be reduced by good coding practices (see <a href="http://callbackhell.com/">http://callbackhell.com/</a>), using a module like <a href="https://www.npmjs.com/package/async">async</a>, or even moving to ES6 features like <a href="/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">Promises</a>.</p>
</div>

<div class="notecard note">
<p><strong>Note:</strong> A common convention for Node and Express is to use error-first callbacks. In this convention, the first value in your <em>callback functions</em> is an error value, while subsequent arguments contain success data. There is a good explanation of why this approach is useful in this blog: <a href="https://fredkschott.com/post/2014/03/understanding-error-first-callbacks-in-node-js">The Node.js Way - Understanding Error-First Callbacks</a> (fredkschott.com).</p>
</div>

<h3 id="Creating_route_handlers">Creating route handlers</h3>

<p>In our <em>Hello World</em> Express example (see above), we defined a (callback) route handler function for HTTP <code>GET</code> requests to the site root (<code>'/'</code>).</p>

<pre class="brush: js">app.get('/', (req, res) =&gt; {
  res.send('Hello World!')
});
</pre>

<p>The callback function takes a request and a response object as arguments. In this case, the method calls <code><a href="https://expressjs.com/en/4x/api.html#res.send">send()</a></code> on the response to return the string "Hello World!" There are a <a href="https://expressjs.com/en/guide/routing.html#response-methods">number of other response methods</a> for ending the request/response cycle, for example, you could call <code><a href="https://expressjs.com/en/4x/api.html#res.json">res.json()</a></code> to send a JSON response or <code><a href="https://expressjs.com/en/4x/api.html#res.sendFile">res.sendFile()</a></code> to send a file.</p>

<div class="notecard note">
<p><strong>Note:</strong> You can use any argument names you like in the callback functions; when the callback is invoked the first argument will always be the request and the second will always be the response. It makes sense to name them such that you can identify the object you're working with in the body of the callback.</p>
</div>

<p>The <em>Express application</em> object also provides methods to define route handlers for all the other HTTP verbs, which are mostly used in exactly the same way:</p>

<p><code>checkout()</code>, <code>copy()</code>, <strong><code>delete()</code></strong>, <strong><code>get()</code></strong>, <code>head()</code>, <code>lock()</code>, <code>merge()</code>, <code>mkactivity()</code>, <code>mkcol()</code>, <code>move()</code>, <code>m-search()</code>, <code>notify()</code>, <code>options()</code>, <code>patch()</code>, <strong><code>post()</code></strong>, <code>purge()</code>, <strong><code>put()</code></strong>, <code>report()</code>, <code>search()</code>, <code>subscribe()</code>, <code>trace()</code>, <code>unlock()</code>, <code>unsubscribe()</code>.</p>

<p>There is a special routing method, <code>app.all()</code>, which will be called in response to any HTTP method. This is used for loading middleware functions at a particular path for all request methods. The following example (from the Express documentation) shows a handler that will be executed for requests to <code>/secret</code> irrespective of the HTTP verb used (provided it is supported by the <a href="https://nodejs.org/api/http.html#http_http_methods">http module</a>).</p>

<pre class="brush: js">app.all('/secret', function(req, res, next) {
  console.log('Accessing the secret section ...');
  next(); // pass control to the next handler
});</pre>

<p>Routes allow you to match particular patterns of characters in a URL, and extract some values from the URL and pass them as parameters to the route handler (as attributes of the request object passed as a parameter).</p>

<p>Often it is useful to group route handlers for a particular part of a site together and access them using a common route-prefix (e.g. a site with a Wiki might have all wiki-related routes in one file and have them accessed with a route prefix of <em>/wiki/</em>). In <em>Express</em> this is achieved by using the <code><a href="https://expressjs.com/en/guide/routing.html#express-router">express.Router</a></code> object. For example, we can create our wiki route in a module named <strong>wiki.js</strong>, and then export the <code>Router</code> object, as shown below:</p>

<pre class="brush: js">// wiki.js - Wiki route module

const express = require('express');
const router = express.Router();

// Home page route
router.get('/', function(req, res) {
  res.send('Wiki home page');
});

// About page route
router.get('/about', function(req, res) {
  res.send('About this wiki');
});

module.exports = router;
</pre>

<div class="notecard note">
<p><strong>Note:</strong> Adding routes to the <code>Router</code> object is just like adding routes to the <code>app</code> object (as shown previously).</p>
</div>

<p>To use the router in our main app file we would then <code>require()</code> the route module (<strong>wiki.js</strong>), then call <code>use()</code> on the <em>Express</em> application to add the Router to the middleware handling path. The two routes will then be accessible from <code>/wiki/</code> and <code>/wiki/about/</code>.</p>

<pre class="brush: js">const wiki = require('./wiki.js');
// ...
app.use('/wiki', wiki);</pre>

<p>We'll show you a lot more about working with routes, and in particular about using the <code>Router</code>, later on in the linked section<a href="/en-US/docs/Learn/Server-side/Express_Nodejs/routes"> Routes and controllers .</a></p>

<h3 id="Using_middleware">Using middleware</h3>

<p>Middleware is used extensively in Express apps, for tasks from serving static files to error handling, to compressing HTTP responses. Whereas route functions end the HTTP request-response cycle by returning some response to the HTTP client, middleware functions <em>typically</em> perform some operation on the request or response and then call the next function in the "stack", which might be more middleware or a route handler. The order in which middleware is called is up to the app developer.</p>

<div class="notecard note">
<p><strong>Note:</strong> The middleware can perform any operation, execute any code, make changes to the request and response object, and it can <em>also end the request-response cycle</em>. If it does not end the cycle then it must call <code>next()</code> to pass control to the next middleware function (or the request will be left hanging).</p>
</div>

<p>Most apps will use <em>third-party</em> middleware in order to simplify common web development tasks like working with cookies, sessions, user authentication, accessing request <code>POST</code> and JSON data, logging, etc. You can find a <a href="https://expressjs.com/en/resources/middleware.html">list of middleware packages maintained by the Express team</a> (which also includes other popular 3rd party packages). Other Express packages are available on the NPM package manager.</p>

<p>To use third party middleware you first need to install it into your app using NPM.
For example, to install the <a href="https://expressjs.com/en/resources/middleware/morgan.html">morgan</a> HTTP request logger middleware, you'd do this:</p>

<pre class="brush: bash">$ npm install morgan
</pre>

<p>You could then call <code>use()</code> on the <em>Express application object</em> to add the middleware to the stack:</p>

<pre class="brush: js">const express = require('express');
const logger = require('morgan');
const app = express();
app.use(logger('dev'));
...</pre>

<div class="notecard note">
  <p><strong>Note:</strong> Middleware and routing functions are called in the order that they are declared. For some middleware the order is important (for example if session middleware depends on cookie middleware, then the cookie handler must be added first). It is almost always the case that middleware is called before setting routes, or your route handlers will not have access to functionality added by your middleware.</p>
</div>

<p>You can write your own middleware functions, and you are likely to have to do so (if only to create error handling code). The <strong>only</strong> difference between a middleware function and a route handler callback is that middleware functions have a third argument <code>next</code>, which middleware functions are expected to call if they are not that which completes the request cycle (when the middleware function is called, this contains the <em>next</em> function that must be called).</p>

<p>You can add a middleware function to the processing chain for <em>all responses</em> with <code>app.use()</code>, or for a specific HTTP verb using the associated method: <code>app.get()</code>, <code>app.post()</code>, etc. Routes are specified in the same way for both cases, though the route is optional when calling <code>app.use()</code>.</p>

<p>The example below shows how you can add the middleware function using both approaches, and with/without a route.</p>

<pre class="brush: js">const express = require('express');
const app = express();

// An example middleware function
let a_middleware_function = function(req, res, <em>next</em>) {
  // ... perform some operations
  next(); // Call next() so Express will call the next middleware function in the chain.
}

// Function added with use() for all routes and verbs
app.use(a_middleware_function);

// Function added with use() for a specific route
app.use('/someroute', a_middleware_function);

// A middleware function added for a specific HTTP verb and route
app.get('/', a_middleware_function);

app.listen(3000);</pre>

<div class="notecard note">
<p><strong>Note:</strong> Above we declare the middleware function separately and then set it as the callback. In our previous route handler function we declared the callback function when it was used. In JavaScript, either approach is valid.</p>
</div>

<p>The Express documentation has a lot more excellent documentation about <a href="https://expressjs.com/en/guide/using-middleware.html">using</a> and <a href="https://expressjs.com/en/guide/writing-middleware.html">writing</a> Express middleware.</p>

<h3 id="Serving_static_files">Serving static files</h3>

<p>You can use the <a href="https://expressjs.com/en/4x/api.html#express.static">express.static</a> middleware to serve static files, including your images, CSS and JavaScript (<code>static()</code> is the only middleware function that is actually <strong>part</strong> of <em>Express</em>). For example, you would use the line below to serve images, CSS files, and JavaScript files from a directory named '<strong>public'</strong> at the same level as where you call node:</p>

<pre class="brush: js">app.use(express.static('public'));
</pre>

<p>Any files in the public directory are served by adding their filename (<em>relative</em> to the base "public" directory) to the base URL. So for example:</p>

<pre class="brush: plain">http://localhost:3000/images/dog.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/about.html
</pre>

<p>You can call <code>static()</code> multiple times to serve multiple directories. If a file cannot be found by one middleware function then it will be passed on to the subsequent middleware (the order that middleware is called is based on your declaration order).</p>

<pre class="brush: js">app.use(express.static('public'));
app.use(express.static('media'));
</pre>

<p>You can also create a virtual prefix for your static URLs, rather than having the files added to the base URL. For example, here we <a href="https://expressjs.com/en/4x/api.html#app.use">specify a mount path</a> so that the files are loaded with the prefix "/media":</p>

<pre class="brush: js">app.use('/media', express.static('public'));
</pre>

<p>Now, you can load the files that are in the <code>public</code> directory from the <code>/media</code> path prefix.</p>

<pre class="brush: plain">http://localhost:3000/media/images/dog.jpg
http://localhost:3000/media/video/cat.mp4
http://localhost:3000/media/cry.mp3
</pre>

<div class="notecard note">
<p><strong>Note:</strong> See also <a href="https://expressjs.com/en/starter/static-files.html">Serving static files in Express</a>.</p>
</div>

<h3 id="Handling_errors">Handling errors</h3>

<p>Errors are handled by one or more special middleware functions that have four arguments, instead of the usual three: <code>(err, req, res, next)</code>. For example:</p>

<pre class="brush: js">app.use(function(err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
</pre>

<p>These can return any content required, but must be called after all other <code>app.use()</code> and routes calls so that they are the last middleware in the request handling process!</p>

<p>Express comes with a built-in error handler, which takes care of any remaining errors that might be encountered in the app. This default error-handling middleware function is added at the end of the middleware function stack. If you pass an error to <code>next()</code> and you do not handle it in an error handler, it will be handled by the built-in error handler; the error will be written to the client with the stack trace.</p>

<div class="notecard note">
<p><strong>Note:</strong> The stack trace is not included in the production environment. To run it in production mode you need to set the environment variable <code>NODE_ENV</code> to '<code>production'</code>.</p>
</div>

<div class="notecard note">
<p><strong>Note:</strong> HTTP404 and other "error" status codes are not treated as errors. If you want to handle these, you can add a middleware function to do so. For more information see the <a href="https://expressjs.com/en/starter/faq.html#how-do-i-handle-404-responses">FAQ</a>.</p>
</div>

<p>For more information see <a href="https://expressjs.com/en/guide/error-handling.html">Error handling</a> (Express docs).</p>

<h3 id="Using_databases">Using databases</h3>

<p><em>Express</em> apps can use any database mechanism supported by <em>Node</em> (<em>Express</em> itself doesn't define any specific additional behavior/requirements for database management). There are many options, including PostgreSQL, MySQL, Redis, SQLite, MongoDB, etc.</p>

<p>In order to use these you have to first install the database driver using NPM. For example, to install the driver for the popular NoSQL MongoDB you would use the command:</p>

<pre class="brush: bash">$ npm install mongodb
</pre>

<p>The database itself can be installed locally or on a cloud server. In your Express code you require the driver, connect to the database, and then perform create, read, update, and delete (CRUD) operations. The example below (from the Express documentation) shows how you can find "mammal" records using MongoDB.</p>

<pre class="brush: js">//this works with older versions of  mongodb version ~ 2.2.33
const MongoClient = require('mongodb').MongoClient;

MongoClient.connect('mongodb://localhost:27017/animals', function(err, db) {
  if (err) throw err;

  db.collection('mammals').find().toArray(function (err, result) {
    if (err) throw err;

    console.log(result);
  });
});

//for mongodb version 3.0 and up
const MongoClient = require('mongodb').MongoClient;
MongoClient.connect('mongodb://localhost:27017/animals', function(err, client){
   if(err) throw err;

   let db = client.db('animals');
   db.collection('mammals').find().toArray(function(err, result){
     if(err) throw err;
     console.log(result);
     client.close();
   });
});
</pre>

<p>Another popular approach is to access your database indirectly, via an Object Relational Mapper ("ORM"). In this approach you define your data as "objects" or "models" and the ORM maps these through to the underlying database format. This approach has the benefit that as a developer you can continue to think in terms of JavaScript objects rather than database semantics, and that there is an obvious place to perform validation and checking of incoming data. We'll talk more about databases in a later article.</p>

<p>For more information see <a href="https://expressjs.com/en/guide/database-integration.html">Database integration</a> (Express docs).</p>

<h3 id="Rendering_data_views">Rendering data (views)</h3>

<p>Template engines (referred to as "view engines" by <em>Express</em>) allow you to specify the <em>structure</em> of an output document in a template, using placeholders for data that will be filled in when a page is generated. Templates are often used to create HTML, but can also create other types of documents. Express has support for <a href="https://github.com/expressjs/express/wiki#template-engines">a number of template engines</a>, and there is a useful comparison of the more popular engines here: <a href="https://strongloop.com/strongblog/compare-javascript-templates-jade-mustache-dust/">Comparing JavaScript Templating Engines: Jade, Mustache, Dust and More</a>.</p>

<p>In your application settings code you set the template engine to use and the location where Express should look for templates using the 'views' and 'view engines' settings, as shown below (you will also have to install the package containing your template library too!)</p>

<pre class="brush: js">const express = require('express');
const path = require('path');
const app = express();

// Set directory to contain the templates ('views')
app.set('views', path.join(__dirname, 'views'));

// Set view engine to use, in this case 'some_template_engine_name'
app.set('view engine', 'some_template_engine_name');
</pre>

<p>The appearance of the template will depend on what engine you use. Assuming that you have a template file named "index.&lt;template_extension&gt;" that contains placeholders for data variables named 'title' and "message", you would call <code><a href="https://expressjs.com/en/4x/api.html#res.render">Response.render()</a></code> in a route handler function to create and send the HTML response:</p>

<pre class="brush: js">app.get('/', function(req, res) {
  res.render('index', { title: 'About dogs', message: 'Dogs rock!' });
});</pre>

<p>For more information see <a href="https://expressjs.com/en/guide/using-template-engines.html">Using template engines with Express</a> (Express docs).</p>

<h3 id="File_structure">File structure</h3>

<p>Express makes no assumptions in terms of structure or what components you use. Routes, views, static files, and other application-specific logic can live in any number of files with any directory structure. While it is perfectly possible to have the whole <em>Express</em> application in one file, typically it makes sense to split your application into files based on function (e.g. account management, blogs, discussion boards) and architectural problem domain (e.g. model, view or controller if you happen to be using an <a href="/en-US/docs/Glossary/MVC">MVC architecture</a>).</p>

<p>In a later topic we'll use the <em>Express Application Generator</em>, which creates a modular app skeleton that we can easily extend for creating web applications.</p>

<h2 id="Summary">Summary</h2>

<p>Congratulations, you've completed the first step in your Express/Node journey! You should now understand Express and Node's main benefits, and roughly what the main parts of an Express app might look like (routes, middleware, error handling, and template code). You should also understand that with Express being an unopinionated framework, the way you pull these parts together and the libraries that you use are largely up to you!</p>

<p>Of course Express is deliberately a very lightweight web application framework, so much of its benefit and potential comes from third party libraries and features. We'll look at those in more detail in the following articles. In our next article we're going to look at setting up a Node development environment, so that you can start seeing some Express code in action.</p>

<h2 id="See_also">See also</h2>

<ul>
 <li><a href="https://medium.com/@ramsunvtech/manage-multiple-node-versions-e3245d5ede44">Venkat.R - Manage Multiple Node versions</a></li>
 <li><a href="https://nodejs.org/api/modules.html#modules_modules">Modules</a> (Node API docs)</li>
 <li><a href="https://expressjs.com/">Express</a> (home page)</li>
 <li><a href="https://expressjs.com/en/starter/basic-routing.html">Basic routing</a> (Express docs)</li>
 <li><a href="https://expressjs.com/en/guide/routing.html">Routing guide</a> (Express docs)</li>
 <li><a href="https://expressjs.com/en/guide/using-template-engines.html">Using template engines with Express</a> (Express docs)</li>
 <li><a href="https://expressjs.com/en/guide/using-middleware.html">Using middleware</a> (Express docs)</li>
 <li><a href="https://expressjs.com/en/guide/writing-middleware.html">Writing middleware for use in Express apps</a> (Express docs)</li>
 <li><a href="https://expressjs.com/en/guide/database-integration.html">Database integration</a> (Express docs)</li>
 <li><a href="https://expressjs.com/en/starter/static-files.html">Serving static files in Express</a> (Express docs)</li>
 <li><a href="https://expressjs.com/en/guide/error-handling.html">Error handling</a> (Express docs)</li>
</ul>

<div>{{NextMenu("Learn/Server-side/Express_Nodejs/development_environment", "Learn/Server-side/Express_Nodejs")}}</div>

<h2 id="In_this_module">In this module</h2>

<ul>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction">Express/Node introduction</a></li>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/development_environment">Setting up a Node (Express) development environment</a></li>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/Tutorial_local_library_website">Express Tutorial: The Local Library website</a></li>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/skeleton_website">Express Tutorial Part 2: Creating a skeleton website</a></li>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose">Express Tutorial Part 3: Using a Database (with Mongoose)</a></li>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/routes">Express Tutorial Part 4: Routes and controllers</a></li>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/Displaying_data">Express Tutorial Part 5: Displaying library data</a></li>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/forms">Express Tutorial Part 6: Working with forms</a></li>
 <li><a href="/en-US/docs/Learn/Server-side/Express_Nodejs/deployment">Express Tutorial Part 7: Deploying to production</a></li>
</ul>