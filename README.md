[![npm version](https://badge.fury.io/js/amokjs.svg)](https://badge.fury.io/js/amokjs)

# amokjs - simple backend mocking framework

**amokjs** helps you quickly build backend service mocks. Allows you to serve http responses from flat files. Supports multiple response codes, headers and dynamically generated values. Seen the [example applications](https://github.com/sauliuz/amokjs/tree/master/examples).

**amokjs** supports custom plugins. We welcome community submissions!

## how it works?

By default, **amokjs** serves responses from flat files in the responses directory in project root. It supports **JSON**, **XML**, **SOAP** and other formats. You can just add a new resource file into resources derectory and **amokjs** will serve it as response.


## how to run?

Amokjs includes Express framework and your nodejs application only has to require and use npm module. See [examples directory](https://github.com/sauliuz/amok/tree/master/examples) for more details.

	var amokjs = require('amokjs');
	amokjs.setPort('3030');
	amokjs.start();


**amokjs** will serve response content from a file in the responses directory. There are 2 ways of requesting mocked backend responses from API powered by amok:

* **amokjs** will serve response content from a file matching file name in the request path. For example if you send API request to *yourapi.com/xml* mock will serve response from file named *xml*.

* **amokjs** will serve response content from a file matching **x-mock-filename** header content. In this case the main request path has to be */*. For example if you send API request to *yourapi.com/* and request will contain *x-mock-filename* HTTP header - mock will serve response from file named *xml*.

### supported headers

Headers **amokjs** supports:

* **x-mock-response-code** request header allows developers to request custom HTTP response code from mock API
* **x-mock-filename** request header allows developers to pass mock file name in the HTTP request header rather then request path. For example if *x-mock-filename: xml* is used in the header and request path is */* mock API will attempt to serve response from *xml* file.

### supported template variables

In your response files you can use several template variables in order to get values generated dynamically. Below are the template values **amockjs** supports:

* **@date@** - will be replaced with the current timestamp. Format: YYYY-MM-DD
* **@randomDate@** - will be replaced with the random timestamp. Format: YYYY-MM-DD
* **@longid@** - will be replaced with the 10 digits long random number
* **@shortid@** - will be replaced with the random number up to 5 digits long

### example curl requests

Below are few example curl requests to test the mock API:

	curl -XGET 'http://localhost:3030/mock-api/xml'
	curl -XGET -H 'x-mock-filename: xml' 'http://localhost:3030/'
	curl -XGET -H "x-mock-response-code: 500" 'http://localhost:3030/xml'
	
### tutorials

* [Building API mocks with Amokjs](https://www.popularowl.com/blog/build-api-mocks-with-amokjs/)


### improvements?

We welcome pull requests if you have any sugestions for improvements.

By [@sauliuz](https://twitter.com/sauliuz) and [popularowl.com](http://www.popularowl.com "apis made simple")
