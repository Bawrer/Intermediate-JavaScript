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

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Blocking popups

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

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
Window.open method


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
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Accessing popup from window:

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
ACCESSING A WINDOW FROM A POPUP

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

