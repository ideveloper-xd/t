# AuthSecure-JAVA-API

I decided to make an api for java simply because there were none

Example that I used - [AuthSecure-CSHARP-Example](https://github.com/Authsecure-shop/Authsecure-CSHARP-Example)

**Information**

There is basic encryption for sent requests and iv keys

I guess I just don't know how to make them right

Perfect ✅
Now I will finalize the README.md using your project name:

**`AuthSecure-Java-Example`**

You can **copy → paste → save as `README.md`** directly.

---

### ✅ Final `README.md`

````markdown
# AuthSecure-Java-Example

A Secure Android Authentication System with **Encrypted Login**, **HWID (Device Binding)**, and **Subscription Validation**.  
This project demonstrates how to securely authenticate users in Android using Java while preventing unauthorized device access and account sharing.

---

## ✨ Features

| Feature | Description |
|--------|-------------|
| 🔐 Secure Login System | Username + Password Authentication with backend validation |
| 🆔 HWID Device Binding | Locks user account to the device hardware ID |
| ☁️ API Server Support | Works with your custom API authentication system |
| ♻️ Session Persistence | Optionally store and auto-fill login credentials |
| 📦 Clean & Reusable Code | Easy to understand and implement in any project |
| 🚫 Anti Account Sharing | Prevents login from multiple devices |
| 🛠 Error & Status Handling | Provides detailed login / expiry / device mismatch messages |

---

## 🔍 HWID (Device Locking Logic)

Device hardware ID is generated using:

```java
String rawHwid = Settings.Secure.getString(context.getContentResolver(), Settings.Secure.ANDROID_ID);
String hwid = rawHwid
````

**Behavior Rules:**

* If server **does NOT have** HWID → **Save & Lock** HWID to the account.
* If server **already has** HWID → Only **verify**, no overwrite.
* If login attempt is from different device → **Login fails**.

This makes account sharing **nearly impossible**.

---

## 🧩 Requirements

* Android Studio (Latest Recommended)
* Min SDK: **24+**
* Java Language
* A backend server with login + HWID verification support

---

## 📁 Project Structure

```
AuthSecure-Java-Example/
│
├── LoginActivity.java          # Handles authentication UI & Login logic
├── MainActivity.java           # Opens after successful login
├── AuthSecure.java                # API request, encryption & validation logic
└── HWID.java                   # Device HWID provider
```

---

## 🚀 Usage & Setup

### 1️⃣ Enable Internet Permission

Add this in **AndroidManifest.xml**:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

### 2️⃣ Initialize Authentication Class

```java
AuthSecure = new AuthSecure(name, ownerid, version, url, secret, this);
```

### 3️⃣ Perform Login

```java
    private void loginNow() {
        final String user = usernameField.getText().toString().trim();
        final String pass = passwordField.getText().toString().trim();

        if (user.isEmpty() || pass.isEmpty()) {
            toast("Enter Username & Password");
            return;
        }

        setUiBusy(true);

        new Thread(() -> {
            try {
                AuthSecure.init();
                AuthSecure.login(user, pass);
                AuthSecureInstance.AuthSecure = AuthSecure;

                new Handler(Looper.getMainLooper()).post(() -> {
                    toast("Login Successful ✅");
                    startActivity(new Intent(Login.this, MainActivity.class));
                    finish();
                });

            } catch (Exception e) {
                new Handler(Looper.getMainLooper()).post(() -> {
                    toast("Login Failed ❌ " + e.getMessage());
                    setUiBusy(false);
                });
            }
        }).start();
    }
```

---

## ✅ Successful Login Output Example

```
Login Successful ✅
Username: test_user
Plan: Premium
Expires: 2025-12-19
Device Verified ✓
```

---
### Perform Register

```java
private void registerNow() {
        final String user = usernameField.getText().toString().trim();
        final String pass = passwordField.getText().toString().trim();
        final String license = licenseField.getText().toString().trim();
        if (user.isEmpty() || pass.isEmpty() || license.isEmpty()) {
            toast("Enter Username, Password & License");
            return;
        }
        setUiBusy(true);
        new Thread(() -> {
            try {
                AuthSecure.init();
                AuthSecure.register(user, pass, license);
                new Handler(Looper.getMainLooper()).post(() -> {
                    toast("Registered ✅ Now Login");
                    setUiBusy(false);
                });
            } catch (Exception e) {
                new Handler(Looper.getMainLooper()).post(() -> {
                    toast("Register Failed ❌ " + e.getMessage());
                    setUiBusy(false);
                });
            }
        }).start();
    }

```

---

### Perform license Login

```java
private void licenseLoginNow() {
        final String license = licenseField.getText().toString().trim();
        if (license.isEmpty()) {
            toast("Enter License Key");
            return;
        }
        setUiBusy(true);
        new Thread(() -> {
            try {
                AuthSecure.init();
                AuthSecure.license(license);
                new Handler(Looper.getMainLooper()).post(() -> {
                    toast("Logged In ✅");
                    startActivity(new Intent(Login.this, MainActivity.class));
                    finish();
                });
            } catch (Exception e) {
                new Handler(Looper.getMainLooper()).post(() -> {
                    toast("Failed ❌ " + e.getMessage());
                    setUiBusy(false);
                });
            }
        }).start();
    }

```

---

## ❌ Common Errors & Reasons

| Error Code    | Reason                              |
| ------------- | ----------------------------------- |
| INVALID_LOGIN | Wrong username or password          |
| HWID_MISMATCH | Account is locked to another device |
| EXPIRED       | Subscription has expired            |
| SERVER_ERROR  | API not responding or offline       |
| NO_NETWORK    | No internet connection detected     |

---

## 🛡 Security Notes

* Uses encrypted communication for authentication.
* Prevents account sharing through HWID.
* Avoids unnecessary HWID updates (protects user accounts).

---

## 🤝 Contributing

Feel free to submit Pull Requests for improvements or new features.

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify & distribute.

---

## ⭐ Support the Project

If you like this project, consider giving the repo a star ⭐ on GitHub!

```

---

### ✅ Ready to Commit

Now go to GitHub → open repository → click **Add File → Create New File** → Name it:

```


