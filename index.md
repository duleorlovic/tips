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
        <li><a href="#javascript">Javascript</a></li>
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

Javascript
===

* [document ready](http://learn.jquery.com/using-jquery-core/document-ready/) can be detected in `$(document).ready(function(){})` or because ready can be used [only on current document](http://www.w3schools.com/jquery/event_ready.asp) selector is not needed `$(function(){});`
* when `<a></a>` does not have href that it will not follow thelink so you do not need to preventDefault. Use this for toggling some part
* `hover` on mobile devices does not work what is expected. It stays in hover state until the user press (click) on the screen next time.
* for popups with buttons, if you want to close popup clicking anywhere outside button, button should not be included in background div to clearly separate when popup should be closed. if it is inside we can workaround with targeting more specifically and stop propagation `$('#letsdoit').click( function(e) { e.stopPropagation();});`
* in rails-ujs click on links with remote:true is not efected with e.preventDefault()
* detect browsers version

    function is_uiwebview(){
      return /(iPhone|iPod|iPad).*AppleWebKit(?!.*Safari)/i.test(navigator.userAgent);
    }
    function is_android(){
      return /Android/i.test(navigator.userAgent);
    }
    function is_idevice(){
      return /(iPhone|iPod|iPad)/i.test(navigator.userAgent);
    }
    
* detect browser type in rails

    def is_android?                                                                           
      request.user_agent =~ /Android/i                                                        
    end                                                                                       
                                                                                              
    def is_iphone_app?                                                                        
      request.user_agent =~ /(iPhone|iPod|iPad).*AppleWebKit(?!.*Safari)/i                    
    end                                                                                       
                                                                                              
    def is_idevice?                                                                           
      request.user_agent =~ /(iPhone|iPod|iPad)/i                                             
    end                                                                                       
                                                                                              
    def is_iphone?                                                                            
      request.user_agent =~ /(iPhone|iPod)/i                                                  
    end                                                                                       
    
    


iSO android and other mobile phone
===

* fadein and fadeout does not work well on mobilephone iOS android, its better to use display: block, display: none
* click event [does not work on iOS](http://stackoverflow.com/questions/3705937/document-click-not-working-correctly-on-iphone-jquery) and element is not clicable. simple solution is to add style: "cursor: pointer".

VIM
===


* **.vimrc** should be copied from  <http://vim.wikia.com/wiki/Example_vimrc> with this addidional lines

~~~
" override this from http://vim.wikia.com/wiki/Example_vimrc
set cmdheight=1  " 2 is to more
set number! " unset number

"custom 
execute pathogen#infect()
" to save history between vim session
set history=1000
" grep current word
nnoremap gr :grep <cword> * -I -R --exclude-dir={log,spec,public,features,tmp,vendor,assets,db}<CR>
" grep yanked word
nnoremap gy :grep "<c-r>"" * --exclude-dir={log,public,tmp,vendor} -R -I<CR>
set hlsearch
" this is for tab completion , to stop cycle press CTRL+E than tab
set wildmode=longest,list,full
~~~

vim

Commands

    dap}p switch two paragraph
    Repeat last colon command  @:  and @@
    :grep subject -R * --exclude-dir={log,spec,public,features,tmp,vendor,assets,db} -I
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
    :set tabstop=2 shiftwidth=2 expandtab # set configuration
    retab # this will actually reformat all source
    `"+y` copy visual selection to system clipboard, ubuntu should run `sudo apt-get install vim-gtk`

Heroku 
===

Heroku problems that we shold not care
* `Could not create resource with vendor, please try again later`
* `Launching... Push failed: could not store slugis a heroku`

To prevent heroku from sleep, add scheduler on every hour: `rake dyno_ping --trace`, and in lib/tasks/dyno_ping.rake

```
desc "Ping"
task :dyno_ping do
#  require "net/http"  # uncomment on ruby 2.0
  uri = URI("http://time-tracklng.herokuapp.com/");
  Net::HTTP.get_response(uri)
end

```

Cucumber
===

* `@temp` is shared between blocks
* pause can be implemented with: `STDIN.getc`

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

* folders in app/assets/* are hidden when you are accessing files, for example: `localhost:3000/assets/file.txt` should be here `app/assets/javascript/file.txt` or `app/assets/img/file.txt` (last one overrides prev). In production files that are listed in application.css.erb would be served as part of application.css, but all other files are served as is on their locations. 
* to undo `rails generate model survey` you can call `rails destroy model survey`
* All files from assets are provided but not all are included in all layouts (default is `app/views/layouts/application.html.erb`)
* comments like `// *= require_tree` . does not exclude it
* `rake stats` shows number of code lines, tests ...
* [debugging tools](http://guides.rubyonrails.org/debugging_rails_applications.html): finish (up backtrace function)
* rendering views instead of writing js partials http://stackoverflow.com/questions/16328472/rails-render-a-view-not-a-partial-from-within-a-view
* in views, render "something" will render partial _something, render "controller/something" will render template, render :partial => 'contr/something' will render partial
* render @products, will render partial _product with local variable product
* to run production version follow this

   RAILS_ENV=production rake db:setup
   RAILS_ENV=production rake assets:precompile
   rails s -e production
   rails c production
   
* you can use `raw` or `.html_safe` but it is advised to use [`sanitize`](http://apidock.com/rails/ActionView/Helpers/SanitizeHelper/sanitize) with it to strip script tags
* for ajax actions (links with remote:true) it should be implemented both, JS and  HTML version, since user can use right click on in new tab for that links
* if you have ajax links, it is advisable to implement notification in case of error since ajax error tends to be silent.

    // ajax error handling, currently only for debugging                                        
    LOG && $(document).on('ajax:error', '[data-remote]', function(e, xhr, status, error) {      
      LOG && console.log("ajax:error [data-remote] e.target="+e.target+" status="+status+" error="+error);
      //disable eventual popups so user can see the message                                     
      $('.active').removeClass('active');
      flash_alert("Please refresh the page. Server responds with: \"" +status+ " " + error + "\".");
    });

* [turbolinks](https://github.com/rails/turbolinks) loads new page, replaces body and title, and use pushState. Any javascript is run after replacement so you can reference all elements in <script> tags on the beggining of the page (if you really want to). [Execution order](http://stackoverflow.com/questions/8996852/load-and-execute-order-of-scripts) of non dymanically (defer or async) script are the same as they appear on the page (inline script is halted until external is loaded).  But with turbolinks, execution is done after replacing, but before external script are loaded, so you probably can not have javascript_include_tag inside a view, because the code it provides will be available after all script on a page is done

## Active record

* Assigning an object to a [belongs_to](http://guides.rubyonrails.org/association_basics.html#belongs-to-association-reference) association does not automatically save the object. It does not save the associated object either.
* you can specify order for association: `has_many :educations, -> {order 'graduation_year DESC'}, :dependent => :destroy`
* instead of `has_many :applied_jobs, through: :applications, source: :job` it is better to use `user.applications.map(&:job)` [link](https://coderwall.com/p/9xk6ra)
* [N+1](http://guides.rubyonrails.org/active_record_querying.html#eager-loading-associations) problem is solved with `includes(:associated_table)` wich is actually LEFT OUTER JOINS, `joins(:associated_table)` is INNER JOIN. If model has_many :associated_table then `joins` will return multiple values because of multi values of :associated_table per item, or none is :associated_table does not exists for current item. `includes` will return the same number of items, with association objectloaded in memory.
* new_record? does not work with associated count. It is beter to use length ie `survey.questions.length` 
* [naming conventions](http://guides.rubyonrails.org/active_record_basics.html#convention-over-configuration-in-active-record) is to have `foreign_table_name_id` for associations (belongs_to :foreign_table_name), `type` for single table inheritance (class Firm < Company), `imageable_id` and `imageable_type` for polymorphic associations (belongs_to :imageable, polymorphic: true).

Migrations:

* if we call Products.update_all :fuzz => 'fuzzy' in migration, it will probably break in the future, because Products will be validated for something that we did not planned. Better is to create local **class Product < ActiveRecord::Base;end**, and call **Product.reset_column_information**
* to change type from string to integer (using cast)
```
class ChangeScoreTypeInFilledAnswers < ActiveRecord::Migration 
  def up 
    change_column :filled_answers, :score, 'integer USING CAST(score AS integer)'
  end 
  def down 
    change_column :filled_answers, :score, :string 
  end 
end
~    
```
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

performance:

* Gem [miniprofiler](https://github.com/MiniProfiler/rack-mini-profiler) for analysing load time, disable with `http://mysite.com?pp=disable`
 
* [Kaminary gem](https://github.com/amatsuda/kaminari) with ajax does not know which params should be [black listed](https://github.com/amatsuda/kaminari/commit/2fd7d36b72af73d2506f8e2ab68704d804f70fc5) so use something like `paginate @jobs, params: { id: nil, action: 'index' }` in response index.js response file like this [ajax example](https://github.com/amatsuda/kaminari_example/tree/ajax)

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

* number of methods for some object can be large, to search method use grep, for example `request.methods.grep /url/`
* `self` in ruby is implicitly assumed, but you can use it for class methods or if you have attr_accessor :name, and have name="asd", name= is local variable assignment
* `p ["a", "b"].map(&:upcase)` is equivalent to `p ["a", "b"].map{|string| string.upcase}`
* regular expression http://www.rubular.com/
* put -w for warning log https://github.com/bbatsov/ruby-style-guide
* lambda literal syntax is: `method = ->(a, b) { a + b }`
* lambda method for multi line blocks:
```
method = lambda do |a, b|
  tmp = a * 7
  tmp * b / 50
end
```
* if dont know if path is array use: ` [*paths].each { |path| do_something(path) }`
* `%w{word}` is non onterpolated, `W{#{some variable} word}` is interpolated array of words separated by space

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
    
Push branch and track

    git push bitbucket development:development
  
Getting existing git branches to track remote branches:  

    git branch --set-upstream gh-pages-bitbucket bitbucket/gh-pages 
    
Git child commit reference with

    git log --reverse --ancestry-path 894e8b4e93d8f3^..master
    
Git stash only unstaged changes

    git stash --keep-index
    
Git checkout previous branch

    git checkout -
  
See all the changed code

    git log -p

Show file at specific revision

    git show HEAD~4:index.html
    
Rebase branches

     git pull --rebase # pull remote changes and rebase you local commits
     git rebase master # call this while you are on some feature branch
Versioning [SEMVER](http://semver.org/)

If there is two accounts on bitbucket or github with different keys use `.ssh/config` file

    Host secure.bitbucket.org
      Hostname bitbucket.org
      IdentityFile ~/.ssh/id_rsa_secure

    Host test.bitbucket.org
      Hostname bitbucket.org
      IdentityFile ~/.ssh/id_rsa_test


To see which username (-T) and wich key (-v) is using:
    
    ssh -T git@bitbucket.org
    ssh -v git@bitbucket.org

If you want to ignore/reignore some files that are tracked (gitignore does not work on tracked files)

    git update-index --[no]-assume-unchanged <file>                                

