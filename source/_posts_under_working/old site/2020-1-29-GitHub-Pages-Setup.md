---
layout: post
title: Building personal blog with GitHub Pages, Jekyll and AMP
date: 2020-1-29 14:00:00
tags: Code Web
categories: OIer
author: ryan

---
Last Update: 20 Oct 2020

I built this Blog with Jekyll, GitHub Pages and AMP (see links at footer). The basic framework is based upon template hanuman, yet significant modifications are made. In this note, I share the basics of using these tools to build and customize your own website. This note is very friendly for starters.

## Connecting to GitHub with SSH
You can check your local SSH key through entering the folder `cd ~/.ssh`.

If it returns "No such file or directory", it simply means you have not yet used Git.

To generate a new SSH key, type `ssh-keygen -t rsa -C "YOUREMIAL"`.

You may change the default file (~/.ssh/id_rsa) and setup a passcode (to stop others from messing up with your project) at this stage. Now, copy the key from `vim ~/.ssh/id_rsa.pub`
<!-- `cp ~/.ssh/id_rsa.pub /c/Users/User_Name/Desktop/` -->

and go to "Settings -> SSH and GPG keys -> New SSH key" (on your GitHub account) and add this key. Once this is done, you may check the connection with `ssh -T git@github.com`

and enter "yes" to continue connecting. If it returns that you have successfully authenticated, you may proceed to setup user information

`git config --global user.name "USERNAME"`

`git config --global user.email  "EMAIL"`

The [GitHub Help](https://help.github.com/en) provides many useful debug information and the two most relevant ones are [Connecting to GitHub with SSH](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh) and [Error: Permission denied (publickey)](https://help.github.com/en/github/authenticating-to-github/error-permission-denied-publickey).

## Creating your Blog
To start, you have to create a new repository with the name *UserName.github.io*. Make sure that you are using exactly the name with your GitHub username and the correct suffixes. The website will not work if you type the wrong repository name.

Now, go to **settings** and you will find **GitHub Pages** under **Options** (just rolling down). Some simple themes are provided here and you may choose a one you like. Once this is done, you may go to "https://UserName.github.io" and you will see you new website!

To start building, you need to edit _index.md_ to customize your **main page**. By adding other _subpage_name.md_ and link it to the main page in _index.md_. Note that _index.md_ is the DEFAULT file for main page, but you can name subpages as you wish.

However, you may find these predefined themes not satisfactory and want a more fancy website. My recommendation is to use [Jekyllrb](https://jekyllrb.com/), which provides a fantastic way to build [static website](https://en.wikipedia.org/wiki/Static_web_page) with GitHub Pages. It would be way too time-consuming if you start building everything from ground by yourself and this is usually necessary.

To find an ideal template, you can either search on GitHub or go to [Jekyll Themes](http://jekyllthemes.org/), which provides versatile nice themes. Of course, you won't find the perfect template for your website, thus, we would like to customize the template.

Depending on the themes you chosen, it may require you to have some basic knowledge of HTML, CSS, Jekyll or AMP. However, don't be panic if you never heard any one of them. In the following, I will walk you through these processes with an example ["hanuman"](https://github.com/samanyougarg/hanuman).

## Customize your Blog - "hanuman" as an exmaple
As I really do not like the origin navigation bar, I replaced it with this template from [AMP Start](https://www.ampstart.com/components#navigation).

Also, to manage the notes, I create several subpages classifying the note using given catalog indices, which are different from the Tags. You may check the assets folder for more information.

Customer domain -- Note add on 20 Oct 2020

Recently, I have registered a new domain "qisland.org" with [Google Domains](https://domains.google) and I'm surprised that the ".org" was open to public years ago. To use a customer domain, you simply need to follow two steps:

1. Create a file "CNAME" in your GitHub page repo and input the customer domain, which is usually somehting like "xxx.ur_domain" in my case.

2. Add a new resource record in DNS of your domain. Input record type "CNAME", name "xxx" and data (or domain name) your GitHub page address (zzz.github.io). You may leave the TTL as default.

After completing the two steps, you should be ready to go! Note that you can also select the "Enforce HTTPS" option under "Settings" to serve your GitHub page over HTTPS but it takes around 24 hours before you can enforce the secure protocol. If something goes wrong, you can always refer to [this site](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site) for more information as well as troubleshooting.

## Latex support
It is usual to write complex math expressions with latex when we are talking about physics or machine learning. However,
GitHub flavored Markdown (GFM) does not support Latex anymore. There are two ways to resolve this problem.

The first one is to use online latex editor and embed it. [CodeCogs](https://www.codecogs.com/latex/eqneditor.php) is good choice and you write it either as Markdown `![](http://latex.codecogs.com/gif.latex?\\frac{1}{1+sin(x)})` or HTML `<img src="http://latex.codecogs.com/gif.latex?\frac{1}{1+sin(x)}" />`. Note that the number of '\\' is different.

The second one with **MathJax** is also my personal choice, which allows you to write equations with "$$", just as in any Latex editor. To do this, we need to
1. Set Build settings in __config.yml_ as `markdown: kramdown`
2. Adding the following code to your header (or the specific page file if you don't want to slow down the loading process of your entire website)

```html
<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>
```

The MathJax configuration can be changed as you need. When using MathJax in markdown, the supported methods might be different from those you are used to. Please refer to this [StackExchange Math page](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference) for supported syntax.

### Reference - Git
- [git - 简易指南](https://www.bootcss.com/p/git-guide/index.html)
- [Git 基本操作](https://www.runoob.com/git/git-basic-operations.html)
- [git 高级用法小抄](https://segmentfault.com/a/1190000021643071)
   
### References - GitHub Pages
- [GitHub Pages - Official Site](https://pages.github.com/)
- [利用Github免费搭建个人主页(个人博客)](https://blog.csdn.net/hitwhylz/article/details/42646197)
- [Git+GitHub+Markdown+Jekyll=Perfect Personal Blog ](https://www.devtalking.com/articles/git-gitHub-markdown-jekyll/)

### Refernece - Jekyll
- [jekyllrb](https://jekyllrb.com/)

### Reference - HTML and CSS
- [W3 School](https://www.w3schools.com/)
- [HTML color code](https://www.w3schools.com/colors/colors_groups.asp)

### Reference - AMP
- [AMP Dev](https://amp.dev/)

### Reference - Latex in GitHub flavored Markdown
- [Full GFM grammar](https://github.com/guodongxiaren/README)
- [stackoverflow](https://stackoverflow.com/questions/26275645/how-to-support-latex-in-github-pages)
- [github上Markdown不支持LaTeX吗？](https://www.zhihu.com/question/26887527)
