## Understanding Common Coding Questions

- **Meaning of writing** `.get('')` in **when** and **given()**:  
   Used to specify the HTTP GET method and the endpoint URL in Rest Assured tests.

- **Meaning of writing** `.header("Content-Type", "application/json")`:  
   Sets the request header to indicate the payload format is JSON.

- **Are** `given()`, `when()`, and `then()` compulsory?:  
   Not strictly compulsory, but they provide a readable structure for Rest Assured tests.

- **Difference between** `res.asString()` and `res.toString()` -- REFER AFFINE:  
   `res.asString()` returns the response body as a string, while `res.toString()` returns the string representation of the response object.

## Topics to Learn

- **JWT (JSON Web Tokens)**:  
   Understand the structure and usage of JWTs, commonly asked in senior-level interviews.

- **Writing a Rest Assured `then()` block to verify token expiration**:  
   Learn to check for a 401 status code to confirm token expiry.

- **Schema Validation**:  
   Learn how to validate the structure of API responses.
