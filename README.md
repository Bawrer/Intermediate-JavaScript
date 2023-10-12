# week1-notes

Week 1 day 1 notes Intermediate JS 
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
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

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
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
CLOSING A POPUP

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
## SCROLLING AND RESIZING---------------------------->>>>>>>>>>>>>>>>>>

win.moveBy(x,y)

Move the window relative to current position x pixels to the right and y pixels down. Negative values are allowed (to move left/up).

win.moveTo(x,y)

Move the window to coordinates (x,y) on the screen.

win.resizeBy(width,height)

Resize the window by given width/height relative to the current size. Negative values are allowed.

win.resizeTo(width,height)

Resize the window to the given size.

There’s also window.onresize event.
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

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

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
