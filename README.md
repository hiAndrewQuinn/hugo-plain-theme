# hugo-plain-theme

Minimum viable Hugo. No CSS, no JS. HTML only. Instructions on how to generate in the README.

![An animated GIF of running through the 'build from scratch' source code, just to show it works exactly as-is.](https://user-images.githubusercontent.com/53230903/178942076-edea1ce5-2b09-4ba7-bc1c-5a686a6590c7.gif)



4 out of 5 web devs have experienced the following:

1. _"Wow, Hugo sounds amazing! Let me try it out!"_
2. _"Okay, I made a new theme and a brand new page of Markdown in `content/`!!"_
3. _"Running `hugo server -D` now!!! ... Where is it!!!!"_

For whatever reason, Hugo, despite being an excellent static site generator for literally any other use case, makes it _unreasonably difficult_ to get a **single page of unformatted, uncomplicated, HTML** serving to your `localhost`.

We're going to fix that. **From scratch.**

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

### [See it in action: A live example website generated from following those instructions exactly and nothing else](https://github.com/hiAndrewQuinn/hugo-plain-theme-example)

_Want to brush up on your theory?_

- [Bryce Wray](https://www.brycewray.com/about/)'s ["Really getting started with Hugo"](https://www.brycewray.com/posts/2022/07/really-getting-started-hugo/) goes into even more detail on what Hugo used to be like, and how to keep things simple with it today, without even touching themes.
- [zwbetz](https://zwbetz.com/)'s ["Make a Hugo Blog from Scratch"](https://zwbetz.com/make-a-hugo-blog-from-scratch/) takes you all the way from `hugo new site` to [a fully-fleshed out vertical slice of a blog](https://make-a-hugo-blog-from-scratch.netlify.app/).

## Or... use this very repo as a submodule instead

![Animated GIF of running the script below to add this repo as a submodule to a new Hugo site and then deploy it.](https://user-images.githubusercontent.com/53230903/178942209-abb0c319-7c69-47d6-990b-0f9f9ac4e1f4.gif)


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

There is **one big benefit** to using this as a submodule - and that's that it actually comes with **HTML comments in the rendered pages** to let you know exactly which layouts were pulled in, where.

So, for example, when I use this theme to build out [`build-100-websites.fun`](https://build-100-websites.fun), I can open the source code of any page generated with this theme and see comments for where the layouts begin and end:

![An example of an HTML comment, telling you that the HTML code rendered below was templated by the file stored in `themes/hugo-plain-themes/layouts/index.html`.](https://user-images.githubusercontent.com/53230903/178942290-3adb07cd-d08a-4ea3-96ed-cd0c5896582b.gif)


For someone who is totally new to Hugo, I think these simple guidepost comments will prove invaluable.

## Deploying to Netlify: Things to check

- [ ] Did you **add the theme as a proper submodule**? Netlify will complain if you give it nested Git repos which aren't in a submodule relationship to one another.
- [ ] Did you **set `drafts` to `False`** for `content/_index.md`? If you didn't, you'll likely still get a blank white screen, with the only HTML in there being a pair of empty `<pre></pre>` tags.
- [ ] Did you **use `hugo --gc --minify`** for your build command? Both flags will save you some space, but `--gc`, I think, strips out the HTML comments the submodule provides.
