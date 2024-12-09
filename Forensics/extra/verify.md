# CTF Challenge: **verify**

## Table of Content

- commands-executed:  
- flag :picoCTF{trust_but_verify_c6c8b911}


### Chain of thought / Learning:
- we have a checksum file which has a sha256 encryption. we need to very to which file it belongs so that we can decrypt that to get the flag
- we'll create  sha256 checksum of all the files and pipe the output to grep with the checksum encryption.
- we just use the verified file to decrypt the flag and voila. 


#### Output:
```console
ctf-player@pico-chall$ ls
checksum.txt  decrypt.sh  files
ctf-player@pico-chall$ ls files/
047MJYW7  58VrA22G  AOgyIEGc  FXHBxQjZ  LmicJDs8  QRakKVta  WBbhtpsN  bf4r768r  gkqJibML  orV7qTqZ  uDj1e5QR  xgBUzxwD
0CbGv6a3  5HYKp822  AlGTwKyO  Fv7iksDZ  Lmt5Y0x2  Qi0CXXRR  WBv990nM  bvPuToXm  gmcsCSX3  oy2oXp1t  uJnJfk8o  xjRhyYW5
0E56AVSC  5Hde480w  AmQLyNou  G244hQnd  Lo86CvQ9  Qir73mSK  WEqguSEY  c6c8b911  hBccpGRH  pGGOwBsr  ukl9M0t5  xrUttVxO
0QUxtltc  5K1a6h06  Ar2IDsE2  GDrafQ2W  LxrBh9k1  R0QJ2VKL  WGlw8QMW  cYQJTzGN  hI05TCz1  pOWsomAC  ulFEMOKX  xxr0iXrr
0XKkalUj  5P2RhVCm  BD8hIik3  GHuWjeJ9  M4k3wbII  R9B10IsM  WWTBLhPp  coJvjQ1h  hONfsBJg  pQNOrEf0  umDaEkFr  yAbc0Rj2
0hBYiFqV  5UGLBciS  BtuwzSy0  GUEnrd1t  Ml2ne9bC  RT9fmHCO  WdGGv43K  d3p6iNNZ  hgfq6lwn  pcG2OMtT  uvq4BDCM  yRrCeSQg
0xx1tyUI  5glLfO3M  C8QQ7gyc  Gp1JEl2h  N18is4D1  RiQGT34B  X7yet6uw  dDSS287o  hnC2Necm  pfB7wztg  uw3TvL3P  yi2zkQtL
1VpyYwwh  60CeHYva  CIcPHsac  H7Ixs9CI  NAKaekRz  SFAQKdZD  XF3VmqVm  dDuPGuwH  hsW2u10K  pn2lFoDd  uwZIBYpw  yj7yobL0
25jFiRcF  69891sbg  CJ5U4hxW  HDYiL2qX  NEc5NL3C  SGQH2HKl  XFrufR80  dEVxJ2qG  i2LDbe1K  poTBHw5o  uz0yrxxD  yxVNk723
2B0GV1AB  6ePyVUQ2  CmGCd6Vt  HNRI4jm0  NH1pCwum  SQrS0l9A  XQJcaZgW  dJzWkU1Q  i4XAopa0  pz7WGxJ4  v0LKVD3h  z333mx7V
2SbMywFt  6nFsOudx  D6DGyxjR  HUiJtVz0  NmuLJcjD  SREVuUw3  XqRw2HGU  e7U2gGar  iKj2d6J4  qJIJZA0v  v9TEcwko  zNtZNpTg
2Yc6IWTg  6wnVCfWh  D9zwUVlq  HhPvJ7d7  NqjC5VXz  Sus5gnJ8  XuigwWF7  eHMqnmO6  iMQMDV0F  qiKkh7L2  vC1tHUr2  zSomJYUc
2oGGasVb  7YlIOxWG  DBQbeL0I  Ht3OiHhF  O7knebdG  SzSn7OcI  Y1tTgMUD  eUp5OdvA  jHRn7Fub  qnxF5I1t  vGHNz4al  zUmtlpHw
2xPyec1z  80btcs9b  DRnArSUC  I1gghDYt  O9vttreT  TDjaKG6o  YEjiR5zf  efPoh96A  jvtAQCHw  rAQk2W0n  vL0JYb7n  zjK7vU2n
3HtK7pJ0  80f71Tlc  DSwFiycn  IJX4r4eM  OGiva8vH  TMEQwqGw  YZ0OB1mt  egSaXF3D  lMx8gj9G  rDBnOYi8  vY5qGrrd  zlkIRSOv
3MWxikbL  85k4844c  DgSvTEwj  JB4PaRNY  OHjloRN0  Tb4MR5ML  Ylaf2TY1  enUaRS4w  lURnFs0v  rHtWBcCX  vvJtzkqH
3P2iIh03  86hYDjno  DhGmqcSh  JqYRPdED  OaQl5g3e  TcfR5Cf6  Yn1Qg1dx  eoYlHLVB  lyYImb9U  rK99ez1a  w3o3t3VK
3ZyNMmFE  8SXF7mDb  DpTMOGCI  K4jUiynD  ObjxHPwy  Td52rYaf  Ypof7Dgr  exyTux3t  mMUJICI9  rUmhKhnU  wJD9dCMd
3eJU0bPR  8h1rOlXM  DxlIKqf0  KDp8EJSk  Ofz0iqFX  Texe1REf  ZM8AYtlG  fB2VnieD  mpJ16YYd  sOhwN7cV  wgvRImaG
3qDZ0GiM  9CrGqrOf  EC1I5QwZ  KbONzfRz  Ot4mYM7x  ThXpDtur  ZVhZ6QYU  fJiZ2bMw  nMTwYBYg  sTktzsdS  whevF4V0
3rXzZWry  9VFp8JdD  EXORCadn  Kd0WNtCU  Ous2JVk2  TtY9kI58  ZWNJ0AhH  fKCy1WTf  niXGrsgK  t3MxVbsm  x1wlAOTr
43UId6P7  9YOFaoZl  EfRHiDLP  Keoo2vTu  PJqcmuRt  TxL3f6fM  ZZSXid5R  fPrKO8V5  nr3IXKgz  t3yYcEve  xCDyjqeT
4MQ26j79  9fSkDlcH  Eg5lVJUw  KvvTfLSK  PfmG9EIR  U7SEpsXd  a76e3swH  fQnfnq06  nvtdmSSg  t7jXqCcv  xE1I24IF
4UWHd6Hh  9spBfMu7  ElM3tYhK  LP8coBqU  PvE5OAg4  URYYNGxZ  aUzIEw0T  fnrslV0R  oQzbBXPT  tQQuoksm  xP8hXfNR
4iAgLaET  A0Xjfjyv  FNRT4oFd  LQJNuVhs  Q94hibhx  VR8O9EAS  bE62hGOU  gDXNNquR  onqK4HP3  tjZsxG5L  xQMWIZBH
51fpnVb7  AOAysod6  FWmPesGL  LkGAamWS  QHkh1WHT  W1Fiysnc  bNDt5rfT  gIhaWdn0  opLYnq5q  tzjdKlhj  xVPXvgB2
ctf-player@pico-chall$ sha256sum ./* | grep 467a10447deb3d4e17634cacc2a68ba6c2bb62a6637dad9145ea673bf0be5e02
sha256sum: ./files: Is a directory
ctf-player@pico-chall$ cd files
ctf-player@pico-chall$ sha256sum ./* | grep 467a10447deb3d4e17634cacc2a68ba6c2bb62a6637dad9145ea673bf0be5e02
467a10447deb3d4e17634cacc2a68ba6c2bb62a6637dad9145ea673bf0be5e02  ./c6c8b911
ctf-player@pico-chall$ ls
checksum.txt  decrypt.sh  files
ctf-player@pico-chall$ ./decrypt.sh files/c6c8b911
picoCTF{trust_but_verify_c6c8b911}
ctf-player@pico-chall$ Connection to rhea.picoctf.net closed by remote host.
Connection to rhea.picoctf.net closed.

```
