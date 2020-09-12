---
title: "Markdown"
excerpt: "A portable shorthand for text styling."
header:
   teaser: "..."
mathjax: true
---

# What is Markdown

Markdown is a text-based text styling language. In layman's terms, it is a couple of additional characters you put in your writing that the computer uses to change how it looks. It allows you to do things like **bold** and *italicize* your text without taking your hands off the keyboard. 

## Some History

Markdown was first codified into a standard in 2006 by a guy named John Gruber, whom I know nothing about, in collaboration with a guy named Aaron Swartz, whom I know enough about to say he died way too early and contributed more to the world of technology than I'll ever accomplish.

## A Brief Aside on Text Styling

Rest assured, dear reader, I'm certain this does not apply to you. I wanted to state that up front.

Why does nobody use text styles? I have worked with multiple dozens of people in the context of Word and Google Docs, and almost *never* does anyone utilize proper "styling" options. Everybody who wants to create a new paragraph hits Enter twice. Everybody who wants a new header just makes the font bigger. The worst is when people who want a new page just enter a ton of blank lines until they get down to the next page. There are proper solutions for **all** of these situations, and they scale much more nicely.

Aside over. Back to Markdown.

# Why is it Popular?

Turns out people are both lazy and expressive. We want the ability to write with *some* level of naunce, but developers don't necessarily want to go through the trouble of building full richtext editors, complete with buttons and menus that allow you to make things **bold** or make hyperlinks. Also such richtext editors expand the size of a webpage that your computer needs to download, interpret, and display. Even if the size is miniscule, there's no reason to take that hit when you've got an easy option that more and more people are learning.

More than that, Markdown serves a purpose of creating a simple text formatting language that can be interpreted by a large number of clients in different environments. If you export your MicroSoft Word files and then try to open them with other applications, you'll find that there aren't a *ton* of available options for you. Moreover, all the available options will come with some sort of interpretation errors.  The core Markdown syntax notation is entirely portable, meaning you can copy your stylized text from one place and put it in another, and it will *probably* look like what you'd expect. Better yet, Markdown was designed to be human-readable. So, even if you look at **plain text Markdown** you'll not only be able to *read* it, you'll probably be able to read it almost as effectively as you would if it were stylized.

```
Markdown block of stylized text
```

Compare that to html...
```
same block, but html
```

# Where can you use it?

The beauty of Markdown is that it *can* be used **anywhere**. You can open notepad on your Windows computer and type out a note using Markdown syntax. You'll be able to read it easily as you're writing it. Markdown files typically end with ".md" (as opposed to ".txt"), but really it doesn't matter what your file extension is. You can copy and paste Markdown text into these platforms (and 1000s more, I'm sure):

- Reddit
- GitHub
- Notion
- Dropbox Paper
- Bear
- 

# How do you Markdown?

## The 80% of Stuff You'll Use Often

### Basic Styling

Bold

Italic

Quote

Unordered List

Ordered Lists

### Other Things

Hyperlinks

Inline images

To do lists

## The 20% of Stuff You Won't

### Tables

These are the biggest pain in the neck for markdown. There's simply no way to manually type a table that looks good to people reading plaintext. There are various methods of making table in Markdown - but none of them are all that satisfing.

### Text coloring

Native markdown has no support for text color changing.

### Underlining

Weirdly there is no support for underlining in the standard Markdown syntax. I suspect it's because the syntax was written with the expectation that underlined text would be resereved for links. Frankly I'm okay without underlined text. It's my least favorite *attention* **grabbing** stylization.