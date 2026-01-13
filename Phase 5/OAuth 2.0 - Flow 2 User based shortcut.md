# OAuth 2.0 - Flow 2 User based shortcut

Rest Assured shortcut to get a token without needing to manually click "Allow" in a browser

***

In real-world automation, we cannot automate the "Google Login" or "GitHub Consent" screen because those are third-party UIs designed to block bots11. As your **Phase 5** notes mention, a Senior SDET understands how to **shortcut** this flow to focus on API testing2.



There are two main "shortcuts" used in the industry to get an `access_token` without a browser.

### 1. The "Postman/Manual" Shortcut (Most Common)

For 90% of projects, you do not automate the *getting* of the token for User-based flows. You get it once and pass it to your framework.

1. **Generate manually:** Use Postman's "OAuth 2.0" tab to perform the login once and get the `access_token`3.
2. **Store in Config:** Put that token in your `config.properties` from **Phase 4**444.
3. **Inject via Builder:** Use the **RequestSpecBuilder** to attach it to all tests5.



***

### 2. The "Refresh Token" Shortcut (The Pro Way)

If your token expires every hour, your automation will fail. To fix this, you use the **Refresh Token** to get a new **Access Token** via code. This is a "Machine-to-Machine" call that doesn't need a browser6.

**The Code Logic:**

```java
public String getNewAccessToken(){
    // We send the 'refresh_token' (which lasts for months) 
    // to get a fresh 'access_token' (which lasts for 1 hour)
    
    return given()
        .formParam("grant_type", "refresh_token")
        .formParam("refresh_token", "your_long_lived_refresh_token")
        .formParam("client_id", "your_id")
        .formParam("client_secret", "your_secret")
    .when()
        .post("https://oauth2.googleapis.com/token")
    .then()
        .extract()
        .path("access_token");
}
```

***

### 3. Combining it with your Phase 4 Framework

Since you already have a **Request Specification**, the best practice is to create a utility that "pre-loads" your suitcase with the token.

```java
@BeforeClass
publicvoidsetup(){
    // 1. Get the token (shortcut)
    String token = TokenUtils.getNewAccessToken(); 

    // 2. Build the Reusable Request Spec (Phase 4 Thinking)
    requestSpec = new RequestSpecBuilder()
        .setBaseUri(config.getProperty("baseURI"))
        .addHeader("Authorization", "Bearer " + token)
        .addFilter(new CookieFilter()) // Block 3: Catching any sticky notes!
        .build();
}
```

### 🧠 Why is this a "Phase 5 Mental Shift"?

* **Junior:** Tries to use Selenium to login to Google (and fails because of CAPTCHA).
* **Senior (You):** Understands the **Token Lifecycle**8. You know that once you have a `refresh_token`, you can stay authenticated forever using pure API calls.

***

