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

Pipes have two typical use cases:

- <b>transformation:</b> transform input data to the desired form (e.g., from string to integer)
- <b>validation:</b> evaluate input data and if valid, simply pass it through unchanged; otherwise, throw an exception

In both cases, pipes operate on the <b>arguments</b> being processed by a <b>controller route handler.</b> Nest interposes a pipe just before a method is invoked, and the pipe receives the arguments destined for the method and operates on them. Any transformation or validation operation takes place at that time, after which the route handler is invoked with any (potentially) transformed arguments.

Nest comes with a number of built-in pipes that you can use out-of-the-box. You can also build your own custom pipes. In this chapter, we'll introduce the built-in pipes and show how to bind them to route handlers. We'll then examine several custom-built pipes to show how you can build one from scratch.

# Guards

A guard is a class annotated with the <b>@Injectable()</b> decorator, which implements the <b>CanActivate</b> interface.

![Guards](https://github.com/omar-gamel/nestjs-topics/blob/main/Guards.PNG)

Guards have a <b>single responsibility.</b> They determine whether a given request will be handled by the route handler or not, depending on certain conditions (like permissions, roles, ACLs, etc.) present at run-time. This is often referred to as <b>authorization.</b> Authorization (and its cousin, <b>authentication,</b> with which it usually collaborates) has typically been handled by <b>middleware</b> in traditional Express applications. Middleware is a fine choice for authentication, since things like token validation and attaching properties to the <b>request</b> object are not strongly connected with a particular route context (and its metadata).

But middleware, by its nature, is dumb. It doesn't know which handler will be executed after calling the <b>next()</b> function. On the other hand, <b>Guards</b> have access to the <b>ExecutionContext</b> instance, and thus know exactly what's going to be executed next. They're designed, much like exception filters, pipes, and interceptors, to let you interpose processing logic at exactly the right point in the request/response cycle, and to do so declaratively. This helps keep your code DRY and declarative.

<h3>HINT</h3>
Guards are executed <b>after</b> all middleware, but <b>before</b> any interceptor or pipe.

# Interceptors

An interceptor is a class annotated with the <b>@Injectable()</b> decorator and implements the <b>NestInterceptor</b> interface.

![Interceptors](https://github.com/omar-gamel/nestjs-topics/blob/main/Interceptors.PNG)

Interceptors have a set of useful capabilities which are inspired by the <b>Aspect Oriented Programming</b> (AOP) technique. They make it possible to:

- bind extra logic before / after method execution
- transform the result returned from a function
- transform the exception thrown from a function
- extend the basic function behavior
- completely override a function depending on specific conditions (e.g., for caching purposes)




