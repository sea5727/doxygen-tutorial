

~~~~~{.py}
# A class
class Dummy:
    pass
~~~~~


~~~~~{.cpp}
int add(int a, int b){
    return a + b;
}
// test

int main(int, char**) {
    std::cout << "Hello, world!\n";
}
~~~~~

`printf()`   
`
int add(int a, int b){
    return a + b;
}


int main(int, char**) {
    std::cout << "Hello, world!\n";
}
`   

``printf()``   

``
int add(int a, int b){
    return a + b;
}


int main(int, char**) {
    std::cout << "Hello, world!\n";
}
``

```cppprintf()```

```cpp
printf()
```


page markdown Markdown support

[TOC]

[Markdown] support 
was introduced in doxygen version 1.8.0. It is a plain text formatting
syntax written by John Gruber, with the following underlying design goal:

> The design goal for Markdown's formatting syntax is to 
> make it as readable as possible. The idea is that a Markdown-formatted 
> document should be publishable as-is, as plain text, without 
> looking like it's been marked up with tags or formatting instructions. 
> While Markdown's syntax has been influenced by several existing 
> text-to-HTML filters, the single biggest source of inspiration 
> for Markdown's syntax is the format of plain text email.

In the \ref markdown_std "next section" the standard Markdown features
are briefly discussed. The reader is referred to the [Markdown site][markdown]
for more details.

Some enhancements were made, for instance [PHP Markdown Extra][mdextra], and
[GitHub flavored Markdown][github]. The section \ref markdown_extra discusses
the extensions that doxygen supports.

Finally section \ref markdown_dox discusses some specifics for doxygen's
implementation of the Markdown standard.

[markdown]: https://daringfireball.net/projects/markdown/ 
[mdextra]:  https://michelf.ca/projects/php-markdown/extra/
[github]:   https://github.github.com/github-flavored-markdown/

\section markdown_std Standard Markdown

\subsection md_para Paragraphs

Even before doxygen had Markdown support it supported the same way
of paragraph handling as Markdown: to make a paragraph you just separate
consecutive lines of text by one or more blank lines.

An example:

    Here is text for one paragraph.

    We continue with more text in another paragraph.

\subsection md_headers Headers

Just like Markdown, doxygen supports two types of headers

Level 1 or 2 headers can be made as the follows

    This is a level 1 header
    ========================

    This is a level 2 header
    ------------------------

A header is followed by a line containing only ='s or -'s.
Note that the exact amount of ='s or -'s is not important as long as
there are at least two.

Alternatively, you can use #'s at the start of a line to make a header. 
The number of #'s at the start of the line determines the level (up to 6 levels are supported).
You can end a header by any number of #'s.

Here is an example:

    # This is a level 1 header

    ### This is level 3 header #######

\subsection md_blockquotes Block quotes

Block quotes can be created by starting each line with one or more >'s, 
similar to what is used in text-only emails.

    > This is a block quote
    > spanning multiple lines

Lists and code blocks (see below) can appear inside a quote block.
Quote blocks can also be nested.

Note that doxygen requires that you put a space after the (last) > character
to avoid false positives, i.e. when writing

    0  if OK\n
    >1 if NOK

the second line will not be seen as a block quote.

\subsection md_lists Lists

Simple bullet lists can be made by starting a line with -, +, or *.

    - Item 1

      More text for this item.

    - Item 2
      + nested list item.
      + another nested item.
    - Item 3

List items can span multiple paragraphs (if each paragraph starts with
the proper indentation) and lists can be nested.
You can also make a numbered list like so

    1. First item.
    2. Second item.

Make sure to also read \ref mddox_lists for doxygen specifics.

\subsection md_codeblock Code Blocks

Preformatted verbatim blocks can be created by indenting
each line in a block of text by at least 4 extra spaces

    This a normal paragraph

        This is a code block

    We continue with a normal paragraph again.

Doxygen will remove the mandatory indentation from the code block.
Note that you cannot start a code block in the middle of a paragraph
(i.e. the line preceding the code block must be empty).

