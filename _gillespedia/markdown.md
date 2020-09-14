---
title: Markdown
excerpt: A portable shorthand for text styling.
date: "2020-09-13"
categories:
- "techology"
header:
   teaser: https://lh3.googleusercontent.com/pw/ACtC-3evmk2lAqS1UmvcOfWgjCdlJrkVPCL0sh4JVY4x4nf6-8kBqgKy2LEQF-98RgZflgYrf5KR5ap5i7MJE0b1IoCWgjfiLOj_7arm-cv79EN-PW6PcBAKopwnUV1w2sdDhF-4Nqkz9_AI2nB7bg2-eRk03g=w250
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
This text is written in *Markdown*. Even if it's not 
properly formatted you can **still** read it pretty 
easily. 
Even links are pretty simple. Read more [here](https://www.markdownguide.org)
```

Compare that to html...
```
<p>This text is written in <i>HTML</i>. If it's not
properly formatted it is <b>not as easy</b> to read.</p>
<p>An easy example to see is with hyperlinks, they are much
harder to read in HTML than they are in  
<a href="http://www.markdownguide.org>Markdown</a></p>
```

# Where can you use it?

The beauty of Markdown is that it *can* be used **anywhere**. You can open notepad on your Windows computer and type out a note using Markdown syntax. You'll be able to read it easily as you're writing it. Markdown files typically end with ".md" (as opposed to ".txt"), but really it doesn't matter what your file extension is. You can copy and paste Markdown text into these platforms (and 1000s more, I'm sure):

- Reddit
- GitHub
- Notion
- Dropbox Paper
- Bear
- Roam
- Obsidian
- Most coding README files

All these services (and hundreds more) will turn '\**this\**' into '**this**'.

# How do you Markdown?

## The 80% of Stuff You'll Use Often

### Basic Styling

The whole idea of Markdown is that you're not taking your hands off the keyboard.

Italic - surround the text to be italicized with single asterisks.

~~~
This text is not italic, other than *these two* words.
~~~

Bold - surround the text to be bolded with double asterisks.

~~~
You can write like **this** if you're feeling **particularly bold**.
~~~

Block quote - start each line to included in the block quote with a greater-than sign. If you don't know what a block quote is...

> A **Block Quote** looks like this.

~~~
I heard this awesome tip:
> Block quotes are a good way to make something stand out.
~~~

Unordered List - start each line to be included in the unordered list with a hyphen (or asterisk), then a space.

~~~
Things Dwight enjoys:
- Bears
- Beats
- Battlestar Gallactica
~~~

Ordered Lists - start each line to be included in the ordered list with a number... weirdly you can use *any* number, and it will automatically render with proper order.

~~~
Steps for making a sandwich:
1. Get bread
2. Get ingredients
3. Text your mom for help
~~~

### Other Things

Hyperlinks - in order to link text, put the text you want to display inside square brackets, and follow them with the hyperlink in parenthesis.

~~~
This is a [pretty okay website I guess](https://aarongilly.com)
~~~

Inline images - not *every* place you can use markdown will support inline images, but those that do will use the same syntax as hyperlinks, but with an exclamation point in front.

~~~
This is a picture of a dog:
![this text will load if the link is broken](https://images.unsplash.com/photo-1561037404-61cd46aa615b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2700&q=80)
~~~

To do lists - this is also not accepted *everywhere*, but places like GitHub and Notion will recognize any line starting with an open and close square bracket as to-do items.

~~~
[] this is an incomplete task
[x] this is a completed task
~~~

## The 20% of Stuff You Won't

### Tables

These are the biggest pain in the neck for markdown. There's simply no way to manually type a table that looks good to people reading plaintext. There are various methods of making table in Markdown - but none of them are all that satisfing.

### Text coloring

Native markdown has no support for text color changing.

### Underlining

Weirdly there is no support for underlining in the standard Markdown syntax. I suspect it's because the syntax was written with the expectation that underlined text would be resereved for links. Frankly I'm okay without underlined text. It's my least favorite *attention* **grabbing** stylization.

# Other Resources
- [The Official Markdown Guide](https://www.markdownguide.org)