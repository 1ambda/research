### @Controller vs @RestController

[SO Answers](http://stackoverflow.com/questions/25242321/difference-between-spring-controller-and-restcontroller-annotation)

```java
@Controller
@ResponseBody
public class MyController { }

@RestController
public class MyRestController { }
```

### @ResponseBody vs @ResponseEntity

[SO Question](http://stackoverflow.com/questions/22725143/what-is-the-difference-between-responseentityt-and-responsebody)

ResponseEntity will give you some added flexibility in defining arbitrary HTTP response headers.

### @RequestParam vs @PathVariable

[RequestParam vs PathVariable ](http://stackoverflow.com/questions/13715811/requestparam-vs-pathvariable)

- `@PathVariable`: is to obtain some placeholder from the uri
- `@RequestParam`: is to obtain an parameter

Assume this Url `http://localhost:8080/MyApp/user/1234/invoices?date=12-05-2013`

```java
@RequestMapping(value="/user/{userId}/invoices", method = RequestMethod.GET)
public List<Invoice> listUsersInvoices(
            @PathVariable("userId") int user,
            @RequestParam(value = "date", required = false) Date dateOrNull) {
  ...
}
```

### POST, GET

```java
@RequestMapping(value="/register",
        method=RequestMethod.POST,
        consumes="application/json")
public ResponseEntity<String> register(@RequestBody User user) {

  if (null != user.getName())
    return new ResponseEntity<String>(HttpStatus.OK);

  return new ResponseEntity<String>(HttpStatus.BAD_REQUEST);
}

@RequestMapping(value="/register/{name}", method=RequestMethod.GET)
public ResponseEntity<User> register(@PathVariable String name) {

  User u = new User();
  u.setName(name);

  return new ResponseEntity<User>(u, HttpStatus.OK);
}

```

### Exception Handler

[SO Answers](http://stackoverflow.com/questions/23580509/how-to-write-a-proper-global-error-handler-with-spring-mvc-spring-boot)

### Bean Validation

[JSR 349 Bean Validation Spec 1.1](https://jcp.org/en/jsr/detail?id=349)
[Example](http://www.journaldev.com/2668/spring-mvc-form-validation-example-using-annotation-and-custom-validator-implementation)

```java
// Domain
import javax.validation.constraints.NotNull;

public class User {
	@NotNull
	private String name;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
}

// Controller
public ResponseEntity<String> register(@Valid @RequestBody User user) {
  ...
}

```

### Controller Examples

[Example1](http://www.baeldung.com/2011/10/25/building-a-restful-web-service-with-spring-3-1-and-java-based-configuration-part-2/)

### Exception Handler

[Link](http://www.journaldev.com/2651/spring-mvc-exception-handling-exceptionhandler-controlleradvice-handlerexceptionresolver-json-response-example)
