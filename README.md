# Hacker's Society Wiki

### Contributing:

All non-sensitive information documentation is welcome here.  The goal of this
wiki is to document the things we have done, or are currently running.  Because
Hacker's Society is a student organization, the group will have entirely new
members approximately every four years.  To help prevent things from getting
lost in the transitions, this wiki was made.

If you'd like to contribute, you have two options:

- If you have push access to this repository, please create a separate branch,
  make all your changes there, and then create a pull request.
- If you do not have push access, please fork the repository, make changes in
  your fork, and then create a pull request.

### Compiling:

This wiki is made using `Sphinx` documentation.  To build the wiki, you must
first [install Sphinx](http://sphinx-doc.org/).  After `Sphinx` has been
installed, issuing a `make html` will generate the HTML seen at
[http://hacsoc.org/wiki/](http://hacsoc.org/wiki/).  Here are some annotated
Bash commands for getting things installed and generating HTML on Linux:

```bash
# Install Sphinx and theme in a virtualenv:
$ virutalenv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
# Each time you'd like to generate documentation:
$ make html
# Generated files will be under _build/html
```

For syntax help, see [here](http://sphinx-doc.org/rest.html).  The syntax used
is ReStructured Text, not MarkDown.

**Please Note:** The `push.sh` script is not for your consumption!  Do not use
it or modify it unless you completely understand everything that goes into the
Travis-CI setup (documented below).

### Travis-CI

This wiki works by combining Sphinx, [Travis-CI](https://travis-ci.org), and
GitHub Pages.  When a commit hits master, here's what happens:

1. Travis-CI creates a VM/container and checks out the latest commit within it.
2. Travis runs Sphinx to create the documentation.
3. Travis clones the `gh-pages` branch.
4. Travis copies the generated documentation into the `gh-pages` branch, and
   commits new changes.
5. Travis pushes these changes back to this repository.
6. GitHub Pages registers the update to `gh-pages` and deploys to
  `hacsoc.org/wiki`.

This process takes about 5 minutes in total.

A few notes on this process:

- `push.sh` is run by Travis to copy and push updates to the `gh-pages` branch.
  In order to have the credentials to push to this repo, Travis requires an
  encrypted access token (this is located in the `.travis.yml` file).  The
  access token was generated under Stephen Brennan's account.
- The Travis machinery was set up by Stephen Brennan, and the process is mostly
  documented in
  [this Gist](https://gist.github.com/brenns10/f48e1021e8befd2221a2).
- The Travis control panel is located
  [here](https://travis-ci.org/hacsoc/wiki).  Only members of the Wiki team in
  the Hacsoc organization may access it.  **Don't touch it unless you know what
  you're doing!**  The settings are probably set that way for a reason.
