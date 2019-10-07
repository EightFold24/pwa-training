# Build a Webapp

## Starter Guide
**_NOTE: This works best on Chrome (but does work on other browsers). Compatibility for any technologies used in this training can be seen on http://caniuse.com/_**

## Prerequisits
* Something to run a simple web server (python/http-server/php)
* ngrok

## Website Specification
Try to build something with the following spec:

- Uses [Materialize](http://materializecss.com/) for style/theme
- Is responsive (use [ngrok](https://ngrok.com) to tunnel your app to a URL that you can use on your phone)
- Single web page with the following components (look at the components section on the Materialize website):
  - Header with title
  - Form with a few fields
  - Submit button for the form

## Running the Website
There are a number of ways to host a web server locally
1. Use a [Python web server](http://www.2ality.com/2014/06/simple-http-server.html) to run locally
    ```
    //Python 2.x
    python -m SimpleHTTPServer
    
    //Python 3.x
    python -m http.server
    ```
2. Use [Node.js](https://nodejs.org/en/)'s HTTP server package
    ```
    npm install http-server -g
    http-server . -p 8000
    ```
3. Use PHP server
    ```
    php -S localhost:8000
    ```
    
**_NOTE: If you are using any templates, make sure to read any READMEs that may be included for how best to build and/or run._**
