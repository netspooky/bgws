# Final Thoughts

We've done a lot in this workshop! Now we know how to:

- Build files from scratch
- Combine files into polyglots
- Identify ways to reduce our files sizes

There's a few things to mention before wrapping up.

## Picking A Target

You may be itching to pick a file format to go and play with now! The question is, which one? There are a lot of file formats, how do you choose good ones to research?

It really depends on your goal.
- Do you want to just make something small?
- Do you want to obfuscate and make it hard to parse?
- Do you need to fit it into a specific size?

Text formats are usually fun to start with, such as the HTML and PDF we covered in the labs. Scripting languages are also fun to play with, and can be surprisingly versatile.

When picking a format, investigate whether or not the magic value has to be at the first byte, or if you can start it anywhere. Next check if there are pointers to other parts of the file, which may allow you to put data after the header or in between chunks. 

Each implementation of a file format parser is different. Some may be more lenient, while others more strict. Once you start digging into your format, test different software that can handle the file format and see what happens!

Map out your file on paper or in a text file, and mark places where you think you might be able to insert your own data, then experiment. You can use xx or yxd's `--py` output option to create easy to manipulate binary data streams.

## Fuzzing

Fuzzing is a very fun way to find small, valid inputs to a program, as well as inputs that make a program crash. 

See the [BGGP3](https://tmpout.sh/bggp/3/) info page for a guide on how to set up and use [honggfuzz](https://github.com/google/honggfuzz). Honggfuzz is one of the easiest fuzzers to get started with, and can be helpful to find small files that crash a program. You can investigate these crashes to see what the limitations of the parser are.

Fuzzing may not always be your best approach, and sometimes you will need to investigate potential optimizations by hand. Check out [ELF Binary Mangling Pt. 4](https://tmpout.sh/2/11.html) for a detailed look into this process.

## Binary Golf Grand Prix

Binary Golf Grand Prix is a yearly competition that challenges people to create the smallest files that do _something_. You can check out the [BGGP repo](https://github.com/netspooky/bggp) containing all of the entries, scores, and writeups from over the years.

Each year has a theme:
    
- BGGP1 (2020) - Palindrome
- BGGP2 (2021) - Polyglot
- BGGP3 (2022) - Crash
- BGGP4 (2023) - ????

Hope to see you next year!

---

Prev: [LAB04 - Golf](08_lab_golf.md)
