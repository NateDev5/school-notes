HTTP is a **stateless protocol** meaning each request is independent

**How it works (HTTP Request)**:
- Specify the method (GET, POST...)
- **URL** specifies the resource the client wants to access
- **Headers** provide additional info about the request
- **Body** (optional): other additional data

**How it works (HTTP response)**
- **Status** line include HTTP version, 3 digit status code and status message
- **Headers** provide additional info about the response and server
- **Body** contains the content

![[java_web_http.png]]

**URI (Uniform Resource Identifier**: General identifier for resource
- http://example.com/page.html
- urn::isn:0451450523

**URL (Uniform Resource Locator)**: URI that shows where & how to access a resource
- https://example.com/

**URN (Uniform Resource Name**: URI that give a *name only*, no location
- urn::isn:0451450523
- urn:ietf:rfc:3986

**Idempotent**: sending the same request many times will have the same result as sending it once
### HTTP Request Types:
- **(idempotent, safe) GET**: Retrieve info from the server, only reads data dosent change anything (accessing resources/webpage)
- **POST**: Used to send new data to server for processing (form, creating accounts)
- **(idempotent) PUT**: Update or replaces an existing resource (updating profile pic)
- **(idempotent) DELETE**: Remove a resource from the server (Deleting a post)
- **PATCH**: Partially update a resource on the server

### HTTP Status Code:
3 digit number that the server returns indicating the status of a request

**1xx Informational**
**2xx (Success)**
- 200 (OK)
**3xx (Redirection)**
- 301 (Permanent Redirect)
- 302 (Temporary Redirect)
- 304 (Not Modified)
**4xx (Client Error)**
- 401 (Unauthorized)
- 403 (Forbidden)
- 404 (Not Found)
- 405 (Method Not Allowed)
**5xx (Server Error)**
- 501 (Not Implemented)
- 502 (Bad Gateway)
- 503 (Service Unavailable)

They are important for:
- Error handling
- Troubleshooting
- API documentation
- User experience
- Security

### HTTP Requests In Spring Boot
`@RestController`: Marks a class as a REST Api Controller, Returns an HTTP response instead of returning HTML pages
`@RequestMapping`: Set entry point (base path) for the controller

```java
@RestController
@RequestMapping("api/v1/cars")
public class CarsController {
}
```

`@PathVariable`: extract value from the URI path
`@GetMapping`: Handle get request
```java
@GetMapping
public String get_car () {
	return "car";
}

@GetMapping("/all")
public String get_all_cars () {
	return "all cars";
}

@GetMapping("/{car_id}")
public String get_all_cars (@PathVariable Long car_id) {
	return "car with id" + car_id;
}
```

`@DeleteMapping`: Delete request
```java
@DeleteMapping("/{car_id}")
public void delete_car (@PathVariable Long car_id) {
	car_service.some_delete_func(car_id);
}
```

`@RequestBody`: extracts the data from the request body and maps it to a java object
`@PostMapping`: Post request
`@PutMapping`: Put request

```java
@PostMapping
public PictureClass post_picture (@RequestBody PictureClass picture) {
	return picture_service.some_save_func(picture);
}

@PutMapping("/{profile_id}")
public ProfileClass update_profile (@RequestBody ProfileClass profile_data, @PathVariable Long profile_id) {
	return user_service.some_update_func(profile_id, profile_data);
}
```

`@RequestParam`: extra info added at the end of URL (part after **?** separated by **&**)

```java
@GetMapping("/search")
public ProfileClass search_profile (@RequestParam String username) {
	return user_service.some_search_func(username);
}
```