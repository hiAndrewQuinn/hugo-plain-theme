# hugo-plain-theme
Minimum viable Hugo. No CSS, no JS. HTML only. Instructions on how to generate in the README.

![](example.gif)

4 out of 5 web devs have experienced the following:

1. _"Wow, Hugo sounds amazing! Let me try it out!"_
2. _"Okay, I made a new theme and a brand new page of Markdown in `content/`!!"_
3. _"Running `hugo server -D` now!!! ... Where is it!!!!"_

For whatever dumb fucking reason, Hugo, despite being an excellent static site generator for literally any other use case, makes it _unreasonably difficult_ to get a **single page of unformatted, uncomplicated, HTML** serving to your `localhost`.

We're going to fix that. **From scratch.** Below is the _absolute simplest explanation_ of how you get 

## Quickstart: Build your own `hugo-plain-theme` from scratch

```bash
# Start a new site, with Hugo.
hugo new site .

# Make a new theme. Tell Hugo we want to use this new theme.
hugo new theme hugo-plain-theme
echo "theme = 'hugo-plain-theme'" >> config.toml

# GOTCHA 1: Hugo doesn't start with any HTML content at all. So we will make some.
hugo new _index.md
echo "Lorem ipsum dolor sit amet" >> content/_index.md

# VERY IMPORTANT: TELL hugo to SERVE CONTENT for your "index.html" template.
# Why the index.html template is left BLANK BY DEFAULT so you see NOTHING BY DEFAULT
# even if you somehow happen upon learning the post has to be named "_index.md" 
# is beyond me.
echo "{{ .Content }}" >> themes/hugo-plain-theme/layouts/index.html

# Serve the site, with drafts on. You should see it now.
hugo server -D
```

# Or... use this very repo as a submodule instead
```bash
# You can't use submodules unless you're already using git. So let's start with that.
git init

# Start a new site, with Hugo.
# --force is necessary because `git init` put stuff in here,
# but hugo normally expects an empty folder.
hugo new site . --force

# Pull this repo in as a submodule.
cd themes/
git submodule add https://github.com/hiAndrewQuinn/hugo-plain-theme.git
cd ..

# Tell Hugo we want to use the plain theme.
echo "theme = 'hugo-plain-theme'" >> config.toml

# GOTCHA 1: Hugo doesn't start with any HTML content at all. So we will make some.
hugo new _index.md
echo "Lorem ipsum dolor sit amet" >> content/_index.md

# Serve the site, with drafts on. You should see it now.
hugo server -D
```