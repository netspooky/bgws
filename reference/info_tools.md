# File Hacking Tools and Resources

There are several useful file analysis tools that you can use. All software listed is free to use. Software that has a paid version will include "paid" in the description.

This is a compilation of tools and resources compiled by myself and other file format hackers. It is by no means exhaustive.

## General Tools

| Software | File Type | Description |
|----------|-----------|-------------|
| [binvis.io](http://binvis.io/#/) | Multi | Binary visualizer online |
| [binwalk](https://github.com/ReFirmLabs/binwalk) | Multi | File signature analyzer and extractor |
| [BVI](https://bvi.sourceforge.net/) | Multi | Binary Visual Editor |
| [exiftool](https://exiftool.org/) | Multi | Can view and edit EXIF metadata in a variety of formats |
| [file](https://en.wikipedia.org/wiki/File_(command)) | Multi | File signature analyzer utility for Linux |
| [hobbits](https://github.com/Mahlet-Inc/hobbits) | Multi | A multi-platform GUI for bit-based analysis, processing, and visualization |
| [kaitai web IDE](https://ide.kaitai.io/) | Multi | Provides an interface for examining files in the browser |
| [kaitai](https://kaitai.io/) | Multi | File parser that uses yaml for templates |
| [lief](https://github.com/lief-project/LIEF) | Multi | Python library for parsing binaries. "Library to Instrument Executable Formats" |
| [rabin2](https://github.com/radareorg/radare2) and [rz-bin](https://github.com/rizinorg/rizin) | Multi | Provides metadata about binaries on the command line. The strings tool is one of the best. |
| [unblob](https://unblob.org/) | Multi | File extraction tool |
| [VirusTotal](https://www.virustotal.com/gui/home/upload) | Multi | Scan a file with many engines and get community signatures to help identify a file |
| [yara](https://virustotal.github.io/yara/) | Multi | Define and search for binary signatures in a file |

## Specialized tools

| Software | File Type | Description |
|----------|-----------|-------------|
| [CFF Explorer](https://ntcore.com/?page_id=388) | Portable Executables | Examine resources in an EXE file |
| [DetectItEasy](https://github.com/horsicq/Detect-It-Easy) | Multi | Program for determining types of files for Windows, Linux and MacOS. | 
| [mgbdis](https://github.com/mattcurrie/mgbdis) | Gameboy ROMs | Disassemble ROM files that can be reassembled using [RGBDS](https://rgbds.gbdev.io/) | 
| [OFRAK](https://github.com/redballoonsecurity/ofrak) | Multi | Firmware analyzer, unpacker, and editor |
| [pebear](https://hshrzd.wordpress.com/pe-bear/) | Portable Executables | Tool for analyzing portable executables with a lot of features. |
| [pefile](https://github.com/erocarrera/pefile) | Portable Executables | Python library for parsing PEs |
| [pesieve](https://github.com/hasherezade/pe-sieve) | Portable Executables | Can find PE files in memory and dump them. |
| [PeStudio](https://www.winitor.com/) | Portable Executables | Analyze and spot anomalies in PE files. Free/Paid.|
| [PNG Chunk Inspector](https://www.nayuki.io/page/png-file-chunk-inspector) | PNG | Examine individual PNG chunks online. |
| [pyelftools](https://github.com/eliben/pyelftools) | ELF | A python library for parsing ELF files |
| [readelf](https://man7.org/linux/man-pages/man1/readelf.1.html) | ELF | Part of binutils. View information about ELF files |
| [Resource Hacker](http://www.angusj.com/resourcehacker/) | Portable Executables | PE Resource compiler and decompiler. Grab media from a PE. |
| [terminus](https://github.com/genonullfree/terminus) | ELF | Used to locate exported functions in ELF libraries |
| [TrID](https://mark0.net/soft-trid-e.html) | Multi | Examine file signatures. An online version is available too. Free. |
| [XELFViewer](https://github.com/horsicq/XELFViewer) | ELF | GUI for ELF viewing and editing |

## Debuggers and Reverse Engineering Tools

When messing with a binary, it is useful to see if the file still runs as expected, and if not, figure out why.

| Software | Platform | Description |
|----------|-----------|-------------|
| [IDA](https://hex-rays.com/ida-pro/) | Windows, Linux, Mac | Well respected debugger and binary analysis tool with a lot of community support. Paid version is expensive but worth it if you can get a license. |
| [ghidra](https://ghidra-sre.org/) | Windows, Linux, Mac | Tax-payer funded Ida competitor that is pretty dang good. |
| [radare2](https://github.com/radareorg/radare2) and [rizin](https://github.com/rizinorg/rizin) | Linux, Mac, Windows, Android | Rizin is a fork of Radare2. Both are useful for debugging and analyzing binaries. |
| [gdb](https://www.sourceware.org/gdb/) | Linux | The GNU Debugger. Powerful debugger for user and kernel level binaries with a suite of tools ([binutils](https://www.gnu.org/software/binutils/)) included. Use [gef](https://github.com/hugsy/gef) to make it nicer. |
| [WinDbg](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/debugger-download-tools) | Windows | Very powerful debugger for Windows. Can debug user applications and the kernel itself. |
| [lldb](https://lldb.llvm.org/) | Mac | Debugger for Mac |
| [Binary Ninja](https://binary.ninja/) | Windows, Linux, Mac | A powerful debugger, has a cloud option. Free to try, paid. |

## Forensics Tools

Sometimes you need to analyze an entire disk or memory dump to find things.

| Software | Description |
|----------|-------------|
| [autopsy](https://github.com/sleuthkit/autopsy) | GUI for [SleuthKit](http://www.sleuthkit.org/). Used for forensics. |
| [volatility](https://github.com/volatilityfoundation/volatility) | A memory forensics framework. |

## Other Helpful Tools

| Software | Description |
|----------|-------------|
| [crccalc](https://crccalc.com/) | Use this to calculate a variety of checksums online. |
| [defuse.ca x86 assembler](https://defuse.ca/online-x86-assembler.htm) | An online disassembler and assembler for x86 and x64 |
| [Online Disassembler](https://onlinedisassembler.com/odaweb/) | An online disassembler for multiple architectures |
| [godbolt compiler explorer](https://godbolt.org/) | See how code compiles using different compilers |
| [CyberChef](https://gchq.github.io/CyberChef/) | A multi-tool for working with different types of data. Webapp. |
| [binref](https://github.com/binref/refinery) | Tool for transforming various types of data on the command line |
| [hexiply](https://remyhax.xyz/tools/hexiply/) | Search for hex constants in various places online |

## Obfuscation and compression

| Software | File Type | Description |
|----------|-----------|-------------|
| [UPX](https://upx.github.io/) | Multi | Pack binaries, useful for golfing |
| [aaencode/aadecode](https://jamtg.github.io/aaencode-and-aadecode/) | Javascript | Javascript obfuscator using text emoticons |
| [jsfuck](http://www.jsfuck.com/) | Javascript | You can execute any javascript by only using 6 characters, this will build and decode jsfuck blobs for you |
| [davinci](https://github.com/elfmaster/davinci) | ELF | An ELF protector |
| [BackdoorFactory](https://github.com/secretsquirrel/the-backdoor-factory) | PE, ELF, Mach-O | Patch binaries with shellcode |

## File Resources

- https://github.com/corkami/pics - Resources for various file formats
- http://fileformats.archiveteam.org/wiki/Main_Page - File formats wiki
- https://wiki.multimedia.cx/index.php/Main_Page - Multimedia Wiki, Audio/Video/Container Formats
- https://github.com/corkami/formats - Several documented formats with notes
- https://formats.kaitai.io/ - Kaitai File Format Diagrams
- https://www.symbolcrash.com/doc/ - Many different file specs
- https://github.com/tmpout/awesome-elf - ELF Resources
- https://forensicswiki.xyz/ - ForensicsWiki - Has a lot of info on different files

## Further Reading

- https://youtu.be/VVdmmN0su6E What is a File Format? - LiveOverflow
- https://youtu.be/hdCs6bPM4is Funky File Formats - Ange Albertini
- https://youtu.be/VLmrsfSE-tA Adventures in Binary Golf - netspooky
- https://www.alchemistowl.org/pocorgtfo/pocorgtfo07.pdf PoC||GTFO 7:6 (pg. 18) Abusing file formats; or, Corkami, the Novella - Ange Albertini

## Lists of Tools

There are too many individual tools to name, here are some that are in the Black Arch Linux repos

- https://blackarch.org/forensic.html - Black Arch forensics tools list
- https://blackarch.org/binary.html - Black Arch binary tools list

## Generators

These generate tiny files of various types.

- https://github.com/corkami/mitra Polyglot Generator
- https://justine.lol/ape.html - Actually Portable Executable. File that runs on Mac, Windows and Linux
- https://forum.spacehey.com/topic?id=89320 - Python3.7+ Multi-arch .pyc shellcode dropper
- https://github.com/netspooky/kimagure) - TinyPE generator with nasm templates

## File Corpus

These are collections of files for inspiration and testing

- https://github.com/corkami/pocs - Many interesting file PoCs
- https://github.com/netspooky/BGGP/ - Git repo of past entries for BGGP
- https://github.com/tmpout/elfs - Various ELF files
- https://github.com/mathiasbynens/small - Smallest possible syntactically valid files of different types
- https://github.com/JonathanSalwan/binary-samples/ - A collection of binary file examples
- https://github.com/radareorg/radare2-testbins - Examples of different binary formats used to test radare2
- https://github.com/rizinorg/rizin-testbins - Examples of different binary formats used to test radare2
- https://github.com/Polydet/polyglot-database Polyglot file PoCs
- https://github.com/netspooky/golfclub - Collection of source code for golfed files
- https://github.com/rcx/tinyPE - A collection of TinyPE Experiments
