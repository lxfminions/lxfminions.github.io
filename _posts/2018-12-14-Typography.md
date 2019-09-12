---
layout: post
title: Typography notes
categories: [it]
tags: [LaTeX, Typography]
date: 2018/12/15
---
Reading the book [BUTTERICK'S PRACTICAL TYPOGRAPHY](https://practicaltypography.com/index.html).
## Punctuation Marks

### Quotation Marks
- *Curly quotes* are the quotation marks used in good typography. There are
four curly quote characters: the opening single quote (&lsquo;), the closing
single quote (&rsquo;), the opening double quote (&ldquo;), and the closing
quote(&rdquo;).
{% highlight latex%}
`` This is double curly quotes examle. ''
` This is single curly quotes examle.'
{% endhighlight %}
- *Straight quotes* are two generic vertical quotation marks located near the
return key: the straight single quote (\') and the straight double quote (\").
{% highlight latex %}
\textquotesingle % product a straight single quote
\textquotedbl % product a straight double quote
{% endhighlight %}
