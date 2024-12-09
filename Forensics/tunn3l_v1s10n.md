# CTF Challenge: tunn3l_v1s10n

## Table of Content

- commands-executed:  
- flag :picoCTF{qu1t3_the_v13w_2020}


### Chain of thought / Learning:
-okay so all i have is a image that is corrupted. we use the hex dump to see the hex data to check if there is any error
- after some researching and watching a lot of John Hammond's icectf videos i've learnt that there is something called a magic number for files.
- A magic number is a sequence of bytes at the beginning of a file that identifies the file's type. When a file is corrupted usually it'll be the magic numbers that'll be corrupted. so exploring in that route may help.
- on using hexedit on the file
```
00000000   42 4D 8E 26  2C 00 00 00  00 00 BA D0  00 00 BA D0  00 00 6E 04  00 00 32 01  00 00 01 00  BM.&,.............n...2.....
0000001C   18 00 00 00  00 00 58 26  2C 00 25 16  00 00 25 16  00 00 00 00  00 00 00 00  00 00 23 1A  ......X&,.%...%...........#.
00000038   17 27 1E 1B  29 20 1D 2A  21 1E 26 1D  1A 31 28 25  35 2C 29 33  2A 27 38 2F  2C 2F 26 23  .'..) .*!.&..1(%5,)3*'8/,/&#
00000054   33 2A 26 2D  24 20 3B 32  2E 32 29 25  30 27 23 33  2A 26 38 2C  28 36 2B 27  39 2D 2B 2F  3*&-$ ;2.2)%0'#3*&8,(6+'9-+/
00000070   26 23 1D 12  0E 23 17 11  29 16 0E 55  3D 31 97 76  66 8B 66 52  99 6D 56 9E  70 58 9E 6F  &#...#..)..U=1.vf.fR.mV.pX.o
0000008C   54 9C 6F 54  AB 7E 63 BA  8C 6D BD 8A  69 C8 97 71  C1 93 71 C1  97 74 C1 94  73 C0 93 72  T.oT.~c..m..i..q..q..t..s..r
000000A8   C0 8F 6F BD  8E 6E BA 8D  6B B7 8D 6A  B0 85 64 A0  74 55 A3 77  5A 98 6F 56  76 52 3A 71  ..o..n..k..j..d.tU.wZ.oVvR:q
000000C4   52 3D 6C 4F  40 6D 52 44  6E 53 49 77  5E 54 53 39  33 70 58 52  76 61 59 73  5F 54 7E 6B  R=lO@mRDnSIw^TS93pXRvaYs_T~k
000000E0   5E 86 74 63  7E 6A 59 76  62 50 76 5E  4C 7A 62 50  87 6D 5D 83  69 59 8D 73  63 9B 81 71  ^.tc~jYvbPv^LzbP.m].iY.sc..q
000000FC   9E 84 74 98  7E 6E 9B 81  71 8D 73 63  73 5A 4A 70  57 47 5A 41  31 4F 36 26  4E 37 27 4F  ..t.~n..q.scsZJpWGZA1O6&N7'O
00000118   38 28 4F 38  28 51 3A 2A  50 39 29 4F  38 29 4B 35  29 50 3A 2F  4B 35 2A 3F  29 1E 42 2E  8(O8(Q:*P9)O8)K5)P:/K5*?).B.
00000134   23 4B 37 2C  45 31 26 3F  2B 20 43 2F  24 43 2F 24  40 2A 1F 48  32 27 4B 32  28 47 2E 24  #K7,E1&?+ C/$C/$@*.H2'K2(G.$
00000150   40 27 1D 45  2C 22 4C 34  28 4C 34 28  4B 33 27 4A  32 26 4C 32  24 4E 34 26  50 35 27 52  @'.E,"L4(L4(K3'J2&L2$N4&P5'R
0000016C   37 29 53 36  28 55 38 2A  4B 30 22 5D  42 34 63 49  39 49 2F 1F  44 2B 1B 4D  34 24 4D 36  7)S6(U8*K0"]B4cI9I/.D+.M4$M6
00000188   27 4A 33 24  46 2C 20 48  2E 22 46 2E  22 44 2E 22  3C 26 1B 32  20 15 30 1F  16 32 23 1A  'J3$F, H."F."D."<&.2 .0..2#.
000001A4   36 27 1E 3C  2B 22 3E 2B  24 42 2C 26  5E 44 3E 66  4C 46 36 1D  19 33 1F 1A  3F 30 2D 13  6'.<+">+$B,&^D>fLF6..3..?0-.
000001C0   0A 06 09 06  02 05 04 00  0A 05 04 0B  06 05 0D 05  05 0B 06 05  0A 06 05 08  06 05 08 06  ............................
000001DC   05 0A 06 05  0D 05 05 0D  05 05 0B 03  04 06 00 01  05 00 00 09  04 03 0B 06  03 0A 05 02  ............................
000001F8   08 05 01 09  06 02 09 06  02 07 04 00  07 04 00 08  05 01 08 04  03 06 02 01  06 01 02 07  ............................
00000214   02 03 06 04  03 04 02 01  06 02 01 06  02 01 05 00  00 1D 18 17  1C 15 12 0E  07 04 14 0B  ............................
00000230   07 16 0D 09  15 0D 06 17  0F 08 1B 13  0C 10 08 01  12 0B 02 16  0F 06 17 0E  05 16 0D 04  ............................
0000024C   16 0D 04 17  0E 05 1A 11  08 16 0D 04  1C 14 0D 1F  17 10 28 20  19 22 1A 13  20 17 13 1B  ..................( .".. ...
00000268   12 0E 18 0F  0B 15 0C 08  12 09 05 16  0D 09 15 0C  08 11 08 04  15 0C 08 13  0A 06 0F 06  ............................
00000284   02 12 09 05  12 0C 07 13  0D 08 11 0B  06 11 0B 06  10 0A 05 10  0A 05 0F 09  04 0E 08 03  ............................
000002A0   0B 07 02 0B  07 02 0A 05  02 08 03 00  08 03 00 06  01 00 0A 05  04 08 03 02  08 04 03 05  ............................
000002BC   01 00 05 01  00 08 04 03  04 02 01 02  00 00 05 03  02 04 02 01  02 00 00 04  02 02 03 01  ............................
000002D8   01 04 02 01  04 02 01 06  06 00 09 06  01 0A 08 00  0C 08 03 0C  08 03 0D 08  07 0B 06 05  ............................
000002F4   0D 05 05 10  08 08 12 09  06 11 08 04  11 08 04 13  0B 04 16 0F  06 0F 08 00  13 0C 03 1B  ............................
00000310   14 0B 1B 14  0B 11 0A 01  16 0F 06 15  0E 05 18 11  08 16 0F 06  10 09 00 16  0F 06 16 0F  ............................
0000032C   06 14 0D 04  0E 07 00 14  0D 04 17 0F  08 16 0E 07  14 0C 05 1B  13 0C 1E 16  0F 19 11 0A  ............................
00000348   19 0F 08 14  0A 03 17 0D  06 18 0E 07  18 0E 07 17  0D 06 16 0C  05 17 0D 06  1A 10 09 1C  ............................
00000364   12 0B 1A 11  0E 18 0F 0C  20 17 14 19  10 0D 11 08  05 15 0C 09  13 0A 07 14  0B 08 14 0B  ........ ...................
00000380   08 16 0D 0A  17 0B 09 15  09 07 1B 0F  0D 17 0B 09  15 09 07 13  07 05 1C 10  0E 18 0C 0A  ............................
0000039C   16 0A 08 17  0B 09 16 0A  08 15 09 07  13 0A 07 16  0D 0A 11 08  05 14 0B 08  17 0E 0A 16  ............................

```
- the important thing is the BM at the beginning, it is a bitmap file and the magic numbers for that is:
![mn](https://github.com/user-attachments/assets/26c14e20-4b98-4d27-a708-75edde9f0258)

-now we know the extension must be bmp. so we try that. 
-brb watching a file signature analysis vid and reserching 
-brb watching a file signature analysis vid and reserching 
https://www.file-recovery.com/bmp-signature-format.html

-okay so i cant use hexedit because it doesnt show offset and i need that cause i m a noob
-i ll use hxd popular software
- okay so couple of things that are imp here
- all the entries are in little endian which basically means the bytes are reversed from normal form
- second we see the bad and bad written on 10th and 14th position. I used a sample bmp working image that i downloaded from the internet
- acc to that i set the values to 8A and 7C respectively.
  this is the sample:
![sample](https://github.com/user-attachments/assets/e6d32db2-6e21-4c32-b6ca-85fee30841d7)

this is the image given:

![11](https://github.com/user-attachments/assets/ffe9c323-3d80-42af-9a0c-da5141cc1cdc)

- the image now opens up
![1](https://github.com/user-attachments/assets/b1582d78-84b3-4f78-8318-92b54c2799f7)
- the image appears to be cropped out, now the way to handle this is we find the hex offset responsible for the height and width.
- the image if we check the properties appears to be of height 1134 and width 306 now we need to find the hex of that
- 1134 : 046E , 306 : 0132 now remember this is big endian to actually find it we need to change it into little endian
- i.e 6E 04 AND 32 01
- we change the height to see if the image lengthens
- now the most common resolution is 1280 height so we use the
- hex is 500 , and little endian 00 05
- okay i really messed up the picture it wasnt working plus the height didnt increase so maybe change the width
- 500 ? hex is 01F4 and little endian F4 01
- okay it worked there is more to the image i just need to increase it further.
![2](https://github.com/user-attachments/assets/34f5f4f5-ae21-4f60-a118-33c96cff70bf)
- change it to 720 maybe?
- hex is 2D0 and little endian D0 02 didnt work still left
- 800 is 0320 so 20 03 and i see a little yellow tinge on top of the image
![3](https://github.com/user-attachments/assets/fa089a19-464b-476f-8587-d215291015d9)

-lets try 900 which is 384 or 84 03 in little endian , it broke the image , so lets go for a quarter 
- 825 that is 03 39 , which is 39 03 and boom we have the flag
![tunn3l_v1s10n](https://github.com/user-attachments/assets/57f73e44-9fc5-4e9a-be5d-9edebb73343e)

