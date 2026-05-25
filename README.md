# Manual Encryption Script

I wanted to see how basic data hiding works at a low level, so I built a simple text shifter in Python using raw ASCII values instead of just installing an encryption library.

### The Logic
The function loops through every single character. If it's a letter, it drops the character down to a 0-25 scale (subtracting 97 for lowercase, 65 for uppercase), applies the shifting key, uses a modulo `% 26` to wrap around the alphabet, and converts it back into text using `chr()`

```python
def encrypt_msg(text, shift):
    out = ""
    for c in text:
        if 'a' <= c <= 'z':
            out += chr((ord(c) - 97 + shift) % 26 + 97)
        elif 'A' <= c <= 'Z':
            out += chr((ord(c) - 65 + shift) % 26 + 65)
        else:
            out += c
    return out
    
    ## testing some code out
wrote a quick script to test xor encryption logic with a single character key. just wanted to see if bitwise operators work on ascii values in python.

```python
# rough draft of xor cipher
def xor_engine(str1, k):
    # turn char into number
    val = ord(k)
    res = []
    
    for c in str1:
        # bitwise xor flip
        flipped = chr(ord(c) ^ val)
        res.append(flipped)
        
    return "".join(res)

# live testing with random data
msg = "Dartmouth CS 2028"
key = "K"

print("--- raw input text ---")
print(msg)

# encrypting it here
cipher_txt = xor_engine(msg, key)
print("encrypted string looks like:")
print(repr(cipher_txt))

# decrypting to see if it brings it back
decrypted = xor_engine(cipher_txt, key)
print("match check:")
print(decrypted)

# simple check to verify it works
if msg == decrypted:
 print("perfect match!")
else:
 print("loop broke somewhere")