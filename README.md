# markdown-thesis

This is the project folder for my Media Arts & Technology Masters Document. I put in a considerable amount of work to set this up, so I figured I would upload it in case it might save someone else some time.

## If you want to do any of the following, feel free to use this project as a starting point:
- Write your thesis or dissertation in markdown without formatting distractions
- Generate the document with all the formatting done for you
- Automatically generate a table of contents form the document contents
- Automatically generate a bibliography from a .bib file

## Requirements:
There are two command line tools you'll need for this to work: `pandoc` and `pdftk`. I've only tried this on Linux (Debian), but it should be doable on Windos or MacOS too.

On Linux, get `pandoc` and `pdftk` through your package manager.

On MacOS, you can probably get these packages through homebrew (i.e. `brew install pandoc pdftk` in terminal).

## Organization:
Text content goes in markdown files in markdown folder. I did each chapter as a separate markdown file, but this is optional. The bib.md file is necessary for compiling the document, but you don't need to add anything to it.

Figures go in the figures folder. Look in my markdown files to see how I reference them.

Formatting stuff goes in "default.yaml". 

"ieee.csl" is the style sheet the determines for example the way citations are formatted.

All references go in a file called "references.bib". I used zotero to generate this automatically.

The front matter (everything before the table of contents) had to be done in another text editor, I couldn't find a satisfactory way to do so in markdown. I exported the front matter to a pdf on its own.

generate_pdf is the script to run in order to, you guessed it, generate the pdf. It first uses pandoc to generate a pdf called "content.pdf" from all the markdown files, then adds the front matter with pdftk.
