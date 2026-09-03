# vault door 6

**Category:** reverse engineering. 
**Date:** 2026-08-27  
**Author:** Luke Bray

---

## Challenge Description

> This vault uses an XOR encryption scheme.
>
> The source code for this vault is here: VaultDoor6.java

**Files provided:** `VaultDoor6.java`

---

## TL;DR

The password is encrypted using XOR. The key is present in the source code. 

---

## Recon

Read the file to see how the password was encoded. The challenge mentions XOR.

```
# commands used

```

---

## Vulnerability / Analysis

The key was present. We can see the bytes are hex with 0x prefixes. And the key is present

```java
for (int i=0; i<32; i++) {
            if (((passBytes[i] ^ 0x55) - myBytes[i]) != 0) {
                return false;
            }
        }
```

---

## Exploitation / Solution

1. Take myBytes and normalise them to remove 0xa. This can be done manually. 
2. Go to cyberchef and use an XOR with the key of 0x55
3. ding ding

```python
# exploit.py / solve script
```

---

## Lessons Learned

I learned what XOR is and that it can be reversed.
I learned more about hex and that the 0x is just an indicator.

---

## References

