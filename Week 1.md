
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


# Clickjacking Attack
The “clickjacking” attack allows an evil page to click on a “victim site” on behalf of the visitor.

## Old-school defences (weak)
The oldest defence is a bit of JavaScript which forbids opening the page in a frame (so-called “framebusting”).

## Blocking top navigation
We can block the transition caused by changing top.location in beforeunload event handler.

Example:

window.onbeforeunload = function() {

  return false;

};

## sandbox attribute
One of the things restricted by the sandbox attribute is navigation. A sandboxed iframe may not change top.location.

Example:
`<iframe sandbox="allow-scripts allow-forms" src="facebook.html"></iframe>`

## X-Frame-options
The server-side header X-Frame-Options can permit or forbid displaying the page inside a frame.

It must be sent exactly as HTTP-header: the browser will ignore it if found in HTML `<meta>` tag. So, <meta http-equiv="X-Frame-Options"...> won’t do anything.

The header may have 3 values:

 Deny, sameorigin, Allow-from domain

 ## Samesite cookie attribute
The samesite cookie attribute can also prevent clickjacking attacks.

A cookie with such attribute is only sent to a website if it’s opened directly, not via a frame, or otherwise


## Cross window messaging 

The postMessage interface allows windows to talk to each other no matter which origin they are from.

The window that wants to send a message calls postMessage method of the receiving window. In other words, if we want to send the message to win, we should call win.postMessage(data, targetOrigin).

# ArrayBuffer
The ArrayBuffer object is used to represent a generic raw binary data buffer.

 To name a few classes:

ArrayBuffer, Uint8Array, DataView, Blob, File, etc.

Binary data in JavaScript is implemented in a non-standard way, compared to other languages. But when we sort things out, everything becomes fairly simple.

To manipulate an ArrayBuffer, we need to use a “view” object.

A view object does not store anything on its own. It’s the “eyeglasses” that give an interpretation of the bytes stored in the ArrayBuffer.

For instance:

**Uint8Array** – treats each byte in ArrayBuffer as a separate number, with possible values from 0 to 255 (a byte is 8-bit, so it can hold only that much). Such value is called a “8-bit unsigned integer”.

**Uint16Array** – treats every 2 bytes as an integer, with possible values from 0 to 65535. That’s called a “16-bit unsigned integer”.

**Uint32Array** – treats every 4 bytes as an integer, with possible values from 0 to 4294967295. That’s called a “32-bit unsigned integer”.

**Float64Array** – treats every 8 bytes as a floating point number with possible values from 5.0x10-324 to 1.8x10308.

## Type array
A typed array in computer programming refers to an array-like data structure that stores elements of a single data type. Unlike regular JavaScript arrays, which can store elements of different data types, typed arrays are designed to store elements of a specific type, such as integers or floating-point numbers, in a more memory-efficient and predictable manner. 
