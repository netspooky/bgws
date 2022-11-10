# Fundamentals

Now that we have the background out of the way, let's talk about some of the fundamental concepts about computers that will aid you in your journey.

## Data Types and Data Structures

All computer data is just a long string of 1's and 0's. In the early days, each computer system had it's own data sizes and methods of ordering data. A turning point for data sizes came with the need for communication between computer systems, and 8 bit [bytes](https://en.wikipedia.org/wiki/Byte) became a standard for both communications protocols, and microprocessors.

### Data Types 

Building off of the 8 bit byte, we have the concept of _data types_. These are a core abstraction of computer programming, and are used to assign special properties to groups of one or more bytes.

A very common set of established data types are the ones used in [C](https://en.wikipedia.org/wiki/C_data_types). There are other names for the data types used by other languages and systems, but they all mean relatively similar things.

Common names and sizes of data types:

| Size | Name |
|------|------|
| 1 byte | char, u8, i8, BYTE |
| 2 bytes | short, u16, i16 WORD |
| 4 bytes | int, u32, DWORD |
| 8 bytes | long, u64, QWORD |

There is also the concept of signed versus unsigned, which just means that the top bit is used to track whether the number is positive or negative. You may see the key words `unsigned` and `signed` before a data type. The shorthand `u` and `i` are also used, eg: `u8` is an unsigned 8 bit number and `i8` is a signed 8 bit number. When the sign bit is set, it reduces the amount of positive numbers that can be reprsented by a power of two, and enabled an equal range of negative bits to be represented.

Check out [this video](https://www.youtube.com/watch?v=vA0Rl6Ne5C8) about how the music video for Gangnam Style overflowed the view counter on YouTube resulting in a negative view count.

> 👻  Spooky Fact: Despite our best efforts at standardization, there can be surprising differences depending on the language and the architecture you're working with. Keep this in mind, especially when working with old or obscure systems and formats!

### Data Structures

Data structures are ordered collections of data types. They can be things like arrays, which typically are a list of values of the same type, or more complex structures with different types.

When reading a structure in a given language, you can get a clear picture of what the program expects when parsing things like files and packets.

This is an example of an [ARP](https://en.wikipedia.org/wiki/Address_Resolution_Protocol) packet struct, written in C, taken from [here](https://www.pdbuchan.com/rawsock/arp.c). This is a message that your computer sends out when it wants to learn what IP address belongs to what computer on your network. You can see what this program expects when parsing a packet:

```c
// Define a struct for ARP header
typedef struct _arp_hdr arp_hdr;
struct _arp_hdr {
  uint16_t htype;
  uint16_t ptype;
  uint8_t hlen;
  uint8_t plen;
  uint16_t opcode;
  uint8_t sender_mac[6];
  uint8_t sender_ip[4];
  uint8_t target_mac[6];
  uint8_t target_ip[4];
};
```

Now we can compare this to what we see when the packet is sent. The ethernet layer isn't described here in the `_arp_hdr` struct, so start from the bottom and work your way up to the top.

![image](https://user-images.githubusercontent.com/26436276/201170741-6d883d48-7bc1-43fc-864d-9096962ad07a.png)

The `uint8_t`  and `uint16_t` data types show what we would expect, 1 and 2 byte data fields.

## Bit fields

![image](https://user-images.githubusercontent.com/26436276/201193088-ef02202d-afd4-4061-81a4-723daebdb221.png)

_Example of bit fields in a single byte_

Bit fields are just individual or groups of bits that represent data in sizes other than a byte. Bitfields tend to work within the bounds of an established data type and size, meaning that a single 8 bit byte can represent up to 8 distinct bit fields.

The elements of a bitfield are usually accessed by doing logical operations such as AND and OR. When you want to get bits, you use AND. When you want to set bits, you use OR.

![image](https://user-images.githubusercontent.com/26436276/201192643-f9f471de-7fb1-4436-b6cf-78ed672bb770.png)

## Endianness

[Endianness](https://en.wikipedia.org/wiki/Endianness) refers to the order of the bytes in a given value.  Let's say we have the hex value 0x12345678, here is how it would be represented in each endianness.

```
12 34 56 78 <-- Big Endian
12 34 56 78 <-- "Network Order" - Seen often in protocol descriptions.
78 56 34 12 <-- Little Endian
```

## Architecture differences

Different CPUs have different data sizes and byte orders. File formats and protocols often reflect these specifics. Many formats were designed for one system 

An example is [octal](https://en.wikipedia.org/wiki/Octal) still being used on Linux for things like file permissions. This is an old pattern from Unix and early mainframes and microcomputers, many of which had processing units with data sizes that were divisible by 3. Three binary digits can represent a maximum of 8 values.

## Bit Order

This is the binary representation of the number 3.
```
       ┌─ Names: Least Significant Bit (LSB). Bit 0. Low Bit. Bottom Bit.
00000011
└─ Most Significant Bit (MSB). Bit 7. High Bit. Top Bit.
```
This is a very common way of referencing bits, and when there are differences for architectural reasons, they are noted in datasheets and specifications.

- https://en.wikipedia.org/wiki/Bit_numbering

## Magic Numbers and File Signatures

[Magic numbers](https://en.wikipedia.org/wiki/Magic_number_(programming)) are values that are used to denote the start or end of a sequence of data. They are often used in file formats and protocols to signal where to start parsing the data. These are also known as "[file signatures](https://en.wikipedia.org/wiki/List_of_file_signatures)" which are used to detect the presence of a file. 

This is how `file` and `binwalk` work, by searching for file signatures or magic values and determining whether or not a specific file type is detected. Sometimes the magic number actually indicates how to parse a file. An example is a PCAP file. The first four bytes tell you whether the file is using big or little endian format for numbers.

![image](https://user-images.githubusercontent.com/26436276/201224213-ac03bcf7-3491-4973-9ba6-95570da5ccbf.png)

## TLV

[TLV](https://en.wikipedia.org/wiki/Type%E2%80%93length%E2%80%93value) also known as Tag-Length-Value or Type-Length-Value, is a common pattern that you may see in file formats. This just means that the individual units of data will describe themselves.

Let's say we have a data stream with two types, binary data, and ASCII data. We can give the binary data the tag `01`, and ASCII data the tag `02`. If we wanted to encode the message "hey!", we would do it like this

```
02 -- Tag: ASCII Text
04 -- Length: 4
68 65 79 21 -- Value: "hey!" in hex
```

If we wanted to encode the number 0x1234, we would do it like this:

```
01 -- Tag: Binary Data
02 -- Length: 2
12 34 -- Value: 0x1234
```

This is very common in both protocols and file formats.

## Encodings

Data is encoded when pieces of data are mapped to agreed upon points. The characters in this sentence are still just numbers under the hood, but the text encoding used assigns these numbers to letters that we recognize.

### Text encodings

![image](https://user-images.githubusercontent.com/26436276/201173992-0dc7e63e-7f5e-47f2-9e27-358fe4766e98.png)

Image Source: https://jbwyatt.com/I/asciiGood.gif

- [ASCII](https://en.wikipedia.org/wiki/ASCII)
- [UTF-8](https://en.wikipedia.org/wiki/UTF-8)
- [UTF-16](https://en.wikipedia.org/wiki/UTF-16)
- https://en.wikipedia.org/wiki/Character_encoding

Other ones you might run into:

- [Shift-JIS](https://en.wikipedia.org/wiki/Shift_JIS) - old Japanese encoding that appears in video game roms
- [CP-437](https://en.wikipedia.org/wiki/Code_page_437) - this is an old spec that you may see in text files

> 👻  Spooky Tip: you can use Sublime text and many other editors to change between text encodings

### Data encodings

- [Base64](https://en.wikipedia.org/wiki/Base64)
    - [Base64url](https://datatracker.ietf.org/doc/html/rfc4648#section-5)
- [Base32](https://en.wikipedia.org/wiki/Base32)
- [Ascii85](https://en.wikipedia.org/wiki/Ascii85) - seen in PDFs

## No implementation is perfect

Software is written by humans, there can be mistakes.

---

Prev: [Background](01_background.md) | Next: [Some theory](03_theory.md)

