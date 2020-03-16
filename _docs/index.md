---
title: Welcome
permalink: /docs/home/
redirect_from: /docs/index.html
---





## News 

```
* 02.03.2020: Added three new data sets from [29].
* 14.01.2020: Added twenty-four new data sets from [24].
* 28.08.2019: Added twenty-two new data sets from [28].
* 09.07.2019: Added two new data sets from [27].
* 23.10.2018: Added five new data sets from [26].
* 13.02.2018: Added Cuneiform data set from [25].
* 11.05.2017: Added twelve new data sets from [24].
* 17.06.2016: Added Synthie data set from [21].
* 10.05.2016: Added eight new data sets from [16].
* 19.04.2016: Added FRANKENSTEIN data set from [15].
* 13.04.2016: Added SYNTHETICnew data set from [3,10].
* 08.04.2016: Added six new data sets from [14].

```


testmfldsfjkdl;fkjsfl;sdjkfl;sdkfjl;kjf;dkf;ldsfksdl;fksdl;fsdkfl;dskfsd;lfkds

[GitHub Pages](https://pages.github.com) can automatically generate and serve the website for you.
Let's say you have a username/organisation `my-org` and project `my-proj`; if you locate Jekyll source under `docs` folder of master branch in your repo `github.com/my-org/my-proj`, the website will be served on `my-org.github.io/my-proj`.
The good thing about coupling your documentation with the source repo is, whenever you merge features with regarding content to master branch, it will also be published on the webpage instantly.

1. Just [download the source](https://github.com/aksakalli/jekyll-doc-theme/archive/gh-pages.zip) into your repo under `docs` folder.
2. Edit site settings in  `_config.yml` file according to your project. !!! `baseurl` should be your website's relative URI like `/my-proj` !!!
3. Replace `favicon.ico` and `assets/img/logonav.png` with your own logo.

## Writing content

### Docs

Docs are [collections](https://jekyllrb.com/docs/collections/) of pages stored under `_docs` folder. To create a new page:

**1.** Create a new Markdown as `_docs/my-page.md` and write [front matter](https://jekyllrb.com/docs/frontmatter/) & content such as:

``
---
title: My Page
permalink: /docs/my-page/
---

Hello World!
```

**2.** Add the pagename to `_data/docs.yml` file in order to list in docs navigation panel:

```
- title: My Group Title
  docs:
  - my-page
```

### Blog posts

Add a new Markdown file such as `2017-05-09-my-post.md` and write the content similar to other post examples.

### Pages

The homepage is located under `index.html` file. You can change the content or design completely different welcome page for your taste. (You can use [bootstrap components](http://getbootstrap.com/components/))

In order to add a new page, create a new `.html` or `.md` (markdown) file under root directory and link it in `_includes/topnav.html`.

| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |

R(N) are regression datasets with N tasks per graph.