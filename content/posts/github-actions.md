---
title: "Github Actions"
date: 2022-07-13T05:49:35-07:00
draft: false
---
*To see an earlier method I used that relies more heavily on git and submodules, see my first post [here](/the-elements-of-this-static-website/).*

I have recently switched workflows to utilize Github Actions [^1].
There are many Github Actions that can be performed on a repository.
For this website, I am using actions from Shohei Ueda aka peaceiris [^2].
Specifically, I use ``actions-gh-pages`` and ``actions-hugo``.
These are absolutely fantastic for my workflow since it enables me to more easily modify and post from my iPhone on the go by using iSH [^3], which provides a GNU/Linux-like shell terminal complete with git, text editors and other command line goodies.
The action is defined as YAML file in a branch in the git repository on which you would like to do something with.
Actions can do many things including running build jobs, creating new branches and pull requesting branches.
Additionally one could run tests, automating an entire continuous integration, continuous development (CI/CD) process.
The action described here is relatively simple compared to what is possible though.
Basically, I ditch the old setup with a single repository, ``username.github.io``.
The ``source`` branch contains the necessary Hugo folder configuration described in [my first post on creating this static website](/the-elements-of-this-static-website/).
The ``main`` branch still has the Hugo-generated HTML files for the static site.
Additionally, there is a ``gh-pages`` branch that stages any newly pushed content which is automatically pull requested to ``main``.
The one caveat with this setup is that the ``source`` branch is somewhat unrelated to the other branches which contain the content but this is a small sacrifice for the convenience that this workflow brings.
In my source branch is the following YAML:

    #.github/workflows/gh-pages.yml
    name: github pages

    on:
      push:
        branches:
          - source  # Set a branch to deploy

    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v2
            with:
              submodules: true  # Fetch Hugo themes (true OR recursive)
              fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

          - name: Setup Hugo
            uses: peaceiris/actions-hugo@v2
            with:
              hugo-version: 'latest'
              extended: true

          - name: Build
            run: hugo

          - name: Deploy
            uses: peaceiris/actions-gh-pages@v3
            if: github.ref == 'refs/heads/source'
            with:
              github_token: ${{ secrets.GITHUB_TOKEN }}
              publish_dir: ./public


[^1]: [https://github.com/features/actions](https://github.com/features/actions)
[^2]: [https://github.com/peaceiris](https://github.com/peaceiris)
[^3]: [https://ish.app/](https://ish.app/)
