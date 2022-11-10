# Polyglot Lab

In this lab we are going to make a polyglot file. A polyglot file is any file that can be interpreted as multiple file formats at the same time.

## Build the flyer

The flyer for this workshop is an xx file that builds a small png of the same image as our NetPBM file.
All of the components of the PNG are described in the flyer which you can play around with. flyer-plain.xx is a simplified version without ANSI colors to make it easier to work with.

Build the PNG:

```
xx flyer.xx -o flyer.png
```

## Planning A Polyglot

Now we want to make a polyglot file. This is a file that valid in multiple formats at the same time. How do you do that?

HTML is one of the hardiest markup languages, allowing arbitrary binary data at different parts of a file. Most browsers will render the most cursed HTML to the best of it's ability. HTML also has a key feature which is very valuable to the polyglotier: it doesn't need to start at the first byte.

This means that HTML will render if it occurs within a given buffer of data. This feature is commonly abused in what is known as [XSS](https://www.youtube.com/watch?v=mKAWpFdVcPY), or Cross Site Scripting. Inputs containing HTML and anything that is renderable within HTML can be given to a website which can then render that within it's context.

> 👻 Spooky Fact: This is also abusable within the related XML mark up language, through what is known as XXE, or [XML External Entity attacks](https://en.wikipedia.org/wiki/XML_external_entity_attack).

## HTML

Let's use a simple HTML page to test. This is `base.html` in the files/ directory.

```html
<html>
<body>
<img src="./polyglot.html">
</body>
</html><!--
```

Make a copy of flyer.png and call it polygot.png.

```
cp flyer.png polyglot.png
```

Then append base.html to the end of polyglot.png and make a copy of it called polyglot.html
```
cat base.html >> polyglot.png
cp polyglot.png polyglot.html
```

Open `polyglot.html` in your browser. You can see some of the strings from the PNG, followed by a bunch of junk characters, and then at the very end, is our PNG. This means that the browser is currently reading the file in two different ways.

At the end of the HTML there is an open comment `<!--`. In HTML, comments are enclosed `<!-- like this -->`. Without a trailing `-->`, the rest of the data is treated as a comment. It should cover up any data after this point unless the sequence `-->` appears.

Now what can we put after here?

## PDF

> A lot of amazing research of the format was done by Ange Albertini. Check out his PDF tricks page [here](https://github.com/corkami/docs/blob/master/PDF/PDF.md), and also check out any PDF from [PoC||GTFO](https://www.alchemistowl.org/pocorgtfo/) for some absolutely mental file trickery.

PDFs are another well loved format for making polyglot files. Like HTML, they don't have to start at the start of the buffer, but there are limitations which can vary between PDF readers.

Let's use the PDF we already made for this. Append it to the end of polyglot.html and name it polyglot.pdf. Update our png as well.

```
cat hi.pdf >> polyglot.zip
cp polyglot.html polyglot.pdf
cp polyglot.html polyglot.png
```

Then open `polyglot.pdf` in the browser. You should be able to see your alert pop up.

## Zip

NetPBM can't be used in this polyglot because the magic value needs to be at the first byte of the file, which is already taken up by a PNG. That doesn't mean we can't include it!

Zip files are extremely versatile for polyglots and golfing. While HTML and PDF are technically "text" based, zip files are intended to be a purely binary format. Unlike most binary formats, zip files can contain chunks with the same magic value `"PK" 03 04` multiple times. The file signature could possibly appear anywhere and still be valid. This trick has been used to transfer files covertly using seemingly benign files as a host.

We will use 7z to make a zip for us. Install `p7zip-full` on Linux/WSL, or `p7zip` on brew for Mac.

Let's create a small zip file containing our NetPBM file:
```
7z a secret.zip mametchi.pbm
```

Now append it to the end of our polyglot and update our other files.
```
cat secret.zip >> polyglot.pdf
cp polyglot.pdf polyglot.zip
cp polyglot.pdf polyglot.png
cp polyglot.pdf polyglot.html
```

You may have a different version of 7z, but the file hash for the version I built was `7ab8f9dbf0517e38b0c4f820ee7dc3ff8b0db7743b853181aca4efbba8909ff8`.

Let's try to open it with `7z`:
```
7z x polyglot.zip
```

You will probably get the error "Is not archive". It can't open it as a "zip" archive because it's in the wrong format. Some zip utilities will be more strict or more lenient with where the file signature is allowed to start if it has the extension "zip". What happens if you try to unzip `polyglot.png`?

```
7z x polyglot.png
```

Success! It unziped `mametchi.pbm`! This happens because 7zip is more permissive with non `.zip` files, and will read deeper into the file. 

> 👻 Spooky Fact: A lot of files are actually just zip files or contain unzippable elements. Try unzipping a .jar, .docx, .exe, then try other random files.

## Going further

Now we've made a 4 file polyglot containing a PNG, a web page, a PDF, and a zip file containing yet another file, our NetPBM image. The file is less 1000 bytes! A word document with nothing in it is 4K. We still have a lot more room for other files.

Some questions you can answer:
- What other files can you fit in here?
- Can you fit other files if you rearrange the order of the files appended?
- Can you render the PDF in the web page too?
- What happens when you upload to social media, text it, send it via email? Does it work? Can you download it and check if it's still usable in all the formats?
- What happens when there's no file extension? How do other software and websites handle it?

## Real World Example: Universal Binaries

Mac OS has a file format called the [Universal Binary](https://en.wikipedia.org/wiki/Universal_binary) which can have code for multiple CPU architectures inside of them. These are useful because they take an existing file format, and extend it to ensure backwards compatibility with other systems. 

More Info: https://www.symbolcrash.com/2019/02/26/mach-o-universal-fat-binaries/

A similar portability issue was addressed by the [Actually Portable Executable](https://justine.lol/ape.html), which is a type of polyglot file which runs on Linux, Mac, and Windows without any changes to the file.

Prev: [LAB02 - NetPBM](06_lab_netpbm.md) | Next: [LAB04 - Golf](08_lab_golf.md)
