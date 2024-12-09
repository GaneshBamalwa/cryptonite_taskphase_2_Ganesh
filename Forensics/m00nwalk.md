# CTF Challenge: m00nwalk

## Table of Content

- commands-executed:  sstv -d message.wav -o output.png
- flag :picoCTF{beep_boop_im_in_space}


### Chain of thought / Learning:
- the hint provided in the ctf is **How did pictures from the moon landing get sent back to Earth?**
- so on some research i found on google:
```
Therefore, Apollo 11's moonwalk video was transmitted from the Apollo TV camera in a monochrome SSTV format at 10 frames per second (fps) with 320 lines of resolution, progressively scanned.
```
- SSTV : slow scan television is a method of converting pictures to audio and transmitting them over radio.
- SSTV works by representing each pixel in an image as a sinusoid of different frequencies. Color is achieved by encoding the brightness of each color component separately. its hella interesting, but coming to the point what we need is an sstv decoder
https://github.com/colaclanth/sstv
-very obv choice so we install it and then decode.
![output](https://github.com/user-attachments/assets/7b555523-9686-45d3-9512-8389bd7c8748)



#### Output:
```console
                                                                                                                                        
┌──(anonymous㉿Anonymous)-[~/investigation/sstv]
└─$ wget https://jupiter.challenges.picoctf.org/static/fc1edf07742e98a480c6aff7d2546107/message.wav
--2024-12-09 14:23:54--  https://jupiter.challenges.picoctf.org/static/fc1edf07742e98a480c6aff7d2546107/message.wav
Resolving jupiter.challenges.pi![output](https://github.com/user-attachments/assets/53465f6b-5f7a-4803-bbc9-68317b87cc95)
coctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 11066998 (11M) [application/octet-stream]
Saving to: ‘message.wav’

message.wav                       100%[=============================================================>]  10.55M   656KB/s    in 13s     

2024-12-09 14:24:08 (862 KB/s) - ‘message.wav’ saved [11066998/11066998]

                                                                                                                                        
┌──(anonymous㉿Anonymous)-[~/investigation/sstv]
└─$ sstv -d message.wav -o output.png
[sstv] Searching for calibration header... Found!    
[sstv] Detected SSTV mode Scottie 1
[sstv] Decoding image...     [####################################################################################################] 100%
[sstv] Drawing image data...
[sstv] ...Done!
                   
```
