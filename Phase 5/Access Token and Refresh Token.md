# Access Token and Refresh Token

In your **Phase 5** journey, understanding the difference between these two is what separates a junior tester from a **Senior Investigator**. As your notes mention, managing the **Token Lifecycle** is a "Big One" for industry exposure.

Think of this like a **Security Pass** for a building.

### 1. Access Token (The "Security Badge")

The Access Token is the actual "Key" or "Hand Stamp" you show the server to get data.

* **Purpose:** It proves you have permission to access a specific API.
* **How to use:** You put it in the header of your request: `Authorization: Bearer <access_token>`.
* **Lifespan:** Very **Short** (usually 30 to 60 minutes).
* **Why it's short:** If a hacker steals it, they can only use it for a few minutes before it "dies".

### 2. Refresh Token (The "Renewal Letter")

The Refresh Token is a special code used only to get a *new* Access Token without making the user log in again.

* **Purpose:** It allows your app to "stay logged in" in the background.
* **How to use:** You send it only to the **Authentication Server** when your Access Token expires.
* **Lifespan:** Very **Long** (days, weeks, or months).
* **Why it's long:** It is kept safely on the server-side (the "Back-Channel") and is never sent with every API call, making it harder to steal.

***

### 🔁 How they work together (The Lifecycle)

In **Block 4** of your roadmap, you learn how these two interact in a cycle:

1. **Login:** You provide credentials and get **both** an Access Token and a Refresh Token.
2. **Activity:** You use the **Access Token** to call APIs for 60 minutes.
3. **Expiry:** Suddenly, the API returns a `401 Unauthorized`. Your Access Token has died.
4. **Refresh:** Your framework automatically sends the **Refresh Token** to the Auth Server.
5. **New Life:** The server gives you a **brand new Access Token**, and your tests continue without stopping.

***

### 📊 Quick Comparison for your Notes

| Feature           | Access Token                  | Refresh Token                       |
| ----------------- | ----------------------------- | ----------------------------------- |
| **Used for...**   | Accessing Business APIs       | Getting a new Access Token          |
| **Visible to...** | The API Server                | Only the Auth Server                |
| **Storage**       | Temporary memory              | Secure storage (config.properties)  |
| **If stolen...**  | Minimal damage (expires fast) | High danger (must be revoked)       |

### 🟢 Why this is "Phase 5 Mastery"

As a Senior Tester, you don't just manually paste a token into your code once. You write a **Utility Method** that checks the time. If the token is older than 50 minutes, your utility uses the **Refresh Token** to fetch a fresh one before the test even starts. This ensures your **CI/CD pipelines** never fail due to "expired sessions."

***



