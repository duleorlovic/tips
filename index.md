---
title: "OK"
---
<link href="stylesheets/tips.css" rel="stylesheet"></link>
<link href="http://kevinburke.bitbucket.org/markdowncss/markdown.css" rel="stylesheet"></link>

You can find this on [http://duleorlovic.github.io/tips](http://duleorlovic.github.io/tips) or edit [https://github.com/duleorlovic/tips/blob/gh-pages/index.md](https://github.com/duleorlovic/tips/blob/gh-pages/index.md)

VIM
===

    .vimrc
    http://vim.wikia.com/wiki/Example_vimrc
    set history=1000 " to save history between vim session
    wild tab, set wildmode=longest,list,full " this is for tab completion , to stop cycle press CTRL+E than tab
    
    Repeat last colon command  @:  and @@
    :grep subject -R * --exclude-dir={log,spec,public,features,tmp,vendor,views,assets,db} -I
    :nnoremap gr :grep <cword> * -I -R<CR>
    
    :set hlsearch
    Ctrl+p  # insert modu radi completion
    ciw
    dE
    yy
    :%s/old/new/gc
    mA i 'A ili `A ili :marks #dva puta ' skace na zadnju lokaciju, a '. zadnje menjano
    :tabe file  i gt
    :vsp #1
    :on ili Ctrl+o #closes all windord except current
    :buffers i :b1 i  :bun
    q: i q/
    5G, gg
    :cw ili :ccl

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
    
Wercker
===

Some notes when you are creating new step for wercker registry.

Since variables that you are using in run.sh are $WERCKER_[stepi-name]_[property-name], they should be renamed to [property-name] just for that user can easily recognize them. For example, env variable PASSWORD in my step is WERCKER_FTP_DEPLOY_PASSWORD and I am using it in script as PASSWORD=$WERCKER_FTP_DEPLOY_PASSWORD
build and deploy are completely separated. WERCKER_OUTPUT_DIR of build process is copied to WERCKER_SOURCE_DIR of deploy process. That is only way to pass data.
to test run.sh on local computer, you can use "function success() { echo "$@";}" and export them with "export -f success debug fail" . run.sh should start with "#!/bin/sh" because wercker is using sh . Export like this:
export WERCKER_FTP_DEPLOY_DESTINATION=ftp://domain/public_html
export WERCKER_FTP_DEPLOY_USERNAME=webdesign
export WERCKER_FTP_DEPLOY_PASSWORD=password
export WERCKER_CACHE_DIR=~/Downloads

function success() { echo "$@";}
function debug() { echo "$@";}
function fail() { echo "$@";exit 1;}
export -f success debug fail
wercker variables:
$WERCKER_GIT_COMMIT  sha
$WERCKER_GIT_BRANCH master
$WERCKER_OUTPUT_DIR /pipeline/output
$WERCKER_SOURCE_DIR /pipeline/build
$WERCKER_CACHE_DIR /cache
but for step from wercker registry this is different
