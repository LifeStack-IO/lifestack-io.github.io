---
layout: page
title: Testing Page
permalink: /test/
hidden: true
---
{% include lead.md %}

# Testing [Markdown][1]{:target='_new'}[^h1]

This page is a generic test document, demonstrating what [Markdown][2] is capable of. Deviations from the original [syntax][3], using [Kramdown][5] / [PHP Markdown Extra][4] will be indicated[^KD]. It is used to verify styling and legibility, using a wide range of stylistic devices.

## Formatting & Blocks[^h2]

A simple paragraphs illustrated here, and created by using a carriage return/blank line in the source text. A paragraph will generate a standard block-level ‘p’ tag in the output HTML. __Bold__ (‘strong’) and _italic_ (‘em’) effects are created by using single/double underscores (‘_’) or asterisks (‘*’). These can also be combined to create __*bold italics*__.

### Inline _Formatting_ & Objects[^h3]

Headings can contain inline formatting too, and (like paragraphs) can also contain `inline code`.

##### Headings[^h5] {#custom-id}

Some headings can even have custom ids/anchors, as above.&nbsp;[^KD] Headings may be used to generate a [table-of-contents](#markdown-toc) on the page as well.

#### Ordered List[^h4]

These are prefixed by numbers in the source document, generating an ‘ol’ tag.

1. The First Item
2. The Second Item
3. The Third Item

#### Unordered List

These are prefixed by asterisks, pluses or dashes in the source document, generating a ‘ul’ tag.

* A List Item
	* Sub-List Item
	* Sub-List Item
* A List Item
* A List Item

---

###### Quotes[^h6]

> Above this quote should be a horizontal line, used to break up the page.

    Example Highlighted Javascript follows, but this line is indented code (not highlighted)!

### Example Javascript

{% highlight javascript %}
(function(document) {
	var toggle = document.querySelector(".nav-toggle");
	var navigation = document.querySelector("#nav-container");
	var checkbox = document.querySelector("#nav-display");
	document.addEventListener("click", function(e) {
		var target = e.target;
		if(!checkbox.checked || navigation.contains(target) || (target === checkbox || target === toggle)) return;
		checkbox.checked = false;
	}, false);
})(document);
{% endhighlight %}

The code above is highlighted using the Rouge Highlighter, which can be found here: <http://rouge.jneen.net/>

    More Javascript code follows, but this time with line numbers

### Some more Javascript

{% capture code %}{% highlight javascript linenos %}
(function(document) {
	var toggle = document.querySelector(".nav-toggle");
	var navigation = document.querySelector("#nav-container");
	var checkbox = document.querySelector("#nav-display");
	document.addEventListener("click", function(e) {
		var target = e.target;
		if(!checkbox.checked || navigation.contains(target) || (target === checkbox || target === toggle)) return;
		checkbox.checked = false;
	}, false);
})(document);
{% endhighlight %}{% endcapture %}{% include lines.html %}{{ code }}

~~~
Finally, here is some more fenced code!
~~~

### Tables

|---
| Default aligned | Left aligned | Center aligned | Right aligned
|-|:-|:-:|-:
| First body part | Second cell | Third cell | fourth cell
| Second line |foo | **strong** | bar
| Third line |for | for | bar
|---
| Second body
| 2 line
|===
| Footer row

*[HTML]: Hypertext Markup Language
*[PHP]: PHP: Hypertext Preprocessor

[^h1]: Heading Level 1 (__H1__).
[^h2]: Heading Level 2 (__H2__).
[^h3]: Heading Level 3 (__H3__).
[^h4]: Heading Level 4 (__H4__).
[^h5]: Heading Level 5 (__H5__).
[^h6]: Heading Level 6 (__H6__).
[^KD]: Kramdown __only__ feature / extension.

  [1]: http://daringfireball.net/projects/markdown/ "Article by Jon Gruber detailing Markdown"
  [2]: http://daringfireball.net/projects/markdown/basics
  [3]: http://daringfireball.net/projects/markdown/syntax
  [4]: http://michelf.com/projects/php-markdown/extra/ "PHP Markdown Extra Package Information"
  [5]: http://kramdown.gettalong.org/syntax.html "Kramdown - Markdown Parser"