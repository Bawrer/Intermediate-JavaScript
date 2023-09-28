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

