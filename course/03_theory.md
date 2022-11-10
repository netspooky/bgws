# Theory

## Ways of Reducing A File's Size

There are many different methods that may come to mind when shrinking the total size of a file. 

[Compression](https://en.wikipedia.org/wiki/Data_compression) is a very common and reliable way of shrinking a file, but it's not always perfect. Complex files can't always be reliably compressed, and the container format that holds the compressed data can also have it's own file overhead that takes up space. Reducing a multimedia format's quality and/or adjusting the codec is also another way to shrink file size. Depending on your needs, this may be fine. 

Stripping a file of it's metadata is another common way to shrink a file's total size. A common utility for binaries is simply called [strip](https://en.wikipedia.org/wiki/Strip_(Unix)), and it removes things like symbol names, build IDs, and debug info from a file. Similarly, compilers may remove unnecessary code in a process known as [dead code eliminiation](https://en.wikipedia.org/wiki/Dead-code_elimination). This removes any excess code which is not used in the binary.

There are other methods that depend on the rules of a given system. Take [base2048](https://github.com/qntm/base2048). This is an encoding scheme that 385 bytes of data in 280 unicode characters. While this may seem like magic, the resulting data is actually much bigger than 280 bytes. It uses UTF-8, which means that each byte can be anywhere from 1 to 4 bytes. While not good for reducing total data size, it's perfect for the known constraints of the platform.

Here is [an example](https://twitter.com/rheolism/status/1587529205427814401) of using base2048 to encode source code for a BBC Micro Emulator: 

<img width="474" alt="image" src="https://user-images.githubusercontent.com/26436276/201197812-f731f9fc-0a8d-48d3-ae39-027e6315524d.png">

## Reading Between The Lines

When pulling apart files, you may start to notice seemingly unnecessary pieces that aren't required by the program to actually run. These are elements that can be used to your advantage.

<img width="466" alt="image" src="https://user-images.githubusercontent.com/26436276/201194492-89f48179-ccc4-4e49-b64f-83427805474d.png">

_Example of padding to a page boundary in a file_

Padding is often used when data needs to be lined up to certain boundaries. Sometimes the padding is to align to a small boundary like 16 bytes (this is common on x86_64) or something as big as a memory page - 4096 (0x1000) bytes. There can be many reasons for using padding, but a common one is consistency of execution. This aims to ensure that the file that is generated by a program such as a compiler will have consistent behavior across the board. This gives us room to play around.

![image](https://user-images.githubusercontent.com/26436276/201193578-057b2338-1c79-4559-83d8-96c154a6d5e0.png)

_Image Source: https://www.insidegadgets.com/2011/04/23/emulating-the-nintendo-logo-on-the-gameboy/_

Take for example [badge.gif](https://thugcrowd.com/chal/badge.gif). This is a polyglot file containing a GIF, a Gameboy ROM, a ZIP file, and a ton of other things that was used in a CTF. The GIF file appears first, and fits within the padding at the top of the Gameboy ROM. The Gameboy ROM's [Cartridge Header](https://gbdev.io/pandocs/The_Cartridge_Header.html) doesn't begin until 0x100 bytes into the file, which gives ample room to fit content before the ROM actually begins.

<img width="470" alt="image" src="https://user-images.githubusercontent.com/26436276/201225748-e7ce1fa4-e682-474a-8e83-d8e7c439c0ab.png">

Padding can be used to fit code into places where they normally don't appear. Take for example the [Dead Bytes](https://tmpout.sh/1/1.html) article by [xcellerator](https://xcellerator.github.io/), which demonstrates the process of writing a library to fit code where it isn't supposed to.

<img width="818" alt="image" src="https://user-images.githubusercontent.com/26436276/201193843-9f870b51-7836-4282-96eb-85509a6dbe64.png">

_Part of xcellerator's write up on LibGolf_

There are also many examples of malware which infects the padding of a file to hide itself in a reliably loaded area. This [paper](https://ivanlef0u.fr/repo/madchat/vxdevl/vdat/tuunix02.htm) by Silvio Cesare is a classic text on these infection methods.

Informational sections can also be used to store data that the file parser will ignore, making it the perfect target for hiding a while other file. These sections can often be omitted from the binary to make it smaller as well.

<img width="546" alt="image" src="https://user-images.githubusercontent.com/26436276/201194111-29ffbe50-8436-499b-bd67-517b9588d721.png">

_An example of ASCII art hidden inside of an informational section of a binary_

Many scripting languages use comments to stop processing data on a given line. When working with a text based file format, take a look at the types of comments supported. What can you put inside them?

A similar approach can be taken with scripting languages and variables. Check out [this](https://github.com/netspooky/BGGP/blob/main/2021/netspooky/ns.bggp2021.asm) file. When built, it is an EXE, a PDF, and a Javascript file. The first two bytes of the EXE "MZ", are ASCII. There is enough room to fit a = and a " after, and then a stream of binary data. The non-printable parts of the file are stored in a variable in javascript, which the browser happily executes without knowing that it's also an EXE and a PDF.

<img width="610" alt="image" src="https://user-images.githubusercontent.com/26436276/201195456-454a7503-deb1-452e-89f1-c99f8a7a36c7.png">

_alert2.exe interpreted as javascript in a text editor, notice the multi-line comments between the MZ variable and alert(2)_

---

Prev: [Fundamentals](02_fundamentals.md)  | Next: [Tools](04_tools.md)

