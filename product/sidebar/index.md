---
title: Sidebar Features
author: aron
layout: page
---

{:.no_toc}

This document describes the features of the Hypothesis Sidebar project. Each
key feature is given a section that documents three things:

1. A basic **description** of the feature and what it does at the most basic
   level.
2. A set of **user stories** in the form "As a user I when I do x the feature
   should do y so I can z". These stories should describe in more detail how
the product works.
3. A **progress** log. This simply documents iterations on a feature in much
   the same way as a change log. When the implementation is changed a new
   iteration entry should be added describing how the feature now works.

This documentation is intended for Hypothesis team members and those wishing
to contribute to the project. It should hopefully provide a quickstart
overview describing what the product can do.

_NOTE:_ Some of these features have a "GitHub Ticket" link. This is just a
reference to a previous version of this document that used a Waffle.io board
and GitHub issues to track the same data. They are included for complexness.

**Contents**

{:.no_toc}

* [PLACEHOLDER] This will be replaced by the TOC.
  http://kramdown.gettalong.org/converter/html.html#toc
{:toc}

### Annotation Editor

**Description**

Allows creating of an annotation from content selected in the document.

**Stories**

[TODO]

**Progress**

Iteration 1

- Ability to add a comment to an annotation.
- Markdown Support
- Public/Private Privacy support.
- Simple Tagging.
- Preview quoted content.

Iteration 2

- Support for previewing the markdown.
- Support for LaTex syntax for entering mathematical expressions.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/59)

### Annotation Deletion

**Description**

Allows deletion of annotation objects.

**User stories**

* As a user I would like to be able to remove content that they no longer need
  or that was created in error.

**Progress**

Iteration 1

- Allows an annotation and comment to be deleted by the creator.
- If the annotation is public and has public replies then an annotation can
  only be redacted.
- Redaction allows a redaction comment to be applied. And removes the user
  data.

Iteration 2

- Redaction has been removed.
- If an annotation is deleted a placeholder card takes it's place.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/60)

### Document Wayfinding

**Description**

Provides an overview of the annotated state of the current document that's easy
to understand at a glance.

* The number of annotations in the document.
* Where the annotations are.
* If there are comments.

**Stories**

- As  user I want to be able to see where annotations appear in a document so
  that I can navigate to interesting areas.

**Phases**

Iteration 1

- Heatmap that represents the document, bright areas have many comments.
- Floating tags indicate where annotations appear in the page.
- Clicking a tag jumps to the highlight.
- Comment tags are bundled at the bottom of the heat map.

Iteration 2

- The heatmap was removed to simplify the toolbar.
- Comment tags are no longer included in the bar.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/62)

### Viewer Wayfinding

**Description**

Represents annotations in the document in the form of a sidebar overview. This
shows all annotations in the document and allows them to be ordered, filtered
etc. This helps when a document has a large number of annotations and they
cannot all be displayed in the sidebar at one time.

Iteration 1

- Modes that filter which annotations are displayed.
- Document: Shows all the current annotations on the page.
- Screen: Shows only annotations visible in the current viewport.
- Comments: Shows any comments attached to the document.
- Selection: Shows any annotations selected in the document. Can be cleared
  by clicking the heat map. Or changing the view mode.

Iteration 2

- Remove the Screen mode to simplify both the codebase and the interface.
- Comments are included at the top of the viewer at all times.
- All annotations in the document are now shown at all times.
- Only sorting is allowed by Location/Oldest/Newest.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/63)

### Email Notifications for Annotation Activity

**Description**

Send notifications to users at key interaction points within.

**Stories**

* As a user I'd like to be notified by email when someone comments on my
  annotation so that I can read it and reply.
* As a user I'd like to be notified by email when someone replies to my comment
  so that I can read it and reply.
* As a user I'd like to be able to disable notifications.
* As a user I'd like to be able to re-enable email notifications.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/44)

### Annotate PDFs

**Description**

The ability to annotate PDF documents.

**Stories**

- As a user when I activate the extension on a PDF, I see the sidebar.
- As a user when selecting text, I see the adder
- As a user when I save an annotation, the anchor persists. Highlights (if on),
  show the selection.
- As a user when I return to the PDF, annotations previously made are
  re-anchored

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/49)

### Document Level Commenting

**Description**

[TODO]

**Stories**

[TODO]

Iteration 1

- Allow adding of document level comments to a page.
- Displayed in custom view mode.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/55)

### Document level filtering of annotations

**Description**

Currently referred to as "page search" allows annotations on the current page
navigation of documents with large numbers of annotations and
surfacing of interesting content.

**Stories**

* As a user I would like to be able to find specific annotations by searching
  for annotation content.
* As a user I would like to be able to find annotations with a specific tag.
* As a user I would like to be able to find annotations by a specific user.
* As a user I would like to be able to find annotations where the comment text
  contains a keyword.
* As a user I would like to be able to find annotations where the quoted text
  contains a keyword.

**Implementation**

Iteration 1

- Allows filtering of annotations on the current page based on querying "user",
  "text", "quote", "tags".
- Allows facets to be queried through search syntax.
- Applies only to the whole document.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/57)

### Standalone Annotation Page

**Description**

A hosted page that displays an annotation and it's comment thread.

**Stories**

* As a user I would like to be able to link to an annotation for reference or
  sharing.

**Phases**

Iteration 1

- Timestamp
- Public Permalink
- Commenting
- Same interface as the annotation card.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/58)


### Account Management

**Description**

[TODO]

**Stories**

* As a user I would like to be able to change my password in order to keep my account secure.
* As a user I would like to be able to change my email address in order to keep it up to date.
* As a user I would like to be able to delete my account to remove my data from the service.

