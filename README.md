# Vymad

Vymad converts MindMap to Markdown - nice to use with Pandoc !

See it in action:

https://www.youtube.com/watch?v=PruTOzDX3fs

Vymad was originally a "markdown generator" from "vym" file format. It is now able to use Freemind and Xmind format.

[Vym](http://www.insilmaril.de/vym/) (View Your Mind) is a very nice Mindmapping software for \*Nix environments. Writing a book, I was searching a way to easilly write content in Vym and to generate something that can be used by [Pandoc](http://pandoc.org/).

I decided to build my own in Go and to share this little tool to make your life easier :)

**Note:** Freemind uses HTML to keep notes and I didn't find any solution to get plain text. You **must** have pandoc installed to let vymad tries to convert HTML to Markdown. Vym and Xmind are able to let notes to be "plain text" (especially Xmind which lets 2 blocks to get HTML and Plain text)

# Installation

## With Go

If you've got "golang" (go) on you computer, you may use:

```
go get -u github.com/metal3d/vymad
```

## Test

Test if you correctly installed "vymad" by typing this in a terminal:

```
vymad -version
```

If no version appears or if you have an error, please check how you've installed vymad.

# Usage

Simply pass a vym file as argument:

```
vymad myfile.vym
```

If the given file is a correct vym file, so the markdown content will be displayed.

Note that vymad will never write something on the given file.

To keep the output in a new file, simply use shell redirection:

```
vymad myfile.vym > myfile.md
```

You may use specific shell syntax to build pdf or other format on-the-fly:

```
# With bash, sh, or zsh
pandoc --toc --chapter <(vymad myfile.vym) -o book.pdf

# With fish
pandoc --toc --chapter (vymad myfile.vym | psub) -o book.pdf

# generic and universal AFAIK
vymad myfile.vym | pandoc --toc --chapter -o book.pdf

```

# Notes about -richtext option

The `-richtext` option is **experimental** - It may try to parse the "notes" from you minmap as HTML. To use this option, you **must** have installed "pandoc".

Vymad will try to make some modification (in memory) to make notes parsables, then it will use pandoc to convert HTML to Markdown. At this time, there are a lot of problems:

- some styles are not correctly detected
- images are not extracted