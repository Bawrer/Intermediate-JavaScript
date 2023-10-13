# notes

## Week 1 day 1 notes Intermediate JS 
 The oldest methods to indicate an additional documents was popup window. 
syntax: window.open('https://javascript.info/')

Most modern browsers are configured to open new tabs instead of separate windows.
We can show another content without closing the main window. we can load content dynamically with fetch and show it in a dynamically generated <div>.  Popups are still used but not everyday.


Still, there are tasks where popups are still used, e.g. for OAuth authorization (login with Google/Facebook/…), because of the following: 

Opening a popup with a third-party non-trusted site is safe.
It’s very easy to open a popup.
A popup can navigate (change URL) and send messages to the opener window.

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## Blocking popups

Blocking popups using JavaScript involves preventing new browser windows or tabs from opening unexpectedly or without user interaction.

we can block popup messages using the following code

window.open('https://javascript.info');

and we can also block the using this one:

button.onclick = () => {

window.open('https://javascript.info');

};

With the above code users are protected from unwanted popups but the functionality of the then is not disabled yet for good.

What if the popup opens from onclick, but after setTimeout?

setTimeout(() => window.open('http://google.com'), 3000); With this amount of time the popups are allowed in chrome but get blocked in firefox but if we lower the delay time for example:

setTimeout(() => window.open('http://google.com'), 1000); the popups are gonna be allowed on both.

The difference is that Firefox treats a timeout of 2000ms or less are acceptable, but after it – removes the “trust”, assuming that now it’s “outside of the user action”. So the first one is blocked, and the second one is not. Blocking popups using JavaScript involves preventing new browser windows or tabs from opening unexpectedly or without user interaction.

we can block popup messages using the following code

window.open('https://javascript.info');

and we can also block the using this one:

button.onclick = () => {

window.open('https://javascript.info');

};

With the above code users are protected from unwanted popups but the functionality of the then is not disabled yet for good.

What if the popup opens from onclick, but after setTimeout?

setTimeout(() => window.open('http://google.com'), 3000); With this amount of time the popups are allowed in chrome but get blocked in firefox but if we lower the delay time for example:

setTimeout(() => window.open('http://google.com'), 1000); the popups are gonna be allowed on both.

The difference is that Firefox treats a timeout of 2000ms or less are acceptable, but after it – removes the “trust”, assuming that now it’s “outside of the user action”. So the first one is blocked, and the second one is not.

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## Window.open method


he window.open() function is a JavaScript method used to open a new browser window or tab (often referred to as a "popup" window) with a specified URL and various optional parameters.

syntax: window.open(url, name, params);

url (string): This is a required parameter that specifies the URL of the web page or resource you want to open in the new window or tab. 

name: (string, optional): This parameter specifies the name of the new window or tab. If a window with the same name already exists, the URL will be loaded in that existing window. If not provided or set to "_blank", a new window or tab will be opened.

params (string, optional): This parameter is used to specify various optional window features, such as the size, position, and behavior of the new window. It is a comma-separated list of feature=value pairs enclosed in single quotes ('').

example:
Opens a new window with Google's homepage.

window.open('https://www.google.com', 'Google', 'width=600,height=400');



menubar (yes/no) – shows or hides the browser menu on the new window.
toolbar (yes/no) – shows or hides the browser navigation bar (back, forward, reload etc) on the new window.
location (yes/no) – shows or hides the URL field in the new window. FF and IE don’t allow to hide it by default.
status (yes/no) – shows or hides the status bar. Again, most browsers force it to show.
resizable (yes/no) – allows to disable the resize for the new window. Not recommended.
scrollbars (yes/no) – allows to disable the scrollbars for the new window. Not recommended.
There is also a number of less supported browser-specific features, which are usually not used. Check window.open in MDN for examples.
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## Accessing popup from window:

The open call returns a reference to the new window. It can be used to manipulate it’s properties, change location and even more.

<!DOCTYPE html>

<script>

"use strict";

let newWindow = open('/', 'example', 'width=300,height=300')

newWindow.focus();

alert(newWindow.location.href); // (*) about:blank, loading hasn't started yet

newWindow.onload = function() {

let html = `<div style="font-size:30px">Welcome!</div>`;

newWindow.document.body.insertAdjacentHTML('afterbegin', html);

};

</script>

immediately after window.open, the new window isn’t loaded yet. That’s demonstrated by alert in line (*). So we wait for onload to modify it. We could also use DOMContentLoaded handler for newWin.document.
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### ACCESSING A WINDOW FROM A POPUP

<!DOCTYPE html>
<html>
<head>
    <title>Popup Window</title>
</head>
<body>
    <button onclick="accessParentWindow()">Access Parent Window</button>
</body>
<script>
    function accessParentWindow() {
        // Access the parent window
        var parentWindow = window.opener;
        
        if (parentWindow) {
            // You can now interact with the parent window
            parentWindow.alert("Accessed the parent window!");
        } else {
            alert("Parent window not found.");
        }
    }
</script>
</html>
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### CLOSING A POPUP

First, make sure you have a reference to the popup window object in your parent window. You can store this reference when you open the popup window using the window.open() method.

var popupWindow; // Declare a variable to store the reference to the popup window


function openPopup() {

// Open the popup window and store the reference

popupWindow = window.open("popup.html", "Popup", "width=400,height=300");

}

//..............................................................................................................................//

To close the popup window, you can use the window.close() method on the popupWindow reference. For example, you can create a function to close the popup window:

function closePopup() {

if (popupWindow && !popupWindow.closed) {

// Check if the popup window is open and not already closed

popupWindow.close();

}

}



a complete code of opening and closing a popup

<!DOCTYPE html>

<html>

<head>

<title>Parent Window</title>

</head>

<body>

<button onclick="openPopup()">Open Popup</button>

</body>

<script>

var popupWindow; // Declare a variable to store the reference to the popup window

function openPopup() {

// Open the popup window and store the reference

popupWindow = window.open("popup.html", "Popup", "width=400,height=300");

}

function closePopup() {

if (popupWindow && !popupWindow.closed) {

// Check if the popup window is open and not already closed

popupWindow.close();

}

}

</script>

</html>
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## SCROLLING AND RESIZING

win.moveBy(x,y)

Move the window relative to current position x pixels to the right and y pixels down. Negative values are allowed (to move left/up).

win.moveTo(x,y)

Move the window to coordinates (x,y) on the screen.

win.resizeBy(width,height)

Resize the window by given width/height relative to the current size. Negative values are allowed.

win.resizeTo(width,height)

Resize the window to the given size.

There’s also window.onresize event.
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### SCROLLING A WINDOW

We already talked about scrolling a window in the chapter Window sizes and scrolling.

win.scrollBy(x,y)

Scroll the window x pixels right and y down relative the current scroll. Negative values are allowed.

win.scrollTo(x,y)

Scroll the window to the given coordinates (x,y).

elem.scrollIntoView(top = true)

Scroll the window to make elem show up at the top (the default) or at the bottom for elem.scrollIntoView(false).

