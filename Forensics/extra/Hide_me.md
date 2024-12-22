# CTF Challenge: Hide me 

## Table of Content

- commands-executed:  
- flag :picoCTF{Hiddinng_An_imag3_within_@n_ima9e_d55982e8}


### Chain of thought / Learning:
-all i have is a png image to start with so i wget to get it on my local machine.
- now i ll follow standard procedure of forensics i ll check the metadata of the image.
**Metadata**
```console
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ exiftool flag.png          
ExifTool Version Number         : 12.76
File Name                       : flag.png
Directory                       : .
File Size                       : 43 kB
File Modification Date/Time     : 2023:03:16 08:46:18+05:30
File Access Date/Time           : 2024:12:22 13:56:09+05:30
File Inode Change Date/Time     : 2024:12:22 13:56:09+05:30
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 512
Image Height                    : 504
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Warning                         : [minor] Trailer data after PNG IEND chunk
Image Size                      : 512x504
Megapixels                      : 0.258

```
- the metadata is normal it has no meaning for us. so i try to perform the file operation to know if it is an actual png file or no.

```console
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ file flag.png 
flag.png: PNG image data, 512 x 504, 8-bit/color RGBA, non-interlaced
```
- turns out it is a png file so thats a dead end. I still performed a hexdump to see if the magic numbers were altered with but they're not.

```console
00000000   89 50 4E 47  0D 0A 1A 0A  00 00 00 0D  49 48 44 52  .PNG........IHDR
00000010   00 00 02 58  00 00 00 32  10 00 00 00  00 F5 6D 26  ...X...2......m&
00000020   56 00 00 00  04 67 41 4D  41 00 00 B1  8F 0B FC 61  V....gAMA......a
00000030   05 00 00 00  20 63 48 52  4D 00 00 7A  26 00 00 80  .... cHRM..z&...
00000040   84 00 00 FA  00 00 00 80  E8 00 00 75  30 00 00 EA  ...........u0...
00000050   60 00 00 3A  98 00 00 17  70 9C BA 51  3C 00 00 00  `..:....p..Q<...
00000060   02 62 4B 47  44 FF FF 14  AB 31 CD 00  00 00 07 74  .bKGD....1.....t
00000070   49 4D 45 07  E7 03 10 02  01 31 9B 6D  49 C0 00 00  IME......1.mI...
00000080   0A DD 49 44  41 54 78 DA  ED D9 69 50  53 57 1B 07  ..IDATx...iPSW..
00000090   F0 87 10 35  10 83 A4 12  88 1A 90 4D  45 25 76 90  ...5.......ME%v.
000000A0   45 22 08 9D  41 8A 55 10  15 3A 58 97  A9 D5 16 AD  E"..A.U..:X.....
000000B0   32 D4 5D 3B  52 11 1D ED  8C 65 44 3B  A0 A0 AD B5  2.];R....eD;....
000000C0   A3 08 6A D4  52 47 C6 A9  83 96 AA 08  C8 BE BB 04  ..j.RG..........
000000D0   15 A1 C0 48  C2 62 40 B2  98 F3 7E C8  9B 17 EF 25  ...H.b@...~....%
000000E0   20 58 A8 BD  7D 9F DF 27  CE B9 E7 3E  CF 39 5C F8   X..}..'...>.9\.
000000F0   13 12 20 6F  45 A7 53 A9  FA 5F 71 E8  D0 F4 E9 79  .. oE.S.._q....y

```
- its 89 50 4E 47 0D 0A 1A so its normal nothing wrong in that.
- then i use the strings operations

```console
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ strings flag.png
IHDR
IDATx^
;/"@
M<g@H
Eu*eW
%m02
-y]:
a/~q;
\OTzZK
|3.8g3MyO
?<a&
.6Umj2-
q]=6
IEND
secret/UT
secret/flag.pngUT
)!!0i
&5@B
T?D@$
        /^0
Fr2;{
V'--Q
|n ir
#@-O
|{l'
cG_
'
'
'
%LMekJ
.]4t
Gedd
zO66
0Ug:
t<X7
WYI#
mib"g
hl,r
:0~3
PUMw
CCXh
Rk^T
f4yx
f!=A=
F;\c
M5u^^
loOP
ptdb25
#L{e
Lr/q
#SS_
ecd54
{)II
UTLDk
})++
-^Mrr0
QPPWP
secret/UT
secret/flag.pngUT

```
- the secret/flag.png here indicates an image hidden in the file so i use binwalk -e to extract.
```console
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ binwalk -e flag.png
/usr/lib/python3/dist-packages/binwalk/core/magic.py:431: SyntaxWarning: invalid escape sequence '\.'
  self.period = re.compile("\.")

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2876, uncompressed size: 3029, name: secret/flag.png
42915         0xA7A3          End of Zip archive, footer length: 22

```
- now i have an extracted image.

```console
┌──(anonymous㉿Anonymous)-[~/investigation/new]
└─$ cd _flag.png.extracted
                                                                                             
┌──(anonymous㉿Anonymous)-[~/investigation/new/_flag.png.extracted]
└─$ ls  
29  29.zlib  9B3B.zip  secret
                                                                                             
┌──(anonymous㉿Anonymous)-[~/investigation/new/_flag.png.extracted]
└─$ cd secret             
                                                                                             
┌──(anonymous㉿Anonymous)-[~/investigation/new/_flag.png.extracted/secret]
└─$ ls       
flag.png
                                                                                             
┌──(anonymous㉿Anonymous)-[~/investigation/new/_flag.png.extracted/secret]
└─$ eog flag.png
```
**Image**
![flag (1)](https://github.com/user-attachments/assets/1027824a-9f9f-4899-884a-52cc8afdfd23)

