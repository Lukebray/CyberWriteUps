# vault-door-3

**Category:** reverse engineering  
**Date:** 2026-08-25  
**Author:** Luke Bray

---

## Challenge Description

> This vault uses for-loops and byte arrays. 
> 
> The source code for this vault is here: VaultDoor3.java
**Files provided:** `VaultDoor3.java`

---

## TL;DR

Check password function is simply trying to obfuscate again without any real security. All it does is rearranges the password. 

---

## Recon

Found the source code and a weak checkPassword method

```
# commands used
cat VaultDoor3.java
```

---

## Vulnerability / Analysis

code was shuffling the letters with loops

```c
// vulnerable code snippet
```

---

## Exploitation / Solution

Step-by-step walkthrough of how you solved it.

1. Pasted the code into an online compiler
2. Added print statements for buffer and s
3. Ran it with the given scrambled password as an argument
4. solved almost by accident

```java
public class MyClass {
  public static void main(String args[])  {
    MyClass mc = new MyClass();
    mc.checkPassword("jU5t_a_sna_3lpm13gf49_u_4_m9r540");
  }
  
  public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        System.out.println("buffer -> " + buffer);
        System.out.println("s -> " + s);

        return s.equals("jU5t_a_sna_3lpm13gf49_u_4_m9r540");
    }
}
```

---

## Lessons Learned

* Understand java loops more
* Learned to use pen and paper and write things down
* Learned that running code is a legitimate technique for reverse engineering

---

## References

