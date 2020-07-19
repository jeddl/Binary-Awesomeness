# Binary Awesomeness

## What Is This Project?
This is a [jekyll](https://jekyllrb.com/) project that is supported and can be hosted by `Github Pages`.

## How Does It Work?
[Here](https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll) is the instruction of how to get it to work.

__NOTE__:
1. `jekyll` is one way of building a Github hosting website. Pure markdown files also does the trick, but here I am only experimenting with `jekyll`. So be aware
that all the configuration listed here is in `jekyll` context.
2. The section that explains how to use `bundle` to create `jekyll` project is not accurate, where one might get a bunch of errors by just following
the `Github Pages` instruction. The best place to know how `bundle` and `jekyll` work is their websites, which are listed in the Github documentation as well.
The main goal here is, if building a personal website, to create a `jekyll` project at the root directory, NOT `/docs` on `master` branch. (Although `/docs`
on master branch or gh-pages branch should work as well by some specific configuration according to the `Github Pages` setup instruction. I had some trouble of
getting `/docs` on master branch to work since when I set the project name as `jeddl.github.io` as recommended, I was not able to select which directory is my
website root directory, unless I change my project name. But it might cause the routing incorrect)

## Potential Issues
I highly recommend that learn some basic knowledge of `Ruby` project, `bundler`, and maybe `jekyll` before jumping on it. The instruction from `Github Pages` seems
really straightforward, but there is a lot going on behind the scene.

One of the possible problem that you might be dealing with is the `gem`/`bundle` directory access problem. That normally if you install `Ruby` with `sudo` command,
and when you try to install `bundler`, it will keep stuff from your `/` directory, and you cerntainly do not want to contaminate your global environment. One of
the solutions would be running `gem install --user-install <gemname>` where `--user-install` will store gems in the `.gem/` from user directory.
