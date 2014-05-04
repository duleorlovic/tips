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

    dap}p switch two paragraph
    Repeat last colon command  @:  and @@
    :grep subject -R * --exclude-dir={log,spec,public,features,tmp,vendor,views,assets,db} -I
    Ctrl+p  # in insert mode is completing the string
    dE # removes to the End of the string
    daw removes the inner word
    yy
    :%s/old/new/gc
    mA then 'A jumb there, :marks gives the jump location, '' is last jump, '. jump and change
    :tabe file  open file in new tab, gt switch between tabs
    :vsp #1  vertically split window with file #1
    :on or Ctrl+W+o #closes all windord except current
    :buffers, :b1, :bun closes the buffer
    q: shows history of commands
    q/ shows history of searches
    5G or :5 goes to the line 5
    gg goes top, G goes bottom
    :args app/*/*  to add all files to arg list
    :argdo %s/foo/bar/ge | update   replace in all arg
    find /home/bruno/old-friends -type f -exec sed -i 's/ugly/beautiful/g' {} \;



Heroku 
===

Could not create resource with vendor, please try again later is a heroku problem, not ours.

Cucumber
===

@temp is shared between blocks

    require 'capybara/dsl'
    => true 
    include Capybara::DSL
    => Object 
    Capybara.default_driver = :selenium
    => :selenium 
    visit "http://google.co.uk"
    => "" 

Rspec
===

* https://www.relishapp.com/rspec/
* https://github.com/jnicklas/capybara
* https://github.com/cucumber/cucumber
* http://rubydoc.info/github/thoughtbot/shoulda-matchers/master/index
* https://github.com/thoughtbot/factory_girl
* let(:form) { mock_model(Form, :success_message => "Success message") }
* gem 'spork-rails' 

    spork --bootstrap 
    in spec/spec_helper.rb move everthing inside Spork.prefork
    add to .rspec --drb

* gem 'guard-rspec'

    guard init spork
    in Guard file on guard 'spork', :test_unit => false


* Do not depend on implementation https://www.youtube.com/watch?v=m3nMrWpIRKo use stub and mock, and check with integration test whole functionality
* should_receive can be before action, but response.should and flash.should have to be after
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

Rails
===

* folders in app/assets/* are hidden when you are accessing files, for example: @domain/assets/file.txt@ should be here app/assets/javascript/file.txt or app/assets/img/file.txt (last one overrides prev).

* All files from assets are provided but not all are included in all layouts (default is app/views/layouts/application.html.erb)
* comments like // *= require_tree . does not exclude it
* rake stats #shows number of code lines, tests ...

Ruby
===

    regular expression http://www.rubular.com/
    put -w for warning log https://github.com/bbatsov/ruby-style-guide
    lambda literal syntax is: method = ->(a, b) { a + b }
    lambda method for multi line blocks:
        method = lambda do |a, b|
          tmp = a * 7
          tmp * b / 50
        end
    if dont know if path is array use: 
        [*paths].each { |path| do_something(path) }

BASH
===

* find and remove files
    find . -type f -name "FILE-TO-FIND" -exec rm -f {} \;

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