There’s also window.onscroll event.

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Focus/Blur on a window

To blur a specific HTML element:

You can use the blur() method to remove focus from a specific HTML element. For example:

// Blur an input element with the id "myInput"
document.getElementById("myInput").blur();


###To focus on the browser window itself:

If you want to bring the entire browser window into focus, you can use the window.focus() method. However, please note that this method may not always work as expected, as modern browsers often restrict focus-related actions to prevent abuse.

// Focus on the current browser window
window.focus();

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# day 2


## SAME ORIGIN

 For URLs to have the same origin they must have the same protocol, domain and port.


The “Same Origin” policy states that:

if we have a reference to another window, e.g. a popup created by window.open or a window inside <iframe>, and that window comes from the same origin, then we have full access to that window.

otherwise, if it comes from another origin, then we can’t access the content of that window: variables, document, anything.
The only exception is location: we can change it (thus redirecting the user). But we cannot read the location (so we can’t see where the user is now, no information leak).
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### In Action: Frame

1. iframe.contentWindow: This property allows you to access the window object inside the <iframe>. You can use it to manipulate the contents of the iframe or perform actions within it.

var iframe = document.getElementById('myIframe');
var iframeWindow = iframe.contentWindow;
iframeWindow.alert('Hello from iframe!');


2.iframe.contentDocument: This property provides access to the document object inside the <iframe>. It is a shorter way to access the document within the iframe compared to iframe.contentWindow.document.

var iframe = document.getElementById('myIframe');
var iframeDocument = iframe.contentDocument;
var iframeBody = iframeDocument.body;
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Windows on subdomains: document.domain


Generally, two URLs with different domains have different origins, if the windows share the same second-level domain , e.g  borah.site.come, tsepo.site.com and site.com. their second-level domain is site.com.

we are able to make the browser ignore  so that that they can be treated like they can be treated like they are coming from the same origin for purpose of cross-window communication.

In order for it to work each window should run the code:
document.domain = 'site.com'

That’s all. Now they can interact without limitations
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Iframe: wrong document pitfall

The "Wrong Document" pitfall in the context of <iframe> elements is a common issue that developers may encounter when trying to manipulate or 
access the content within an iframe, particularly when dealing with cross-origin iframes.
This pitfall arises because web browsers enforce a security policy known as the Same-Origin Policy, which restricts JavaScript interactions between documents from different origins (i.e., domains).

### Here's what the "Wrong Document" pitfall entails:

Cross-Origin Limitations: If you have an iframe on your page that loads content from a different origin (i.e., a different domain), 
JavaScript running in the parent page (the main document) is generally not allowed to directly access or
manipulate the content within the iframe (the child document).

#Access Denied Errors:
f you attempt to access the iframe's content using techniques like iframe.contentWindow or iframe.contentDocument when the iframe is from a different origin,
you may encounter "Access Denied" or "Permission Denied" errors.

Security Protections: This restriction is in place for security reasons to prevent malicious scripts from one domain from tampering with the content of another domain's iframe.

To work around this pitfall and enable communication between the parent document and the iframe from a different origin, you can use the postMessage API, which allows secure cross-origin communication.
With postMessage, you can send messages and data between the parent and child documents, even if they are from different origins
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Collection: window.frames
Accessing an iframe by index: You can access a specific iframe within the collection using its numerical index. For example:

var firstFrame = window.frames[0]; // Accesses the first iframe
--------------------------------------------------------------------------------
Accessing an iframe by name:
 If an iframe has a name attribute, you can access it by name as well:

var myFrame = window.frames['frameName']; // Accesses the iframe with the name "frameName"
---------------------------------------------------------------------------
Iterating through all iframes: 
You can iterate through all iframes within the current window using a loop:

for (var i = 0; i < window.frames.length; i++) {
  var frame = window.frames[i];
  // Do something with the iframe
}
-----------------------------------------------------------------------------
#### Manipulating iframes:
 You can modify the content, properties, and attributes of iframes through the window.frames collection. For example, you can change the source (URL) of an iframe:

window.frames[0].src = 'newpage.html'; // Changes the source of the first iframe
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## The “sandbox” iframe attribute

The "sandbox" attribute can have several values or a combination of values separated by spaces, each of which represents a specific set of restrictions on the iframe's content. 
The following are some common values:

allow-same-origin: This value allows the iframe's content to be treated as coming from the same origin as the parent page, meaning it can access resources and interact with JavaScript from the same origin.

allow-top-navigation: This value allows the iframe's content to navigate the top-level window (the parent window). Without this value, the content cannot change the URL of the parent window.

allow-forms: If this value is present, the iframe's content is allowed to submit forms. It means that forms inside the iframe can perform form submissions.

allow-scripts: This value permits the execution of JavaScript code within the iframe. Without it, JavaScript execution is disabled within the iframe.

allow-popups: If this value is set, the iframe can open new browser windows or tabs. Without it, attempts to open new windows or tabs will be blocked.

allow-modals: This allows the iframe to open modal dialogs (e.g., alert, confirm, or prompt dialogs).

allow-pointer-lock: If set, the iframe can use the Pointer Lock API to gain control of the mouse cursor.

allow-orientation-lock: If set, the iframe can use the Orientation Lock API to control the screen orientation.

allow-presentation: This allows the iframe to start a presentation session.
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Window Messaging

PostMessage allows windows from different origins to communicate by ignoring some of the restrictions.

So, it’s a way around the “Same Origin” policy. It allows a window from john-smith.com to talk to gmail.comand exchange information, but only if they both agree and call corresponding JavaScript functions. That makes it safe for users.

postMessage() Method: The window.postMessage() method is used to send messages from one window to another. This method takes two parameters: the data you want to send and the target window or window.postMessage(message, targetOrigin).

message: This is the data you want to send, which can be a string, an object, or any serializable data.
targetOrigin: This is the origin of the target window (e.g., "https://example.com"). It specifies the domain of the receiving window and is used as a security measure to prevent cross-origin messaging.
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# Day 3

## Introduction to Clickjacking

It is a technique used by hackers to to make visitors of a certain page to perform a certain action without knowing.

They hide elements under each other . They can do that with the help of CSS properties like: opacity and blur.

we can prevent that using intersection observer.


## Old school defenses (weak)

The old school defense is like the:

if (top != window) {

  top.location = window.location;

} ;

In this case, the window checks if it's the top then if not it makes itself the top.
This is not a reliable defense, because there are many ways to hack around it.

Blocking top-navigation typically refers to a web development practice where certain actions or elements in a web page's user interface are disabled or restricted to the user. This can be done for various reasons, such as to prevent users from navigating away from a particular page, to restrict access to certain features, or to guide users through a specific flow or process.

We can block the transition caused by changing top.location in beforeunload event handler.

The top page (enclosing one, belonging to the hacker) sets a preventing handler to it, like this:

window.onbeforeunload = function() {

  return false;

};

When the iframe tries to change top.location, the visitor gets a message asking them whether they want to leave.

