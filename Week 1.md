
A popup window is one of the oldest methods to show the additional documents to the user.

Basically, you just run:
 
1. **Window Open Method** (`window.open()`):
   - The `window.open()` method is used to open a new browser window or tab. It can be used to create pop-up windows, new browser windows, or to open external URLs.

   javascript
   // Example of opening a new window
   var newWindow = window.open("https://www.example.com", "Example", "width=400,height=300");
   
**Window Close Method (window.close()):**

The `window.close()` method is used to close the current browser window or tab. However, it can only be used to close windows that were opened using JavaScript (i.e., windows created with window.open()).
javascript

// Example of closing a window
var myWindow = window.open("https://www.example.com", "Example", "width=400,height=300");
myWindow.close();

3. **Alert Method** (`window.alert()`):
   - The `window.alert()` method displays a pop-up dialog box with a specified message and an OK button. It is often used to provide information or messages to the user.

   javascript
   // Example of displaying an alert
   window.alert("This is an alert message.");

In this example, we generate popup content from JavaScript:

let newWin = window.open("about:blank", "hello", "width=200,height=200");

newWin.document.write("Hello, world!");

And here we modify the contents after loading:

let newWindow = open('/', 'example', 'width=300,height=300')

newWindow.focus();

alert(newWin.location.href); // (*) about:blank, loading hasn't started yet

newWindow.onload = function() {

  let html = `<div style="font-size:30px">Welcome!</div>`;

  newWindow.document.body.insertAdjacentHTML('afterbegin', html);

};  


# Cross-window Communication

## Same Origin

Two URLs are said to have the “same origin” if they have the same protocol, domain, and port.

The “Same Origin” policy states that:

if we have a reference to another window, e.g. a popup created by window.open or a window inside `<iframe>`, and that window comes from the same origin, then we have full access to that window.


**In Action iFrame**

The `<iframe>` tag embeds another webpage within the current one. You can access the embedded window and document using `iframe.contentWindow` and `iframe.contentDocument`. However, the browser enforces a security rule called the "same-origin policy," which restricts access to embedded content if it comes from a different origin, except for certain exceptions like writing to the location. This policy helps prevent security vulnerabilities in web applications.

## Sandbox attribute for iFrame

The sandbox attribute allows for the exclusion of certain actions inside an `<iframe>` in order to prevent it from executing untrusted code.

**allow-same-origin**
By default "sandbox" forces the “different origin” policy for the iframe. In other words, it makes the browser to treat the iframe as coming from another origin, even if its src points to the same site. With all implied restrictions for scripts. This option removes that feature.

**allow-top-navigation**
Allows the iframe to change parent.location.

**allow-forms**
Allows to submit forms from iframe.

**allow-scripts**
Allows to run scripts from the iframe.

**allow-popups**
Allows to window.open popups from the iframe


## Cross window messaging 

The postMessage interface allows windows to talk to each other no matter which origin they are from.

The window that wants to send a message calls postMessage method of the receiving window. In other words, if we want to send the message to win, we should call win.postMessage(data, targetOrigin).