# vault-door-4

**Category:** reverse engineering  
**Date:** 2026-08-25  
**Author:** Luke Bray

---

## Challenge Description

> This vault uses ASCII encoding for the password.
> 
> The source code for this vault is here: VaultDoor4.java

**Files provided:** `VaultDoor4.java`

---

## TL;DR

the password was stored in code but encoded in different ascii forms.

---

## Recon

I opened the code and examined the checkPassword method

```
# commands used
cat VaultDoor4.java
```

---

## Vulnerability / Analysis

The password was stored in an array called myBytes and it had the bytes but they were obfuscated in different ascii forms - decimal, hexadecimal and octodecimal

```c
// vulnerable code snippet
```

---

## Exploitation / Solution

Step-by-step walkthrough of how you solved it.

1. Go to cyber chef
2. Use either from decimal, from hex or from octa and convert. Make sure deliminter is comma
3. Paste the relevant row from myBytes
4. Past the output to construct the flag

---

## Flag

```
flag{...}
```

---

## Lessons Learned

* learned to identify hexa and octadecimal

---

