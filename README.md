# June 2019 CCEM Summer School Presentation

This repository contains the files for a [reveal.js](https://github.com/hakimel/reveal.js/) presentation
that was given at the 2019 CCEM Summer Electron Microscopy School at McMaster University in Hamilton, ON.

## Creating the presentation

The files to build the presentation are in the [reveal_md_presentation](./reveal_md_presentation) directory.
To use them, one will need to install the `reveal_md` tool. First, install [Node.js](https://nodejs.org/en/),
and then run the command:

```bash
npm install -g reveal-md
```

Once this is installed, navigate to the `reveal_md_presentation` directory, and run the following command
to serve the presentation from a local HTML server:

```bash
reveal-md presentation.md -w
```

The `-w` flag means the server will watch for any files that change on disk, and rebuild the presentation
as necessary (useful when writing the presentation to see how everything looks).

## Saving to PDF

There is a functionality within `reveal-md` to save directly to PDF, but it appears (in my trials) to be broken.
To save to PDF, install the `decktape` package:

```bash
npm install -g decktape
```

And then (with the presentation server running in another terminal) run:

```bash
 decktape reveal http://localhost:1948/presentation.md slides.pdf --chrome-arg=--no-sandbox --chrome-arg=--allow-file-access-from-files
```

This seems to do a pretty good job of rendering the presentation appropriately.
