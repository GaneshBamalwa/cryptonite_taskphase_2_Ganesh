# CTF Challenge: 

## Table of Content

- commands-executed:  
- flag :picoCTF{learning_about_converting_values_00a975ff}


### Chain of thought / Learning:
- okay so on connecting i have to convert binary to text for which i use an online tool.
- then i have an octal to text for which i create my own program for octal to binary and then use the tool.
- last one is a hex to text  for  which i write a prog in python and use the tool again.

- octal to binary script:

```python
def octal_to_binary(octal_str):
    decimal_number = int(octal_str, 8)
    binary_number = bin(decimal_number)[2:]
    return binary_number
    
    
    
    
d = "156 165 162 163 145" 
l =[]

l = d.split(" ")
res = ""  

for x in l: 
    t=octal_to_binary(str(x))
    res = res +" " +t
    
print(res)
```

- hex to binary script:

```python
import re 

def hex_to_binary(hex_str):
    decimal_number = int(hex_str, 16)
    binary_number = bin(decimal_number)[2:]
    return binary_number
    
d = "7461626c65"
l = re.findall(".." , str(d))
for x in l:
    print(hex_to_binary(str(x)),end=" ")
```


#### Output:
```console
┌──(anonymous㉿Anonymous)-[~/investigation]
└─$ nc jupiter.challenges.picoctf.org 29221
Let us see how data is stored
test
Please give the 01110100 01100101 01110011 01110100 as a word.
...
you have 45 seconds.....

Input:
test
Please give me the  156 165 162 163 145 as a word.
Input:
nurse
Please give me the 7461626c65 as a word.
Input:
table
You've beaten the challenge
Flag: picoCTF{learning_about_converting_values_00a975ff}

```
