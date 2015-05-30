### JSON Response

[ref1: Spring MVC Best Error Handling](https://stormpath.com/blog/spring-mvc-rest-exception-handling-best-practices-part-1/)

[ref2: REST Design, What about errors? ](https://blog.apigee.com/detail/restful_api_design_what_about_errors)

```json
// Twilio Example

{
    "status": 404,
    "code": 40483,
    "message": "Oops! It looks like that file does not exist.",
    "developerMessage": "File resource for path /uploads/foobar.txt does not exist.  Please wait 10 minutes until the upload batch completes before checking again.",
    "moreInfo": "http://www.mycompany.com/errors/40483"
}
```
- **code:** The code property is an error code specific to your particular REST API. It is usually something that conveys information very specific to your problem domain.


### HTTP Status Code

When you boil it down, there are really only 3 outcomes in the interaction between an app and an API:

- 200 OK
- 404 Not Found (Client Error)
- 500 Internal Server Error

Start by using the following 3 codes. If you need more, add them. But you shouldn't go beyond 8.

- 201 Created
- 304 Not Modified
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden

### 401 vs 403

[REST API Crafting](http://blog.thefrontiergroup.com.au/2012/08/http-status-codes-and-restful-api-crafting/)
[SO Answer](http://stackoverflow.com/questions/3297048/403-forbidden-vs-401-unauthorized-http-responses)

- **401 Unauthorized** status indicates that the request had missing/invalid authentication credentials.
- **403 Forbidden** status indicates that although the request was valid the action requested failed authorization constraints.

401 response will always include a WWW-Authenticate header that describes how to authenticate.

### Versioning

[Ref](https://blog.apigee.com/detail/restful_api_design_tips_for_versioning/)

![](https://blog.apigee.com/sites/blog/files/Prag_REST_versioning.png)