See section \ref mddox_code_blocks for more info how doxygen handles
indentation as this is slightly different than standard Markdown.

\subsection md_rulers Horizontal Rulers

A horizontal ruler will be produced for lines containing at least three or more
hyphens, asterisks, or underscores. The line may also include any amount of whitespace.

Examples:

    - - -
    ______

Note that using asterisks in comment blocks does not work. See 
\ref mddox_stars for details.<br>
Note that when using hyphens and the previous line is not empty you have to
use at least one whitespace in the sequence of hyphens otherwise it might be
seen as a level 2 header (see \ref md_headers).

\subsection md_emphasis Emphasis

To emphasize a text fragment you start and end the fragment with an underscore or star.
Using two stars or underscores will produce strong emphasis.

Examples:

*    *single asterisks*
*
*    _single underscores_
*
*    **double asterisks**
*
*    __double underscores__

See section \ref mddox_emph_spans for more info how doxygen handles
emphasis / strikethrough spans slightly different than standard / Markdown GitHub Flavored Markdown.

\subsection md_strikethrough Strikethrough

To strikethrough a text fragment you start and end the fragment with two tildes.

Examples:

*    ~~double tilde~~

See section \ref mddox_emph_spans for more info how doxygen handles
emphasis / strikethrough spans slightly different than standard Markdown / GitHub Flavored Markdown.

\subsection md_codespan code spans

