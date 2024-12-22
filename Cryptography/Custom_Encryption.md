# CTF Challenge: Custom_Encryption

## Table of Content

- commands-executed:  
- flag :picoCTF{custom_d2cr0pt6d_dc499538} 


### Chain of thought / Learning:

-Looks like all I have is a python code that applies a custom encryption to a message. 
-lets analyze all the functions one by one. 

```python
def test(plain_text, text_key):                      //2 parameters where plain_text is input message and text+key = trudeau
    p = 97                                           
    g = 31
    if not is_prime(p) and not is_prime(g):          // not true and not true therefore true.
        print("Enter prime numbers")                  
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')
```
- I ll write a python script to decrypt it , basically reverse every operation starting from the end. 

#### Script used:
```python 
a = 89
b = 27
cipher =  [33588, 276168, 261240, 302292, 343344, 328416, 242580, 85836, 82104, 156744, 0, 309756, 78372, 18660, 253776, 0, 82104, 320952, 3732, 231384, 89568, 100764, 22392, 22392, 63444, 22392, 97032, 190332, 119424, 182868, 97032, 26124, 44784, 63444]


# okay so the last part is encrypting the semi cipher with the shared key , i ll start with finding the key. 
p = 97
g = 31


def generator(g, x, p):
    return pow(g, x) % p


def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)

    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]

        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char

    return cipher_text


v = generator(g, b, p)
key = generator(v, a, p)
# okay so i ll decrypt the encrypt function.
# basically  x = ord(char) * key *  311
# so  ord(char) = x / (key * 311) i can use chr of this to get the character. 
dec = ""
for x in cipher : 
    dec += chr((x // (key*311)))

print(dec)

# okay for dynamic xor we kno0w flag starts with picoCTF{ so i ll send that as the input and see what i get in return. 


k = dynamic_xor_encrypt(dec,"picoCTF{")
print(k)

# okay so picoctf{ changes to sm string aedurtuavxeiXLxz&⌂c+FA§{Z⌂t↨ but see aedurtu is the rearrangement of our original message trudeau just placed the u in the end and reversed. so we send this with the decipher and see if we get the result. 

print(dynamic_xor_encrypt(dec , "aedurtu"))
```
#### Output: 
```
JFQ\XA↨▬*S§♣D▬V☺>↑♠♠◄♠→3 1→♀◄
aedurtuavxeiXLxz&⌂c+FA§{Z⌂t↨:`
picoCTF{custom_d2cr0pt6d_dc499538}
```
