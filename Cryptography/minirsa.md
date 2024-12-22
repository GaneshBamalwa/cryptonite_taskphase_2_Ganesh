# CTF Challenge: Mini Rsa

## Table of Content

- commands-executed:  
- flag : picoCTF{n33d_a_lArg3r_e_606ce004}


### Chain of thought / Learning:
- okay this challenge took up a lot of research and time.
- a hint given by picoCTF
```
How could having too small an e affect the security of this 2048 bit key?
```
- so on researching this what i ve learnt is that it has something to do with the modulo functions.
- actual formula is **m^e mod n** where m is the actual text , so if e is very small and m is small then even after m^e it ll be smaller than n, so therefore you can approximate this to m^e with mod n having no effect in which case i can simply find the cube root of the number mod n has no effect. This research fried my brain but i got a lot of help from chatgpt so ... ya.
- moving on what i can do is find the cube root of the cipher text which is a very very veryy very big number so i ll use a python scirpt i found online.
```python
def find_invpow(x,n):
    """Finds the integer component of the n'th root of x,
    an integer such that y ** n <= x < (y + 1) ** n.
    """
    high = 1
    while high ** n < x:
        high *= 2
    low = high/2
    while low < high:
        mid = (low + high) // 2
        if low < mid and mid**n < x:
            low = mid
        elif high > mid and mid**n > x:
            high = mid
        else:
            return mid
    return mid + 1
```
- all i get is an integer and i m stuck. okay after some research i found that the integer can be converted to ascii directly using a python scirpt. 
- okay so this script gives us an integer and what i do is to get a string from it is to convert it into ascii or bytes
- i ll use blackbox.ai to write a function to convert a long integer to bytes. basically find the last 8 bits take bitwise and with 255 or 0xFF and left shift.
- final script :
```python
def find_invpow(x, n):
    """Finds the integer component of the n'th root of x,
    an integer such that y ** n <= x < (y + 1) ** n.
    """
    high = 1
    while high ** n < x:
        high *= 2
    low = high // 2  # Use integer division

    while low < high:
        mid = (low + high + 1) // 2  # Use (low + high + 1) to avoid infinite loop
        if mid ** n < x:
            low = mid  # mid is a candidate
        else:
            high = mid - 1  # mid is too high

    return low  # Return the largest integer y such that y ** n <= x


def long_to_bytes(value: int) -> bytes:
    """Converts a long integer to bytes."""
    if not isinstance(value, int):
        raise TypeError("Value must be an integer.")
    if value < 0:
        raise ValueError("Value must be a non-negative integer.")
    
    # Initialize an empty list to hold the byte values
    byte_list = []
    
    # Convert the integer to bytes
    while value > 0:
        byte_list.append(value & 0xFF)  # Get the last 8 bits
        value >>= 8  # Shift right by 8 bits to process the next byte
    
    # If the byte_list is empty, it means the value was 0
    if not byte_list:
        byte_list.append(0)
    
    # Reverse the list to get the correct byte order and convert to bytes
    byte_list.reverse()
    return bytes(byte_list)


# Example usage
if __name__ == "__main__":
    # Very large integer
    x = 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125
    n = 3  # We want to find the cube root

    # Find the integer component of the nth root
    t = find_invpow(x, n)

    # Convert the result to bytes
    byte_representation = long_to_bytes(t)

    # Print the byte representation
    print(byte_representation)
```
- the output of this code is:
```console
                                                                                                                                                                                            
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ gedit inv_pow.py  

(gedit:25826): tepl-WARNING **: 17:38:44.730: Style scheme 'Kali-Light' cannot be found, falling back to 'Kali-Light' default style scheme.

(gedit:25826): tepl-WARNING **: 17:38:44.731: Default style scheme 'Kali-Light' cannot be found, check your installation.

(gedit:25826): Gtk-WARNING **: 17:39:30.111: Calling org.xfce.Session.Manager.Inhibit failed: GDBus.Error:org.freedesktop.DBus.Error.UnknownMethod: No such method “Inhibit”
                                                                                                                                                                                            
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ python3 inv_pow.py
b'picoCTF{n33d_a_lArg3r_e_606ce004|'

```
- okay it worked. and we have the flag **picoCTF{n33d_a_lArg3r_e_606ce004}**
