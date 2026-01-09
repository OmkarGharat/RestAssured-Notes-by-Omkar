
# 🟢 FLOW 1 — CLIENT CREDENTIALS (MOST USED IN AUTOMATION)


## 🌱 सर्वात आधी एक वाक्य (मनात बसव)

> **Client Credentials = Machine to Machine**  
> 👉 _User नाही. Login नाही. Browser नाही._

बस. हे लक्षात ठेवलंस की 50% काम झालं.

---

## 🧠 Real-life story (आणि हाच game आहे)

कल्पना कर 👇

- तू = **Automation Framework**
    
- API Server = **Company backend**
    
- User = ❌ नाहीच
    

Framework म्हणते:

> “मी trusted system आहे.  
> मला API access हवा आहे.”

Server म्हणतो:

> “ठीक आहे.  
> आधी तुझी ओळख दाखव.”

---

## 🪪 ओळख म्हणजे काय? (VERY IMPORTANT)

Framework कडे दोन गोष्टी असतात:

| नाव             | Meaning         |
| --------------- | --------------- |
| `client_id`     | _मी कोण आहे_    |
| `client_secret` | _माझा password_ |

👉 **हे user credentials नाहीत**  
👉 हे **application credentials** आहेत

---

## 🔁 FLOW — Step by Step

### 🔹 STEP 1: Token मागणं

Framework Auth Server ला request करते:

> “मी `client_id + client_secret` देतो  
> मला token दे.”

---

### 🔹 STEP 2: Token मिळणं

Server verify करतो  
✔️ credentials बरोबर  
✔️ permission आहे

मग म्हणतो:

> “हा घे **access_token**.”

---

### 🔹 STEP 3: API call token वापरून

Framework आता API ला कॉल करते:

```http
Authorization: Bearer <access_token>
```

API म्हणते:

> “ओके. तू allowed आहेस.”

---

## 🧠 Important clarity (इथेच लोक गडबडतात)

### ❌ OAuth call = API call

### ❌ Token API = Business API

👉 **Token API वेगळी असते**  
👉 **Business API वेगळी असते**

पहिली:

> _“मला token दे”_

दुसरी:

> _“मला data दे”_

---

# For more information, Refer 

![[OAuth 2.0 - More detailed Explaination]]