In most cases the visitor would answer negatively because they don’t know about the iframe – all they can see is the top page, there’s no reason to leave. So top.location won’t change.


Sandbox attribute
One of the things restricted by the sandbox attribute is navigation. A sandboxed iframe may not change top.location.

So we can add the iframe with sandbox="allow-scripts allow-forms". That would relax the restrictions, permitting scripts and forms. But we omit allow-top-navigation so that changing top.location is forbidden.

Here’s the code:

<iframe sandbox="allow-scripts allow-forms" src="facebook.html"></iframe>

There are other ways to work around that simple protection too.
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## X-Frame-Options
X-Frame-Options header to control whether a web page can be displayed within a frame when you are building a web application.
To do this, you typically work on the server side to set the header in the HTTP response. 

The header may have 3 values:

##### DENY
Never ever show the page inside a frame.

##### SAMEORIGIN
Allow inside a frame if the parent document comes from the same origin.

#####ALLOW-FROM domain
Allow inside a frame if the parent document is from the given domain.

For instance, Twitter uses X-Frame-Options: SAMEORIGIN.

Here’s the result:

<iframe src="https://twitter.com"></iframe>

Depending on your browser, the iframe above is either empty or alerting you that the browser won’t permit that page to be navigating in this way.

Showing with disabled functionality
The X-Frame-Options header has a side-effect. Other sites won’t be able to show our page in a frame, even if they have good reasons to do so.

So there are other solutions… For instance, we can “cover” the page with a <div> with styles height: 100%; width: 100%;, so that it will intercept all clicks.
That <div> is to be removed if window == top or if we figure out that we don’t need the protection.
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## SAMESITE COOKIES ATTRIBUTE
Another method to prevent clickjacking is samesite cookies attribute.
A cookie with such attribute is only sent to a website if it’s opened directly, not via a frame, or otherwise.
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
# day 4

## ArrayBuffer
TypedArray is the combination of uit8Array, uint16array, uint32array etc. 
They have indexes and iterable.

A typed array constructor (be it Int8Array or Float64Array, doesn’t matter) behaves differently depending on argument types.

#### There are 5 variants of arguments:

new TypedArray(buffer, [byteOffset], [length]);

new TypedArray(object);

new TypedArray(typedArray);

new TypedArray(length);

new TypedArray();


Data Types: TypedArrays provide a way to work with binary data using a fixed type. 
The available data types include Int8Array, Uint8Array, Int16Array, Uint16Array, Int32Array, Uint32Array, Float32Array, and Float64Array.

Fixed Length: Each TypedArray has a fixed length, meaning you cannot change the number of elements after creation. To change the length, you must create a new TypedArray.

Memory Efficiency: TypedArrays are memory-efficient because they store data in a contiguous memory block and have a fixed type. 
This is especially useful when dealing with large datasets or interfacing with lower-level APIs.

Creation: You can create a TypedArray from various sources, including existing arrays, ArrayBuffer, or shared memory using constructors like Uint8Array, Int32Array, etc.

const array = new Uint8Array([1, 2, 3]);


ArrayBuffer: TypedArrays are often used in conjunction with ArrayBuffer, which is a low-level binary data buffer. ArrayBuffer can be shared among different TypedArrays.

 eg, const buffer = new ArrayBuffer(16);
const view1 = new Int8Array(buffer);
const view2 = new Uint32Array(buffer);

Indexed Access: You can access elements in a TypedArray using the standard array indexing notation.

const value = array[0];

data Manipulation: TypedArrays provide methods to manipulate data, such as set, subarray, and more, to copy, slice, or modify portions of the data efficiently.

eg, const newArray = array.subarray(1, 3);

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Out-bound-behaviour
 In JavaScript, out-of-bounds behavior refers to attempting to access or modify elements in an array or other data structures at an index that is outside the valid range of indices.

for example:

const arr = [1, 2, 3];
console.log(arr[10]); // Outputs: undefined

Array Length: The length property of an array indicates the number of elements in the array. If you access an index greater than or equal to the length, you're accessing an out-of-bounds index.
example:

const arr = [1, 2, 3];
console.log(arr.length); // Outputs: 3
console.log(arr[3]); // Outputs: undefined (out of bounds)

Bounds Checking:
JavaScript does not perform bounds checking by default. It's up to the developer to ensure that they don't access out-of-bounds indices.

example: const arr = [1, 2, 3];
const index = 10;

if (index >= 0 && index < arr.length) {
  console.log(arr[index]);
} else {
  console.log("Index is out of bounds");
}
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## TypedDataArray
TypedArray has regular Array methods, with notable exceptions.

We can iterate, map, slice, find, reduce, etc.

There are a few things we can’t do though:

No splice – we can’t “delete” a value, because typed arrays are views on a buffer, and these are fixed, contiguous areas of memory. All we can do is to assign a zero.
No concat method.
There are two additional methods:

arr.set(fromArr, [offset]) copies all elements from fromArr to the arr, starting at position offset (0 by default).
arr.subarray([begin, end]) creates a new view of the same type from begin to end (exclusive). That’s similar to slice method (that’s also supported), but doesn’t copy anything – just creates a new view, to operate on the given piece of data.
These methods allow us to copy typed arrays, mix them, create new arrays from existing ones, and so on.

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## TypedArray methods

TypedArrays in JavaScript come with various methods for manipulating and working with binary data efficiently. Here are short notes on some of the commonly used methods for TypedArrays:


subarray(begin[, end]):

Returns a new TypedArray that references a portion of the original TypedArray, specified by the begin and optional end indices.
Useful for creating views into the same underlying data.


slice(begin[, end]):

Similar to subarray but returns a new TypedArray with the specified portion of the original TypedArray.
Creates a copy of the data if the TypedArray is not backed by an ArrayBuffer.


set(array[, offset]):

Copies the values from a regular array or TypedArray array into the current TypedArray, starting at the optional offset position.
Useful for combining or copying data between TypedArrays.


copyWithin(target, start[, end]):

Copies a portion of the TypedArray and pastes it within the same TypedArray, starting at the target index and replacing elements from start to end.
Modifies the original TypedArray in place.


sort([compareFunction]):

Sorts the elements in the TypedArray, optionally using a custom comparison function specified by compareFunction.
Modifies the original TypedArray.


map(callback[, thisArg]):

Creates a new TypedArray by applying the provided callback function to each element in the original TypedArray.
The thisArg parameter allows setting the context for the callback.


reduce(callback[, initialValue]):

Applies a callback function to the elements of the TypedArray, accumulating a single result.
The initialValue is an optional starting value for the accumulation.


indexOf(searchElement[, fromIndex]):

Searches for the first occurrence of searchElement in the TypedArray, starting from the optional fromIndex.
Returns the index of the found element or -1 if not found.

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## DataView
DataView is a JavaScript object that provides a way to access and manipulate binary data in a more flexible and fine-grained manner compared to TypedArrays.

