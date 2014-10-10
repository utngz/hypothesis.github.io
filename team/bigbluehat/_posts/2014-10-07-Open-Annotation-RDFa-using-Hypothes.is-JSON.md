---
layout: post
title: Open Annotation RDFa using Hypothes.is JSON
author: bigbluehat
---

The [Open Annotation Core Data Model](http://openannotation.org/spec/core/) is something we're keen to
include in future [Hypothes.is](http://hypothes.is/) releases. We're exploring using it via
[JSON-LD](http://json-ld.org/) natively in [AnnotatorJS](http://annotatorjs.org/). Along the way,
we're experimenting and growing our understanding of the specification.

[RDFa](http://rdfa.info/) allows us to mix the Open Annotation Core Data Model into existing HTML
markup. In an effort to understand how this all might work, I built a small
[RequireBin](http://requirebin.com) to see how far I could get using the existing
Hypothes.is/AnnotatorJS JSON object.

Here's the result (or [view it on RequireBin](http://requirebin.com/?gist=f47e6cfda27afccc03be)):

<iframe width="100%" height="700" src="http://requirebin.com/embed?gist=f47e6cfda27afccc03be" frameborder="0" allowfullscreen></iframe>

The `<textarea>` contents are the most interesting part (so far). There some minimal HTML markup
with some explanatory RDFa attributes that use the Open Annotation Core Data Model to "explain"
the data in the markup.

If you're curious what this might look like visualized as a graph or represented in [Turtle](http://www.w3.org/TR/turtle/), copy and paste the contents of that text area into [RDFa Play](http://rdfa.info/play).

### Feedback extremely welcome!

It's early days yet, so any and all input is welcome. Feel free to annotate this post using
the Hypothes.is sidebar (it's in the top right corner). Or send an email to bigbluehat[at]hypothes[dot]is.

Cheers!
