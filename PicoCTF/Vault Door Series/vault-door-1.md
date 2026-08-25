# vault-door-1

**Category:** Reverse Engineering   
**Date:** 2026-08-25  
**Author:** Luke Bray

---

## Challenge Description

> This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: VaultDoor1.java

**Files provided:** `VaultDoor1.java`

---

## TL;DR

The vulnerability having hardcoded credentials in source code. CWE-798. Attempted security through obscurity adds no additional protection.  

---

## Recon

Checked out the source code.

```
# commands used
cat VaultDoor1.java
```

---

## Vulnerability / Analysis

Source code had a function `checkPassword(String password)` which returns `true` if the entered password matches the criteria. There is an attempt at obfuscation but it is basic.

The function to construct the flag is also present in code.

```c
public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               //continues with random charAt
               password.charAt(31) == '8';
}
```

---

## Exploitation / Solution

Step-by-step walkthrough of how you solved it.

1. Copy the vulnerable function to check.txt
2. Create exploit.py
3. Run exploit.py
4. Paste the password in the flag format. 

```python
import re

text = open("check.txt").read()
pairs = re.findall(r"charAt\((\d+)\)\s*==\s*'(.)'", text)
pairs = [(int(i), c) for i, c in pairs]
pairs.sort()
print("".join(c for i, c in pairs))
```

---

## Flag

```
picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_29e8d8}
```

---

## Lessons Learned

* Regex to do a split

---

## References

