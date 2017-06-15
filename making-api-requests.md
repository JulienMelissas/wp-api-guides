# Making WordPress REST API Requests

This guide is to help you get setup with making requests to the WordPress REST API.

## Making REST API Requests in the Browser

The easiest way to make requests to the WordPress REST API is in your browser.  If you navigate to the root of the WP REST API you can view it in the browser.

Try these links:

- http://demo.wp-api.org/wp-json/
- http://demo.wp-api.org/wp-json/wp/v2/posts

Technically, the WP REST API pages are JSON files, not HTML. However, they will still display in a browser.

While this can be helpful for exploring API Endpoints and seeing what is available, it is not helpful for pulling the WP API into our own projects like themes or plugins.

## Requests with CURL from Command Line

CURL is a command line resource for making requests to web sites.  CURL can also be used for making requests to WordPress REST API Endpoints.

To make a request with CURL, open your Terminal (or command line application) and run the following:

```
curl -X OPTIONS -i http://demo.wp-api.org/wp-json/wp/v2/posts
```

This will pull the JSON document into your command line.  If you are building apps or sites that leverage executable commands from the command CURL can be helpful.  However, if you are not using the command line then it would not be a recommended solution.

## Making API Requests with Fetch and Vanilla JavaScript in a Theme

Fetch is a web api that is aimed to replace XMLHTTPRequests, the original method for working with AJAX and HTTP Requests.  Fetch is supported in the latest version of modern web browsers (see a [polyfill here if needed](https://www.npmjs.com/package/whatwg-fetch)).

In order to get

```php
<?php

  function apidemo_setup() {

    wp_enqueue_script( 'apidemo', get_template_directory_uri() . '/assets/js/api.js', array('jquery'), null, true );

  }
  add_action( 'wp_enqueue_scripts', 'apidemo_scripts' );

;?>
```

With that setup in your functions.php you can create an assets/js/api.js file to put your XMLHTTPRequests code.  This code will handle pulling in your API Requests into JavaScript.

```js


```


## Making API Requests with jQuery in a Theme

jQuery has great built AJAX functionality that makes WordPress API Requests easy.  The first step is to load a new JavaScript file in your theme or plugin.

Here is an example of including an "api.js" file in your theme and have it dependent on jQuery, which will also take care of making sure jQuery is loaded on the page.

```php
<?php

  function apidemo_setup() {

    wp_enqueue_script( 'apidemo', get_template_directory_uri() . '/assets/js/api.js', array('jquery'), null, true );

  }
  add_action( 'wp_enqueue_scripts', 'apidemo_scripts' );

;?>
```


Placed in your functions.php file, the code above will load jQuery and your app.js file in the current theme.  Once that is loaded you can setup your jQuery AJAX code inside of your api.js file.

Like all jQuery files in WordPress, you will want to open up the document with a no conflict wrapper.  Then inside of that we can setup our jQuery AJAX request as follows:

```js
(function($) {

  var apiURL = 'http://demo.wp-api.org/wp-json';

  // Make a request for posts
  $.ajax( {
	  url: apiURL + '/wp/v2/posts/',
	  success: function ( posts ) {
			console.log( 'Array of posts', posts );
	  },
		error:  function( err ) {
			console.log( 'Error: ', err );
		}
	} );

  // Make a request for a single post with an ID of 1
  $.ajax( {
	  url: apiURL + '/wp/v2/posts/1',
	  success: function ( post ) {
			console.log( 'Array of posts', post );
	  },
		error:  function( err ) {
			console.log( 'Error: ', err );
		}
	});

})( jQuery );
```

At the top of our document we setup the root URL for the WordPress site we want to make queries to.  This can be the site our theme is loaded on or another site somewhere else.

We set this root at the top so that it can be reused in different requests.

In the first AJAX setup we make a request to "/wp/v2/posts/" which will return a JSON string of the latest posts from the site.

Then in the next AJAX setup we change the query string to "/wp/v2/posts/1" which will return a JSON string of the post with an ID of 1.

When you use $.ajax it will automatically convert the JSON into native JavaScript arrays and objects.  This will allow you to easily work with REST API data in the same way you would with native JavaScript arrays and objects.
