# FLOW 2 - Final Notes

# 🛡️ Phase 5: Block 4 — Authentication

## Topic: OAuth 2.0 Authorization Code Flow (User-Based)

### 🧠 The Core Logic

Unlike **Client Credentials** (Machine-to-Machine), this flow is for **Human Users**. It allows a "Third-Party App" to access your data without you ever sharing your personal Google/GitHub password with that app.

![OAuth 2.0 Authorization Code Flow (User-Based)](../assets/oauth2-auth-code-flow-user-based.png)

### 🔁 The Detailed FLOW — Step-by-Step

#### **🔹 STEP 1: The Request for Consent**

- **Action:** The App redirects the User to the Provider's (e.g., Google) Login Page.
- **What is sent:** The App sends its `client_id` (Public ID) and a `redirect_uri`.
- **The Goal:** To ask Google, "Can I have permission to see Omkar's data?"

#### **🔹 STEP 2: The User Login & Permission**

- **Action:** The **Human User** enters their **Personal Password** on Google's secure page.
- **The Goal:** Proof that **Omkar** is who he says he is.
- **Security Note:** The App **never** sees this password.

#### **🔹 STEP 3: The Authorization Code (The Receipt)**

- **Action:** Google redirects the User back to the App with a temporary `?code=xyz`.
- **What it is:** This is a short-lived "Receipt" or "Coupon" that proves the user clicked "Allow."
- **The Goal:** To move the process from the Browser back to the App.

#### **🔹 STEP 4: The Back-Channel Exchange (Identity Check)**

- **Action:** The App's Server calls Google’s Token API directly.
- **What is sent:** The `Authorization Code` (from Step 3) + the **`client_secret`**.
- **The Goal:** Proof that the requester is the **Real App** and not a hacker.
- **Clarity:** This `client_secret` is the **App's Password**, not the User's password.

#### **🔹 STEP 5: The Access Token Delivery**

- **Action:** Google verifies the code and the `client_secret`.
- **Result:** Google sends the **`access_token`** to the App.
- **The Final Goal:** The App now uses this token to fetch your data.

---

### 🕵️ Senior Tester Notes (Phase 5 Mastery)

| Item              | Who owns it?       | Purpose                                        |
| ----------------- | ------------------ | ---------------------------------------------- |
| **User Password** | Human (Omkar)      | Proves User's identity to Google.              |
| **Auth Code**     | System (Temporary) | A one-time "receipt" linking User to App.      |
| **Client Secret** | App (Permanent)    | Proves the **Framework's Identity** to Google. |
| **Access Token**  | App (Temporary)    | The final "Hand Stamp" used for Business APIs. |

### 🧪 Automation Shortcut (How we test this in Rest Assured)

Since Backend API tests cannot click "Allow" buttons in a browser, we often use **"Pre-generated Tokens"** for our **Request Specs**:

1. Manually get a token once (via Postman or a browser).
2. Store it in your `config.properties`.
3. Inject it into your `RequestSpecBuilder`.
4. Focus your test on the **Token Lifecycle**—how the API behaves when the token is valid, expired, or missing.

---

**Does this merged flow make the distinction between the "User Password" and the "App Secret" 100% clear?** If you're ready, we can wrap up Block 3 and 4 by talking about **JWT (JSON Web Tokens)**—the actual "text" that makes up these tokens! (This is a favorite topic for Senior level interviews).This is a great idea. Merging these two concepts is essential for your **Phase 5 notes** because it clarifies the "Identity" of every player in the game. In **Block 4**, the biggest confusion is usually "who is talking to whom," so this combined flow will clear that up. 1

---

### 🕵️ Senior Tester Notes (Phase 5 Mastery)

| Item              | Who owns it        | Purpose                                          |
| ----------------- | ------------------ | ------------------------------------------------ |
| **User Password** | Human (Omkar)      | Proves User's identity to Google.                |
| **Auth Code**     | System (Temporary) | A one-time "receipt" linking User to App.        |
| **Client Secret** | App (Permanent)    | Proves the **Framework's Identity** to Google.   |
| **Access Token**  | App (Temporary)    | The final "Hand Stamp" used for Business APIs. 3 |