To indicate a span of code, you should wrap it in backticks (`). Unlike code blocks,
code spans appear inline in a paragraph. An example:

    Use the `printf()` function.

To show a literal backtick or single quote inside a code span use double backticks, i.e.

    To assign the output of command `ls` to `var` use ``var=`ls```.

    To assign the text 'text' to `var` use ``var='text'``.

See section \ref mddox_code_spans for more info how doxygen handles
code spans slightly different than standard Markdown.

\subsection md_links Links

Doxygen supports both styles of make links defined by Markdown: *inline* and *reference*.

For both styles the link definition starts with the link text delimited by [square 
brackets].

\subsubsection md_inlinelinks Inline Links

For an inline link the link text is followed by a URL and an optional link title which
together are enclosed in a set of regular parenthesis. 
The link title itself is surrounded by quotes.

Examples:

    [The link text](http://example.net/)
    [The link text](http://example.net/ "Link title")
    [The link text](/relative/path/to/index.html "Link title") 
    [The link text](somefile.html) 

In addition doxygen provides a similar way to link a documented entity:

    [The link text](@ref MyClass) 

\subsubsection md_reflinks Reference Links

Instead of putting the URL inline, you can also define the link separately
and then refer to it from within the text.

The link definition looks as follows:

    [link name]: http://www.example.com "Optional title"

Instead of double quotes also single quotes or parenthesis can
be used for the title part.

Once defined, the link looks as follows
  
    [link text][link name]

If the link text and name are the same, also

    [link name][]

or even

    [link name]

can be used to refer to the link.
Note that the link name matching is not case sensitive
as is shown in the following example:

    I get 10 times more traffic from [Google] than from
    [Yahoo] or [MSN].

    [google]: http://google.com/        "Google"
    [yahoo]:  http://search.yahoo.com/  "Yahoo Search"
    [msn]:    http://search.msn.com/    "MSN Search"

Link definitions will not be visible in the output.

Like for inline links doxygen also supports \@ref inside a link definition:

    [myclass]: @ref MyClass "My class"

\subsection md_images Images

Markdown syntax for images is similar to that for links.
The only difference is an additional ! before the link text.

Examples:

    ![Caption text](/path/to/img.jpg)
    ![Caption text](/path/to/img.jpg "Image title")
    ![Caption text][img def]
    ![img def]

    [img def]: /path/to/img.jpg "Optional Title"

Also here you can use \@ref to link to an image:

    ![Caption text](@ref image.png)
    ![img def]

    [img def]: @ref image.png "Caption text"

The caption text is optional.

\subsection md_autolink Automatic Linking

To create a link to an URL or e-mail address Markdown supports the following
syntax:

    <http://www.example.com>
    <https://www.example.com>
    <ftp://www.example.com>
    <mailto:address@example.com>
    <address@example.com>

Note that doxygen will also produce the links without the angle brackets.

\section markdown_extra Markdown Extensions

\subsection md_toc Table of Contents

Doxygen supports a special link marker `[TOC]` which can be placed in a page
to produce a table of contents at the start of the page, listing all sections.

Note that using `[TOC]` is the same as using a
\ref cmdtableofcontents "\\tableofcontents" command.

Note that the \ref cfg_toc_include_headings "TOC_INCLUDE_HEADINGS" has to be set
to a value > 0 otherwise no table of contents is shown when using \ref md_headers "Markdown Headers".

\subsection md_tables Tables

Of the features defined by "Markdown Extra" is support for
<a href="https://michelf.ca/projects/php-markdown/extra/#table">simple tables</a>:

A table consists of a header line, a separator line, and at least one
row line. Table columns are separated by the pipe (|) character.

Here is an example:

    First Header  | Second Header
    ------------- | -------------
    Content Cell  | Content Cell 
    Content Cell  | Content Cell 

which will produce the following table:

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell 
Content Cell  | Content Cell 

Column alignment can be controlled via one or two colons 
at the header separator line:

    | Right | Center | Left  |
    | ----: | :----: | :---- |
    | 10    | 10     | 10    |
    | 1000  | 1000   | 1000  |

which will look as follows:

| Right | Center | Left  |
| ----: | :----: | :---- |
| 10    | 10     | 10    |
| 1000  | 1000   | 1000  |

Additionally, column and row spans are supported.  Using a caret ("^")
in a cell indicates that the cell above should span rows.  Sequences
of carets may be used for any number of row spans.  For example:

    | Right | Center | Left  |
    | ----: | :----: | :---- |
    | 10    | 10     | 10    |
    | ^     | 1000   | 1000  |

which will look as follows:

| Right | Center | Left  |
| ----: | :----: | :---- |
| 10    | 10     | 10    |
| ^     | 1000   | 1000  |

Column spans are supported by means of directly adjacent vertical bars
("|").  Each additional vertical bar indicates an additional column to
be spanned.  To put it another way, a single vertical bar indicates a
single column span, two vertical bars indicates a 2 columns span, and
so on.  For example:

    | Right | Center | Left  |
    | ----: | :----: | :---- |
    | 10    | 10     | 10    |
    | 1000  |||

which will look as follows:

| Right | Center | Left  |
| ----: | :----: | :---- |
| 10    | 10     | 10    |
| 1000  |||   

For more complex tables in doxygen please have a look at: \ref tables

\subsection md_fenced Fenced Code Blocks

Another feature defined by "Markdown Extra" is support for
<a href="https://michelf.ca/projects/php-markdown/extra/#fenced-code-blocks">
fenced code blocks</a>:

A fenced code block does not require indentation, and is
defined by a pair of "fence lines". Such a line consists of 3 or
more tilde (~) characters on a line. The end of the block should have the
same number of tildes. Here is an example:


    This is a paragraph introducing:

    ~~~~~~~~~~~~~~~~~~~~~
    a one-line code block
    ~~~~~~~~~~~~~~~~~~~~~

By default the output is the same as for a normal code block.

For languages supported by doxygen you can also make the code block
appear with syntax highlighting. To do so you need to 
indicate the typical file extension that corresponds to the 
programming language after the opening fence. For highlighting according
to the Python language for instance, you would need to write the following:

    ~~~~~~~~~~~~~{.py}
    # A class
    class Dummy:
        pass
    ~~~~~~~~~~~~~

which will produce:
~~~~~~~~~~~~~{.py}
# A class
class Dummy:
    pass
~~~~~~~~~~~~~

and for C you would write:

    ~~~~~~~~~~~~~~~{.c}
    int func(int a,int b) { return a*b; }
    ~~~~~~~~~~~~~~~

which will produce:

~~~~~~~~~~~~~~~{.c}
int func(int a,int b) { return a*b; }
~~~~~~~~~~~~~~~

The curly braces and dot are optional by the way.

Another way to denote fenced code blocks is to use 3 or more backticks (```):

    ```
    also a fenced code block
    ```