syntax:
const buffer = new ArrayBuffer(bufferLength); // Create an ArrayBuffer with a specified length in bytes.
const dataView = new DataView(buffer); // Create a DataView to work with the ArrayBuffer.

reading data:
// Reading methods: get<Type>(byteOffset, [littleEndian])

const intValue = dataView.getInt32(byteOffset, littleEndian);
const floatValue = dataView.getFloat32(byteOffset, littleEndian);
const stringValue = dataView.getString(byteOffset, byteLength, encoding);
// ...and more, where <Type> can be Int8, Uint8, Int16, Uint16, Int32, Uint32, Float32, or Float64.

writing data:
// Writing methods: set<Type>(byteOffset, value, [littleEndian])

dataView.setInt32(byteOffset, intValue, littleEndian);
dataView.setFloat32(byteOffset, floatValue, littleEndian);
dataView.setString(byteOffset, stringValue, encoding);
// ...and more, where <Type> can be Int8, Uint8, Int16, Uint16, Int32, Uint32, Float32, or Float64.

combination of the above syntax:

const buffer = new ArrayBuffer(4); // Create a 4-byte buffer
const dataView = new DataView(buffer); // Create a DataView to work with the buffer

dataView.setInt32(0, 12345, true); // Write a 32-bit integer with little-endian byte order
const readValue = dataView.getInt32(0, true); // Read the integer back

console.log(readValue); // Output: 12345
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

 # week 2

# Day 1
## File and FileReader
file object inherits from the Blob. It can be extended to filesystem-related facilities.

You can obtain it in two ways:

-The first way is using a constructor similar to Blob:
new File(fileParts, fileName, [options])

-file can be received from <input type="file">, or drag and drop or other browser interfaces.

Let’s see how the File object can be received from <input type="file">:

<!DOCTYPE html>
  <head>
    <title>Title of the Document</title>
  </head>
  <body>
    <input onchange="showFile(this)" type="file">
    <script>
      function showFile(input) {
        let file = input.files[0];
        alert(`File name: ${file.name}`); 
        alert(`Last modified: ${file.lastModified}`);
      }
    </script>
  </body>
</html>

///////////////////////////////////////////////////////////////////////////////////////////////

                              ## fileReader

The purpose of the fileReader is to read data from Blob objects. It provides data with the usage of events because reading from disk might take long.

The constructor of the FileReader is the following:

let fileReader = new FileReader(); // not a arguments

Its primary methods are as follows:

readAsArrayBuffer(blob) – reading data in binary format ArrayBuffer.
readAsText(blob, [encoding]) – reading the data like a text string with particular encoding (utf-8 by default).

readAsDataURL(blob) – reading the binary data and 
encoding that as base64 data url.

abort() – canceling the action.

The choice of read method depends on which format we prefer, how we are going to use data.

readAsArrayBuffer – for binary files, to do low-level binary operations. For high-level operations, like slicing, File inherits from Blob, so we can call them directly, without reading.

readAsText – for text files, when we’d like to get a string.

readAsDataURL – when we’d like to use this data in src for img or another tag. There’s an alternative to reading a file for that, as discussed in chapter Blob: URL.createObjectURL(file).

The events that can trigger during the process of reading are the following:

### loadstart
progress
load-This event is triggered when the file is successfully loaded.
abort- This event is triggered if the reading operation is aborted.
error-This event is triggered if an error occurs while reading the file.
loadend

##### When the reading is finished, we can access the result as:

reader.result is the result (if successful)
reader.error is the error (if failed).
The most widely used events are for sure load and error.

#### An example of reading a file will look as follows:

 <!DOCTYPE html>
  <head>
    <meta charset="utf-8">
    <title>Title of the Document</title>
  </head>
  <body>
    <input onchange="readFile(this)" type="file">
    <script>
      function readFile(input) {
        let file = input.files[0]; 
        let reader = new FileReader(); 
        reader.readAsText(file); 
        reader.onload = function() {
         console.log(fileReader.result);
        }; 
        reader.onload = function() {
          console.log(fileReader.error);
        }; 
      }
    </script>
  </body>
</html>
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

#### Here’s an example of reading a file

Here’s an example of reading a file:

<!DOCTYPE html>
  <head>
    <meta charset="utf-8">
    <title>Title of the Document</title>
  </head>
  <body>
    <input onchange="readFile(this)" type="file">
    <script>
      function readFile(input) {
        let file = input.files[0]; 
        let reader = new FileReader(); 
        reader.readAsText(file); 
        reader.onload = function() {
         console.log(fileReader.result);
        }; 
        reader.onload = function() {
          console.log(fileReader.error);
        }; 
      }
    </script>
  </body>
</html>

## FileReader for blobs:

FileReadercan read not just files, but any blobs.

we can also use it convert blobs to another format.

Use the readAsArrayBuffer, readAsDataURL, or readAsText method of the FileReader object to read the Blob's data and convert it to a different format.

FileReaderSync is available inside Web Workers:

there is also a syncrocronous variant of fileReader called fileRaedersync and its reading methods read* do not generate events, but rather return a result, as regular functions do.
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


## FETCH

The fetch API is used for making network requests, typically HTTP requests, to retrieve data from a server or API.
we can: 
Submit an order,
Load user information,
Receive latest updates from the server. We can achoeve all this with the use of AJAX term( Asynchronous JavaScript and Xml).

one of the methods that we can use to send a network request and get information from the server and the modern one is fetch() method.

The basic syntax is:

let promise = fetch(url, [options])

url – the URL to access.

options – optional parameters: method, headers etc.

the promise resolves with an object of the built-in Response class as soon as the server responds with headers.
The we check if the HTTP was successful or not. The promise reject if the fetch was unable to make HTTP request.
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## POST REQUEST
you can make POST requests to send data to a server using the fetch API .

// Define the URL and data to send
const url = 'https://example.com/api';
const data = {
  key1: 'value1',
  key2: 'value2'
};

// Create the request object
const requestOptions = {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json' // Set the content type to JSON
  },
  body: JSON.stringify(data) // Convert data to JSON string
};

// Make the POST request
fetch(url, requestOptions)
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json(); // Parse the response as JSON
  })
  .then(data => {
    console.log(data); // Handle the response data
  })
  .catch(error => {
    console.error('There was a problem with the fetch operation:', error);
  });

  /////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

  ## SENDING IMAGE IN JS
  response.status – HTTP code of the response,

response.ok – true is the status is 200-299.

response.headers – Map-like object with HTTP headers.

Methods to get response body:

response.json() – parse the response as JSON object,

response.text() – return the response as text,

response.formData() – return the response as FormData object (form/multipart encoding, see the next chapter),

response.blob() – return the response as Blob(binary data with type),

response.arrayBuffer() – return the response as ArrayBuffer (pure binary data),

Fetch options so far:

method – HTTP-method,

headers – an object with request headers (not any header is allowed),

body – string, FormData, BufferSource, Blob or UrlSearchParams object to send.
..............................................................................................................

## FECTHING USER FROM GITHUB

