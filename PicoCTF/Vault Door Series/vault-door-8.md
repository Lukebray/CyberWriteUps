# vault door 8

**Category:** rev    
**Date:** 2026-08-31   
**Author:** Luke Bray

---

## Challenge Description

> Apparently Dr. Evil's minions knew that our agency was making copies of their source code, because they intentionally sabotaged this source code in order to make it harder for our agents to analyze and crack into! The result is a quite mess, but I trust that my best special agent will find a way to solve it.

**Files provided:** `VaultDoor8.java`

---

## TL;DR

The technique used was bit shifting via a switchBits helper that swaps two specific bit positions in a byte. scramble() applies this 8 times with fixed position-pairs. Because each individual swap is self-inverse, the transformation can be undone by replaying the same swaps in reverse order.

---

## Recon

Format the source code to be able to read it properly. Read the comments in the source left by the developers. Look up what bit shifting is. 

---

## Vulnerability / Analysis

scramble() is a fixed, deterministic sequence of bit swaps with no secret key involved — every swap is self-inverse, and the full sequence can be undone by reversing the call order. This makes the encoding trivially reversible once the algorithm is understood.

---

## Exploitation / Solution

Step-by-step walkthrough of how you solved it.

1. Use an online formatter to make the code readable
2. Create the python script below and run it
3. Construct the flag with the picoCTF{} format. 

```python
def switchBits(c, p1, p2):
    mask1 = 1 << p1
    mask2 = 1 << p2
    
    bit1 = c & mask1
    bit2 = c & mask2
    
    rest = c & ~ (mask1 | mask2)
    shift = p2 - p1
    result = ((bit1 << shift) | (bit2 >> shift) | rest)
    return result
    
def unscramble(pwd):
    a = list(pwd)
    for c in a:
        ind = a.index(c)
        c = switchBits(c, 6, 7)
        c = switchBits(c, 2, 5)
        c = switchBits(c, 3, 4)
        c = switchBits(c, 0, 1)
        c = switchBits(c, 4, 7)
        c = switchBits(c, 5, 6)
        c = switchBits(c, 0, 3)
        c = switchBits(c, 1, 2)
        a[ind] = chr(c)
    return a

expected = [0xF4, 0xC0,
      0x97,
      0xF0,
      0x77,
      0x97,
      0xC0,
      0xE4,
      0xF0,
      0x77,
      0xA4,
      0xD0,
      0xC5,
      0x77,
      0xF4,
      0x86,
      0xD0,
      0xA5,
      0x45,
      0x96,
      0x27,
      0xB5,
      0x77,
      0xF1,
      0xC2,
      0xD1,
      0xB4,
      0xD1,
      0xB4,
      0xF1,
      0xF1,
      0x85]
      
my_pass = []
for c in unscramble(expected):
    my_pass.append(c)
    
print(''.join(my_pass))
```

---

## Lessons Learned

- Learned what bit shifting is 
- Learned much more about binary and what each bit represents
- Further understood the different number systems and that decimal, hex, binary etc are just different representations of the same thing
- Took a while to realise that it is the order of switchBits that should be reversed. So where scramble does a certain order of switchBits calls, unscramble should do these in reverse. First I tried to reverse the switchBits function. For example I did the below:
  ```python
  #original
  rest = c & ~ (mask1 | mask2)

  #my attempt
  rest = c | ^ (mask1 & mask2)
  ```
  This doesn't work because bitwise operators don't have direct opposites like +/-


