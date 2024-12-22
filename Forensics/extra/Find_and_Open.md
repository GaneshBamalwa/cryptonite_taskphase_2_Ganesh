# CTF Challenge: Find_and_Open

## Table of Content

- commands-executed:  
- flag :picoCTF{R34DING_LOKd_fil56_succ3ss_0f2afb1a}


### Chain of thought / Learning:

- okay so i have a trace file which is a pcap file i open it using wireshark and i get couple of hints. 
**Images:**
![fao1](https://github.com/user-attachments/assets/2d84180e-e5d2-4896-a0cd-950f197c5deb)

- the image here shows a hint that **Ethernet Secret: Is this the flag **

![fao2](https://github.com/user-attachments/assets/fd65fdd8-a16e-432a-bdda-93d978bf78c3)

- The second hint is : **could the flag have been splitted**
- on analyzing the packages i see an ethernet protocal that is diff than the rest.

![fao3](https://github.com/user-attachments/assets/d0daea31-6623-4f06-a459-7afa0fb07ff1)

- the value it has is **VGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8=**
- which is a base64 string so i use cyberchef

![fao4](https://github.com/user-attachments/assets/624365fe-4dcc-49ce-bfdd-e35bbbdae0e8)

- we get : **This is the secret: picoCTF{R34DING_LOKd_**
- i also got a zip file that requires a password so i ll open that
- the password req is the decoded base64 and voila
```console
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ unzip flag.zip 
Archive:  flag.zip
[flag.zip] flag password: 
 extracting: flag                    
                                                                                                                                                                                             
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ ls 
dump.pcap  dump.pcap.1  flag  flag.zip
                                                                                                                                                                                             
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ cat flag     
picoCTF{R34DING_LOKd_fil56_succ3ss_0f2afb1a}

```
