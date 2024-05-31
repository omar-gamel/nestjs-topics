# Middleware

Middleware is a function which is called <b>before</b> the route handler. Middleware functions have access to the <b>request</b> and <b>response</b> objects, and the <b>next()</b> middleware function in the application’s request-response cycle. The <b>next</b> middleware function is commonly denoted by a variable named <b>next.</b>

![Middleware](https://github.com/omar-gamel/nestjs-topics/blob/main/Middleware.PNG)

Nest middleware are, by default, equivalent to express middleware. The following description from the official <b>express</b> documentation describes the capabilities of middleware:

Middleware functions can perform the following tasks:
- execute any code.
- make changes to the request and the response objects.
- end the request-response cycle.
- call the next middleware function in the stack.
- if the current middleware function does not end the request-response cycle, it must call <b>next()</b> to pass control to the next middleware function. Otherwise, the request will be left hanging.

# Exception Filters

Nest comes with a built-in <b>exceptions layer</b> which is responsible for processing all unhandled exceptions across an application. When an exception is not handled by your application code, it is caught by this layer, which then automatically sends an appropriate user-friendly response.

![Exception Filters](https://github.com/omar-gamel/nestjs-topics/blob/main/Exception-Filters.PNG)

Out of the box, this action is performed by a built-in <b>global exception filter</b>, which handles exceptions of type <b>HttpException</b> (and subclasses of it). When an exception is <b>unrecognized</b> (is neither <b>HttpException</b> nor a class that inherits from HttpException), the built-in exception filter generates the following default JSON response:

``` json

{
  "statusCode": 500,
  "message": "Internal server error"
}

```

# Pipes

A pipe is a class annotated with the <b>@Injectable()</b> decorator, which implements the <b>PipeTransform</b> interface.

![Pipes](https://github.com/omar-gamel/nestjs-topics/blob/main/Pipes.PNG)

ads via Carbon
Design and Development tips in your inbox. Every weekday.
ADS VIA CARBON
Pipes
A pipe is a class annotated with the @Injectable() decorator, which implements the PipeTransform interface.


Pipes have two typical use cases:

- <b>transformation:</b> transform input data to the desired form (e.g., from string to integer)
- <b>validation:</b> evaluate input data and if valid, simply pass it through unchanged; otherwise, throw an exception

In both cases, pipes operate on the <b>arguments</b> being processed by a <b>controller route handler.</b> Nest interposes a pipe just before a method is invoked, and the pipe receives the arguments destined for the method and operates on them. Any transformation or validation operation takes place at that time, after which the route handler is invoked with any (potentially) transformed arguments.

Nest comes with a number of built-in pipes that you can use out-of-the-box. You can also build your own custom pipes. In this chapter, we'll introduce the built-in pipes and show how to bind them to route handlers. We'll then examine several custom-built pipes to show how you can build one from scratch.
