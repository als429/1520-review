# Midterm

## Static Files 
* Static files, by definition, are plain files that aren't dynamically generated. 
* Can be served over a CDN 
* 
## Cache
* Allows quicker retrieval of resources
* Remember, the further we get from the processor, the slower things are
* Can cache from memory, disk, *or* from a remote server
* To avoid, set headers:
```
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
Expires: 0
```
* Think of all the ways we can do this in a web environment:
	* Cache data from the server in JavaScript running in the browser
	* Use Local Storage to store data in the browser
	* The browser can cache static resources to reduce network traffic
	* CDNs can cache and replicate static resources
	* We can use our Python code to cache data from the datastore
	* We can use a memory cache to share resources across VMs

## DNS

## Versions
* Benefits: 
	* Easier to roll back if errors are encountered
	* Enables experimentation with different site features
	* Consistent UX


## Virtual Machines

## Asyncronous 

## HTTP

## Data Management
* Normalization
  * Normalizing data is the process of eliminating redundant data.
  * Normalization often separates data into different tables or other logical structures; references are used to connect the data.
  * This introduces complexity in retrieval, but simplifies updates.

* Denormalization
  * Denormalized data has repeated entries.
  * Denormalization involves duplicating data in ways that make it easier to query.
  * is introduces complexity in updating, but simplifies retrieval.
 
* Key: a way of identifying data
* Primary Key: a unique identifier for a particular entry of data
* Natural Key: has meaning outside of the database - occurs naturally
* Artificial Key: has meaning only inside of the database; often generated
* Foreign Key: uses primary keys of other data to maintain referential integrity

* Indexing
  * Indexing allows us to look up data very quickly.
  * We don't index *all* the data, but some data is useful to index.
  * Different databases take different approaches, but by organizing some data into a structure that supports fast lookup and providing pointers to where the data is persisted, database access can be very fast.
 * Indexing allows databases to associate (or join) data in different places quickly.


## Templating
* Why templates?
  * Iterate over lists
  * Conditionally display content
  * Show variables
  * Create templated sites
* In Flask: `{% and %}` are used to denote logic execution
* object properties can be output to your HTML easily (`{{ user.username }}`)
* blocks allow you to set areas that will be replaced later
  * `{% block title %}` `{% endblock %}`
  * `{% for user in users %}` `{% endfor %}`
* Example: https://github.com/timothyrjames/cs1520/tree/master/week05/gae/project6


## Data transmission (AJAX + JSON) 
* XMLHttpRequest is a JS object that can be used to communicate HTTP requests and receive responses from your server
* XMLHttpRequest readystate property:
  * 0 - the request isn’t yet initialized.  This is the first state for the XML HTTP object.
  * 1 - a connection to the server has been established.
  * 2 - the HTTP request was received by the server.
  * 3 - the server is processing the HTTP request.
  * 4 - the server has completed processing and has sent a response.
* AJAX Lifecycle:
  1. XMLHttpRequest Object created
  2. Open Connection `.open()`
  3. Send `.send()`
  4. `onreadystatechange` event handler called
  5. Callback Function called
* There are 2 main ways to handle errors from XMLHttpRequest:
  1. Check the "status" property for the HTTP code to make sure it's 200 / OK: `if (xmlHttp.status === 200)` 
  2. Use try-catch to handle parse errors:
```
		try {
		  let myObject = JSON.parse(xmlHttp.responseText);
		} catch (err) {
		  // handle error
		}
```
* **Creating the XMLHttpRequest Object:**
```
function createXmlHttp() {
    var xmlhttp;
    if (window.XMLHttpRequest) {
        xmlhttp = new XMLHttpRequest();
    } else {
        xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    if (!(xmlhttp)) {
        alert("Your browser does not support AJAX!");
    }
    return xmlhttp;
}
```
* **Sending Parameters to the Server**
```
function postParameters(xmlHttp, target, parameters) {
    if (xmlHttp) {
        xmlHttp.open("POST", target, true);
        var contentType = "application/x-www-form-urlencoded";
        xmlHttp.setRequestHeader("Content-type", contentType); //setRequestHeader() allows us to identify the inclusion of parameters
        xmlHttp.send(parameters);
    }
}
```
* **Responding to a JSON Request**
```
function sendJsonRequest(targetUrl, parameters, callbackFunction) {
    var xmlHttp = createXmlHttp();
    xmlHttp.onreadystatechange = function() {
        if (xmlHttp.readyState == 4) {
            var myObject = JSON.parse(xmlHttp.responseText);
            callbackFunction(myObject, targetUrl, parameters);
        }
    }
    postParameters(xmlHttp, targetUrl, parameters);
}
```
* We can use the JSON package in Python to easily convert primitives, lists, and dictionaries to JSON objects.
   * `import json`

## Design Patterns
* Solve common problems
* Programming language independent
* Generally accepted, historically proven approach to solution
* Communicate best practices
* n-Tier Systems
	* Many applications are single tier; there is one system or component running in the application.
	* 2-tier systems usually separate some part of the application from the other; an application may use a database, or the application may have a UI component separate from the rest of the application.
	* 3-tier systems usually consist of 3 tiers - **data model**, **business logic**, and **presentation logic**.
