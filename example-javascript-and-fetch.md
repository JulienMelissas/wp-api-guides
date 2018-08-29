## Making API Requests with Fetch and Vanilla JavaScript in a Theme

Fetch is a web api that is aimed to replace XMLHTTPRequests, the original method for working with AJAX and HTTP Requests.  Fetch is supported in the latest version of modern web browsers (see a [polyfill here if needed](https://www.npmjs.com/package/whatwg-fetch)).

In order to get our JavaScript working, we first have to enqueue the JavaScript in our functions.php file.  This will work for themes, but could be adapted to work in a plugin.  

```php
<?php

  function apidemo_setup() {

    wp_enqueue_script( 'apidemo', get_template_directory_uri() . '/assets/js/api.js', array('jquery'), null, true );

  }
  add_action( 'wp_enqueue_scripts', 'apidemo_scripts' );

?>
```

With that setup in your functions.php you can create an assets/js/api.js file to put your Fetch code for the API Request.  This code will handle pulling in your API Requests into JavaScript.

```js
var apiRoot = 'http://demo.wp-api.org/wp-json';

// Request latest posts
fetch(  apiRoot + '/wp/v2/posts/' )
  .then( response => {
    if (response.status !== 200) {
      throw new Error('Problem! Status Code: ' + response.status);
    }
    response.json().then( posts => {
      console.log( posts );
    });
  })
  .catch(function(err) {
    console.log('Error: ', err);
  });

// Request post with ID of 1
fetch(  apiRoot + '/wp/v2/posts/1' )
  .then( response => {
    if (response.status !== 200) {
      throw new Error('Problem! Status Code: ' + response.status);
    }
    response.json().then( post => {
      console.log( post );
    });
  })
  .catch(function( err ) {
    console.error( err );
  });


```

In the example code above we first setup our apiURL for the root of the WordPress REST API we want to request.

In the first Fetch example we look at pulling in the latest posts via the API.  Then in the second example we make a request for the post with ID of 1.

In both of the examples we start with throwing an error if a Success 200 message is not returned.  Then, if successful, we get the response, parse the JSON into native JavaScript and then log it out in the console.

At the very end we catch any errors that may occur if the request does not go through.
