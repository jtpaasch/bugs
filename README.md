BUGS
====

A simple tool to run lots of HTTP requests.

It relies on tornado, so make sure you have tornado installed (preferably in a virtual environment).

Usage
-----

Run the script followed by a list of URLs to make HTTP requests to.

    $ python bugs http://www.google.com http://www.bing.com http://yahoo.com ...

If you like, you can replace each url with a json object specifying a request:

    $ python bugs '{"url": "http://google.com"}' '{"url": "http://bing.com", "user_agent": "foo"}' ...

The properties you put in the request can be any of those found in the tornado.HTTPRequest object.


Output
------

When you run the `bugs` program, it spits out the response to each request as it receives the response. It is asynchronous, so some responses might come back before others. The response is formatted as indented JSON.


Loading URLs from files
-----------------------

If you programatically generate your list of URLs or Requests and store them in a file, you can pipe those into `bugs`. For instance, you might have a file called test_urls.txt which contains:

    http://www.google.com
    http://www.bing.com
    http://www.yahoo.com
    ...

You can `cat` that file, and pass it as arguments (using `xargs`) to the `bugs` script:

    $ cat test_urls.txt | xargs python bugs

You can also put requests in a file too. For example, if a file named test_requests.txt contains this:

    '{"url": "http://google.com"}'
    '{"url": "http://bing.com", "user_agent": "foo"}'
    '{"url": "http://yahoo.com", "user_agent": "bar", ... }'
    ...

You can pipe that in:

    $ cat test_requests.txt | xargs python bugs

The `bugs` program will run all those requests and spit out the responses.

You can also pipe the response into a file, since it's just JSON.
