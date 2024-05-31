# Middleware

Middleware is a function which is called <b>before</b> the route handler. Middleware functions have access to the <b>request</b> and <b>response</b> objects, and the <b>next()</b> middleware function in the application’s request-response cycle. The <b>next</b> middleware function is commonly denoted by a variable named <b>next.</b>

![Alt text](https://example.com/path/to/image.png)

Nest middleware are, by default, equivalent to express middleware. The following description from the official <b>express</b> documentation describes the capabilities of middleware:

Middleware functions can perform the following tasks:
- execute any code.
- make changes to the request and the response objects.
- end the request-response cycle.
- call the next middleware function in the stack.
- if the current middleware function does not end the request-response cycle, it must call <b>next()</b> to pass control to the next middleware function. Otherwise, the request will be left hanging.


