# item-under-trigger

Hide a HTML item behind a trigger using `CSS` and `JavaScript`.

## Usage

The HTML example code contains a `div` element with an `id` of `myDiv`, which contains a heading and some text. There is also a button element with an `onclick` attribute set to `hideDiv()`, which will call the `hideDiv()` function when the button is clicked.

```html
<div id="myDiv">
  <h2>My Div</h2>
  <p>This is my div.</p>
</div>

<button onclick="hideDiv()">Hide Div</button>
```

The `hideDiv()` function is defined in the JavaScript code. This function uses the `getElementById()` method to select the `div` element with the `myDiv` ID and sets its `display` property to "none". This will hide the `div` element from view when the button is clicked.

```javascript
function hideDiv() {
  document.getElementById("myDiv").style.display = "none";
}
```

In summary, the example code provides a simple way to hide a `div` element when a trigger event occurs. This can be adapted for various purposes by replacing the trigger event and the function that is called within the event handler.

## Example: hide a `<div>` guarding an email under Cloudflare's CAPTCHA service Turnstile

### HTML

The CSS code sets the `display` property of elements with class `captcha-box` to "none". This means that when the webpage is first loaded, the captcha box will be hidden.

The HTML code consists of two `div` elements. The first `div` has an `id` of `turnstile-widget` and a class of `turnstile-widget`. This is where the Turnstile widget will be displayed.

The second `div` has a class of `captcha-box`. This is where the captcha box will be displayed after the user completes the Turnstile widget. The contents of the `div` include a heading and a link to an email address.

When the Turnstile widget is successfully completed by the user, the callback function specified in the JavaScript code will be executed. This function calls the `showDiv()` function, which changes the CSS style of the `div` with class `captcha-box` to "block", causing it to become visible on the webpage. The `div` with `id` `turnstile-widget` will also have its `display` property set to "none", causing it to be hidden.

```html
<style>.captcha-box { display: none;  }</style>

<div id="turnstile-widget" class="turnstile-widget"><h2 class="email-title">Verifying your browser, please hold...</h2></div>

<div class="captcha-box">
    <h2 class="email-title">Captcha successfully completed!<br></h2>Here is my email address:<br>
    <a id="email-content" href='mailto:contacto@jfalava.eu'>contacto@jfalava.eu</a>&nbsp;<img style="vertical-align:-5px;display:inline;" width="20" height="20" id="email-copy" src="resources/copy.png">
</div>
```

### JavaScript

This is a block of JavaScript code that defines two functions, `showDiv()` and `window.onloadTurnstileCallback()`, and sets up a Turnstile widget.

`showDiv()` is a function that modifies the CSS style of two elements on the webpage. Specifically, it sets the `display` property of the element with class `captcha-box` to "block", and sets the `display` property of the element with ID `turnstile-widget` to "none". This will hide the Turnstile widget and reveal a captcha box on the webpage.

`window.onloadTurnstileCallback()` is a function that sets up a Turnstile widget with the provided options. When the widget is successfully completed by the user (i.e. they solve the captcha), the function passed as the `callback` option will be executed. In this case, the callback function logs a message to the console indicating success, and calls `showDiv()` to hide the widget and reveal the captcha box. The `sitekey` option is a unique identifier for the site using the widget, and the `theme` option specifies the color scheme of the widget.

```javascript
function showDiv() {
    document.querySelector(".captcha-box").style.display = "block";
    document.querySelector("#turnstile-widget").style.display = "none";
    }
window.onloadTurnstileCallback = function() {
    turnstile.render('#turnstile-widget', {
        sitekey: '<SITE KEY>',
        theme: 'dark',
        callback: function(token) {
            console.log(`Challenge Success ${token}`);
            showDiv();
        },
    });
};
```
