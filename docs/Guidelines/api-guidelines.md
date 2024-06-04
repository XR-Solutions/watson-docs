# API Guidelines
API's are often the gateway between different systems and therefore an API must have a concrete definition and versioning to make sure the system does not break upon changes. To enforce this we have listed some best practices and naming conventions below.

## API Naming Conventions
An API call is a combination of the domain, application and system name. Lets have a look at the following link:

```
http://localhost:8000/{application}/{version}/{entity}/{action}
```

- **Domain:** The domain in this context is simply the base adress that the api listens to. In example above, the domain would be `localhost:8000`
- **Application:** Our API will define it's application name right after the domain name. In the case of the Watson REST API, this has just simply been translated to `api`.
- **Version:** Versioning is a key feature within a good API. Right after the application name, we define the version of the API.
- **Entity:** Right after the version is where we specify what entity we are interacting with. This way our API is clear and easy to navigate. 
- **Action:** Actions are optional. In case that an entity has many more actions related to it, a specific action can be specified by adding an `{action}` path to it. Some examples of why an api endpoint could have an action are below:

Let's say we have a `POST` request available on the `chat` endpoint where we create a new chat.

```
http://localhost:8000/api/v1/chat
```

But we want to add another `POST` method on this entity, where we add a new message to the existing chat. In this case we can simply add the message action.

```
http://localhost:8000/api/v1/chat/message
```

## API Design
The following points are key when developing our API:

- **REST:** The API should have a RESTful Architecture.
- **Entities:** The API should be organized around resources and bring focus on the business entities that the API exposes.
- **Relationships:** Avoid complex navigation through several levels of relationships and make it no more complex than `entity/item/collection`.
- **Pagination:** A GET request returning a collection should always use pagination to limit the amount of data returned.
- **HTTP Methods:** Define operations in terms of HTTP Methods; GET, POST, PUT, PATCH, DELETE.
- **HTTP Response Codes:** The API should return proper response codes; 1xx, 2xx, 3xx, 4xx, 5xx.
- **Errors:** Provide a clear user readable description when an error occurs.
- **Versioning:** Versioning is key in the API and a version will start with a `v` e.g. `v1`
- **camelCase:** Endpoints will be named with `camelCase`. E.g. `https://example.com/api/v1/**salesOrders**`.
- **Stateless:** Always keep application servers state free so that they can be easily scaled.
- **Design for intent:** Don't just expose internal business objects through the API. Design it to have semantic meaning and to match use cases that client application require access for.
- **Documentation:** Provide clear documentation around API Endpoints using the OpenAPI Specification.

## API Security
- **HTTPS:** Always use HTTPS
- **Access Control:** Access Control should be implemented on all non-public endpoints via user authentication.
- **Input Validation:** Always check input parameters and objects and reject unexpected or illegal content.
- **Validate Content Type:** Reject requests containing unexpected or missing content type headers with HTTP `406` or `415`
- **Response Content Types:** Send supported content type headers in the respnse. E.g. `application/json`.
- **Error Handling:** Do not return stack traces and avoid reveiling specific details on the cause of an error. Do not pass technical details to the client and keep error messages generic.  
- **Security Headers:** The API should always send the Content-Type header with the correct content type, and preferably the Content-Type header should include a charset. The server should also send the `X-Content-Type-Options: nosniff` to make sure the browser does not try to detect a different Content-Type than what is actually sent (this can otherwise lead to XSS).
- **Cross-Origin Resource Sharing (CORS):** Limit the origins that should be allowed to make cross-origin calls to the API to only the origins we expect it to be called from.

> More information can be found [here](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/REST_Security_Cheat_Sheet.md)

## Api Documentation
Documentation is key when consuming the API. Not only is it helpful for users, but many tools can process the OpenAPI documentation specification. Therefore API documentation is key. Api documentation should consist of:
- Quick reference ot all the functionality provided by the API
- Allowed HTTP requests (GET, POST, etc.)
- Description of possible responses
- Request; Headers, Parameters and Example requests
- Example Response request
- Authentication process documentation to explain how a user can authenticate with the API