async function getUsers(names) {
  try {
    const githubUsers = [];

    // Loop through each username and fetch user data
    for (const name of names) {
      const response = await fetch(`https://api.github.com/users/${name}`);
      
      if (!response.ok) {
        throw new Error(`Failed to fetch GitHub user for ${name}`);
      }
      
      const user = await response.json();
      githubUsers.push(user);
    }

    return githubUsers;
  } catch (error) {
    console.error('Error:', error);
    return []; // Return an empty array in case of an error
  }
}

// Example usage:
const usernames = ['user1', 'user2', 'user3']; // Replace with the GitHub usernames you want to fetch
getUsers(usernames)
  .then(users => {
    console.log('GitHub Users:', users);
  })
  .catch(err => {
    console.error('Error:', err);
  });


This code defines an async function called getUsers that takes an array of GitHub usernames (names) as an argument.

Inside the function, it initializes an empty array called githubUsers to store the fetched user data.

It uses a for...of loop to iterate through each username in the input array.

Within the loop, it makes a fetch request to the GitHub API to retrieve the user data for each username.

If the fetch request is successful (response.ok), it parses the JSON response and pushes the user object into the githubUsers array.

If there's any error during the fetch or parsing, it catches the error and logs it to the console, returning an empty array.

Finally, it returns the githubUsers array containing the GitHub user data.

You can call this getUsers function with an array of GitHub usernames, and it will return an array of GitHub users' data based on the input usernames.

 ///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# Day 2
 

## SENDING A SIMPLE FORM

Create an HTML Form:
First, create an HTML form in your HTML file.

Add Event Listener:
Next, add an event listener to the form to handle the submission. You can use the addEventListener method to do this.

Define a Function to Send Data:
Create a JavaScript function (sendDataToServer in this example) that will handle the form data. You can send the data to a server using an HTTP request, or you can process it locally in JavaScript.

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## FORMDATA METHODS

in javaScript, the FormData object provides methods and properties for working with HTML forms and their data. It's particularly useful for handling form data in a way that makes it easy to send to a server via AJAX or fetch requests.

here is the list of commonly used method:
1) Constructor: You can create a FormData object by passing a form element or a DOM document as an argument to the constructor. 

const form = document.querySelector('form');
const formData = new FormData(form);

2) append(name, value): This method adds a new field with a specified name and value to the FormData object. If a field with the same name already exists, it appends a new value to it.
formData.append('username', 'john_doe');

3) delete(name): This method deletes a field with the specified name from the FormData object.

formData.delete('username');


4)get(name): This method retrieves the first value associated with a specified name from the FormData object.
const username = formData.get('username');

5) has(name): This method checks if a field with the specified name exists in the FormData object and returns a boolean value.
const hasUsername = formData.has('username');
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## SENDING A FORM WITH A FILE

This is how we can send a form with a file:

<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Document</title>
</head>
<body>
   <form id="formEl">
      <input type="text" name="firstName" value="BORAH">
      picture: <input type="file" name="Picture" 
 accept="image/*">
      <input type="submit">

      <script>
         formEle.onsubmit = async(e) => {
         e.preventDefault();

         let response = await 
           fetch('/article/formdata/post/user-avater',{
            method: 'POST',
            body: new Formdata(formEle)
         });

         let result = await response.json();

         alert(result.message);
         };
      </script>
   </form>
   
</body>
</html>
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# DAY 3

## Fetch: Cross-Origin Requests 

 Cross-Origin Requests is a security feature implemented by web browsers to control and restrict web pages from making requests to a different domain than the one from which the web page originated. 
 
This security measure is designed to prevent malicious websites from accessing sensitive data on other websites without permission. 
 
To successfully make cross-origin requests with fetch(): 
try { 
 
await fetch('http://example.com'); 
 
} catch(err) { 
 
alert(err); // Failed to fetch 
 
} 
 
Fetch fails, as expected, because cross-origin restrictions protect the internet from evil hackers. 

 

## Using Forms 

 One way to communicate with another server was to submit a <form> there. People submitted it into <iframe>, just to stay on the current page. 
 
it was possible to make a GET/POST request to another site, even without networking methods. But as it’s forbidden to access the content of an <iframe>from another site, it wasn’t possible to read the response. 
 
As we can see, forms allowed to send data anywhere, but not receive the response. To be precise, there were actually tricks for that (required special scripts at both the iframe and the page), but let these dinosaurs rest in peace. 

 

## Simple Requests 

 A simple request is a request that satisfies two conditions: 
 
Simple method: GET, POST or HEAD 
 
Simple headers – the only allowed custom headers are: 
 
Accept, 
Accept-Language, 
Content-Language, 
Content-Type with the value application/x-www-form-urlencoded, multipart/form-data or text/plain. 

CORS for Simple Requests 

 If a request is cross-origin, the browser always adds Origin header to it. 
 
For instance, if we request https://anywhere.com/request from https://javascript.info/page, the headers will be like: 
 
GET /request 
Host: anywhere.com 
Origin: https://javascript.info 
 
As you can see, Origin contains exactly the origin (domain/protocol/port), without a path. 
 
