<p align="center">
  <img src="screenshots/image.png" alt="TryHackMe Logo" width="400"/>
</p>

# Tryhackme
# Name of the Challenge - Neighbour
# Difficulty level - Easy

## Challenge Link:
https://tryhackme.com/room/neighbour

![Screenshot](screenshots/Screenshot%20(599).png)
![Screenshot](screenshots/Screenshot%20(600).png)

---

## What is this room about?

This room is based on **IDOR (Insecure Direct Object Reference)**, one of the most common web application vulnerabilities.

## What is IDOR?

IDOR stands for **Insecure Direct Object Reference**. It is a type of access control vulnerability that occurs when a web application uses user-supplied input to directly access objects such as files, database records, or URLs without proper authorization checks.

For example, imagine you are logged in as a regular user and the URL looks like this:

```
https://example.com/profile?user=1001
```

If you simply change the `user` parameter to another value like `1002`, and the application shows you someone else's profile without verifying whether you are allowed to view it — that's an IDOR vulnerability.

In simple terms, **the application trusts the user's input blindly and does not check if the user actually has permission to access the requested resource.**

### Why is IDOR dangerous?

- Attackers can access other users' data (personal info, files, messages).
- It can lead to unauthorized actions like modifying or deleting someone else's account.
- It is easy to exploit — often just by changing a number in the URL or request.

---

## Walkthrough

### Step 1: Start the Machine and Connect via OpenVPN

First, start the machine in the TryHackMe room. Make sure you are connected to TryHackMe servers using **OpenVPN**. Once the machine is up and running, open the target website in your browser using the IP address provided.

![Website](screenshots/Screenshot%20(601).png)

---

### Step 2: No Need for Scanning Tools

Since we already know this room is about **IDOR**, we don't need to use **Nmap** or any other scanning tools. The vulnerability lies in how the web application handles user authorization — not in open ports or services.

Our next thought is to inspect the page. We can **view the page source** by simply **right-clicking** on the page and selecting **"View Page Source"**.

![View Page Source](screenshots/Screenshot%20(602).png)

---

### Step 3: Inspect the Source Code

Here is the output of the source code. Let's take a closer look at what's inside.

![Source Code Output](screenshots/Screenshot%20(603).png)

Here we found the **login credentials** hidden in the source code:

- **Username:** `guest`
- **Password:** `guest`

---

### Step 4: Login with the Credentials

Type the credentials (`guest` / `guest`) into the input fields on the login page and log in.

![Login Page](screenshots/Screenshot%20(604).png)

---

### Step 5: Exploit the IDOR Vulnerability

The vulnerability of this page is **IDOR**. Since the application does not properly validate user access, we can simply **change the parameter in the URL from `guest` to `admin`** to gain access to the admin's page and retrieve the flag to complete this room.

![Before Changing Parameter](screenshots/Screenshot%20(605).png)

After changing the URL parameter from `guest` to `admin`, we successfully get the **flag**! 🚩

![Flag Retrieved](screenshots/Screenshot%20(606).png)

---

<p align="center"><b>Author:</b> vsaidaiwik</p>
