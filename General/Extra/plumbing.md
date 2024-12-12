
# CTF Challenge: Plumbing

## Table of Content

- commands-executed:  nc jupiter.challenges.picoctf.org 7480 | grep picoCTF
- flag :picoCTF{digital_plumb3r_06e9d954}

### Chain of thought / Learning:
- on running the netcat command i get a biggg string.

```
Again, I really don't think this is a flag
This is defintely not a flag
This is defintely not a flag
Not a flag either
I don't think this is a flag either
Not a flag either
I don't think this is a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
Not a flag either
This is defintely not a flag
I don't think this is a flag either
Not a flag either
This is defintely not a flag
This is defintely not a flag
This is defintely not a flag
Not a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
I don't think this is a flag either
This is defintely not a flag
Not a flag either
I don't think this is a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Again, I really don't think this is a flag
I don't think this is a flag either
This is defintely not a flag
I don't think this is a flag either
Again, I really don't think this is a flag
This is defintely not a flag
I don't think this is a flag either
Not a flag either
I don't think this is a flag either
This is defintely not a flag
This is defintely not a flag
This is defintely not a flag
Not a flag either
I don't think this is a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
Not a flag either
Not a flag either
Not a flag either
Not a flag either
I don't think this is a flag either
Not a flag either
I don't think this is a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
Again, I really don't think this is a flag
I don't think this is a flag either
This is defintely not a flag
Not a flag either
Again, I really don't think this is a flag
Not a flag either
Again, I really don't think this is a flag
Not a flag either
Not a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
Not a flag either
Not a flag either
Not a flag either
Not a flag either
This is defintely not a flag
I don't think this is a flag either
I don't think this is a flag either
Not a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
Not a flag either
Again, I really don't think this is a flag
This is defintely not a flag
I don't think this is a flag either
I don't think this is a flag either
I don't think this is a flag either
Again, I really don't think this is a flag
Not a flag either
Again, I really don't think this is a flag
Again, I really don't think this is a flag
I don't think this is a flag either
This is defintely not a flag
This is defintely not a flag
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
Not a flag either
This is defintely not a flag
I don't think this is a flag either
I don't think this is a flag either
I don't think this is a flag either
I don't think this is a flag either
This is defintely not a flag
This is defintely not a flag
Again, I really don't think this is a flag
Not a flag either
This is defintely not a flag
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
I don't think this is a flag either
Not a flag either
Not a flag either
I don't think this is a flag either
This is defintely not a flag
This is defintely not a flag
Not a flag either
This is defintely not a flag
This is defintely not a flag
Not a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
This is defintely not a flag
Not a flag either
Again, I really don't think this is a flag
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
I don't think this is a flag either

```
- this is just the half of it , it this big text to find the flag we use piping with grep to find the flag

#### Output:
```console
┌──(anonymous㉿Anonymous)-[~/investigation]
└─$ nc jupiter.challenges.picoctf.org 7480 | grep picoCTF
picoCTF{digital_plumb3r_06e9d954}


```
