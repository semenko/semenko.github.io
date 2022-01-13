# Personal Website

This repo is an amalgamation of a few forks. It's closest to [Leonid Keselman's site](https://github.com/leonidk/new_website), which uses [Jekyll Now](https://github.com/barryclark/jekyll-now) (a tweaked [Jekyll](https://github.com/jekyll/jekyll) template for GitHub blogs), combined with the crisp website design from [Jon Barron](https://jonbarron.info/). **You are free to use this for your own purposes**, but please respect my copyright for my personal material (images, PDFs, _posts, etc.).

## Getting Started
1. Create & clone your own `username.github.io` repository
2. Run `gem install GitHub-pages` -- this should install Jekyll and all the dependencies needed for GitHub Pages
3. Run `_make_thumbnails.sh` and `_make_favicon.sh` (note you may need to install `imagemagick`, e.g. `brew install imagemagick`)
4. In your repo, run `jekyll serve`
5. When your site looks nice, commit any changes and push your repo.


## Tips & Tweaks 
* Jekyll will try to build a full page for every post. This is skipped with `permalink: /`, which creates multiple entries in sitemap.xml for index.html.
