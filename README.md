# robomimic project website

This repository contains the code for the robomimic project website, which can be found at https://arise-initiative.github.io/robomimic-web/

## Serving website locally

Make sure you have a valid ruby installation. Use the reference Gemfile `ref_Gemfile` to create a local Gemfile, and then build.
```sh
$ cp ref_Gemfile Gemfile
$ bundle install
$ bundle exec jekyll serve
```

## Updating docs folder using sphinx-generated docs

First, generate docs using the Makefile in `robomimic/docs`, which should result in the folder `robomimic/docs/_build/html`. 
Copy the contents of this folder into `robomimic-web/docs`, then, rename `docs/_static` to `docs/static` and update all 
html references in the `docs` folder to point to `static` instead of `_static`. Do the same for `_images` , and `_sources`. You may also
need to copy additional images from `robomimic/docs/images` into that folder as well, and remove an existing `_images` folder.
