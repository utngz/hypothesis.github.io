Hypotheses Project
==================

This site contains documentation for the Hypothesis project. It's a Jekyll[1]
project hosted by GitHub using Github Pages[2] at http://project.hypothes.is/.

[1]: http://jekyllrb.com
[2]: https://pages.github.com

Creating Content
----------------

Check out the Jekyll documentation for more information.

Development
-----------

For local development we use the github-pages[1] gem to ensure we're running
the same stack as GitHub. To get the project running you'll need Ruby and the
bundler gem installed on your system. Then clone the repository:

    $ git clone git@github.com:hypothesis/hypothesis.github.io.git

Move into then newly cloned directory and install dependencies:

    $ cd hypothesis.github.io
    $ bundle

This will install the jekyll gem and various other libraries. To view the site
run:

    $ bundle exec jekyll serve

This will start a web server hosting a local version of the site. You can view
the site by visiting http://0.0.0.0:4000 in your browser.

This server will also watch the local files for changes and rebuild the site
each time a file is saved.

[1]: https://github.com/github/pages-gem

Dependencies
------------

As mentioned we use the github-pages gem for local development, we need to
ensure this is kept up to date with the current hosted version used by GitHub
so periodically it's useful to run:

    $ bundle update

Then if necessary commit the updated Gemfile.lock file.
