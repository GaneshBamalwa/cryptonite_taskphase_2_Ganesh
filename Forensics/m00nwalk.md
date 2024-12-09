# CTF Challenge: m00nwalk

## Table of Content

- commands-executed:  
- flag :


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

#### Output:
```console

```