The server can inspect the Origin and, if it agrees to accept such a request, adds a special header Access-Control-Allow-Origin to the response. That header should contain the allowed origin (in our case https://javascript.info), or a star *. Then the response is successful, otherwise an error. 
 
The browser plays the role of a trusted mediator here: 
 
It ensures that the correct Origin is sent with a cross-domain request. 
 
If checks for correct Access-Control-Allow-Origin in the response, if it is so, then JavaScript access, otherwise forbids with an error. 

Response Headers 

 For cross-origin request, by default JavaScript may only access “simple response headers”: 
 
Cache-Control 
Content-Language 
Content-Type 
Expires 
Last-Modified 
Pragma 
 
Any other response header is forbidden. 

Non-simple Requests 

 Non-simple requests refer to certain types of HTTP requests made from a web page to a different domain (origin) using JavaScript's XMLHttpRequest or the Fetch API. 
These requests are considered non-simple because they trigger additional security checks due to the potential for cross-origin security issues. 
 
A preflight request uses method OPTIONS and has nobody. 
 
Access-Control-Request-Method header has the requested method. 
Access-Control-Request-Headers header provides a comma-separated list of non-simple HTTP-headers. 
If the server agrees to serve the requests, then it should respond with status 200, without body. 
 
The response header Access-Control-Allow-Methods must have the allowed method. 
The response header Access-Control-Allow-Headers must have a list of allowed headers. 
Additionally, the header Access-Control-Max-Age may specify a number of seconds to cache the permissions. So the browser won’t have to send a preflight for subsequent requests that satisfy given permissions. 

 ## Credentials 

 A cross-origin request by default does not bring any credentials (cookies or HTTP authentication). 
 
That’s uncommon for HTTP-requests. Usually, a request to http://site.com is accompanied by all cookies from that domain. But cross-domain requests made by JavaScript methods are an exception. 
 
For example, fetch('http://another.com') does not send any cookies, even those that belong to another.com domain. 
 
Why? 
 
That’s because a request with credentials is much more powerful than an anonymous one. If allowed, it grants JavaScript the full power to act and access sensitive information on behalf of a user. 
 
Does the server really trust pages from Origin that much? Then it must explicitly allow requests with credentials with an additional header. 
 
To send credentials, we need to add the option credentials. 

 ## Fetch API 

 The Fetch API is a modern JavaScript interface for making network requests, such as fetching resources from a server or making API calls, in a web browser. 
It provides a more powerful and flexible alternative to the older XMLHttpRequest (XHR) API. 
The Fetch API is designed to be more straightforward to use and is based on promises, making it easier to work with asynchronous operations. 
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# DAY 4

# Regular Expressions 

A regular expression consists of a pattern and optional flags. 
 
## There are two syntaxes to create a regular expression object. 
 
#### 1. The long syntax: 
 
regexp = new RegExp("pattern", "flags"); 
 
### 2 The short one, using slashes "/": 
 
regexp = /pattern/; // no flags 
regexp = /pattern/gmi; // with flags g,m and i (to be covered soon) 
 
Slashes "/" tell JavaScript that we are creating a regular expression. They play the same role as quotes for strings. 

## Patterns and Flags 

 A regular expression consists of a pattern and optional flags. 
 
There are two syntaxes to create a regular expression object. 
 
1. The long syntax: 
 
regexp = new RegExp("pattern", "flags"); 
 
2 The short one, using slashes "/": 
 
regexp = /pattern/; // no flags 
regexp = /pattern/gmi; // with flags g,m and i (to be covered soon) 
 
Slashes "/" tell JavaScript that we are creating a regular expression. They play the same role as quotes for strings. 

Usage 

 To search inside a string, we can use method search. 
 
Here’s an example: 
 
let str = "I love JavaScript!"; // will search here 
 
let regexp = /love/; 
 
alert( str.search(regexp) ); // 2 
 
Colors 
 
From here on the color scheme is: 
 
regexp – red 
string (where we search) – blue 
result – green 
 
#### When to use new RegExp? 
 
Normally we use the short syntax /.../. But it does not support variable insertions ${...}. 
 
On the other hand, new RegExp allows to construct a pattern dynamically from a string, so it’s more flexible. 
 
Here’s an example of a dynamically generated regexp: 
 
let tag = prompt("Which tag you want to search?", "h2"); 
 
let regexp = new RegExp([Math Processing Error]); 
 
// finds <h2> by default 
 
alert( "<h1> <h2> <h3>".search(regexp)); 

 Regular expressions may have flags that affect the search. 
 
There are only 6 of them in JavaScript: 
 
i 
With this flag the search is case-insensitive: no difference between A and a . 
 
g 
With this flag the search looks for all matches, without it – only the first one 
 
m 
Multiline mode. 
 
s 
“Dotall” mode, allows . to match newlines. 
 
u 
Enables full unicode support. The flag enables correct processing of surrogate pairs. 
 
y 
Sticky mode 

Flags 

 Regular expressions may have flags that affect the search. 
 
There are only 6 of them in JavaScript: 
 
i 
With this flag the search is case-insensitive: no difference between A and a . 
 
g 
With this flag the search looks for all matches, without it – only the first one 
 
m 
Multiline mode. 
 
s 
“Dotall” mode, allows . to match newlines. 
 
u 
Enables full unicode support. The flag enables correct processing of surrogate pairs. 
 
y 
Sticky mode. 

Methods of RegExp and String 

 To search for all matches: 
 
Use regexp g flag and: 
 
Get a flat array of matches – str.match(reg) 
Get an array or matches with details – str.matchAll(reg). 
To search for the first match only: 
 
Get the full first match – str.match(reg) (without g flag). 
Get the string position of the first match – str.search(reg). 
Check if there’s a match – regexp.test(str). 
Find the match from the given position – regexp.exec(str) (set regexp.lastIndex to position). 
To replace all matches: 
 
Replace with another string or a function result – str.replace(reg, str|func) 
To split the string by a separator: 
 
str.split(str|reg) 

Character classes 

 A character class is a special notation that matches any symbol from a certain set. 
 
For the start, let’s explore a “digit” class. It’s written as \d. We put it in the pattern, that means “any single digit”. 
 
For instance, the let’s find the first digit in the phone number: 
 
let str = "+7(903)-123-45-67"; 
 
let reg = /\d/; 
 
alert( str.match(reg) ); // 7 
 
Without the flag g, the regular expression only looks for the first match, that is the first digit \d. 
 
Let’s add the g flag to find all digits: 
 
let str = "+7(903)-123-45-67"; 
 
let reg = /\d/g; 
 
alert( str.match(reg) ); // array of matches: 7,9,0,3,1,2,3,4,5,6,7 
 
alert( str.match(reg).join('') ); // 79035419441 
 
That was a character class for digits. There are other character classes as well. 
 
Most used are: 
 
\d (“d” is from “digit”) 
 
A digit: a character from 0 to 9. 
 
\s (“s” is from “space”) 
 
A space symbol: that includes spaces, tabs, newlines. 

Word boundary \b 

 A word boundary \b – is a special character class. 
 
It does not denote a character, but rather a boundary between characters. 
 
For instance, \bJava\b matches Java in the string Hello, Java!, but not in the script Hello, JavaScript!. 
 
alert( "Hello, Java!".match(/\bJava\b/) ); // Java 
 
alert( "Hello, JavaScript!".match(/\bJava\b/) ); // null 
 
The boundary has “zero width” in a sense that usually a character class means a character in the result (like a wordly character or a digit), but not in this case. 
 
The boundary is a test. 
 
When regular expression engine is doing the search, it’s moving along the string in an attempt to find the match. At each string position it tries to find the pattern. 

Inverse Classes 

 For every character class there exists an “inverse class”, denoted with the same letter, but uppercased. 
 
The “reverse” means that it matches all other characters, for instance: 
 
\D 
Non-digit: any character except \d, for instance a letter. 
 
\S 
Non-space: any character except \s, for instance a letter. 
 
\W 
Non-wordly character: anything but \w. 
 
\B 
Non-boundary: a test reverse to \b. 
 
In the beginning of the chapter we saw how to get all digits from the phone +7(903)-123-45-67. 
 
One way was to match all digits and join them: 
 
let str = "+7(903)-123-45-67"; 
 
alert( str.match(/\d/g).join('') ); // 79031234567 
 
An alternative, shorter way is to find non-digits \D and remove them from the string: 
 
let str = "+7(903)-123-45-67"; 
 
alert( str.replace(/\D/g, "") ); // 79031234567 

 

Spaces are regular characters 

 Usually we pay little attention to spaces. For us strings 1-5 and 1 - 5 are nearly identical. 
But if a regexp doesn’t take spaces into account, it may fail to work. 
Let’s try to find digits separated by a dash: 
alert( "1 - 5".match(/\d-\d/) ); // null, no match! 
Here we fix it by adding spaces into the regexp \d - \d: 
alert( "1 - 5".match(/\d - \d/) ); // 1 - 5, now it works 
A space is a character. Equal in importance with any other character. 
Of course, spaces in a regexp are needed only if we look for them. Extra spaces (just like any other extra characters) may prevent a match: 
alert( "1-5".match(/\d - \d/) ); // null, because the string 1-5 has no spaces 
In other words, in a regular expression all characters matter, spaces too. 

A dot is any character 

 The dot "." is a special character class that matches “any character except a newline”. 
 
For instance: 
 
alert( "Z".match(/./) ); // Z 
 
Or in the middle of a regexp: 
 
let reg = /CS.4/; 
 
alert( "CSS4".match(reg) ); // CSS4 
 
alert( "CS-4".match(reg) ); // CS-4 
 
alert( "CS 4".match(reg) ); // CS 4 (space is also a character) 
 
Please note that the dot means “any character”, but not the “absense of a character”. There must be a character to match it: 
 
alert( "CS4".match(/CS.4/) ); // null, no match because there's no character for the dot 

The dotall “s” flag 

 Usually a dot doesn’t match a newline character. 
 
For instance, A.B matches A, and then B with any character between them, except a newline. 
 
This doesn’t match: 
 
alert( "A\nB".match(/A.B/) ); // null (no match) 
 
// a space character would match, or a letter, but not \n 
 
Sometimes it’s inconvenient, we really want “any character”, newline included. 
 
That’s what s flag does. If a regexp has it, then the dot "." match literally any character: 
 
alert( "A\nB".match(/A.B/s) ); // A\nB (match!) 

 

## Escaping, Special character 

 As we’ve seen, a backslash "\" is used to denote character classes. So it’s a special character in regexps (just like in a regular string). 
 
There are other special characters as well, that have special meaning in a regexp. They are used to do more powerful searches. Here’s a full list of them: [ \ ^ $ . | ? * + ( ). 
 
Don’t try to remember the list – soon we’ll deal with each of them separately and you’ll know them by heart automatically. 
 
Escaping 
Let’s say we want to find a dot literally. Not “any character”, but just a dot. 
 
To use a special character as a regular one, prepend it with a backslash: \.. 
 
That’s also called “escaping a character”. 
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# Week-3
# DAY  1
**Node.js Introduction:**

1. **What is Node.js?**
   - Node.js is an open-source, server-side JavaScript runtime environment.
   - It allows you to execute JavaScript code on the server, as opposed to just in the browser.
   - Node.js is built on the V8 JavaScript engine, which is the same engine used by Google Chrome.

2. **Key Features:**
   - **Non-Blocking & Asynchronous:** Node.js is designed to be non-blocking and event-driven. It uses an event loop to handle multiple requests efficiently without blocking the execution of other code.
   - **High Performance:** Due to its non-blocking nature and V8 engine, Node.js is highly performant and can handle a large number of concurrent connections.
   - **NPM (Node Package Manager):** Node.js comes with NPM, a package manager that allows you to easily install and manage libraries and packages for your applications.
   - **Cross-Platform:** Node.js is cross-platform and runs on Windows, macOS, and various Linux distributions.
   - **Single Language:** Using JavaScript both on the front end and the back end can simplify development and code sharing.

**Notes on Node.js:**

1. **Setting Up Node.js:**
   - Download and install Node.js from the official website.
   - Verify the installation by running `node -v` and `npm -v` in your terminal.

2. **Creating a Basic Node.js Application:**
   - You can create a Node.js application by creating a JavaScript file (e.g., `app.js`) and writing your code in it.
   - Use the `require` function to include built-in or external modules.

3. **Modules:**
   - Node.js provides a modular system where you can break your application into smaller, reusable modules.
   - Use the `module.exports` to export functions, objects, or variables from a module, and `require` to import them.

4. **NPM (Node Package Manager):**
   - NPM is a package manager for Node.js that allows you to easily install, update, and manage third-party libraries.
   - Use `npm init` to create a `package.json` file, which tracks your project's dependencies and settings.
   - Install packages using `npm install package-name` and manage dependencies in your project.

5. **Event Loop:**
   - Node.js is event-driven, and it uses an event loop to manage and handle asynchronous operations.
   - Callbacks are often used to handle the results of asynchronous operations.

6. **Common Use Cases:**
   - Building web servers and APIs using frameworks like Express.js.
   - Real-time applications such as chat applications or online games.
   - Development of build tools and task automation using tools like Grunt or Gulp.
   - Data streaming and processing.

7. **Debugging and Testing:**
   - Node.js provides debugging and testing tools. You can use the built-in debugger and libraries like Mocha for testing.

8. **Community and Resources:**
   - Node.js has a large and active community, and there are numerous resources, tutorials, and libraries available.

9. **Security:**
   - Be mindful of security, as Node.js applications can be vulnerable to common web application security issues. Follow best practices to secure your applications.

10. **Scalability:**
    - Node.js is well-suited for building scalable applications, but you may need to consider load balancing and clustering for high-traffic applications.

Node.js is a powerful and versatile runtime environment for building a wide range of applications. It has gained popularity for its speed, scalability, and the ability to use JavaScript both on the client and server sides.


# DAY 2
## Libraries of Node.js 
explanation with example

### Express.js (Web Framework):
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, Node.js!');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});


### Mongoose (MongoDB Interaction):const http = require('http');
const server = http.createServer(app);
const io = require('socket.io')(server);

io.on('connection', (socket) => {
  console.log('A user connected');
  socket.on('chat message', (msg) => {
    io.emit('chat message', msg);
  });
});


const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  email: String,
});

