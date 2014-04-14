---
---
<link href="stylesheets/tips.css" rel="stylesheet"></link>
<link href="http://kevinburke.bitbucket.org/markdowncss/markdown.css" rel="stylesheet"></link>

You can find this on [http://duleorlovic.github.io/tips](http://duleorlovic.github.io/tips) or edit [https://github.com/duleorlovic/tips/blob/gh-pages/index.md](https://github.com/duleorlovic/tips/blob/gh-pages/index.md)


VIM
===

.vimrc http://vim.wikia.com/wiki/Example_vimrc


    set history=1000 " to save history between vim session
    wild tab, set wildmode=longest,list,full " this is for tab completion , to stop cycle press CTRL+E than tab
    :nnoremap gr :grep <cword> * -I -R --exclude-dir={log,spec,public,features,tmp,vendor,views,assets,db}<CR>
    :nnoremap gy :grep "<c-r>"" features/ spec/ -R -I<CR>
    :set hlsearch


Commands

- dap}p switch two paragraph
- Repeat last colon command and 
- :grep subject -R --exclude-dir



Heroku 
===

Could not create resource with vendor, please try again later is a heroku problem, not ours.

Cucumber
===

@temp is shared between blocks

Rspec
===

* https://www.relishapp.com/rspec/
* https://github.com/jnicklas/capybara
* https://github.com/cucumber/cucumber
* http://rubydoc.info/github/thoughtbot/shoulda-matchers/master/index
* https://github.com/thoughtbot/factory_girl

* Do not depend on implementation https://www.youtube.com/watch?v=m3nMrWpIRKo use stub and mock, and check with integration test whole functionality
* testing static pages: 

    subject { page } 
    shared_examples_for "all static pages" do
      it { should have_selector('h1', text: heading) }
    end
    describe "GET Home page" do
      before { visit root_path }
      let(:heading) { 'Home page' }
  
      it_should_behave_like "all static pages"
    end
    
* testing model validation:
    
    before do
      @user = User.new(name: "Example User", email: "user@example.com")
    end
    describe "when email is not present" do
      before { @user.email = " " }
      it { should_not be_valid }
    end


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