* All of this inter-system communication can be expensive. Remember, processors are fast, memory is less fast, storage is even slower, and networking / intermachine communication is slowest of all.
* Why, then, do we pursue this approach?
	* Separation of concerns - it allows us to build more focused systems.
	* Testing - tiers can be tested independently.
	* Scaling - we can add resources to provide more capacity to specific tiers in our application as needed.
* Example of 3-tiered system = MVC -> Model-View-Controller Design Pattern

### MVC
* We often build systems using the 3-tier approach of Model-View-Controller.
* The "model" is the data model itself; how we store the information for the application.
* The "view" is the user interface for the application; how users interact with it.
* The "controller" connects the two, supplying data to the view, and reading / transforming the data or leveraging the business logic for the application.


## RDBMS (Relational Databased) - ACID
* ACID
  * Atomicity
  * Consistency
  * Isolation
  * Durability
* Need strong transactional support.
* Consistent, enforced structure of data is a high priority.
* Focused in a particular region.
* Large size
* Requires SQL access.

## Non-Relational Data Storage - BASE
* BASE
  * Basically Available
  * Softstate
  * Eventual Consistency
* Example: NoSQL
* Sustained performance is more important than Atomicity, Consistency, or Isolation.
* Flexible structure of data is OK (or necessary).
* Broad distribution of the location of the data.
* **Very** large size.
* Data size requirements beyond dozens of TB

## Cloud Datastore
Entity: a thing we need to store
Namespace: allows segmentation of entities
probably won't be needed by your projects
Kind: identifies "type" of entity	
Key: identifier for the entity - can be string or int
Ancestor: an "owner" for the entity
probably won't be needed  by your projects
Descendant: entities "owned" by an ancestor

## How things operate (HTML, CSS, JS)

## Events

## DOM
* Manipulating the DOM
	* `var element = document.getElementById("SomeID");`
	* `element.innerHTML = 'Whatever you want it to be';`
* Handle clicks
	* `<button onclick="someFunction();">Click This</button>`
	* `<input type="button" onclick="someOtherFunction();" value="Click Here">`
	* This can also be done in JavaScript:
```	 
document.getElementById("SomeElementID").onclick = function() {
	// your function body
};
```

* Common events
	* onblur: when an element loses focus
	* onchange: when an element changes
	* onfocus: when an element gains focus
	* onload: when an element is loaded in the page
	* onmouseenter: when the mouse cursor enters the element
	* onmouseleave: when the mouse cursor exits the element

		
## Data Residency 

## Globle Scale

## HTTP Stuff / Status codes
* 401: Unauthorized
* 405: Method Not Allowed
* 408: Request Timeout
* 501: Not Implemented
* 504: Gateway Timeout
* Uniform Resource Locator = URL
* Protocol + domain + path + resource
* HTTP request methods:
	* GET (parameters on the URL, as in the previous URL slide)
	* POST (parameters are within the body of the HTTP request)
	* HEAD
	* PUT
	* DELETE


## Lecture Slides
* https://docs.google.com/presentation/d/1vihnHBeovazPzePKEU_c1AR1w4N1BDVKNPoYrAsEwKc/edit?usp=sharing
* https://docs.google.com/presentation/d/1coW_MUloUeaUof_5sQFrXVZ7PqtaQvUdbshKEaE7Cxg/edit?usp=sharing
* https://docs.google.com/presentation/d/16KShDrt8r7wgipU4GVCLisiYA-3OrY1rBgVO9VH5v9w/edit?usp=sharing
* https://docs.google.com/presentation/d/1Xv1UtC0hygJ5DyN7acHjazoOZwcXh_JzO_ZXqaPcDSQ/edit?usp=sharing
* https://docs.google.com/presentation/d/11hWuV4g_vrzPcXyu1FbrCuFjY4Hg1XEE5o3lmmJ9lwA/edit?usp=sharing
* Versions and Tiers and MVC: https://docs.google.com/presentation/d/1Ic76WJrirtQI3LH0ohOlk6Ea7nAThJpyYBdkirGmHq4/edit?usp=sharing
* Static Files and Caching: https://docs.google.com/presentation/d/10-lvuj6vXJwxmQOOyKxliLBqwIPRIDT7fj3pD1i2SV4/edit?usp=sharing
* HTTP and HTML Samples: https://docs.google.com/presentation/d/1-C0G66zJLk1cuorsxdhPa1REGY475-UyDDn1M6FJX-o/edit?usp=sharing
* Announcements / Guidelines: https://docs.google.com/presentation/d/1C9UmGIu-uVYlInQOqRmr_KVE0k9coUOvqMN8wkoVCtM/edit?usp=sharing
* CSS & JavaScript Basics: https://docs.google.com/presentation/d/1ea9t4ogGXUbvlo1RFdkSpjc85JsKFtLeTKNaLLniE4E/edit?usp=sharing
* JSON & AJAX: https://docs.google.com/presentation/d/1RKLPxAjWq_vhAw6e1dioRFMDLTWg_xLEfu9qvp_6EUw/edit?usp=sharing
* Templates: https://docs.google.com/presentation/d/1K-fqqYvliVyjOj1_0trrnNEeisVi6VxlgLhGHEe6jMM/edit?usp=sharing
* https://docs.google.com/presentation/d/1o_AD9YeOnM8lUko3bqFHTolf8ptx1SFvwSIFZP8qxvE/edit?usp=sharing