const User = mongoose.model('User', userSchema);


### Socket.io (Real-Time Communication):
const http = require('http');
const server = http.createServer(app);
const io = require('socket.io')(server);

io.on('connection', (socket) => {
  console.log('A user connected');
  socket.on('chat message', (msg) => {
    io.emit('chat message', msg);
  });
});

### Passport (Authentication):

const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

passport.use(new LocalStrategy((username, password, done) => {
  // Check user credentials and call done() accordingly
}));


### Passport (Authentication):
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

passport.use(new LocalStrategy((username, password, done) => {
  // Check user credentials and call done() accordingly
}));

# DAY 3
## Sprites  in game development:
**Sprites in Game Development: A Summary**

**What is a Sprite?**

- In game development, a sprite is a 2D image or animation used to represent game objects, characters, or other elements within a video game.
- Sprites can be characters, items, enemies, background elements, and more.

**Key Concepts and Notes:**

1. **2D Graphics:**
   - Sprites are primarily used in 2D games, although they can also be employed in some 3D games for special effects or user interface elements.

2. **Animation:**
   - Sprites can be static images or animated sequences of images, allowing for movement and interaction within the game.

3. **Sprite Sheets:**
   - To efficiently manage and animate sprites, game developers often use sprite sheets, which are large images containing multiple frames or states of a sprite.

