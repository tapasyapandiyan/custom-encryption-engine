# Manual Encryption Script

I wanted to see how basic data obfuscation works at a low level, so I built a simple text shifter in Python using raw ASCII values instead of just installing an encryption library.

### The Logic
The function loops through every single character. If it's a letter, it drops the character down to a 0-25 scale (subtracting 97 for lowercase, 65 for uppercase), applies the shifting key, uses a modulo `% 26` to wrap around the alphabet, and converts it back into text using `chr()`.

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