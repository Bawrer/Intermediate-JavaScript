# week1-notes

## Week 1 day 1 notes Intermediate JS 
 The oldest methods to indicate an additional documents was popup window. 
syntax: window.open('https://javascript.info/')

Most modern browsers are configured to open new tabs instead of separate windows.
We can show another content without closing the main window. we can load content dynamically with fetch and show it in a dynamically generated <div>.  Popups are still used but not everyday.


Still, there are tasks where popups are still used, e.g. for OAuth authorization (login with Google/Facebook/…), because of the following: 

Opening a popup with a third-party non-trusted site is safe.
It’s very easy to open a popup.
A popup can navigate (change URL) and send messages to the opener window.

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

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

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

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
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

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
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

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

###CLOSING A POPUP

First, make sure you have a reference to the popup window object in your parent window. You can store this reference when you open the popup window using the window.open() method.

var popupWindow; // Declare a variable to store the reference to the popup window

//..................................................................................................................................//

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

//.................................................................................//

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
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

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

###Focus/Blur on a window

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

###Windows on subdomains: document.domain


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
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<The “sandbox” iframe attribute>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
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
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

###Window Messaging

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

DENY
Never ever show the page inside a frame.

SAMEORIGIN
Allow inside a frame if the parent document comes from the same origin.

ALLOW-FROM domain
Allow inside a frame if the parent document is from the given domain.

For instance, Twitter uses X-Frame-Options: SAMEORIGIN.

Here’s the result:

<iframe src="https://twitter.com"></iframe>

Depending on your browser, the iframe above is either empty or alerting you that the browser won’t permit that page to be navigating in this way.

Showing with disabled functionality
The X-Frame-Options header has a side-effect. Other sites won’t be able to show our page in a frame, even if they have good reasons to do so.

So there are other solutions… For instance, we can “cover” the page with a <div> with styles height: 100%; width: 100%;, so that it will intercept all clicks.
That <div> is to be removed if window == top or if we figure out that we don’t need the protection.
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

## SAMESITE COOKIES ATTRIBUTE
Another method to prevent clickjacking is samesite cookies attribute.
A cookie with such attribute is only sent to a website if it’s opened directly, not via a frame, or otherwise.


