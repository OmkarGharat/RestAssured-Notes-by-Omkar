Here are the structured notes for **Phase 5: Block 4**, focusing on the **OAuth 2.0 Client Credentials Flow**. You can save these to your study folder or Obsidian.

---

# 🛡️ Phase 5: Block 4 — Authentication

## Topic: OAuth 2.0 Client Credentials Flow (Machine-to-Machine)

1. Core Concept: The "System Identity"

- **Machine-to-Machine (M2M):** This flow is used when there is no human user involved.

- **The Actor:** The "Omkar Automation Framework" itself is the entity being authenticated, not a person.

- **Credentials:** Instead of a username/password, the framework uses:
- **Client ID:** The "Public Username" of the framework.
- **Client Secret:** The "High-Security Password" of the framework.

2. The Two-Step Execution (API Chaining)

In professional testing, you must call two different APIs to complete one task.

#### **Step 1: The Token Request**

- **Target:** The **Authentication Server** (Token API).

- **Action:** Send `client_id` + `client_secret`.

- **Result:** You receive a short-lived `access_token`.

#### **Step 2: The Business Request**

- **Target:** The **Business API** (e.g., Get Employee, Update Booking).

- **Action:** Add the token to the header: `Authorization: Bearer <access_token>`.

- **Result:** Access to the protected data.

3. Server Architecture: Same vs. Different Hosts

Understanding the URL structure is part of **Request Anatomy Mastery**.

- **Architecture A (Shared Host):** \* One Base URL handles both.
- _Example:_ `api.company.com/oauth/token` and `api.company.com/v1/resource`.

- **Architecture B (Dedicated Auth Server):** \* Authentication is handled by a separate high-security machine.
- _Example:_ `auth.company.com/token` and `resource.company.com/api`.

### 4. Why Use Tokens Instead of Passwords? (Security Logic)

- **Exposure Risk:** You only send the "Master Password" (`client_secret`) once to get the token, rather than sending it with every single API call.

- **Token Lifecycle:** Tokens are temporary and expire (usually in 30-60 mins). If stolen, the damage is limited.

- **Performance:** Business APIs can verify a token much faster than checking a database for a full username/password.

5. Integration with Phase 4 Framework

- **Environment Config:** Store `client_id` and `client_secret` in the `config.properties` file for different environments (Dev, QA, Prod).

- **Reusable Request Spec:** Use the **Request Builder Pattern** to automatically inject the Bearer token into headers once it is fetched.

---

**Next Step for your Phase 5 Journey:**
Would you like me to show you how to write the **Rest Assured Code** that automatically detects when a token is expired and fetches a new one? (This is the "Token Lifecycle" mastery mentioned in your roadmap ).
