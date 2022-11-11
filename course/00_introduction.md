# Introduction

Welcome to the Binary Golf Workshop! This workshop will give you the rundown on the theory and practice of binary golf in a series of short guides and labs.

All that you will need follow along is a \*nix based shell and a text editor.

- Linux - bash
- Mac - zsh/bash
- Windows - Install wsl
- Or you can ssh into a VPS or a computer like a raspberry pi or an Android phone

We will also be using [xx](https://github.com/netspooky/xx), a file format created to aid in file format hacking. There are no special dependencies, so all you need to do is clone the repo!

```
git clone https://github.com/netspooky/xx
```

In lieu of installing, you can also add this line to your `~/.bashrc` file. Just change the path to xx.py.

```
alias xx="python3 /path/to/xx/xx.py"
```

## Contents

This is an outline of contents for this course

- [Introduction](00_introduction.md)
- [Background](01_background.md)
- [Fundamentals](02_fundamentals.md)
- [Theory](03_theory.md)
- [Tools](04_tools.md)
  - [Assemblers](../reference/info_assemblers.md)
  - [Hex Editors](../reference/info_hexeditors.md)
  - [xx](../reference/info_xx.md)
  - [File Hacking Tools](../reference/info_tools.md)
- [Lab: PDF](05_lab_pdf.md)
- [Lab: NetPBM](06_lab_netpbm.md)
- [Lab: Polyglot](07_lab_polyglot.md)
- [Lab: Golf](08_lab_golf.md)
- [Final Thoughts](09_final_thoughts.md)

Repo Layout
- files/ - contains files for the labs
- reference/ - Contains reference material
- course/ - This contains the course materials

## About The Author

netspooky is a reverse engineer and hardware vulnerability researcher at $company. His specialties include network protocols, file formats, and embedded devices. He is the founder of the annual Binary Golf Grand Prix, a co-founder and editor of the Linux virus zine "tmp.0ut" and has been published in PoC||GTFO, VX-Underground, and other security focused works. He is the creator of tools such as inhale, pdiff, and the xx file format.


