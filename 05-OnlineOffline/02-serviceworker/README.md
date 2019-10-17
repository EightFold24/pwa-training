# Service Workers
A service worker is a script that your browser runs in the background, separate from a web page, opening the door to features that don't need a web page or user interaction. Today, they already include features like push notifications and background sync. In the future, service workers might support other things like periodic sync or geofencing. The core feature discussed in this tutorial is the ability to intercept and handle network requests, including programmatically managing a cache of responses.

The reason this is such an exciting API is that it allows you to support offline experiences, giving developers complete control over the experience.

Before service worker, there was one other API that gave users an offline experience on the web called AppCache. There are a number of issues with the AppCache API that service workers were designed to avoid.

Things to note about a service worker:

* It's a JavaScript Worker, so it can't access the DOM directly. Instead, a service worker can communicate with the pages it controls by responding to messages sent via the postMessage interface, and those pages can manipulate the DOM if needed.
* Service worker is a programmable network proxy, allowing you to control how network requests from your page are handled.
* It's terminated when not in use, and restarted when it's next needed, so you cannot rely on global state within a service worker's onfetch and onmessage handlers. If there is information that you need to persist and reuse across restarts, service workers do have access to the IndexedDB API.
* Service workers make extensive use of promises, so if you're new to promises, then you should stop reading this and check out Promises, an introduction.

## Research
* Check out this [Jake Archibald introduction video](https://www.youtube.com/watch?v=4uQMl7mFB6g)
* Have a flick through the code of [this tutorial](https://github.com/jakearchibald/simple-serviceworker-tutorial) to get an idea for how ServiceWorker is used
* Refer to the [MDN Mozilla documentation](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorker)
* Watch this [video](https://youtu.be/dXuvT4oollQ) from the Google Developers
* Have a quick look at this [implementation](https://github.com/GoogleChrome/samples/tree/gh-pages/service-worker/prefetch)
* See the included [service worker tutorial](guide.md)

## TODO
* Using the guide & any other resources above, implement a service into your form website that caches assets to appear to work offline
* Run another lighthouse audit to see that some of the PWA statistics are fixed

***Content from this document is adapted from https://developers.google.com/web/fundamentals/primers/service-workers***
