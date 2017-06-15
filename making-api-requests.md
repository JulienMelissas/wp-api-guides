# Making WordPress REST API Requests

This guide is to help you get setup with making requests to the WordPress REST API. The hope is to get these guides into the [REST API Handbook](https://developer.wordpress.org/rest-api/).

Can’t find what you’re looking for? [Open an issue](https://github.com/JulienMelissas/wp-api-guides/issues) to request improvements.


## Making REST API Requests in the Browser

The easiest way to make requests to the WordPress REST API is in your browser.

Try these links:
1. http://demo.wp-api.org/wp-json/
2. http://demo.wp-api.org/wp-json/wp/v2/posts

Technically, the WP REST API pages are JSON files, not HTML. However, they will still display in most browsers. Using browser extensions can help to make default JSON responses more readable.

The [first link](http://demo.wp-api.org/wp-json/) returns some basic information about the site/API, as well as some details that API parsers might need to use, such as available routes. For now, you don't have to worry about any of this.

The [second link](http://demo.wp-api.org/wp-json/wp/v2/posts) returns an array of post objects, much like the results from a default `WP_Query` or `get_posts()`, but in JSON format. You will see each post object includes data about the post, such as the id, title, content, and date published.
 
You can also get data about individual posts by adding the ID of the post at the end of the url like this: http://demo.wp-api.org/wp-json/wp/v2/posts/1. Instead of returning an array of posts, this returns just the post object for that one post.
   
The `/pages/` endpoint is also available in the WordPress API so you can get data for pages in the same way. http://demo.wp-api.org/wp-json/wp/v2/pages/ will return an array of pages.

To see all of the endpoints, head here: https://developer.wordpress.org/rest-api/reference/#rest-api-developer-endpoint-reference.

While viewing JSON endpoints can be helpful for exploring API endpoints it is not helpful for pulling the WP API into our own projects like themes or plugins.


## Requests with CURL from Command Line

CURL is a command line resource for making requests to web sites.  CURL can also be used for making requests to WordPress REST API Endpoints.

To make a request with CURL, open your Terminal (or command line application) and run the following:

```
curl GET http://demo.wp-api.org/wp-json/wp/v2/posts
```

This will pull the JSON document into your command line.  If you are building apps or sites that leverage executable commands from the command CURL can be helpful.  However, if you are not using the command line then it would not be a recommended solution.


## Making API Requests with JavaScript

Something here about how great JS is, blablabla.

Take a deeper dive with these examples:
 - [Using JavaScript with `fetch()`](example-javascript-and-fetch.md)
 - [Using jQuery and `jQuery.ajax()`](example-jquery-ajax.md)
 - [Using Backbone and the Backbone Javascript Client](example-backbone-wpapi-client.md)


## Making API Requests with PHP

Something here about how great PHP is, blablabla.

Take a deeper dive with these examples:
 - [Using PHP with `wp_remote_get()` and `wp_remote_post()`](example-php-remote.md)
 - [Using PHP with `rest_do_request()`](example-php-rest-do-request.md)
 