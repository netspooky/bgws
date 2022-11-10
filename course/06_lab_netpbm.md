# LAB02 - NetPBM

In this lab we are building a [NetPBM](https://en.wikipedia.org/wiki/Netpbm) image.

NetPBM is a very simple bitmap format. This is a monochrome one. Each bit in the binary number represents a pixel.

```
-- mametchi.xx by netspooky 2022-11-05
-- Requires xx v0.4.4 or later
-- This is a NetPBM file of a Tamagotchi sprite. 
-- Uses 0y binary representation for pixels
-- Generates mametchi.030270c4.bin, can use -o mametchi.pbm and open in an image viewer.
"P4" 0a -- Magic Value
"16 14" 0a -- Height and Width
╭──── Pixel Data ───╮ 
0y00111000 0y00011100 
0y01111100 0y00111110 
0y00111111 0y11111100 
0y00100000 0y00000100 
0y01001100 0y00110010 
0y01010010 0y01001010 
0y00100001 0y10000100 
0y01011111 0y11111010 
0y01000000 0y00000010 
0y01100000 0y00000110 
0y00011000 0y00011000 
0y00001000 0y00010000 
0y00010011 0y11001000 
0y00011100 0y00111000
```

Build this file using xx.

```
python3 xx.py mametchi.xx -o mametchi.pbm
```

You can open this image and view it. It's really tiny so you will have to zoom in!

Change some of the bytes in the file, what happens?

## About NetPBM

NetPBM is an old image format, and is supported on many operating systems. The P4 type is known as a "Portable Bit Map", which is a monochrome bit map that "maps" each pixel into the grid we established for the height and width.

There are other types of files in the NetPBM family that you can use. It's quite a versatile format!

| Magic | Description |
|-------|-------------|
| "P1" | [Plain PBM](https://netpbm.sourceforge.net/doc/pbm.html#plainpbm) "Portable Bit Map" |
| "P2" | [Plain PGM](https://netpbm.sourceforge.net/doc/pgm.html#plainpgm) "Portable Grey Map" |
| "P3" | [Plain PPM](https://netpbm.sourceforge.net/doc/ppm.html#plainppm) "Portable Pixel Map" |
| "P4" | [PBM](https://netpbm.sourceforge.net/doc/pbm.html) "Portable Bit Map" |
| "P5" | [PGM](https://netpbm.sourceforge.net/doc/pgm.html) "Portable Grey Map" |
| "P6" | [PPM](https://netpbm.sourceforge.net/doc/ppm.html) "Portable Pixel Map" |
| "P7" | [PAM](https://netpbm.sourceforge.net/doc/pam.html) "Portable Arbitrary Map" |

Here is an example of a NetPBM polyglot file made by [retr0id](https://twitter.com/David3141593/status/1584052622352584704) for [BGGP2](https://github.com/netspooky/BGGP/blob/main/2021/retr0id/two.chip8.pbm):

![image](https://user-images.githubusercontent.com/26436276/201176496-f0a26973-cef5-4840-bb59-864cd3ff7438.png)

## Visualizing Data

You can use these formats to help visualize binary data. Because they are bit maps, data can be added to any of these files to create a visual representation of the file contents. Here is a penguin that was found in a firmware image using NetPBM: https://twitter.com/lethalbit/status/1491637042475941888

Instead of using PBM, let's us a PGM so that each byte can represent a shade of grey.

Type this into viz.pgm
```
P5
16 16
255
```

Then type this into getbytes.py. It will create a file called bytes.bin containing all of the bytes from 0 to 255 in a row.

```python
import struct

buf = b""
for i in range(0,256):
  buf += struct.pack("B",i)

with open("bytes.bin","wb") as f:
    f.write(buf)
    f.close()
```

Now attach this file to end of viz.pgm.
```
cat bytes.bin >> viz.pgm
```

Now you should see a gradient of 16 grey bars.

You can use this trick to visualize files! Fiddle with the height and width, and read the spec (it's short!) to learn how you can use NetPBM files to do even more.


Prev: [LAB01 - PDF](05_lab_pdf.md) | Next: [LAB03 - Polyglot](07_lab_polyglot.md)




