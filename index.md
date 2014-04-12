---
title: "OK"
---
<link href="stylesheets/tips.css"></link>
<link href="http://kevinburke.bitbucket.org/markdowncss/markdown.css" rel="stylesheet"></link>

You can find this on [http://duleorlovic.github.io/tips](http://duleorlovic.github.io/tips) or [https://github.com/duleorlovic/tips/blob/gh-pages/index.md](https://github.com/duleorlovic/tips/blob/gh-pages/index.md)

GIT
===

track remote branch if we did not have this branch already

    git checkout -t origin/branch
    
push branch and track

    git push bitbucket development:development
  
Getting existing git branches to track remote branches:  

    git branch --set-upstream gh-pages-bitbucket bitbucket/gh-pages 
    
Git child commit reference with

    git log --reverse --ancestry-path 894e8b4e93d8f3^..master
    
Git stash only unstaged changes

    git stash --keep-index
    
Git checkout previous branch

    git checkout -
  
see all the changed cod

    git log -p