4. **Transparency:**
   - Sprites often feature transparency (alpha channels) to create non-rectangular shapes or smooth edges, eliminating the need for a rectangular bounding box.

5. **Collision Detection:**
   - Collision detection algorithms are used to determine when sprites interact or collide within the game world. Precise collision shapes can be defined for each sprite.

6. **Rendering:**
   - Sprites are rendered on the screen in layers to create the game world. Proper ordering of sprite layers is crucial for realistic gameplay.

7. **Performance Optimization:**
   - Techniques like sprite batching, object pooling, and efficient rendering pipelines are employed to optimize sprite performance, especially in games with a large number of sprites.

8. **Physics and Motion:**
   - Game engines often include physics engines that help manage the motion and behavior of sprites. This includes factors like gravity, acceleration, and friction.

9. **Z-Ordering:**
   - Z-ordering is used to determine the depth or layering of sprites, allowing certain sprites to appear in front of or behind others.

**Examples:**

- In a platformer game, a character sprite represents the player's character and includes various animations for walking, jumping, and attacking.
- In a top-down shooter, enemy sprites represent various types of enemies, each with distinct behaviors and attack patterns.
- In a puzzle game, puzzle piece sprites are manipulated by the player to solve puzzles.
- In a racing game, car sprites represent different vehicles and have animations for movement and collisions.

**Tools and Frameworks:**

- Game developers often use graphic design software like Adobe Photoshop, GIMP, or Aseprite to create sprites.
- Game engines like Unity, Godot, and Unreal Engine provide tools for importing, animating, and managing sprites within a game project.

Sprites are fundamental elements in 2D game development, and their design and implementation play a crucial role in creating an engaging and visually appealing gaming experience.

# day 4
## Assigning a Sprite to a Player in Game Development: 
A Summary**

In game development, assigning a sprite to a player involves associating a 2D image or animation (the sprite) with a game character or entity (the player). Here's a summary of the key concepts and steps involved in this process:

**1. Player Representation:**
   - A player in a game needs a visual representation to interact with the game world. This representation is typically a sprite, which can be a character, object, or any other visual element.

**2. Sprite Creation:**
   - Create or import a sprite that represents the player character. The sprite can be designed using graphic design software or obtained from sprite libraries.

**3. Sprite Sheets:**
   - If the player character has multiple animations or states (e.g., walking, running, jumping), organize these frames into a sprite sheet. Sprite sheets are efficient for managing animations.

**4. Integration with Game Engine:**
   - Use a game engine or development framework to integrate the sprite into the game project. Most engines provide tools for importing, managing, and animating sprites.

**5. Positioning and Rendering:**
   - Define the position of the player character in the game world. Ensure that the sprite is rendered at the correct location on the screen.

**6. Animation Handling:**
   - Implement the logic for animating the sprite. Depending on the game engine, this can involve setting up animations within the engine, updating frames, and controlling animations based on player actions.

**7. Interaction and Control:**
   - Program the player's interactions and control mechanisms. For example, map keyboard or controller inputs to the player's movement and actions.

**8. Collision Detection:**
   - Implement collision detection to ensure that the player sprite interacts correctly with other game elements, such as objects, enemies, or obstacles.

**9. Z-Ordering:**
   - Determine the sprite's Z-order or layering to ensure that the player character appears in front of or behind other game elements as appropriate.

**10. Feedback and Feedback:**
   - Implement feedback mechanisms like sound effects, particle effects, and visual indicators to enhance the player's experience.

**11. Testing and Iteration:**
   - Thoroughly test the player's interaction with the sprite, including movement, animations, and collision detection. Refine and iterate on the implementation as needed.

**12. Player Customization (Optional):**
   - In some games, players can customize their characters with different sprites or appearances. Implement player customization options if relevant to the game.

Assigning a sprite to a player is a fundamental aspect of game development, enabling players to visually engage with and control their in-game avatars. Careful design and implementation of player sprites contribute to the overall gaming experience.


## managing a game server:

**Managing the Game Server: Key Notes**

Managing a game server is a critical aspect of multiplayer and online gaming. It involves setting up, maintaining, and optimizing the server to ensure a smooth and enjoyable gaming experience for players. Here are some key notes on managing a game server:

1. **Server Hosting:**
   - Choose a reliable hosting provider or cloud platform to host your game server. Common choices include AWS, Azure, Google Cloud, or specialized game server hosting services.

2. **Server Hardware and Resources:**
   - Select hardware and resources that match your game's requirements, including CPU, RAM, storage, and network bandwidth. Ensure scalability for player demand.

3. **Server Software:**
   - Install and configure the necessary server software. Popular choices include game server engines like Unity, Unreal Engine, or custom server implementations using Node.js, Java, C++, etc.

4. **Server Security:**
   - Implement robust security measures to protect the server from DDoS attacks, cheating, and unauthorized access. Use firewalls, anti-cheat systems, and encryption.

5. **Data Management:**
   - Manage player data, including profiles, progress, and in-game assets. Implement a secure database system to store and retrieve player data.

6. **Player Authentication:**
   - Use authentication systems to verify the identity of players. Common methods include username/password, OAuth, or token-based authentication.

7. **Game Logic and Networking:**
   - Develop and manage game logic on the server-side to ensure consistency and fairness. Implement efficient networking code for real-time multiplayer interactions.

8. **Server Monitoring:**
   - Implement monitoring tools to track server performance, player activity, and potential issues. Tools like Prometheus, Grafana, or custom dashboards can help.

9. **Scalability:**
   - Design the server architecture to scale horizontally to accommodate a growing player base. Load balancers can distribute traffic across multiple server instances.

10. **Player Matching:**
    - Implement matchmaking systems to pair players with opponents or teammates of similar skill levels. This ensures balanced gameplay.

11. **Server Updates and Maintenance:**
    - Regularly update the server software and game code to fix bugs, enhance security, and introduce new features. Plan for scheduled maintenance and downtime.

12. **Backups and Disaster Recovery:**
    - Implement data backups and disaster recovery plans to prevent data loss and recover from server failures.

13. **Server Performance Optimization:**
    - Optimize server performance by reducing latency, minimizing network traffic, and managing server resources efficiently.

14. **Community Management:**
    - Manage player communities by providing support, addressing issues, and moderating in-game interactions.

15. **Legal and Compliance:**
    - Ensure that the server and game comply with legal regulations and user agreements, including data protection laws and terms of service.

16. **Communication Channels:**
    - Set up communication channels for players, such as forums, in-game chat, or support tickets, to address questions and concerns.

17. **Documentation and Reporting:**
    - Maintain detailed documentation for server configurations, incidents, and player support interactions. Reporting tools can help track server performance and player feedback.

18. **User Authentication and Authorization:**
    - Implement user authentication to ensure that only authorized players can access the game server. Also, manage user roles and permissions as needed.

Managing a game server is a complex and ongoing process that requires a deep understanding of game development, server administration, security, and player management. Regular updates, monitoring, and player engagement are crucial for a successful gaming experience.

 

 
