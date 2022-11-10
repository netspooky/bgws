# LAB01 - PDF

For our first lab, we will start with a simple example of a file. [PDF](https://en.wikipedia.org/wiki/PDF)s are as ubiquitous as they are mysterious. At their core, PDFs are just text files that can also contain binary data.

Let's play around with this format a bit with a very small PDF that pop's up an alert box that reads "hi!" when put into a browser.

```
%PDF-1.0
1 0 obj<</Pages 2 0 R /Names 4 0 R>>endobj
2 0 obj<</Kids [3 0 R]/Count 1>>endobj
3 0 obj<</MediaBox [0 0 3 3]>>endobj
4 0 obj<</JavaScript 5 0 R>>endobj
5 0 obj<</Names [(b) 6 0 R]>>endobj
6 0 obj<</JS (app.alert("hi!");) /S /JavaScript>>endobj
trailer<</Root 1 0 R>>
```

Check out this [minimal PDF](https://brendanzagaeski.appspot.com/0004.html) as well.

What can you make these files do? Can you add or take away features? How does your PDF reader feel about that?

Links:
- https://stackoverflow.com/questions/17279712/what-is-the-smallest-possible-valid-pdf - Many good examples of small PDFs
- https://github.com/corkami/docs/blob/master/PDF/PDF.md - List of PDF Tricks 
- https://resources.infosecinstitute.com/topic/pdf-file-format-basic-structure/ - General Info

---

Prev: [Tools](04_tools.md) | Next: [LAB02 - NetPBM](06_lab_netpbm.md)
