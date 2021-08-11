# Guide
See if this syncs
# Markdown

## Locations of key files/directories
-   Basic config options: _config.yml
-   Top navigation bar config: _data/navigation.yml
-   Single pages: _pages/
-   Collections of pages are .md or .html files in:
    -   _publications/
    -   _portfolio/
    -   _posts/
    -   _teaching/
    -   _talks/
-   Footer: _includes/footer.html
-   Static files (like PDFs): /files/
-   Profile image (can set in _config.yml): images/profile.png

## Tips and hints
-   Name a file “.md” to have it render in markdown, name it “.html” to render in HTML.
-   Go to the [commit list](https://github.com/academicpages/academicpages.github.io/commits/master) (on your repo) to find the last version Github built with Jekyll.
    -   Green check: successful build
    -   Orange circle: building
    -   Red X: error
    -   No icon: not built

## Resources
-   [Liquid syntax guide](https://shopify.github.io/liquid/tags/control-flow/)
## Markdown guide
### Header three
#### Header four
##### Header five
###### Header six

## Blockquotes
Single line blockquote:
> Quotes are cool.

## Tables
### Table 1
Entry
Item
[John Doe](https://karthisrinivasan.github.io/markdown/#)
2016
Description of the item in the list
[Jane Doe](https://karthisrinivasan.github.io/markdown/#)
2019
Description of the item in the list
[Doe Doe](https://karthisrinivasan.github.io/markdown/#)
2022
Description of the item in the list

### Table 2
Header1
Header2
Header3
cell1
cell2
cell3
cell4
cell5
cell6
cell1
cell2
cell3
cell4
cell5
cell6
Foot1
Foot2
Foot3

## Definition Lists
Definition List Title
Definition list division.
Startup
A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.
#dowork
Coined by Rob Dyrdek and his personal body guard Christopher “Big Black” Boykins, “Do Work” works as a self motivator, to motivating your friends.
Do It Live

I’ll let Bill O’Reilly [explain](https://www.youtube.com/watch?v=O_HyZ5aW76c "We'll Do It Live") this one.

## Unordered Lists (Nested)
-   List item one
    -   List item one
        -   List item one
        -   List item two
        -   List item three
        -   List item four
    -   List item two
    -   List item three
    -   List item four
-   List item two
-   List item three
-   List item four

## Ordered List (Nested)
1.  List item one
    1.  List item one
        1.  List item one
        2.  List item two
        3.  List item three
        4.  List item four
    2.  List item two
    3.  List item three
    4.  List item four
2.  List item two
3.  List item three
4.  List item four

## Buttons
Make any link standout more when applying the `.btn` class.

## Notices
**Watch out!** You can also add notices by appending `{: .notice}` to a paragraph.

## HTML Tags

### Address Tag
1 Infinite Loop  
Cupertino, CA 95014  
United States

### Anchor Tag (aka. Link)
This is an example of a [link](http://github.com/ "Github").

### Abbreviation Tag
The abbreviation CSS stands for “Cascading Style Sheets”.

### Cite Tag
“Code is poetry.” —Automattic

### Code Tag
You will learn later on in these tests that `word-wrap: break-word;` will be your best friend.

### Strike Tag
This tag will let you strikeout text.

### Emphasize Tag
The emphasize tag should _italicize_ text.

### Insert Tag
This tag should denote inserted text.

### Keyboard Tag
This scarcely known tag emulates keyboard text, which is usually styled like the `<code>` tag.

### Preformatted Tag
This tag styles large blocks of code.

.post-title {
  margin: 0 0 5px;
  font-weight: bold;
  font-size: 38px;
  line-height: 1.2;
  and here's a line of some really, really, really, really long text, just to see how the PRE tag handles it and to find out how it overflows;
}

### Quote Tag
Developers, developers, developers… –Steve Ballmer

### Strong Tag
This tag shows **bold text**.

### Subscript Tag
Getting our science styling on with H2O, which should push the “2” down.

### Superscript Tag
Still sticking with science and Isaac Newton’s E = MC2, which should lift the 2 up.

### Variable Tag
This allows you to denote variables.