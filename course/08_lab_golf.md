
# LAB: Golfing

Now that we've made a small polyglot file, let's focus on golfing. To golf this file, we can take what we know about the files we use, and combine it with experimentation.

Reading the specs of each format is good, but that's a lot of info. The best way to get acquainted with not only the file format, but the implementation of the file parsing logic in whatever software you use to read it. A lot of software uses it's own custom file parser, and may or may not allow certain features based on what it intends to do with the file. 

There are three key factors at play for a given file parser:
- The intent of the file format creators
- The intent of the software developers using the format
- The reality of the software implementation

Some file formats will not have specific things defined. Some are intended to be used by people who want to add extensions to the format. Others aren't defined because they expect things to exist within certain bounds, to be enforced via software. These are often good places to look at when thinking of potential optimizations.


## Golfing HTML

HTML is extremely lax, and there are many ways to remove bytes in our file.

Here are a few we can start with:

| Optimization | Note |
|--------------|------|
| Make the filename smaller | Rename the file to p.html and update the img src tag. |
| Remove new lines | All of the HTML can be on one line|
| Get rid of tags after the img src tag, keep the comment | The HTML document technically doesn't need to close out those tags, technically. |

## Golfing PDF

PDF can be very tricky when you start messing with the core elements of the format. These are some known optimizations for this file.

| Optimization | Note |
|--------------|------|
| Remove the ; at the end of `app.alert()` | Javascript is also quite versatile. |
| Remove the "0 0 3 3" in MediaBox | This is the dimensions of the page that gets rendered, but removing them gives us the default page size |
| Remove the brackets in MediaBox | While we are at it, we don't need those brackets at all, can instead just use the tag |
| Version number can be "1." instead of "1.0" | A byte saved is a byte earned. |
| Remove unnecessary spaces | There's a few of these |

## More Golfing

There are more possible opportunities to shave off some bytes. Take some time to explore.

It may be helpful to convert this buffer into an xx file or opening it in a hex editor. These files are editable in vim and other text editors, but there can be strange results when modifying a binary file.

You can use yxd to convert your binary file into an xx file:
```
yxd -f polyglot.png --xx
```

Prev: [LAB03 - Polyglot](07_lab_polyglot.md) | Next: [Final Thoughts](09_final_thoughts.md)
