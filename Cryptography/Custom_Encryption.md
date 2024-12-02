# CTF Challenge: Custom_Encryption

## Table of Content

- commands-executed:  
- flag :


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



#### Output:
```console

```
