# The XHR Object

Just like how the `document` is provided by the JavaScript engine, the JavaScript engine also provides a way for us to make asynchronous HTTP requests. We do that with an `XMLHttpRequest` object. We can create these objects with the provided `XMLHttpRequest` constructor function.

One of the best ways to learn is to get your hands dirty and try things out! So go to [Unsplash](https://unsplash.com/), open up the developer tools, and run the following on the console:

```js
const asyncRequestObject = new XMLHttpRequest();
```

Confusingly, the constructor function has "XML" in it, but it's not limited to only XML documents. Remember that the "AJAX" acronym used to stand for "Asynchronous JavaScript and XML". Since the main file format that was originally used for asynchronous data exchange were XML files, it's easy to see why the function is called `XMLHttpRequest`!

XMLHttpRequests (commonly abbreviated as XHR or xhr) can be used to request any file type (e.g. plain text files, HTML files, JSON files, image files, etc.) or data from an API.



> **Note:** We'll be digging into the `XMLHttpRequest` object. We'll look at how to create it, what methods and properties need to be used, and how to actually send asynchronous requests. For even more info on using the XHR object to make async requests, check out these links:
>
> - MDN's docs - <https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/open>
> - WHATWG Spec - <https://xhr.spec.whatwg.org/>
> - W3C Spec - <https://www.w3.org/TR/XMLHttpRequest/>



## XHR's .open() method

So we've constructed an XHR object named `asyncRequestObject`. There are a number of methods that are available to us. One of the most important is the [open method](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/open).

```js
asyncRequestObject.open();
```

`.open()` takes a number of parameters, but the most important are its first two: the HTTP method URL to send the request

If we want to asynchronously request the homepage from the popular high-res image site, Unsplash, we'd use a `GET` request and provide the URL:

```js
asyncRequestObject.open('GET', 'https://unsplash.com');
```

## A little rusty on your HTTP methods?

The main two that you'll be using are:

- `GET` - to retrieve data
- `POST` - to send data

For more info, check out our course on [HTTP & Web Servers](https://classroom.udacity.com/courses/ud303)!



> **Warning:** For security reasons, you can only make requests for assets and data on the same domain as the site that will end up loading the data. For example, to asynchronously request data from google.com your browser needs to be on google.com. This is known as the [same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy). This might seem extremely limiting, and it is!

> The reason for this is because JavaScript has control over so much information on the page. It has access to all cookies and can determine passwords since it can track what keys are pressed. However, the web wouldn't be what it is today if all information was bordered off in its own silos. The way to circumvent the same-origin policy is with [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS) (Cross-Origin Resource Sharing). CORS must a technology that is implemented on the server. Services that provide APIs use CORS to allow developers to circumvent the same-origin policy and access their information.



## XHR's .send() method

To actually send the request, we need to use the [send method](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/send):

```js
asyncRequestObject.send();
```

It's a little pointless to make a request for something but then do absolutely nothing with it! Why would you order some cake and then not go to pick it up or not eat it? The horror! We want to eat our cake, too!



### Handling Success

To handle the successful response of an XHR request, we set the [onload property](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequestEventTarget/onload) on the object to a function that will handle it:

```js
function handleSuccess () {
    // in the function, the `this` value is the XHR object
    // this.responseText holds the response from the server

    console.log( this.responseText ); // the HTML of https://unsplash.com/
}

asyncRequestObject.onload = handleSuccess;
```

As we just saw, if `onload` isn't set, then the request *does* return...but nothing happens with it.



### Handling Errors

You might've picked up that **onload** is called when the response is *successful*. If something happens with the request and it can't be fulfilled, then we need to use the **onerror property**:

```js
function handleError () {
    // in the function, the `this` value is the XHR object
    console.log( 'An error occurred 😞' );
}

asyncRequestObject.onerror = handleError;
```

As with `onload`, if `onerror` isn't set and an error occurs, that error will just fail silently and your code (and your user!) won't have any idea what's wrong or any way to recover.



## XHR Usage Review

There are a number of steps you need to take to send an HTTP request asynchronously with JavaScript.

### To Send An Async Request

- create an XHR object with the `XMLHttpRequest` constructor function
- use the `.open()` method - set the HTTP method and the URL of the resource to be fetched
- set the `.onload` property - set this to a function that will run upon a successful fetch
- set the `.onerror` property - set this to a function that will run when an error occurs
- use the `.send()` method - send the request

### To Use The Response

- use the `.responseText` property - holds the text of the async request's response





> **Note:** The original XHR specification was created in 2006. This was version 1 of the specification. A number of years with minimal changes to the spec.

> In 2012, work was started on a version 2 of the XHR specification. In 2014, the XHR2 spec was merged into the XHR1 spec so that there wouldn't be diverging standards. There are still references to XHR2, but the XHR specification now fully incorporates XHR2.

> Check out this HTML5Rocks article for info on the [new tricks in XHR2](http://www.html5rocks.com/en/tutorials/file/xhr2/) that are now in the XHR spec.