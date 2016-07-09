# My Markdown Notes

## Headings
- One to six # symbols before heading text
```
# Header one
## Header two
### Header three
#### Header four
##### Header five
###### Header six
```
# Header one
## Header two
### Header three
#### Header four
##### Header five
###### Header six

## Styling text
- **Bold**: `** **` or `__ __`
- _Italic_: `* *` or `_ _`
- ~~Strikethrough~~: `~~ ~~`
- **Bold and _italic_**: `** **` and `_ _`

## Quoting text
- Quote text with a `>` before text
> This is a quoting text.

## Quoting code
- Inline quote: single backticks (\`\`) like `git status`
- Code block: triple backticks like
```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```
- Syntax highlighting: add an optional language identifier to enable syntax highlighting in your fenced code block

## Links
- An inlink link by wrapping link text in brackets `[ ]`, and then wrapping the URL in parentheses `( )`.
>`[GitHub Pages](https://pages.github.com)`
>
>[GitHub Pages](https://pages.github.com)

- A reference link. The link is actually a reference to another place in the document. Have **issue** for it.
> ```
> Here's [a link to something else][another place].
>
> Here's [yet another link][another-link].
>
> And now back to [the first link][another place].
>
> [another place]: www.github.com
>
> [another-link]: www.google.com
> ```
>
> Here's [a link to something else][another place].
>
> Here's [yet another link][another-link].
>
> And now back to [the first link][another place].

[another place]: www.github.com

[another-link]: www.google.com
- Links to image : The difference is that an image is prefaced with an exclamation point ( ! ), followed by the same two brackets, and a pair of parentheses containing the image URL. Within the image brackets, you can place some "alt text," which is a phrase or sentence that describes the image for the visually impaired.


## Lists
- Make a list by preceding one or more lines of text with - or *.
- Make a ordered list, precede each line with a number.
- Create nested lists by indenting lines by two spaces.

## Task lists
- Create task lists by prefacing list items with [ ]. To mark a task as complete, use [x].

## Paragraphs and line breaks
- Create a new paragraph by leaving a blank line between lines of text (hard break)
- Soft break: inserting two spaces after each new line.

## Ignoring Markdown formatting
- Ignore (or escape) Markdown formatting by using \ before the Markdown character.

## Organizing information with tables
### Creating a table
- Create tables with pipes | and hyphens -. Hyphens are used to create each column's header, while pipes separate each column.
- The pipes on either end of the table are optional.
- Cells can vary in width and do not need to be perfectly aligned within columns. There must be at least three hyphens in each column of the header row.

### Formatting content within your table
- Use formatting such as links, inline coee blocks, and text styling within your table.
- Align text to the left, right, or center of a column by including colons : to the left, right, or on both sides of the hyphens within the header row.
- To include a pipe | as content within your cell, use a \ before the pipe.
```
| Column 1 | Column 2 | Column 3 |
| :-- | :-: | --: |
| left-aligned | centered | right-aligned |
| 1 | 1 | 1 |
| 20 | 20 | 20 |
```

| Column 1 | Column 2 | Column 3 |
| :-- | :-: | --: |
| left-aligned | centered | right-aligned |
| 1 | 1 | 1 |
| 20 | 20 | 20 |

## Reference links
- http://www.markdowntutorial.com/conclusion/
- https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
- https://help.github.com/enterprise/11.10.340/user/articles/github-flavored-markdown/
- https://help.github.com/categories/writing-on-github/
- https://daringfireball.net/projects/markdown/syntax
- https://guides.github.com/features/mastering-markdown/
