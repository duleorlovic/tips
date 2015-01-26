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


HTML
===

* if option select is required, we usually prompt user with one more option "Please select", but it is bad to allow user to pick that option "Please select". You can disable option, and you should force selected on it if other option is not selected [demo](http://jsfiddle.net/u8PWX/1/)
  
    <select onchange="this.form.submit()">
      <option selected="selected" disabled="true">--Please Select --</option>
      <option value="volvo">Volvo</option>
      <option value="saab">Saab</option>
    </select>

In rails, you can use something like

    <%= select_tag "job[job_type_id]",("<option #{ "selected='selected'".html_safe unless fjob.object.job_type_id } disabled='disabled'>Job Type</option>".html_safe+ options_from_collection_for_select(JobType.active.all, :id, :name,{selected: fjob.object.job_type_id})), { class: "e1" } %>

Javascript
===

* to check if element(s) exists `if( $('#selector').length ) `
* scope of variable is from a moment of declaration to the end of function where it is declared (global context acts like one big function encompassing the code on the page), scope of a function is **entire** function where it is declared. block nesting like in `if` statement, does not affect scope. Scope of inline function `var b=function a(){}` is only inside function
* function context (*this* variable) is *window* for invocation as function `a()`, current object for invocation as method `b={};b.a=a;b.a()`. Invocation as contructor `var n=new A();` creates new object and passed to function as *this*, and if not return statements, it returns that object (they usually change new objects and are written Uppcase). Invocation with a.apply(b,[1,2]) and a.call(b,1,2) set manually the context `b` of a function (apply and call are function methods).
* [document ready](http://learn.jquery.com/using-jquery-core/document-ready/) can be detected in `$(document).ready(function(){})` or because ready can be used [only on current document](http://www.w3schools.com/jquery/event_ready.asp) selector is not needed `$(function(){});`
* when `<a></a>` does not have href that it will not follow thelink so you do not need to preventDefault. Use this for toggling some part
* `hover` on mobile devices does not work what is expected. It stays in hover state until the user press (click) on the screen next time.
* for popups with buttons, if you want to close popup clicking anywhere outside button, button should not be included in background div to clearly separate when popup should be closed. if it is inside we can workaround with targeting more specifically and stop propagation `$('#letsdoit').click( function(e) { e.stopPropagation();});`
* in rails-ujs click on links with remote:true is not efected with e.preventDefault()
* get the user agent online [http://ifconfig.me/all](http://ifconfig.me/all)
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
    
* if you are using `window.location.replace('http://a.b');` then browser back button is not working as espected. Its better to use `window.location.assign('new_page');` because the page is stored in history
* when user click back button previous page is reshown, and chrome reruns the javascript, but mozilla don't. if you want in mozilla to run again, write `window.onunload = function(){};`
 
    
* [enabling CORS](http://blog.jetthoughts.com/2010/12/22/allow-multiple-access-control-requests-for-rails/) add before filter:


    headers['Access-Control-Allow-Origin'] = '*'
    
    headers['Access-Control-Request-Method'] = '*'

* console.log(data) is ok for objects, but if you append to a string you should use JSON.stringify

    console.log("data="+JSON.stringify(data));
    
* disable turbolinks `document.body.setAttribute('data-no-turbolink','true')`
* turbolinks are good if some of page content is changed using ajax. Browser back button when turbolink is enabled shows last content (not first that was fatched). When turbolinks is disabled, you can force refreshing the page with set_cache_buster before filter. Note that any input field stays populated (also hidden input field which you eventually populated in javascript):

  def set_cache_buster
    response.headers["Cache-Control"] = "no-cache, no-store, max-age=0, must-revalidate"
    response.headers["Pragma"] = "no-cache"
    response.headers["Expires"] = "Fri, 01 Jan 1990 00:00:00 GMT"
  end



REGEX
===

* great source for regular expression explanation http://www.regexr.com/ http://regex101.com/
* grep lines not containig word, you need to use param -P. Vim example find non disable buttons: `:grep -P "^.*button(?!.*disable.*)" app/views/* -R`
* to extract url params (subject,body) from mailto href you can use URI to un-escape html characters: 
    subject_match = mailto.match(/[?&]subject=([^&]+)[&$]/)[1]
    if subject_match
      subject_from_mailto = URI.unescape subject_match
    end

iSO android and other mobile phone
===

* fadein and fadeout does not work well on mobilephone iOS android, its better to use display: block, display: none
* click event [does not work on iOS](http://stackoverflow.com/questions/3705937/document-click-not-working-correctly-on-iphone-jquery) and element is not clicable. simple solution is to add style: "cursor: pointer".

VIM
===

* install [pathogen](https://github.com/tpope/vim-pathogen) and other interesting plugins:

~~~
mkdir -p ~/.vim/autoload ~/.vim/bundle && \
curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim

cd ~/.vim/bundle
git clone git://github.com/tpope/vim-rails.git # example: Rview
git clone git://github.com/tpope/vim-bundler.git # Bopen
git clone git://github.com/tpope/vim-fugitive.git # Gblame, Gbrowse
vim -u NONE -c "helptags vim-fugitive/doc" -c q
~~~

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
" search selected text, press // while in visual mode
vnorem // y/<c-r>"<cr>
" change paste toggle key to F12 since F11 is maximize
set pastetoggle=<F12>   
~~~

~~~
" http://modal.us/blog/2013/07/27/back-to-vim-with-nerdtree-nope-netrw/
" Toggle Vexplore with Ctrl-E
function! ToggleVExplorer()
  if exists("t:expl_buf_num")
      let expl_win_num = bufwinnr(t:expl_buf_num)
      if expl_win_num != -1
          let cur_win_nr = winnr()
          exec expl_win_num . 'wincmd w'
          close
          exec cur_win_nr . 'wincmd w'
          unlet t:expl_buf_num
      else
          unlet t:expl_buf_num
      endif
  else
      exec '1wincmd w'
      Vexplore
      let t:expl_buf_num = bufnr("%")
  endif
endfunction
map <silent> <C-E> :call ToggleVExplorer()<CR>

" Hit enter in the file browser to open the selected
" file with :vsplit to the right of the browser.
let g:netrw_browse_split = 4
let g:netrw_altv = 1

" Default to tree mode
let g:netrw_liststyle=3

" Change directory to the current buffer when opening files.
" set autochdir
~~~

* usefull commands:

~~~
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
`vit` inner or `vat` outer visual select tag, jump with `o` more on `:help visual-operators` `:help v_it`
:help Ctrl-W_T open current buffer in new tab
~~~

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
* [selenium-webdriver](http://selenium.googlecode.com/git/docs/api/rb/Selenium/WebDriver.html) scripts can be debuged with 

    driver = ""                                                                                
    eval File.open('./scraping_selenium.rb').read
    
or something like
 
    require 'rubygems'
    require 'ruby-debug'
    x = 23
    puts "welcome"
    debugger
    puts "end"
    
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

* params usually need to be striped, so you can use this code to get rid of all unnecessary spaces

~~~
params_contact_striped = params[:contact].each_with_object({}) { |(k,v),o| o[k] = v.split.join(" ") } # strip spaces
~~~

* rails use cache for activerecord, and if you need to send query again and fetch fresh data, you can use `.reload`
* [truncate_html](https://github.com/hgmnz/truncate_html) is when you want to truncate text inside html. When you are using `raw` than it is advisable to use [sanitize](http://api.rubyonrails.org/classes/ActionView/Helpers/SanitizeHelper.html#method-i-sanitize) 
* target with `data-` attributes when you put some javascript on elements. When new markup come, you just need to copy data attributes. Also they can contain some real data: id or array of some id's. In rails do not use `data: { total_value: 0}` because its hard to search. It's better to use `"data-total-value" => 0` 
* when form is submitted and when there are errors, scaffold rails render again :new action, but the browser url is changed to the requested url so if than user refresh the page, it is another template (usually it's a index action of the same controller, but could be another controller)
* when you want to create nested models on the same form, its nice to generate template on server and change id (rails cast)[https://github.com/ryanb/complex-form-examples/blob/master/app/helpers/application_helper.rb] (stack)[http://stackoverflow.com/questions/2879208/rails-fields-for-child-index-option-explanation] but its easier to just use hidden template with name that is the same as for nested model, for example `email_message[proposal_attributes][proposal_item_attributes][][price]`. Form need to be configured to send array instead of hash for nested parameters parameters, that is `child_index: ''`. Whay we need hash and ids ?
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

* [turbolinks](https://github.com/rails/turbolinks) loads new page, replaces body and title, and use pushState. Any javascript is run after replacement so you can reference all elements in <script> tags on the beggining of the page (if you really want to). [Execution order](http://stackoverflow.com/questions/8996852/load-and-execute-order-of-scripts) of non dymanically ([defer or async](http://www.w3schools.com/tags/att_script_async.asp)) script are the same as they appear on the page (inline script is halted until external is loaded).  But with turbolinks, as with other dynamic loading where you can not know the order, execution is done after replacing, but before external script is loaded, so you probably can not have javascript_include_tag inside a view, because the code it provides will be available after all script on a page is done, and if you have several includes, the order is not preserved since the shortest one can be executed before all others. So the solution is to render all javascript inside the template with `<%= render 'app/assets/javascript/custom_script', formats: [:js] %>`
* accessing helper functions in controller can be done using `view_context` (including ApplicationHelper is not generally a good idea)

* mail attachments.inline['logo.png'] = File.read('app/assets/images/logo.png') will be attached with disposition="attachments" if there is no `<%= image_tag attachments['logo.png'].url %>` in a view [url](http://guides.rubyonrails.org/action_mailer_basics.html#making-inline-attachments). Rails look for its reference and if it does not find it will not include it as "inline". One way to include all inline attachments but not to show them (that is the case when you already have a inline img tag inside the view, for example forwarding emails)

    <% attachments.each do |a| %>
      <% if a.content_disposition[0..5] == "inline" %>
        <%  image_tag a.url, size: "0x0" %>
      <% end %>
    <% end %>

This way they are using its own content_id. To include inline attachments for existing mails, you have to use the same content_id

     @email_message.temp_images.each do |mandrill_image_cid, mandrill_image_hash|
        # mandrill_image_hash.keys = ["name", "type", "content"] and they are always base64
        attachments.inline[mandrill_image_cid] = { mime_type: mandrill_image_hash["type"], content: Base64.decode64(mandrill_image_hash["content"]), content_id: mandrill_image_hash["name"]} # we have to set mime type and content_id because we are using the original email with refers this content_id
      end
 
And as we have refenece for those images in email body, we do not need to use img_tag with size "0".

* sorting could be done with this helper that is used like `<th><%= sortable "id" %></th>`:

      
    def sortable(column, title = nil)
     title ||= column.titleize
     css_class = (column == sort_column) ? "current #{sort_direction}" : nil
     direction = (column == sort_column && sort_direction == "asc") ? "desc" : "asc"
     link_to title, { :sort => column, :direction => direction }, { :class => css_class }
    end

and this two methods:
    
    def sort_column
      User.column_names.include?(params[:sort]) ? params[:sort] : "id"
    end

    def sort_direction
      %w[asc desc].include?(params[:direction]) ? params[:direction] : "desc"
    end

so in controller we can write `@users = User.order(sort_column+" "+sort_direction) 


## Active record

* to make some fields private you can use [link](http://stackoverflow.com/questions/3764899/is-there-a-way-to-make-rails-activerecord-attributes-private)


    class YourModel < ActiveRecord::Base
    private
      def my_private_attribute
        self[:my_private_attribute]
      end
      def my_private_attribute=(val)
        write_attribute :my_private_attribute, val
      end
    end


* its better to use `destroy` instead of `delete` since it will trigger [destroying associated models](http://api.rubyonrails.org/classes/ActiveRecord/Associations/ClassMethods.html#module-ActiveRecord::Associations::ClassMethods-label-Delete+or+destroy%3F) but its better not to remove anything since it is blocking operation
* when you are adding new validations (for example title needs to be present) write also a migration file to make sure all items in database are valid. To check if some unvalid object exists in database you can run `Rails.application.eager_load!` and `e=ActiveRecord::Base.descendants.select { |c| c.all.select {|i| !i.save}.present? }.map {|c| c.all.select {|i| !i.save}.map { |i| i.save;puts c;i.errors} }`. 
* [default_scope is appended to all queries][http://rails-bestpractices.com/posts/806-default_scope-is-evil], only way to remove it is `uncope`
* Assigning an object to a [belongs_to](http://guides.rubyonrails.org/association_basics.html#belongs-to-association-reference) association does not automatically save the object. It does not save the associated object either.
* you can specify order for association: `has_many :educations, -> {order 'graduation_year DESC'}, :dependent => :destroy`
* instead of `has_many :applied_jobs, through: :applications, source: :job` it is better to use `user.applications.map(&:job)` [link](https://coderwall.com/p/9xk6ra)
* [N+1](http://guides.rubyonrails.org/active_record_querying.html#eager-loading-associations) problem is solved with `includes(:associated_table)` wich is actually LEFT OUTER JOINS, `joins(:associated_table)` is INNER JOIN. If model has_many :associated_table then `joins` will return multiple values because of multi values of :associated_table per item, or none is :associated_table does not exists for current item. `includes` will return the same number of items, with association objectloaded in memory.
* new_record? does not work with associated count. It is beter to use length ie `survey.questions.length` 
* [naming conventions](http://guides.rubyonrails.org/active_record_basics.html#convention-over-configuration-in-active-record) is to have `foreign_table_name_id` for associations (belongs_to :foreign_table_name), `type` for single table inheritance (class Firm < Company), `imageable_id` and `imageable_type` for polymorphic associations (belongs_to :imageable, polymorphic: true).
* you can set any user in config/database.yml (even without password), but you need to change postgres config and create that user, simple:

    has_many :attachments, as: :attachmentable, conditions: { is_image: false }
    has_many :images, as: :attachmentable, class_name: 'Attachments', conditions: { is_image: true }

* you can attach multiple polimorphic association with conditions:

    has_many :attachments, as: :attachmentable, conditions: { is_image: false }
    has_many :images, as: :attachmentable, class_name: 'Attachments', conditions: { is_image: true }
* instead of `has_many :applied_jobs, through: :applications, source: :job` it is better to use `user.applications.map(&:job)` [link](https://coderwall.com/p/9xk6ra)
* [N+1](http://guides.rubyonrails.org/active_record_querying.html#eager-loading-associations) problem is solved with `includes(:associated_table)` wich is actually LEFT OUTER JOINS, `joins(:associated_table)` is INNER JOIN. If model has_many :associated_table then `joins` will return multiple values because of multi values of :associated_table per item, or none is :associated_table does not exists for current item. `includes` will return the same number of items, with association objectloaded in memory.
* new_record? does not work with associated count. It is beter to use length ie `survey.questions.length` 
* [naming conventions](http://guides.rubyonrails.org/active_record_basics.html#convention-over-configuration-in-active-record) is to have `foreign_table_name_id` for associations (belongs_to :foreign_table_name), `type` for single table inheritance (class Firm < Company), `imageable_id` and `imageable_type` for polymorphic associations (belongs_to :imageable, polymorphic: true).
* you can set any user in config/database.yml (even without password), but you need to change postgres config and create that user, simple:

    sudo vi /etc/postgresql/9.1/main/pg_hba.conf 
    # change all this words [md5, ident, peer] to trust 
    sudo /etc/init.d/postgresql restart 
    psql postgres 
    CREATE USER "Dusan" CREATEDB ; 
    \q 
    # if it does not work because previous command created `dusan` instead of `Dusan` 
    ALTER ROLE dusan RENAME TO "Dusan"; 
    # or 
    pgadmin3 # login as postgres without password and chage it to Dusan

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
* use db/seed.rb to add some working data (users, products) that should not go to production. add data to migration file if something needs to be in db (select box, customer plans) and use `rake db:migrate:reset & rake db:seed` instead of `rake db:setup` so migrations are actually perfomed
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

* performance:
  * [miniprofiler](https://github.com/MiniProfiler/rack-mini-profiler) for analysing load time, disable with `http://mysite.com?pp=disable`
* when using pagination on page where you have some activating/archiving [Kaminary gem](https://github.com/amatsuda/kaminari) with ajax does not know which params should be [black listed](https://github.com/amatsuda/kaminari/commit/2fd7d36b72af73d2506f8e2ab68704d804f70fc5) so use something like `paginate @jobs, params: { id: nil, action: 'index' }` in response index.js response file like this [ajax example](https://github.com/amatsuda/kaminari_example/tree/ajax)
* get the country based on ip address:
  * [geocoder](https://github.com/alexreisner/geocoder), [geo_ip](http://rubygems.org/gems/geo_ip) [instructions](http://igotrailed.wordpress.com/2013/11/19/detecting-user-location-with-rails/), [geoip](http://rubygems.org/gems/geoip) which can be downloaded as database [geolite](http://dev.maxmind.com/geoip/legacy/geolite/) and have country code based on [iso3166](http://dev.maxmind.com/geoip/legacy/codes/iso3166/), ISO 3166-1 alpha2 are country codes ('gb', 'rs'), ISO 639-1 alpha2 are language names ('en', 'sr')
  * get locale based on country: [i18n_data](https://github.com/grosser/i18n_data)
  * country gem using currency gem to get currency [countries](https://github.com/hexorx/countries/)
* [browser-timezone-rails](https://github.com/kbaum/browser-timezone-rails) is best gem to display local time withouht any calculation (using jsTimezoneDetect)
* pdf generator [wickedpdf](https://github.com/mileszs/wicked_pdf)

CANCAN
===

 * if you set `can :manage, :all` in ability file, then after that you should define only what cannot. Only way that you need to define can after 'can :manage, :all' is for index, create or update actions, if you want to populate with hash, for example `can :index, Produc, { user: current_user }`, no block definitions for abilitity for managers since they can magane all!
 * for [load_and_authorize_resource](https://github.com/ryanb/cancan/wiki/Authorizing-controller-actions) for :index, if you define ability in a [block](https://github.com/ryanb/cancan/wiki/Defining-Abilities-with-Blocks) instead of hash, then [load_resource](https://github.com/ryanb/cancan/wiki/Authorizing-controller-actions#index-action) will not populate @products since it does not know how to do it. For :show, :edit, :update and :destroy it will fetch by params[:id], for :new and :create it will create new one if you define hash, and it will be overwritten with params[:class] attributes 

BACKGROUND WORKER
===

 * is your server need to use third party api, it is advisable to put it in background, so in case of traffic congestion (for example you and target api) user do not receive 'not responding page' since browsers have timeout 30 sec.
 * [SuckerPunch](https://github.com/brandonhilkert/sucker_punch) is done in the same thread and can be run on heroku on single dyno (drawback is that it is cleaned on each restart, deploy, even error with exception)
 * [DelayedJob](https://github.com/collectiveidea/delayed_job) is peristent since it stores serialized object in db, and when it comes to run it, it retrive object and run method (drawback is number of ActiveRecord connections to db, since each worker need two, one to retreive the object, another to use with ActiveRecord. Watch out when you backup database, delayed jobs should not be restored).
 * [Sidekiq](http://sidekiq.org/) is identical to Socker Punch, fast and run on single thread, better than delayed_job since it can run 20 processes in same time, threadsafe, works on [one heroky dyno with unicorn webserver](https://coderwall.com/p/fprnhg) set up heroku `config:set REDIS_PROVIDER=REDISTOGO_URL` (drawback is that you need to use Redis server for in memory database storage)
If there is an error *invalid byte sequence in US-ASCII* try to *export LANG=en_US.UTF-8* before installing a gem

For rvm put ```source ~/.bash_profile``` in your **~/.bashrc** file and you do not need to enable terminal settings to "Run command as login shell"

Ruby
===

* condition *if* or *? :* in parameters lists to check if function argument should be passed can be used in two ways for hash argumests: merge or conditional. Since hash argument need key/value pair you can not pass `a(b:2,{c:3}` since {c:3} is not pair.  note that we usually need extra () around conditions
  * merge example `form_for @user, {}.merge( @contition ? {class: 'main'} : {} )` (key 'class' is not always passed in form), note that we have to pass hash to merge and we can not use `{class: 'main'} if @condition` since it will try to merge nil and raise exception if @condition == false
  * conditional `form_for @user, class: ('main' if @condition)`(key 'class' always exists as param, but value is nil unless @contidion). 
* if you want to see all methods for some object, you can `a.methods.grep /what/`. If you want to list all  instance methods, but not methods of superclass `a.class.instance_methods(false)`. To see where it is defined `a.method(:what).source_location`
* if you want to return hash as result on some collection (map always return array), you can use `{ "x" => 1, "y" => 2, "z" => 3 }.each_with_object({}) {|(k,v),o| o[k.to_sym]=v }`
* remove duplicate repettitive spaces from string `str.split.join(" ")`
* default params for function could be set like `def f(a=1);end`, and default values for variables if not defined `var = true unless defined? var` (do not use `var||=true` since it will override `var=false`)
* if you want to save output of ruby script `ruby a.rb |tee output` and want to see output in realtime you need to call flush after each puts `$stdout.flush` or you can set that for whole script `STDOUT.sync = true`
* [rescue_from](http://api.rubyonrails.org/classes/ActiveSupport/Rescuable/ClassMethods.html) are searched from bootom to top.
* break two nested loops (two levels)
 
   bank.branches do |branch|
    break unless branch.employees.each do |employee|
      break if employee.name == "John Doe"
    end
  end

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
* ! has greater priority then == so use () to determine precedence, for example `if ! a==3` is not the same as `if a!=3`

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
* test the speed, download: `curl -o /dev/null http://speedtest.qsc.de/1GB.qsc`, crate big files `fallocate -l 1G gentoo_root.img` and use scp to test upload link.

GIT
===

track remote branch if we did not have this branch already

    git checkout -t origin/branch
    
Push branch and track

    git push bitbucket development:development
  
Getting existing git branches to track remote branches:  

    git branch --set-upstream gh-pages-bitbucket bitbucket/gh-pages 
    
Git log

    git log --reverse --ancestry-path commit1^..commit2 # show commits that are descendant of commit1 AND ancestors of commit2, in the same time
    git log $(git merge-base HEAD branch)..branch  # show commits only on branch
    
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

If there is two accounts on bitbucket or github with different keys use `.ssh/config` file and put:

    Host secure.bitbucket.org
      Hostname bitbucket.org
      IdentityFile ~/.ssh/id_rsa_secure

    Host test.bitbucket.org
      Hostname bitbucket.org
      IdentityFile ~/.ssh/id_rsa_test

To see which username (-T) and wich key (-v) is using:
    
    ssh -T git@bitbucket.org
    ssh -v git@secure.bitbucket.org
    
If you want, you can generate id_rsa_secure with password, so it will asked each time you use git command.
Heroku uses keys from `~/.netrc` which is created when you type `heroku login` (once is setup, it stays forever)

If you want to ignore/reignore some files that are tracked (gitignore does not work on tracked files)

    git update-index --[no]-assume-unchanged <file>

                                
Third party
===

* fundamentals
  * [W3.org](http://www.w3.org/TR/selectors/)
  * [OWASP](https://www.owasp.org/index.php/Category:Attack) nice examples of attack and vulnerability
* opensource crowdsourcing
  * [catarse](https://github.com/catarse/catarse)
  * [tilt](https://github.com/crowdtilt/crowdtiltopen/) is not actually opensource, since their api should be used
* jquery plugins
  * [jbox](http://stephanwagner.me/jBox) notifications, popups ...
  * "One minute ago" can be updated automatically in this [timeago](http://timeago.yarp.com/) plugin
* javascript
  * [jsPDF](https://github.com/MrRio/jsPDF) pdf generator [examples](http://mrrio.github.io/jsPDF/#)
  * [graphs gallery](https://github.com/mbostock/d3/wiki/Gallery)

 

