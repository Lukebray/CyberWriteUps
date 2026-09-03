# vault door 5

**Category:** reverse engineering  
**Date:** 2026-08-27  
**Author:** Luke Bray

---

## Challenge Description

> In the last challenge, you mastered octal (base 8), decimal (base 10), and hexadecimal (base 16) numbers, but this vault door uses a different change of base as well as URL encoding!
>
> The source code for this vault is here: VaultDoor5.java

**Files provided:** `VaultDoor5.java`

---

## TL;DR

The vulnerability was a comment that describes the encoding behaviour. Then in the code we can see what has been encoded. The encoded password is provided also and just needs to be decoded.

---

## Recon

The source code had comments in it explaining what had been done. I read the source code.

```
# commands used
cat VaultDoor5.java
```

---

## Vulnerability / Analysis

The encoded password was stored directly in the source code along with the encoding methods that had been used. 

```java
String urlEncoded = urlEncode(password.getBytes());
String base64Encoded = base64Encode(urlEncoded.getBytes());
String expected = "JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm" + "JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2" + "JTM0JTVmJTYyJTY1JTM5JTY2JTMxJTMwJTYxJTM0";
```

---

## Exploitation / Solution

1. Go to https://gchq.github.io/CyberChef/
2. add a From Base64
3. Below that add a URL Decode
4. Copy `String expected` into cyberchef
5. The flag is returned

```python
# exploit.py / solve script
```

---

## Lessons Learned

I learned how java class StringBuffer works

---

## References

- [Link 1](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html)
