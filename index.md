---
---
<link href="//netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap.min.css" rel="stylesheet">
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="//netdna.bootstrapcdn.com/bootstrap/3.1.1/js/bootstrap.min.js"></script>
<link href="stylesheets/tips.css" rel="stylesheet">
  
<div class="navbar navbar-default navbar-fixed-top" role="navigation">
  <div class="container">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
    </div>
    <div class="navbar-collapse collapse">
      <ul class="nav navbar-nav">
        <li><a href="http://duleorlovic.github.io/tips">Home</a></li>
        <li><a href="#vim">Vim</a></li>
        <li><a href="#heroku">Heroku</a></li>
        <li><a href="#cucumber">Cucumber</a></li>
        <li><a href="#rspec">Rspec</a></li>
        <li><a href="#rails">Rails</a></li>
        <li><a href="#ruby">Ruby</a></li>
        <li><a href="#gems">Gems</a></li>
        <li><a href="#jekyll">Jekyll</a></li>
        <li><a href="#bash">Bash</a></li>
        <li><a href="#git">Git</a></li>
      </ul>
      <ul class="nav navbar-nav navbar-right">
        <li><a href="https://github.com/duleorlovic/tips/blob/gh-pages/index.md">Edit</a></li>
      </ul>
    </div><!--/.nav-collapse -->
  </div>
</div>

VIM
===


* **.vimrc** should be copied from  <http://vim.wikia.com/wiki/Example_vimrc> with this addidional lines
~~~
" override this from http://vim.wikia.com/wiki/Example_vimrc
set cmdheight=1  " 2 is to more
set number! " unset number

"custom 
execute pathogen#infect()
set history=1000 " to save history between vim session
nnoremap gr :grep <cword> * -I -R --exclude-dir={log,spec,public,features,tmp,vendor,views,assets,db}<CR> " grep current word
nnoremap gy :grep "<c-r>"" * --exclude-dir={log,public,tmp,vendor} -R -I<CR> " grep yanked word
set hlsearch
wild tab, set wildmode=longest,list,full " this is for tab completion , to stop cycle press CTRL+E than tab
set history=1000 " to save history between vim session
~~~

vim

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
    CTRL+^ (shift+6) jump to previous buffer  

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

* double('output').as_null_object ignore other messages (unexpected messages are recorded) so this will work:

      output.should_receive(:puts).with('Second guess:')

* let will create memoized local variable so you do not need @var

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

Migrations:

* if we call Products.update_all :fuzz => 'fuzzy' in migration, it will probably break in the future, because Products will be validated for something that we did not planned. Better is to create local **class Product < ActiveRecord::Base;end**, and call **Product.reset_column_information**
* To change class **fields_with_error** you can override ActionView::Base.field_error_proc in any controller
~~~
ActionView::Base.field_error_proc = Proc.new { |html_tag, instance|
  #html = %(<div class="field_with_errors">#{html_tag}</div>).html_safe
  # add nokogiri gem to Gemfile
  elements = Nokogiri::HTML::DocumentFragment.parse(html_tag).css "label, input"
  elements.each do |e|
    if e.node_name.eql? 'input'
      e['class'] ||= ''
      e['class'] = e['class'] << " error"
      html_tag = "#{e}".html_safe
    end
  end
  html_tag
}
~~~


Gems
===

get the country based on ip address: 

* https://github.com/alexreisner/geocoder, 
* http://rubygems.org/gems/geo_ip (instructions http://igotrailed.wordpress.com/2013/11/19/detecting-user-location-with-rails/)
* http://rubygems.org/gems/geoip (which can be downloaded as database http://dev.maxmind.com/geoip/legacy/geolite/) and have country code based on [iso3166](http://dev.maxmind.com/geoip/legacy/codes/iso3166/)
* https://github.com/scottwater/detect_timezone_rails or https://github.com/kbaum/browser-timezone-rails using jsTimezoneDetect

get locale based on country: https://github.com/grosser/i18n_data:

* country gem using currency gem to get currency https://github.com/hexorx/countries/
* Query perfomance analyser https://github.com/nesquena/query_reviewer

If there is an error *invalid byte sequence in US-ASCII* try to *export LANG=en_US.UTF-8* before installing a gem

For rvm put ```source ~/.bash_profile``` in your **~/.bashrc** file and you do not need to enable terminal settings to "Run command as login shell"

Ruby
===

* `p ["a", "b"].map(&:upcase)` is equivalent to `p ["a", "b"].map{|string| string.upcase}`
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

Jekyll
===

http://cheat.markdunkley.com/

Difference betweet page and post:

* Post file name contains the title and the date of the post. invalid date in the filename cause an error.
* Posts are Comparable objects, which means two posts can be compared. The comparison is made by the post date and the post slugs.
* The generated default relative url of Post and Page are different (eg. /2000/01/01/my-post.html and /about.html).
* Page can be placed anywhere but Post can only be placed under "_posts" folder.
* Post has more data out of the box for use in Liquid templates (title, url, date, id, categories, next, previous, tags, content).
* Posts has unique id.

Interesting plugins:

* search with js: http://10consulting.com/2013/03/06/jekyll-and-lunr-js-static-websites-with-powerful-full-text-search-using-javascript/
* another js search: https://github.com/mathaywarduk/jekyll-search
* 

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
  
see all the changed code

    git log -p

Show file at specific revision

    git show HEAD~4:index.html
    
Versioning [SEMVER](http://semver.org/)

If there is two accounts on bitbucket or github with different keys use `.ssh/config` file

    Host secure.bitbucket.org
      Hostname bitbucket.org
      IdentityFile ~/.ssh/id_rsa_secure

    Host test.bitbucket.org
      Hostname bitbucket.org
      IdentityFile ~/.ssh/id_rsa_test
~                                 

