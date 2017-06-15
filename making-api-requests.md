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

`
curl -X OPTIONS -i http://demo.wp-api.org/wp-json/wp/v2/posts
`

This will pull the JSON document into your command line.  If you are building apps or sites that leverage executable commands from the command CURL can be helpful.  However, if you are not using the command line then it would not be a recommended solution.

## Requests with jQuery in a Theme

jQuery has a great built AJAX functionality that makes making
