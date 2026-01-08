# Rest Assured - TRICKS

* File I/O is slow compared to memory access. A configuration reader should load data once at application startup.
* In your Java POJOs, make sure to use Jackson annotations so the JSON matches the API exactly -- \<u>Need to learn\</u>
* Local variables do not get an automatic default value. Java forces you to explicitly initialize them before you can use them in any way, ensuring you don't accidentally try to operate on an undefined memory space. This is why the compiler throws an error.
* Even if you run mvn test -Denv=dev from the command line, the if condition always evaluates to false because you hardcoded workEnv="" just before the check, and you never reach the line workEnv = System.getProperty("env"); inside the if block.
* In your current code, th&#x65;**&#x20;if&#x20;**&#x62;lock that reads System.getProperty("env") never runs if you use the 'Run' button in your IDE.

```java
public static void overrideEnvIfProvideddddd() {
	
	String workEnv = System.getProperty("env");
	
	if(workEnv != null && !workEnv.isEmpty()) {
		
		properties.setProperty("env", workEnv.toLowerCase());
		System.out.println("⚡ Environment overridden from command line: " + workEnv);
	} else {
		workEnv = "qa";
		properties.setProperty("qa", workEnv.toLowerCase());
		System.out.println("⚡ Default Environment Set to: " + workEnv);
	}
	loadPropertiesFile(workEnv);
}
```

* The **`static`****&#x20;****block in the code runs first.&#x20;**&#x49;t loads your base properties into memory.

## The Status code 422 Problem

As noted previously, a 422 with the gorest.co.in API almost always means one of two things:

The Problem is Data Validation

1. The Email Address in your test.json is a Duplicate: The exact email "[omkar1765379568156@gmail.com](mailto:omkar1765379568156@gmail.com)" is already registered in their database from a previous test run.
2. Your Token 3b7...1 is Expired: The API is validating your request but rejecting the operation because the bearer token is invalid/expired.

***

# Learn about the following:  #doubt

```java
private static synchronized void loadPropertiesFile(String fileName)
```

Ask God Amu 😇 on this...

***

### TestBase class

The`TestBase`class typically serves as the foundation for all your test classes. Its purpose is to handle global setup and teardown procedures that apply to your entire test run.

In a standard automation framework, the`@BeforeSuite`method in`TestBase`is where you would usually put things like:

1. **Reporting Setup:**&#x49;nitializing your test reporting framework (e.g., Extent Reports, Allure).
2. **Driver Management Setup:**&#x45;nsuring the necessary browser drivers (e.g., Chrome, Firefox) are downloaded and accessible on the machine running the tests.
3. **Database Connections:**&#x45;stablishing a connection pool to your test database.
4. **Logging Configuration:**&#x53;etting up log file paths and log levels.

***

## Centralized (Global) Logging (Best Practice)

For a professional framework, you define filters in a base configuration or`RequestSpecification`builder, applying them to*all*tests.

***

## POST

When you write`.post("/users")`without specifying a`baseURI`or`port`, REST Assured uses its default values, which typically resolve to`http://localhost:8080`.

***

## Logging Terms

Logging the Request Body (Before the call) --> i.e. in the given()

Logging the Response Body (After the call) --> i.e. in the .then()

***

**Automatic URL Encoding:&#x20;**&#x52;est Assured handles necessary encoding of special characters in the parameter values, which prevents errors and security issues.

```java
// Rest Assured automatically encodes "a/b" to "a%2Fb" in the URL
given()
    .pathParam("path", "a/b")
.when()
    .get("/files/{path}"); 
// Resulting URL: .../files/a%2Fb
```



***

### 💡 The Big Secret

In a real job, 99% of the time "Conditional Headers" refers to these specific HTTP keys:

1. **If-Match**
2. **If-None-Match**
3. **If-Modified-Since**

***

In Rest Assured, we try to use **Method Chaining**. It looks like a single sentence: `given().header().param().when().get().then().statusCode();`

When you insert an `if` statement in the middle, you **break the chain**.

***

### 💡 The Rule of Thumb for Cookies

As an Automation Tester, you **almost never** care what is inside the cookie value (the long random string). You only care about:

1. **Does it exist?** (Did the login work?)
2. **Can I send it back?** (Can I stay logged in for the next step?)

***

### 💁‍♂️ Secret about Cookies

Most of the time, as an automation tester, you don't need to know the "secret meaning" inside the cookie. You treat it like a "Black Box."

If the server gives you 5 cookies, you just catch all 5 and send them back in the next request. You don't care if Cookie #1 is for Dark Mode and Cookie #2 is for your Username. You just know that **without those cookies, the API will fail.**

***

### 2️⃣ How can you know about cookies if you're curious?

If you really wanted to find out what a cookie does, here is how humans do it:

* **API Documentation:** In a professional company, the developers will write a document (like Swagger) that says: *"After login, we will send a cookie named 'session\_id'. You must include this in all future calls."*
* **Browser DevTools (The "Detective" Method):**
  1. Open any website (like Google).
  2. Right-click -> **Inspect** -> Go to the **Application** tab.
  3. Click on **Cookies** on the left.
  4. You will see a table with the Name, Value, Domain, and Expiry.
  5. Often, the "Value" is gibberish, but the "Name" or the "Path" gives you a hint.

***

### ⚠️ The "Real World" Catch

On professional websites, many cookies are marked as **`HttpOnly`**.

* **What it means:** A hacker using JavaScript cannot steal the cookie.
* **For you:** Rest Assured *can* still see and grab them because Rest Assured acts like a browser engine, not a piece of JavaScript.

***

### 💡 What happens if the cookie "Expires"?

If you wait too long between Step 1 and Step 3 (or if the server is set to expire cookies every 60 seconds), Step 3 will fail or the server will ignore the cookie and give you a **new** one. This is exactly what happens when you get "automatically logged out" of your bank app after 5 minutes of inactivity.

***

### ⚠️ A Small Warning for the Future (RestAssured.baseURI)

Using `RestAssured.baseURI` (Static) can be dangerous when you start running tests in **Parallel** (multiple tests running at the exact same time).

If Test A sets it to `google.com` and Test B sets it to `github.com` at the same microsecond, they might "overwrite" each other, and your requests will go to the wrong website! That is why many advanced users prefer the `RequestSpecBuilder` we talked about earlier.

***

In a professional framework, we use **CamelCase** for Java variables and reserve the JSON keys for the annotation only. This makes your code look like "Java" rather than a copy-paste of the API.

***

**Senior Secret:** A junior tester waits for a developer to give them a token. A **Senior Investigator** (Phase 5) writes a script to hit the Auth Server, grabs the token, and passes it to the next test automatically.

***