\subsection md_header_id Header Id Attributes

Standard Markdown has no support for labeling headers, which
is a problem if you want to link to a section.

PHP Markdown Extra allows you to label a header by adding
the following to the header

    Header 1                {#labelid}
    ========

    ## Header 2 ##          {#labelid2}

To link to a section in the same comment block you can use

    [Link text](#labelid)

to link to a section in general, doxygen allows you to use \@ref

    [Link text](@ref labelid)

Note this only works for the headers of level 1 to 4.

\section markdown_dox Doxygen specifics

Even though doxygen tries to following the Markdown standard as closely as
possible, there are couple of deviation and doxygen specifics additions.

\subsection md_page_header Including Markdown files as pages

Doxygen can process files with Markdown formatting. 
For this to work the extension for such a file should 
be `.md` or `.markdown` (see 
\ref cfg_extension_mapping "EXTENSION_MAPPING" if your Markdown files have 
a different extension, and use `md` as the name of the parser).
Each file is converted to a page (see the \ref cmdpage "page" command for
details). 

By default the name and title of the page are derived from the file name.
If the file starts with a level 1 header however, it is used as the title
of the page. If you specify a label for the 
header (as shown in \ref md_header_id) doxygen will use that as the
page name. 

If the label is called `index` or `mainpage` doxygen will put the
documentation on the front page (`index.html`).

Here is an example of a file `README.md` that will appear as the main page
when processed by doxygen:

    My Main Page                         {#mainpage}
    ============

    Documentation that will appear on the main page

If a page has a label you can link to it using \ref cmdref "\@ref" as 
is shown above. To refer to a markdown page without
such label you can simple use the file name of the page, e.g.

    See [the other page](other.md) for more info.

\subsection md_html_blocks Treatment of HTML blocks

Markdown is quite strict in the way it processes block-level HTML:

> block-level HTML elements — e.g. 
> `<div>`, `<table>`, `<pre>`, `<p>`, etc. — 
> must be separated from surrounding content by blank lines, 
> and the start and end tags of the block should not be indented 
> with tabs or spaces.

Doxygen does not have this requirement, and will also process 
Markdown formatting inside such HTML blocks. The only exception is
`<pre>` blocks, which are passed untouched (handy for ASCII art).

Doxygen will not process Markdown formatting inside verbatim or code blocks,
and in other sections that need to be processed without changes
(for instance formulas or inline dot graphs).

\subsection mddox_code_blocks Code Block Indentation

Markdown allows both a single tab or 4 spaces to start a code block.
Since doxygen already replaces tabs by spaces before doing Markdown
processing, the effect will only be same if TAB_SIZE in the configuration file
has been set to 4. When it is set to a higher value spaces will be
present in the code block. A lower value will prevent a single tab to be 
interpreted as the start of a code block.

With Markdown any block that is indented by 4 spaces (and 8 spaces
inside lists) is treated as a code block. This indentation amount
is absolute, i.e. counting from the start of the line.

Since doxygen comments can appear at any indentation level
that is required by the programming language, it
uses a relative indentation instead. The amount of 
indentation is counted relative to the preceding paragraph.
In case there is no preceding paragraph (i.e. you want to start with a
code block), the minimal amount of indentation of the whole comment block 
is used as a reference.

In most cases this difference does not result in different output.
Only if you play with the indentation of paragraphs the difference
is noticeable:

    text

     text

      text
  
       code

In this case Markdown will put the word code in a code block,
whereas doxygen will treat it as normal text, since although the absolute
indentation is 4, the indentation with respect to the previous paragraph
is only 1.

Note that list markers are not counted when determining the
relative indent:

    1.  Item1

        More text for item1

    2.  Item2

            Code block for item2

For Item1 the indentation is 4 (when treating the list marker as whitespace), 
so the next paragraph "More text..." starts at the same indentation level 
and is therefore not seen as a code block.

\subsection mddox_emph_spans Emphasis and strikethrough limits

Unlike standard Markdown and Github Flavored Markdown doxygen will not touch internal underscores or
stars or tildes, so the following will appear as-is:

    a_nice_identifier

Furthermore, a `*` or `_` only starts an emphasis  and a `~` only starts a strikethrough if
- it is followed by an alphanumerical character, and
- it is preceded by a space, newline, or one the following characters `<{([,:;`

An emphasis or a strikethrough ends if
- it is not followed by an alphanumerical character, and
- it is not preceded by a space, newline, or one the following characters `({[<=+-\@`

Lastly, the span of the emphasis or strikethrough is limited to a single paragraph.


\subsection mddox_code_spans Code Spans Limits

Note that unlike standard Markdown, doxygen leaves the following untouched.

    A `cool' word in a `nice' sentence.

In other words; a single quote cancels the special treatment of a code span
wrapped in a pair of backtick characters. This extra restriction was
added for backward compatibility reasons.

In case you want to have single quotes inside a code span, don't use 
one backtick but two backticks around the code span.

\subsection mddox_lists Lists Extensions

With Markdown two lists separated by an empty line are joined together into
a single list which can be rather unexpected and many people consider it to
be a bug. Doxygen, however, will make two separate lists as you would expect.

Example:
  
    - Item1 of list 1
    - Item2 of list 1

    1. Item1 of list 2
    2. Item2 of list 2

With Markdown the actual numbers you use to mark the list have no 
effect on the HTML output Markdown produces. I.e. standard Markdown treats the 
following as one list with 3 numbered items:

    1. Item1
    1. Item2
    1. Item3

Doxygen however requires that the numbers used as marks are in 
strictly ascending order, so the above example would produce 3 lists 
with one item. An item with an equal or lower number than 
the preceding item, will start a new list. For example:

    1. Item1 of list 1
    3. Item2 of list 1
    2. Item1 of list 2
    4. Item2 of list 2

will produce:

1. Item1 of list 1
3. Item2 of list 1
2. Item1 of list 2
4. Item2 of list 2
    
Historically doxygen has an additional way to create numbered 
lists by using `-#` markers:

    -# item1
    -# item2

\subsection mddox_stars Use of asterisks

Special care has to be taken when using *'s in a comment block 
to start a list or make a ruler.

Doxygen will strip off any leading *'s from the comment before doing
Markdown processing. So although the following works fine

@verbatim
    /** A list:
     *  * item1
     *  * item2
     */
@endverbatim

When you remove the leading *'s doxygen will strip the other stars
as well, making the list disappear!

Rulers created with *'s will not be visible at all. They only work
in Markdown files.

\subsection mddox_limits Limits on markup scope

To avoid that a stray * or _ matches something many paragraphs later,
and shows everything in between with emphasis, doxygen limits the scope
of a * and _ to a single paragraph.

For a code span, between the starting and ending backtick only two
new lines are allowed. 

Also for links there are limits; the link text, and link title each can
contain only one new line, the URL may not contain any newlines. 

\section markdown_debug Debugging of problems

When doxygen parses the source code it first extracts the comments blocks,
then passes these through the Markdown preprocessor. The output of the
Markdown preprocessing consists of text with \ref cmd_intro "special commands" 
and \ref htmlcmds "HTML commands".
A second pass takes the output of the Markdown preprocessor and
converts it into the various output formats.

During Markdown preprocessing no errors are produced. Anything that
does not fit the Markdown syntax is simply passed on as-is. In the subsequent
parsing phase this could lead to errors, which may not always be obvious
as they are based on the intermediate format.

To see the result after Markdown processing you can run doxygen with the
`-d Markdown` option. It will then print each comment block before and
after Markdown processing.

\htmlonly
Go to the <a href="lists.html">next</a> section or return to the
 <a href="index.html">index</a>.
\endhtmlonly
