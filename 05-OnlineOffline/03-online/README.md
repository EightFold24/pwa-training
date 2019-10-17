# Navigator.online
Now that we have cached our app assets, we should be able to view it even when our connection goes down.
In this section we're going to use the [navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) interface to let our cached app know if the user is connected to the internet, and git it the ability to perform an action if this connectivity status changes (both _**online -> offline**_ and _**offline -> online**_).

## TODO
* Check your app is visible when offline using ngrok
* Have a quick look at [this example](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorOnLine/onLine) of using the navigator online functionality
* Follow [this example](https://developer.mozilla.org/en/docs/Online_and_offline_events) on how to work with online and offline events
* Display the connection status of your web app
    * Hint: You should use **_both_** the document and navigator APIs
* Follow the below specification to modify your form to submit its queued submissions when online
    
## Specification
- Implement a queue in LocalStorage for form data to be added to when the submit button is pressed. We are using the offline-first principal so we queue first!
- If there is a connection, submit any entries
    * Don't worry about creating a server to submit to just yet
    * A function with a `console.log` will suffice
    * Use `navigator.onLine` to check connectivity
    * Don't forget to remove queue items as they're uploaded!
- Register to the "online" event to upload the entries when a connection is re-established.
- **Note:** `navigator.onLine` depends on your internet connection, not necessarily your connection to the server (which will likely be locally hosted).
