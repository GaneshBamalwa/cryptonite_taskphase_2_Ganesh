# CTF Challenge: trivial_flag_transfer_protocol

## Table of Content

- commands-executed:  
- flag :picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}


### Chain of thought / Learning:
- All i have is pcapng file which is a wireshark intercepted data.
- i open it in wireshark and there is a lot of data that was trafered using the tftp protocol.
- first simple step is to export the objects of the tftp to a folder and analyze them properly.
- i have 3 pictures one deb pack and 2 texts with some encrypted text.
- **Instruction.txt** : GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA
- on analyzing the first portion of the instruction.txt i.e GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE we see its a rot13 so we use cyberchef to bruteforce it 

-output:
  ![tftp](https://github.com/user-attachments/assets/c272d614-bc69-411e-93de-245be778aadb)
  ```
  Amount = 13:TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER
  ```
-the second part of the cipher also is rot13 so we use the brute force method and boom
![tftp2](https://github.com/user-attachments/assets/9910be91-837e-4df6-ab4d-e8684b64bb60)
```
output:Amount = 13: FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN
```

- **Plan.txt** :VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF
- the first part is also a rot 13 so follow the same steps
```
Amount =  1: WIGSRHVSDFCUFOAOBRVWRWHKWHV-RISRWZWUSBQS
Amount =  2: XJHTSIWTEGDVGPBPCSWXSXILXIW-SJTSXAXVTCRT
Amount =  3: YKIUTJXUFHEWHQCQDTXYTYJMYJX-TKUTYBYWUDSU
Amount =  4: ZLJVUKYVGIFXIRDREUYZUZKNZKY-ULVUZCZXVETV
Amount =  5: AMKWVLZWHJGYJSESFVZAVALOALZ-VMWVADAYWFUW
Amount =  6: BNLXWMAXIKHZKTFTGWABWBMPBMA-WNXWBEBZXGVX
Amount =  7: COMYXNBYJLIALUGUHXBCXCNQCNB-XOYXCFCAYHWY
Amount =  8: DPNZYOCZKMJBMVHVIYCDYDORDOC-YPZYDGDBZIXZ
Amount =  9: EQOAZPDALNKCNWIWJZDEZEPSEPD-ZQAZEHECAJYA
Amount = 10: FRPBAQEBMOLDOXJXKAEFAFQTFQE-ARBAFIFDBKZB
Amount = 11: GSQCBRFCNPMEPYKYLBFGBGRUGRF-BSCBGJGECLAC
Amount = 12: HTRDCSGDOQNFQZLZMCGHCHSVHSG-CTDCHKHFDMBD
**Amount = 13: IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE**
```
-the second part
```
Amount =  1: QVSQYCIHHVSDVCHCG
Amount =  2: RWTRZDJIIWTEWDIDH
Amount =  3: SXUSAEKJJXUFXEJEI
Amount =  4: TYVTBFLKKYVGYFKFJ
Amount =  5: UZWUCGMLLZWHZGLGK
Amount =  6: VAXVDHNMMAXIAHMHL
Amount =  7: WBYWEIONNBYJBINIM
Amount =  8: XCZXFJPOOCZKCJOJN
Amount =  9: YDAYGKQPPDALDKPKO
Amount = 10: ZEBZHLRQQEBMELQLP
Amount = 11: AFCAIMSRRFCNFMRMQ
Amount = 12: BGDBJNTSSGDOGNSNR
Amount = 13: CHECKOUTTHEPHOTOS
```
- so now if i club all the hints
```
TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER
FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN
IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE
CHECKOUTTHEPHOTOS
```
- the photos are 3 simple pictures of a valley or mountain but the program.deb has a steghid file. so basically they are steg images.
- Steganography is a technique for hiding information in a way that avoids detection , in here pictures are used to hide ther flag.
- so we use the kali steghide program to maybe try and extract the message from the steg images.
- okay so to decode we need a passphrase and the hints clearly mention **DUEDILIGENCE**
- we try it for all the images
```
                                                                                                                                         
┌──(anonymous㉿Anonymous)-[~/investigation/flag tranfer]
└─$ steghide --extract -sf picture1.bmp
Enter passphrase: 
steghide: could not extract any data with that passphrase!
                                                                                                                                         
┌──(anonymous㉿Anonymous)-[~/investigation/flag tranfer]
└─$ steghide --extract -sf picture2.bmp
Enter passphrase: 
steghide: could not extract any data with that passphrase!
                                                                                                                                         
┌──(anonymous㉿Anonymous)-[~/investigation/flag tranfer]
└─$ steghide --extract -sf picture3.bmp
Enter passphrase: 
wrote extracted data to "flag.txt".
                                                                                                                                         
┌──(anonymous㉿Anonymous)-[~/investigation/flag tranfer]
└─$ ls 
flag.txt  instructions.txt  picture1.bmp  picture2.bmp  picture3.bmp  plan  program.deb
                                                                                                                                         
┌──(anonymous㉿Anonymous)-[~/investigation/flag tranfer]
└─$ cat flag.txt   
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}

```
-voila we have the flag. 
