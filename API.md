

https://medium.com/techcompose/create-rest-api-in-laravel-with-authentication-using-passport-133a1678a876

See 
* [Eloquent: API Resources](https://laravel.com/docs/5.6/eloquent-resources)
* [API Authentication (Passport)](https://laravel.com/docs/5.6/passport)


The following is from: https://www.toptal.com/laravel/restful-laravel-api-tutorial
Writen by André Castelo
JavaScript Developer

````
A Note on HTTP Status Codes and the Response Format
We’ve also added the response()->json() call to our endpoints. This lets us explicitly return JSON data as well as send an HTTP code that can be parsed by the client. The most common codes you’ll be returning will be:

200: OK. The standard success code and default option.
201: Object created. Useful for the store actions.
204: No content. When an action was executed successfully, but there is no content to return.
206: Partial content. Useful when you have to return a paginated list of resources.
400: Bad request. The standard option for requests that fail to pass validation.
401: Unauthorized. The user needs to be authenticated.
403: Forbidden. The user is authenticated, but does not have the permissions to perform an action.
404: Not found. This will be returned automatically by Laravel when the resource is not found.
500: Internal server error. Ideally you're not going to be explicitly returning this, but if something unexpected breaks, this is what your user is going to receive.
503: Service unavailable. Pretty self explanatory, but also another code that is not going to be returned explicitly by the application.
Sending a Correct 404 Response
If you tried to fetch a non-existent resource, you’ll be thrown an exception and you’ll receive the whole stacktrace, like this:

NotFoundHttpException Stacktrace

We can fix that by editing our exception handler class, located in app/Exceptions/Handler.php, to return a JSON response:

public function render($request, Exception $exception)
{
    // This will replace our 404 response with
    // a JSON response.
    if ($exception instanceof ModelNotFoundException) {
        return response()->json([
            'error' => 'Resource not found'
        ], 404);
    }

    return parent::render($request, $exception);
}
Here’s an example of the return:

{
    data: "Resource not found"
}
If you’re using Laravel to serve other pages, you have to edit the code to work with the Accept header, otherwise 404 errors from regular requests will return a JSON as well.

public function render($request, Exception $exception)
{
    // This will replace our 404 response with
    // a JSON response.
    if ($exception instanceof ModelNotFoundException &&
        $request->wantsJson())
    {
        return response()->json([
            'data' => 'Resource not found'
        ], 404);
    }

    return parent::render($request, $exception);
}
In this case, the API requests will need the header Accept: application/json.
````

