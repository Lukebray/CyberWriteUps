# Old Sessions

**Category:** Web  
**Date:** 2026-09-02  
**Author:** Luke Bray

---

## Challenge Description

> Proper session timeout controls are critical for securing user accounts. If a user logs in on a public or shared computer but doesn’t explicitly log out (instead simply closing the browser tab), and session expiration dates are misconfigured, the session may remain active indefinitely.
>
> This then allows an attacker using the same browser later to access the user’s account without needing credentials, exploiting the fact that sessions never expire and remain authenticated.
>
> Your friend tells you to check out a new social media platform he built a few years ago. Although its still under development, he said the site is almost complete. He also mentioned that he hates constantly logging into sites, and so has made his page that 'once you login, you never have to log-out again'!

---

## TL;DR

Sessions were never deleted and were set to be permanent sessions. The session key was exposed. It was exploited by setting the session cookie with the exposed session key. 

---

## Recon

First I created an account and logged in. On the homepage there was a message:
> Hey I found a strange page at /sessions

I navigated to this page and was able to see the session for admin. 

I checked out which cookies and sessions were being stored locally. 


---

## Vulnerability / Analysis

The route cause was leaving sessions permanently open. Sessions cookie was not set with the `Secure` attribute which should always be done as it instructs browsers to send the cookie through secure HTTPS.  


---

## Exploitation / Solution

Step-by-step walkthrough of how you solved it.

1. Create a user account and login
2. Navigate to /sessions in the url 
3. Copy the value for the admin session. It will look like this: session:[VALUE HERE COPY THIS]
4. Navigate back to the home page
5. Open chrome console and navigate to the Application tab
6. Open the cookie for http://dolphin-cove...It will be the only one there
7. Double click the value next to session and paste the admin session key

---

## Lessons Learned

Learned about how session cookies should always be set as secure
Learned that the session is set in the cooking and not in the session storage. I tried to add the admin session to my session storage but you can't do anything with it even if it is there. The cookie needs to be modified. 

---

## References

- [Link 1]([https://](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html#cookies))
- [Link 2]