**Progress**

Iteration One

- Email/password Change
- Account deletion (deletion of user data)

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/69)

### User Tags

**Description**

User generated tags. Plain strings that can be applied by the creator to
collect annotations or comments for personal organisation. Allows personal
curation of content, bookmarking organisation.

**Stories**

* As a researcher I need to be able to organise my annotations.
* As a commenter I need to be able to keep track of my discussions.
* As a copy-editor I need to be able to track which discussions have been
  resolved.

**Phases**

Iteration 1

- Allows text strings to be associated with annotations.
- Applied on create/edit.
- Clicking a tag opens a stream search for the tag.
- These can be searched via the page search too.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/64)

### Visually Linking Document & Viewer

**Description**

This provides visual ties between a card in the sidebar and the matching
annotation in the document.

**Stories**

* As a user looking at an annotation in the page, I want to find the card in
  the sidebar.
* As a user looking at a card in the sidebar I want to find it in the document.

**Phases**

Iteration 1

- Mousing over a card "focuses" the annotation in the document.
- Mousing over an annotation in the document "focuses" the card.
- Clicking a card activates it (it expands) and focuses the card in the
  document.
- Clicking an annotation in the document selects the card and enters
  "selection" mode.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/65)

### Document Highlight Toggle

**Description**

Toggles the annotations in a page on and off.

**Stories**

* As a user I would like to be able to see all annotations in a document to get
  an idea of how heavily annotated the document is.
* As a user I would like to be able to turn all annotations in a document off
  so that I can read the document without visual obstruction.

**Progress**

Iteration 1

- Allows highlights to be toggled on/off through a menu button.
- Highlighter mode forces this feature on.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/66)

### Sharing

**Description**

Allows a user to share a piece of annotated content.

**Stories**

* As a user I would like to be able to reference an annotation so that I can
  refer to it in the future.
* As a user I would like to be able to reference an annotation so that I can
  send it to someone else.

**Progress**

Iteration 1

- Every annotation card has a share action that provides a permalink to the
  standalone annotation page.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/67)

### Privacy Controls

**Description**

Controls the visibility of content created via the platform.

**Stories**

* As a user I would like to make my annotations private so that others cannot
  see them because I'm undertaking private research, making personal notes.
* As a user I would like to make my annotations private so that others can see
  them because I want to discuss them, share them, display them.

**Progress**

Iteration 1

- Annotations can be public/private
- Highlights can only be private as the provide little value in a public
  space. Other than quotations and popularity indicators.
- Comments can be public/private regardless of the state of the parent.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/70)

### Theming and Extension

**Description**

Allow the h repository to be consumed as a dependency and built upon.

**Stories**

* As a partner I would like to be able to change the templates and styles to
  that I can bring the app inline with my own product.

**Progress**

Iteration 1

[TODO]

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/71)

### Stream

**Description**

Annotation is an activity that happens all over the web (across URIs), and the
stream is the place where it can all come together.

**Stories**

* I want to look at all my notes and annotations. Perhaps querying for a tag
  such as "Hypothes.is Notes" or "Sci-fi inspiration."
* A teacher is grading class annotations over a reading list. Since the
  articles are distributed all over the web, he's happy that with a simple
search he can have a stream of a particular student's annotations.
* As a website owner or blogger who embeds h on their site: the stream provides
  a means of seeing conversation happening on the site, again without having to
visit each page individually.
* I'm interested in what another user has annotated, I like being able to click
  on their user name and see a stream of their annotations.
* I click on a tag to see other places and annotations where that tag has
  occurred. In the context of a class I might click on a tag for "Assignment 1"
and be able to see what other students have commented for the first assignment.
* A developer for a e-magazine is building a track changes like feature for the
  magazine's Wordpress CMS, it involves querying our search api for annotations
on any of the magazines articles that are tagged with a special copyediting
ontology.
* A group wants to have a stream of it's annotation, a place where users can go
  and see what everyone has been reading and annotating all over the web. This
could be a study group, a research group, or an editor who's interested in the
activity of the authors writing articles she is editing.

**Progress**

Iteration 1

[TODO]

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/88)

### Authentication

**Description**

Allow a user to register with the service so that we identify them against the
annotations that they create. Allow them to login so that they can move between
devices. And reset their password if it's forgotten.

**Stories**

* As a user I would like to be able to log into my existing account so that I
  can CRUD annotations.
* As a prospective user I would like to be able to create a new account.
* As a user I would like to be able to reset my password so that I can still
  access my account if I forget my password.
* As a user I would like to be able to create an account using my access code
  so that I can claim my reserved username.
* As a logged out user that has made a highlight I would like to be able to
  finish creating the highlight after login so as not to lose my selection.
* As a logged out user when I switch on highlight mode, I would like it to
  remain enabled after logging in.

**Progress**

Iteration 1

- Login requires username/password
- Forgot password form sends an email
- Account creation requires username/email/password
- Username reservation and recovery
- Authentication flow restores in-progress annotation creation after login.
- Authentication flow ensures highlighter mode is enabled after login (when
    the button is clicked when logged out).

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/68)

### Highlighter Mode

**Description**

Allows a user to make quick annotations on a page without going through the
edit workflow. Essentially creating just the highlight.

**Stories**

- As a user I'd like to quickly be able to highlight text for reference.

**Progress**

Iteration 1

- Allow highlights to be created through a "highlight only mode".
- Highlights are always private.
- Highlights appear in the page viewer.

[Old GitHub Ticket](https://github.com/hypothesis/vision/issues/54)
