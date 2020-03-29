# This page is a module template reference page.

# Tags & formatting
[Minimal Mistakes Reference](https://mmistakes.github.io/minimal-mistakes/markup/markup-html-tags-and-formatting/)
[MM Raw](https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/docs/_posts/2013-01-11-markup-html-tags-and-formatting.md)
[Full Reference](https://kramdown.gettalong.org/quickref.html#inline-attributes)

## Quotes

> People think focus means saying yes to the thing you've got to focus on. But that's not what it means at all. It means saying no to the hundred other good ideas that there are. You have to pick carefully. I'm actually as proud of the things we haven't done as the things I have done. Innovation is saying no to 1,000 things.

<cite>Steve Jobs</cite> --- Apple Worldwide Developers' Conference, 1997
{: .small}

## Preformatted Bits
```html
<a href="#" class="btn--success">Success Button</a>
```

or 

```markdown
[Default Button Text](#link){: .btn}
[Primary Button Text](#link){: .btn .btn--primary}
[Success Button Text](#link){: .btn .btn--success}
[Warning Button Text](#link){: .btn .btn--warning}
[Danger Button Text](#link){: .btn .btn--danger}
[Info Button Text](#link){: .btn .btn--info}
[Inverse Button](#link){: .btn .btn--inverse}
[Light Outline Button](#link){: .btn .btn--light-outline}
```

## Tables
[Helpful generator](https://www.tablesgenerator.com/markdown_tables)

| Employee         | Salary |                                                              |
| --------         | ------ | ------------------------------------------------------------ |
| [John Doe](#)    | $1     | Because that's all Steve Jobs needed for a salary.           |
| [Jane Doe](#)    | $100K  | For all the blogging she does.                               |
| [Fred Bloggs](#) | $100M  | Pictures are worth a thousand words, right? So Jane × 1,000. |
| [Jane Bloggs](#) | $100B  | With hair like that?! Enough said.                           |

## Callouts

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice}` class.
{: .notice}

**GREY** This paragraph of text has been [emphasized](#) with the `{: .notice--primary}` class.
{: .notice--primary}

**BLUE** This paragraph of text has been [emphasized](#) with the `{: .notice--info}` class.
{: .notice--info}

**ORANGE** This paragraph of text has been [emphasized](#) with the `{: .notice--warning}` class.
{: .notice--warning}

**GREEN** This paragraph of text has been [emphasized](#) with the `{: .notice--success}` class.
{: .notice--success}

**RED** This paragraph of text has been [emphasized](#) with the `{: .notice--danger}` class.
{: .notice--danger}

👉 Results are a lagging measure of habits.
{: .notice--primary}

# Image Alignment
Place these immmediately after image:


# Mathematics
Utilizes [MathJax](https://docs.mathjax.org/en/latest/input/tex/index.html)
Include "mathjax: true" in frontmatter.
Utilizes [LaTeX](https://en.wikibooks.org/wiki/LaTeX/Mathematics)
Formula syntax:

# JavaScript Stuff

## Forms

<form>
  <fieldset>
    <legend>Personalia:</legend>
    Name: <input type="text" size="30"><br>
    Email: <input type="text" size="30"><br>
    Date of birth: <input type="text" size="10">
  </fieldset>
</form>