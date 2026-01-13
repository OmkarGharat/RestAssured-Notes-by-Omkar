# Token Lifecycle

In your **Phase 5** journey, the **Token Lifecycle** is one of the most important concepts because it moves you away from "static" testing to "dynamic" automation. As your roadmap mentions, this is pure industry exposure.

Think of the Token Lifecycle as the **"Birth, Life, and Death"** of your access to an API.

***

### 👶 1. The Birth (Authentication)

The lifecycle begins when your framework proves its identity.

* **The Trigger:** Your code sends `client_id` and `client_secret` (the application password) to the Auth Server.
* **The Result:** The server issues a JSON response containing an **Access Token** and a **Refresh Token**.

### 🏃 2. The Active Life (Authorization)

Now your token is "alive" and ready to work.

* **The Action:** For every API call (Get User, Delete Booking), you attach the Access Token in the header: `Authorization: Bearer <token>`.
* **The Status:** As long as the token is valid, the server returns a `200 OK`.

### 💀 3. The Death (Expiration)

Access Tokens are designed to be short-lived for security (usually 60 minutes).

* **The Symptom:** Your API request suddenly fails with a **401 Unauthorized** status code.
* **The Reason:** The server has checked its clock and decided your "hand stamp" has expired.

### 🔄 4. The Rebirth (Refreshing)

This is where the **Refresh Token** saves the day. Instead of making the user log in again (or manually updating your code), your framework uses the Refresh Token to "re-birth" a new Access Token.

* **The Action:** You hit the `/token` endpoint using the `grant_type=refresh_token`.
* **The Result:** You get a brand new Access Token, and the cycle starts all over again.

***

### 🛠️ Why this is "Senior Tester" (Phase 5) Knowledge

As per your **Phase 5 Blocks**, understanding this lifecycle allows you to automate "Edge Cases":

| Scenario             | What a Senior Investigator does                                                              |
| -------------------- | -------------------------------------------------------------------------------------------- |
| **Token is Expired** | Writes a utility to catch the `401`, refresh the token, and retry the request automatically. |
| **Token is Invalid** | Validates that the server correctly rejects "fake" or tampered tokens.                       |
| **Token Scopes**     | Checks if a token meant for "Read" access is correctly blocked from "Delete" actions.        |

***

### 📝 Pro-Tip for your Notes

In your **Phase 4 Framework**, you learned to generate test data. In **Phase 5**, you should treat your **Token** as dynamic data.

> **Never** hardcode a token. **Always** write a method that fetches a fresh one before the test suite starts. This ensures your **CI/CD pipeline** (Phase 6) never fails due to an expired session.

***

![](assets/token-lifecycle.png)
