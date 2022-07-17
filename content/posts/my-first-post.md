---
title: "This Static Website"
date: 2022-07-13T11:51:15-05:00
draft: false
---
*Update: I have since switched to using Github Actions[^1]. See my post [here](/github-actions/) for the details. This way can still serve many people however, so this post will remain. What I like about using Github Actions is that it enables me to more easily update this site on the go.*

This is a simple static website as a portfolio of my work and interests.
I wanted to create a legitimate website and not only use social media (although I want to start using Twitter and Soundcloud too).

The following approach worked for me but I know it is also fairly technical.
There are many managed approaches to creating a website that are pretty cheap and do not require technical skills.
I stumbled upon blot.im[^2] for example. It is only a few dollars a month and reduces making a website to putting files in a folder.

For this website however, I decided to use Hugo[^3] and my Github account with Github Pages[^4]. Hugo is a simple static website generator written in the Go programming language.
Github Pages is a way of turning your repository named ``username.github.io`` into a static website with that same URL.
It is a fast and easy enough workflow for me and only Markdown[^5] is needed to edit posts. Additionally, this is all free (meaning there is no cost).
The skills required to do this are a proficiency with git version control[^6] and using command line tools in general.

For themeing, as of this writing, I am using the etch[^7] theme which I chose for its absolute simplicity.
I really want the site to be focused on content and this theme is great at staying out of the way.

Tools Recap:

* Git, Github Repositories and Github Pages (for version control and hosting)
* Markdown Editor for posts (Apostrophe[^8], Marker[^9] or VS Code[^10] for example)
* Hugo to generate the website

I did this on a GNU/Linux system installed on an old HP Stream laptop. I installed Hugo with Snap[^11] since it is the latest version.
Git can be installed from your Linux distributions package repository in the usual way. The same or similar procedures should work with Windows or MacOS.
But basically, with these tools one can create a user website via a repository in Github called ``username.github.io`` (which is also the website URL).
This is then used as a submodule to your Hugo project repository (``username.generator`` in my case). The theme is also a submodule in case it gets updated upstream.
Using this approach keeps everything clean and version controlled: you can always roll back if your website breaks.

Here is a tree of the directory/repository structure:

    ~/Public/adrochoa.generator$ tree -d -L 2
    .
    ├── adrochoa.github.io
    │   ├── about
    │   ├── categories
    │   ├── css
    │   ├── my-first-post
    │   ├── posts
    │   └── tags
    ├── archetypes
    ├── content
    │   ├── about
    │   └── posts
    ├── resources
    │   └── _gen
    └── themes
        └── etch

``etch``, ``adrochoa.github.io`` and ``adrochoa.generator`` are separate repositories.
Using the submodule approach, the outer repository, ``adrochoa.generator`` commits the commit hashes of the subrepositories, but not the content.
The inner repositories, ``etch`` and ``adrochoa.github.io``, are independent of any other repository as far as Git is concerned.
We never directly modify ``adrochoa.github.io`` or ``etch``: Hugo will modify ``adrochoa.github.io`` for us based on our Markdown file posts and we leave themeing to the etch folks.
So once this is set up, we only need to edit some Markdown and run Hugo in the command-line.
Then we just commit and push everything. Github Pages will render the update. Here are some links with more details on these tools and the nuts and bolts of this approach.

[^1]: [https://github.com/features/actions](https://github.com/features/actions)
[^2]: [https://blot.im/](https://blot.im/)
[^3]: [https://gohugo.io/](https://gohugo.io/)
[^4]: [https://pages.github.com/](https://pages.github.com/)
[^5]: [https://www.markdownguide.org/](https://www.markdownguide.org/)
[^6]: [https://git-scm.com/](https://git-scm.com/)
[^7]: [https://github.com/LukasJoswiak/etch](https://github.com/LukasJoswiak/etch)
[^8]: [https://gitlab.gnome.org/World/apostrophe](https://gitlab.gnome.org/World/apostrophe)
[^9]: [https://fabiocolacio.github.io/Marker/](https://fabiocolacio.github.io/Marker/)
[^10]: [https://code.visualstudio.com/](https://code.visualstudio.com/)
[^11]: [https://snapcraft.io/hugo](https://snapcraft.io/hugo)
