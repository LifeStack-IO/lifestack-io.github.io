LifeStack
=========

The best of the 'cloud' from an educational perspective.

_Articles, tutorials reviews and guidance. Information and advice to help you get the most from technology._

Rationale
---------

The web we know is crammed with _valuable_ and _insightful_ information. Yet we frequently struggle to ask the _right questions_ as we drown in this rich and varied sea of possibilities. Too often the potential of technology is overlooked as it is considered '__complex__' or '__time-consuming__'.

Even the most diligent of us are also _guilty_ of glancing at tutorials, articles and examples without actually reading them. A 'search-first' world has dented our capacity to really pay attention to the written word, reducing our own 'information seeking' habits to merely skimming and discarding when gratification is not immediately forthcoming.

This site is an attempt to swim against this tide, by sharing guidance and thoughts on what has become commonly known as 'cloud' technologies. The article format, with a focus on _words_ and _explanations_ rather than screenshots and step-by-step instructions, is aimed at encouraging _thinking_ & _understanding_.

###### Why the name?

In computer science, a stack has a particular [technical meaning][18]. More recently, it has begun to be used as shorthand for a _development_ or _solution_ [stack][19]. In these technological terms, it describes a group of applications, or services, which come together to build a platform for work. The tools you use every day to get your job done, to function fully in a connected world. This site is all about those tools, how they can work smoothly together and how you can use them better. In short, it's about the __stacks__ upon which we build our _technological lives_.

### Content

All the content for this site is original work, the culmination of work and experience with a wide range of technologies. Everything is authored in a simple text-based language called [Markdown][1], which was originally proposed and design by [Jon Gruber][2]. It is a simple format that allows for a clean separation of these words from their style and presentation on your screen. Like technology itself, all __[posts][3]__ on this site should be considered as '_work in progress_' and are available online (under an open-source license - see below) for amendment by anyone who would like to propose changes or improvements.

To do this you will need a free [Github](https://github.com/, "Github Homepage") account. Once you have an account, you can click on the small Github Logo (the [octocat][4]) at the bottom right of each post which will take you directly to the source of the article on Github. From here, you can edit your own version of the article (part of what is known as a [fork][5]) by clicking on the small pencil/edit icon near the top of the page. Once you have completed your edit, you can ask that your change be _merged_ into the __[live]({{ site.url }})__ version of this site by creating a _pull request_ (or, more simply, a request that your changed be 'pulled' into the live version of this site). If you supply a reason with your request, and your request is accepted, your change will be published and the article will be __updated__.

### Design

###### Typography

The [typefaces][6] for this site are open-source and are served from [Google Fonts][7]. They have been selected to deliver a timeless aesthetic, aid readability, encourage focus & help concentration. The page & post headings are set in [Baumans](https://fonts.google.com/specimen/Baumans) (as is the lifestack logo), headings are in [Raleway](https://fonts.google.com/specimen/Raleway) and the body is in [Crimson Text](https://fonts.google.com/specimen/Crimson+Text). Text emphasis is provided by __bolds__ and _italics_, with clickable link denoted by small CAPITALISATION (rather than the normal yet inelegant underlining).

###### Colours

A simple _three-layer_ scheme is used throughout the site, with deep blacks & greys for the _main content_, lighter greys for background _information_ or_icons_. A __bold__ red highlight is used for _links_, _titles_ and the _navigation menu_. As above, this simplicity is a deliberate design decision to help focus attention on the __words__ themselves.

###### Layout

The layout of the site is build around a __content column__, restricted to a maximum [line-length](https://en.wikipedia.org/wiki/Line_length) to ensure _readability_ whilst also making the most of larger screens. A left-hand column & wide spacing-gutter is home to explanatory notes and used for header links to help structure and navigate longer posts. On smaller screen devices (e.g. mobiles), this column will fold into a _single-column design_ taking up the full width of the screen. Navigation is provided by a 'fly-out' navigation __menu__ that remains normally hidden to reduce visual clutter and distraction.

###### Illustration

Illustrations, rather than screenshots or photos, are used to illustrate individual posts. These help ensure a consistent _style_ and also don't age as quickly as screenshots (for the exact design of web-applications changes frequently). For this reason, and to ensure longevity of utility, actions tend to be _described_ (e.g. submit the registration form) rather than _narrated_ (e.g. click on the large blue button entitled 'submit' at the bottom left hand side of the form).

### Architecture & Process

This site is a [static][8] website, meaning __no__ _server-side code_ runs when you request each page. This makes it _easier_ to author, manage and host. It should also be _faster_ to load. When the site content or design is changed in anyway, the whole site is re-generated using a tool called [Jekyll][9] which runs on a programming language called [Ruby][10]. Jekyll helps _manage_ index pages and _merge_ the files containing text content with the style & layout of the site (authored in standard HTML and [SASS][11]). The static HTML content is compressed to help ensure it is delivered as [quickly & efficiently][12] as possible. All the content & styling is authored using [Codeanywhere][13] or Google Docs and the [Gabriel][14] add-on to convert the document to markdown and publish it.

### Copyright & Licensing

To help you use the content on this site in _useful ways_, everything is _[open-source][17]_, and here is a summary of how the site is __licensed__.

![Creative Commons Licence](https://i.creativecommons.org/l/by-nc-sa/4.0/80x15.png) All the written content on this site is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/). This means you are free to _link to_, _copy_, _redistribute_ and _build upon_ this work providing you share the results, give attribution and don't use it for commercial purposes.

Unless otherwise stated in the code, the operational plumbing of the site (code, CSS etc.) are made available under a [GNU GPL v3 licence][15], so you are free to redistribute it under the same terms but this means there is _absolute no warranty_.

Finally, any __code__ examples that are used for _illustrative_ or _educational purposes_ within the content on the site is provided under a permissive [MIT license][16], meaning you can use it in pretty much anyway you wish (including commercial works!).

&copy; 2014-2016 LifeStack.io.

  [1]: https://en.wikipedia.org/wiki/Markdown "Wikipedia Article about Markdown"
  [2]: http://daringfireball.net/projects/markdown "Article by Jon Gruber detailing Markdown"
  [3]: https://en.wikipedia.org/wiki/Blog
  [4]: https://octodex.github.com/ "Octocats of the World"
  [5]: https://help.github.com/articles/fork-a-repo/ "What is a fork in software development"
  [6]: https://en.wikipedia.org/wiki/Typeface "What is a typeface?"
  [7]: https://fonts.google.com/ "Google Fonts"
  [8]: https://en.wikipedia.org/wiki/Static_web_page "Static Web Pages"
  [9]: https://jekyllrb.com/ "Jekyll Homepage"
  [10]: https://www.ruby-lang.org "Ruby Homepage"
  [11]: http://sass-lang.com/ "All about SASS"
  [12]: https://developers.google.com/speed/pagespeed/insights/?url={{site.url}} "Google PageSpeed Insights"
  [13]: https://codeanywhere.com/ "Codeanywhere, Cloud IDE"
  [14]: https://chrome.google.com/webstore/detail/gabriel/okimajjeocnndpifeelaajdebkkbckff "Gabriel Add-On for Google Docs"
  [15]: http://www.gnu.org/licenses/gpl.html "GNU GPL v3 Licence Terms"
  [16]: https://opensource.org/licenses/MIT "MIT License"
  [17]: https://en.wikipedia.org/wiki/Open-source_software "Wikipedia - What is open-source software"
  [18]: https://en.wikipedia.org/wiki/Stack_(abstract_data_type) "Wikipedia - What is a stack"
  [19]: https://en.wikipedia.org/wiki/Solution_stack "Wikipedia - What is a solution stack"