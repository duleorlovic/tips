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
        <li><a href="http://tips.trk.in.rs">Home</a></li>
        <li><a href="#nodejs">Node.js</a></li>
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
        <li><a href="#other">Other</a></li>
        <li><a href="https://github.com/duleorlovic/tips/blob/gh-pages/index.md">Edit</a></li>
      </ul>
    </div><!--/.nav-collapse -->
  </div>
</div>

Node.js
===

* `npm config set prefix '~/.npm-packages'` and `export PATH="$PATH:$HOME/.npm-packages/bin"`

Gulp
===

* `gulp --tasks` to list all gulp tasks

HTML
===

* **inline**: `<span>`, `<a>`, `<em>`, `<strong>`, `<img>`,`<input>`. Inline elements do not cause transitions to a new line, but will be displayed one next to the other horizontally. `<br>` [link](http://webdesignfromscratch.com/html-css/css-block-and-inline/) The line-break is an odd case, as it’s an inline element that forces a new line. However, as the text carries on on the next line, it’s not a block-level element.
* **block-level**: `<div>`, `<p>`, `<article>`,`<h1>`,`<ol><li>`,`<table>`,`<form>`. Block elements are set like blocks that stack on top of each other and will never display next to one another horizontally
* **inline-block**: `<label>`, `<input>`, and `<textarea>`. Inline blocks will act as inline elements (elements are displayed next to each other), but differ in that they can be for instance resized. For example, the `<textarea>` field can be displayed as a large rectangle, but it can take up space beyond a single line of text.
* to make `<li>` horizontal, change its style to **display: inline**, or **float: left**
* `onmouseover` is not fired when element is disabled, but you can easily wrap inside another elemenent with padding 1px


XPATH
===

* [usefull selectors](http://ejohn.org/blog/xpath-css-selectors/)

CSS
===

* to set with for anchor `a` tag (or any other `inlin` element), you need to change it's display to `block` or `inline-block`, than you can use `max-width` or `width`
* keep text in one line `span { white-space: nowrap; }`
* when you want to have different child of first element, you can with

~~~
.target-parent li:first-child .target-child {
  display: none;
}
~~~

* z-index only works on positioned elements (position:absolute, position:relative, or position:fixed).
* `border: 1px` needs to be defined before `border-style: solid` or `border-color: red`
* to overwrite `!important` write another rule with *Simply add another CSS rule with !important, and either give the selector a higher specificity (adding an additional tag, id or class to the selector), or add a CSS rule with the same selector at a later point than the existing one (in a tie, the last one defined wins).*
* cascade rules are [http://www.w3.org/TR/2011/REC-CSS2-20110607/cascade.html#cascade](http://www.w3.org/TR/2011/REC-CSS2-20110607/cascade.html#cascade)
* position element in center `margin: auto` works for <div> but not for <button>, so try this [link](https://css-tricks.com/quick-css-trick-how-to-center-an-object-exactly-in-the-center/)

~~~
.centered {
  position: fixed;
  top: 50%;
  left: 50%;
  /* if you don't know the size... bring your own prefixes */
  transform: translate(-50%, -50%);
  /* if you know the size
  margin-top: -50px;
  margin-left: -100px; */
}
~~~

## SASS

* [parent selector reference](http://thesassway.com/intermediate/referencing-parent-selectors-using-ampersand) parent is not direct parrent, its parrent of whole sequence !

~~~
h3 {
  font-size: 20px;
  div {
    .some-parent-selector & { // this will compile to .some-parent-selector h3 div { font-size: 24px }
      font-size: 24px;
    }
  }
}
~~~

Javascript
===

* to check if element is visible and to scroll into view

~~~

function check_if_in_view($element, options) {
  // https://developer.mozilla.org/en-US/docs/Web/API/Element.scrollIntoView
  // use options parameter to force scrolling even element is visible on current view
  // if options == true/false, the top of the element will be aligned to the top/bottom of the visible area of the scrollable ancestor.
  if (typeof document.getElementsByTagName('body')[0].scrollIntoView == 'undefined')
  {
    console.log("scrollIntoView not defined");
    return true;
  }
  else if (typeof options != 'undefined')
  {
    console.log("ckeckIfInView "+options);
    $element[0].scrollIntoView(options);
  }
  else
  {
    // check if visible
    var offset = $element.offset().top - $(window).scrollTop();
    if(offset < 0){
        console.log("alignWithTop=true");
        $element[0].scrollIntoView();
        return false;
    }
    else if (offset > window.innerHeight){
        console.log("alignWithTop=false");
        $element[0].scrollIntoView(false);
        return false;
    }
    else
    {
      console.log("no scroll, its visible");
      return true;
    }
  }
}
~~~


* if element is hidden, some older browser security restrictions do not allow it to trigger a click with `$("#test").click();`. So it is better to show element but move it out of visible area `style="position:absolute; top:-100px;"` [link](http://stackoverflow.com/questions/793014/jquery-trigger-file-input).
* to detect jQuery and load if needed  [follow this](https://docs.shopify.com/api/unlinked/using-javascript-responsibly) (you can put check onload `window.onload = function(e) { it (type jQuery == 'undefined')...}`) so you can wait for eventual later on page jQuery include
* select elements by data attribute `$('a[data-color=true]')` or `$('a:data(collor)');`
* to check if element(s) exists `if( $('#selector').length ) `
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

SQL
===

* `PG::InvalidColumnReference: ERROR:  SELECT DISTINCT ON expressions must match initial ORDER BY expressions` is a problem when you do not include column `a` for which you want to order, so it should be `SELECT DINSTINCT ON (dinstinct,a)...`


REGEX
===

* to regex email in text stream 

~~~
r = Regexp.new(/\b[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}\b/)     
emails = content.scan(r).uniq  
~~~

* in Rails you can use default devise `validates_format_of :recipient_email_address, with: User.email_regexp, allow_blank: true`
* `(a|b)` when you want to match a OR b
* `.*?` when you want to force minimum rather than maximum match
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
* click event [does not work on iOS](http://stackoverflow.com/questions/3705937/document-click-not-working-correctly-on-iphone-jquery) when element is not clicable. simple solution is to add style: "cursor: pointer".
* on android when file field input is **display: none**, you can not trigger click on it. Better is to use `style="position:absolute; left:-1000px"`

Vim
===

* look at blog [http://duleorlovic.github.io/blog/2015/12/01/vim-tips/](http://duleorlovic.github.io/blog/2015/12/01/vim-tips/)

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

Vagrant
===

* if you get a problem with SSL  certificate

~~~
An error occurred while downloading the remote file. The error
message, if any, is reproduced below. Please fix this error and try
again.

SSL certificate problem: unable to get local issuer certificate
More details here: http://curl.haxx.se/docs/sslcerts.html

curl performs SSL certificate verification by default, using a "bundle"
 of Certificate Authority (CA) public keys (CA certs). If the default
 bundle file isn't adequate, you can specify an alternate file
 using the --cacert option.
If this HTTPS server uses a certificate signed by a CA represented in
 the bundle, the certificate verification probably failed due to a
 problem with the certificate (it might be expired, or the name might
 not match the domain name in the URL).
If you'd like to turn off curl's verification of the certificate, use
 the -k (or --insecure) option.
~~~

solution is to `sudo cp /etc/ssl/certs/ca-certificates.crt /opt/vagrant/embedded/cacert.pem` [link](https://github.com/mitchellh/vagrant/issues/5001) or to add `config.vm.box_download_insecure = true` to Vagrantfile [link](http://stackoverflow.com/questions/27878131/solved-how-to-vagrant-up-with-puphpet-on-windows-7-x64-with-vagrant-1-7-2)


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

* form_for `method` param can be ignored since for new object is POST,  updating is PATCH... but if you are using form objects where nested elements sometimes exists, sometimes not, this method should be fixed (also in routing)
* when using username: first_name.last_name instead of id `resources :users, :constraints => { :id => /[^\/]+(?=\.html\z|\.json\z)|[^\/]+/ }, except: :new do`, users with first_name in ['new','edit','show'] will not be able to work properly
* keys in locale files for i18n can be relative to current file: [lazy lookup](http://guides.rubyonrails.org/i18n.html#lazy-lookup) `<%= t '.title' %>` in *app/views/books/index.html.erb* is the same as `<%= t 'books.index.title' %>`. Also works for partials (skip leading _). Template could use locale extension *sr.html* for example: *app/views/books/index.sr.html.erb*. List of locale files on [i18n](https://github.com/svenfuchs/rails-i18n/tree/master/rails/locale) gem.
* [pry](http://pryrepl.org/) in rails with `pry -r /home/orlovic/rails/produceruncatarse/config/environment.rb` or in user [pry-rails](https://github.com/pry/pry/wiki/Setting-up-Rails-or-Heroku-to-use-Pry) gem 
* if you need asset_path in some class (for example uploader) you can use this `ActionController::Base.helpers.asset_path 'image.png'`
* access url route helpers in model `Rails.application.routes.url_helpers.menu_url(link)` and define host with `Rails.application.routes.default_url_options[:host] = Rails.application.secrets.default_url_options`. You can `delegate :url_helpers, to: 'Rails.application.routes'` in class definition.
* rails use cache for activerecord, and if you need to send query again and fetch fresh data, you can use `.reload`
* [truncate_html](https://github.com/hgmnz/truncate_html) is when you want to truncate text inside html. When you are using `raw` than it is advisable to use [sanitize](http://api.rubyonrails.org/classes/ActionView/Helpers/SanitizeHelper.html#method-i-sanitize) 
* target with `data-` attributes when you put some javascript on elements. When new markup come, you just need to copy data attributes. Also they can contain some real data: id or array of some id's. In rails do not use `data: { total_value: 0}` because its hard to search. It's better to use `"data-total-value" => 0` 
* when form is submitted and when there are errors, scaffold rails render again :new action, but the browser url is changed to the requested url so if than user refresh the page, it is another template (usually it's a index action of the same controller, but could be another controller)
* when you want to create nested models on the same form, its nice to generate template on server and change id [rails cast](https://github.com/ryanb/complex-form-examples/blob/master/app/helpers/application_helper.rb) [stack](http://stackoverflow.com/questions/2879208/rails-fields-for-child-index-option-explanation). If you are only creating its easier to just use hidden template with name that is the same as for nested model, for example `email_message[proposal_attributes][proposal_item_attributes][][price]`. Form need to be configured to send array instead of hash for nested parameters parameters, that is `child_index: ''`. Edit is problematic without id, so this is usefull only for creating.
* folders in app/assets/* are hidden when you are accessing files, for example: `localhost:3000/assets/file.txt` should be here `app/assets/javascript/file.txt` or `app/assets/img/file.txt` (last one overrides prev). In production files that are listed in application.css.erb would be served as part of application.css, but all other files are served as is on their locations
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
* for ajax actions (links with `remote:true`) it should be implemented both, JS and  HTML version, since user can use right click on in new tab for that links. It can be `respond to` `format.html`, or in before filter `before_action :reload_on_html_request, only: [ :active, :pause]` and
~~~
  def reload_on_html_request
    # we have ajax link (not buttons) that can be opened in new window which causes an error... we redirect them to back (referrer)
    # http://api.rubyonrails.org/classes/ActionController/Redirecting.html
    # http://stackoverflow.com/questions/771656/correctly-doing-redirect-to-back-in-ruby-on-rails-when-referrer-is-not-availabl
    if ! request.xhr?
      redirect_to :back # that is the same as request.env["HTTP_REFERER"]
    end
  rescue ActionController::RedirectBackError
    redirect_to root_path
  end
~~~

* if you have ajax links, it is advisable to implement notification in case of error since ajax error tends to be silent:
 
~~~
    // ajax error handling, currently only for debugging                                        
    LOG && $(document).on('ajax:error', '[data-remote]', function(e, xhr, status, error) {      
      LOG && console.log("ajax:error [data-remote] e.target="+e.target+" status="+status+" error="+error);
      //disable eventual popups so user can see the message                                     
      $('.active').removeClass('active');
      flash_alert("Please refresh the page. Server responds with: \"" +status+ " " + error + "\".");
    });
~~~

* `data-disable-with` is provided with [rails-ujs](https://github.com/rails/jquery-ujs/blob/master/src/rails.js#L335) and if you want to manually send ajax requests than you need to manually fire up `ajax:complete` events. For example ` $(this).trigger("ajax:complete");` in:

~~~
  $(document).on('click', '[data-check-if-in-editing-mode]', checkIfInEditingMode);
  function checkIfInEditingMode(e) {
    LOG && console.log("checkIfInEditingMode");
    e.preventDefault();
    // do not submit automatically
    // if there are open questions title or description, warn the user
    if ($(this).data('check-if-in-editing-mode') != "ignore" && $('[data-in-editing-mode]').length )
    {
      $('[data-in-editing-mode]').first().each( function() {
        checkIfInView($(this));
        alert($(this).data('in-editing-mode'));
      });
      $(this).trigger("ajax:complete");
    }
    else
    {
      $.ajax({
        url: $(e.target).attr('href'),
        type: 'put',
        dataType: 'script',
        error: function(jqXHR, textStatus, errorThrown) {
          flash_alert("Please refresh the page. Server responds with: \"" +textStatus+ " " + errorThrown + "\".");
          $('[data-check-if-in-editing-mode]').trigger("ajax:complete");
        },
        success: function( data, textStatus, jqXHR ) {
          $('[data-check-if-in-editing-mode]').trigger("ajax:complete");
        },
      });
    }
  }
~~~

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

## Rails console

* `puts Readline::HISTORY.entries.split("exit").last[0..-2].join("\n")` show last commands so you can copy and paste to some code

## Active record

* in User class usually we have `before_filter :generate_referral_token`
~~~
  def generate_referral_token
    # http://stackoverflow.com/questions/6021372/best-way-to-create-unique-token-in-rails
    self.referral_token = loop do
      # http://ruby-doc.org/stdlib-2.1.0/libdoc/securerandom/rdoc/SecureRandom.html
      random_token = SecureRandom.urlsafe_base64(nil, false)[0..REFERRAL_TOKEN_LENGTH-1].upcase
      break random_token unless self.class.exists?(referral_token: random_token)
    end
  end
~~~
* if question mark is used in activerecord query `scope :customers, -> { where('role = ?', ROLE_EMPLOYER)}` than you should use table name because in joins some other table could have role column `scope :customers, -> { where('users.role = ?', ROLE_EMPLOYER)}`, but the best is if you use hash `scope :customers, -> { where( role: ROLE_EMPLOYER)}` (you can even build new customer with `User.customers.build`
* [has_and_belongs_to_many](http://guides.rubyonrails.org/association_basics.html#the-has-and-belongs-to-many-association) needs a table model1_model2 (where model1 name is less than model2 in alphabet)
* for HABTM you can use `f.collection_check_boxes :min_qualification_ids, MinQualification.active.all, :id, :name`. Trick here is to use *min_qualification_ids*. That *_ids* is provided for all has_many association. In controller you need just to update parent record and all has_many_and_belongs associated records mapping will be updated (here is table min_qualifications_users)

~~~
min_qualifications_params = params.require(:user).permit( min_qualification_ids: [])
non_empty_min_qualifications_params = min_qualifications_params.each_with_object({}) { |(k,v),o| o[k] = v.reject &:blank? }
@user.update!(non_empty_min_qualifications_params)
~~~

* you can join several tables,just use their name: Job <-> MinQualitication <-> User

~~~
class Job
  def suggested_jobseekers
    User.active_job_seekers.joins(min_qualifications: [:jobs]).where(jobs_min_qualifications: { id: id} )
  end
end
~~~

* validate with if contition `validates_presence_of :user_id, if: Proc.new{ |u| u.active? }`
* when you add validation `validate_presence_of :username` which you generate, you should also write migration for existing users and `before_create` hook to populate that field, update seed file
* `accept_nested_attributes :jobs` is needed if you want to use `f.fields_for :jobs do |fjob|` for `user.jobs.new` nested form. Usually you add validations in jobs model, for example `validates :user, presence: true`, but than you need to insert funky **inverse_of** in user model `has_many :jobs, :dependent => :destroy, inverse_of: :user` if you want this validation to pass for nested attributes
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

* you can attach multiple polymorphic association with conditions:

    has_many :attachments, as: :attachmentable, conditions: { is_image: false }
    has_many :images, as: :attachmentable, class_name: 'Attachments', conditions: { is_image: true }
    
* [naming conventions](http://guides.rubyonrails.org/active_record_basics.html#convention-over-configuration-in-active-record) is to have `foreign_table_name_id` for associations (belongs_to :foreign_table_name), `type` for single table inheritance (class Firm < Company), `imageable_id` and `imageable_type` for polymorphic associations (belongs_to :imageable, polymorphic: true)
* polymorphic items belogs to one object so you should not use someting like `new_user.location = Location.where(:address => address).first_or_create` because it will steal location object from old user. Better is to always build new `new_user.build_location address: address`
* polymorphic example `user.location = Location.new address: address` will create (!) new location object, but `user.build_location address: address` won't
* instead of `has_many :applied_jobs, through: :applications, source: :job` it is better to use `user.applications.map(&:job)` [link](https://coderwall.com/p/9xk6ra)

* new_record? does not work with associated count. It is beter to use length ie `survey.questions.length` 

Gems
===

* paperclip: 
  * default image path in assets pipeline is using helper in controller `ActionController::Base.helpers.asset_path('missing_:style.png')`
  * `new = menu_item.dup` will copy attributes. to copy image `new.photo = menu_item.photo` it will download image and upload images
* performance:
  * [miniprofiler](https://github.com/MiniProfiler/rack-mini-profiler) for analysing load time, disable with `http://mysite.com?pp=disable`
* when using pagination on page where you have some activating/archiving [Kaminary gem](https://github.com/amatsuda/kaminari) with ajax does not know which params should be [black listed](https://github.com/amatsuda/kaminari/commit/2fd7d36b72af73d2506f8e2ab68704d804f70fc5) so use something like `paginate @jobs, params: { id: nil, action: 'index' }` in response index.js response file like this [ajax example](https://github.com/amatsuda/kaminari_example/tree/ajax)
* get the country based on ip address:
  * [geocoder](https://github.com/alexreisner/geocoder), [geo_ip](http://rubygems.org/gems/geo_ip) [instructions](http://igotrailed.wordpress.com/2013/11/19/detecting-user-location-with-rails/), [geoip](http://rubygems.org/gems/geoip) which can be downloaded as database [geolite](http://dev.maxmind.com/geoip/legacy/geolite/) and have country code based on [iso3166](http://dev.maxmind.com/geoip/legacy/codes/iso3166/), ISO 3166-1 alpha2 are country codes ('gb', 'rs'), ISO 639-1 alpha2 are language names ('en', 'sr')
  * get locale based on country: [i18n_data](https://github.com/grosser/i18n_data)
  * country gem using currency gem to get currency [countries](https://github.com/hexorx/countries/)
  * <http://www.geoplugin.com/> free
* [browser-timezone-rails](https://github.com/kbaum/browser-timezone-rails) is best gem to display local time withouht any calculation (using jsTimezoneDetect)
* pdf generator [wickedpdf](https://github.com/mileszs/wicked_pdf)

HTTPARTY
===

* examples [https://github.com/jnunemaker/httparty/tree/master/examples](https://github.com/jnunemaker/httparty/tree/master/examples)
* in irb `response = HTTParty.post(url, :body => some_data.to_json, :basic_auth => auth, :headers => {"X-Custom" => "foo"}, :debug_output => $stdout)`

CANCAN
===

 * if you set `can :manage, :all` in ability file, then after that you should define only what cannot. Only way that you need to define can after 'can :manage, :all' is for index, create or update actions, if you want to populate with hash, for example `can :index, Produc, { user: current_user }`, no block definitions for abilitity for managers since they can magane all!
 * for [load_and_authorize_resource](https://github.com/ryanb/cancan/wiki/Authorizing-controller-actions) for :index, if you define ability in a [block](https://github.com/ryanb/cancan/wiki/Defining-Abilities-with-Blocks) instead of hash, then [load_resource](https://github.com/ryanb/cancan/wiki/Authorizing-controller-actions#index-action) will not populate @products since it does not know how to do it. For :show, :edit, :update and :destroy it will fetch by params[:id], for :new and :create it will create new one if you define hash, and it will be overwritten with params[:class] attributes 

CARRIERWAVE
===

* when you want to update remote url, or create object with mount_uploader, you can use [`remote_avatar_url` field](https://github.com/carrierwaveuploader/carrierwave#uploading-files-from-a-remote-location)

> If you're using ActiveRecord, CarrierWave will indicate invalid URLs and download failures automatically with attribute validation errors. If you aren't, or you disable CarrierWave's validate_download option, you'll need to handle those errors yourself.

* another way is to use `key` attribute, for example: `user.key` or `user.avatar.key = 'http://asd.asd'`


DEVISE
===

* in facebook omniauth callbacks params do not see actuall param my_param in `user_omniauth_authorize_path(:facebook, my_param: 1)`. You can access it in `request.env['omniauth.params']['my_param']`
* you should not write `after_create :my_func` hook in User model, since devise `resource.save` will return true, but `resource.error` will contain some fanky error *Email can't be blank* [link](https://github.com/plataformatec/devise/issues/2841)
* if you do not allow users do destroy accounts, in your `class RegistrationsController < Devise::RegistrationsController` you should overide destroy with something like ([notification](http://duleorlovic.github.io/blog/ruby-on-rails/exception-notification/2015/01/11/good-rails-exception-notification-better-than-tests/))
    
    def destroy
        ExceptionNotifier.notify_exception(Exception.new('destroy user'), env: request.env, data: { current_user: current_user });
    end


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

* dummy ruby objects [OpenStruct](http://ruby-doc.org/stdlib-2.0/libdoc/ostruct/rdoc/OpenStruct.html)
* condition *if* or *? :* in parameters lists to check if function argument should be passed can be used in two ways for hash argumests: merge or conditional. Since hash argument need key/value pair you can not pass `a(b:2,{c:3}` since {c:3} is not pair.  note that we usually need extra () around conditions
  * merge example `form_for @user, {}.merge( @contition ? {class: 'main'} : {} )` (key 'class' is not always passed in form), note that we have to pass hash to merge and we can not use `{class: 'main'} if @condition` since it will try to merge nil and raise exception if @condition == false
  * conditional `form_for @user, class: ('main' if @condition)`(key 'class' always exists as param, but value is nil unless @contidion). 
* if you want to see all methods for some object, you can `a.methods.grep /what/`. If you want to list all  instance methods, but not methods of superclass `a.class.instance_methods(false)`. To see where it is defined `a.method(:what).source_location`
* if you want to return hash as result on some collection (map always return array), you can use `{ "x" => 1, "y" => 2, "z" => 3 }.each_with_object({}) {|(k,v),o| o[k.to_sym]=v }`
* remove duplicate repettitive spaces from string `str.split.join(" ")`
* default params for function could be set like `def f(a=1);end`, and default values for variables if not defined `var = true unless defined? var` (do not use `var||=true` since it will override `var=false`)
* if you want to save output of ruby script `ruby a.rb |tee output` and want to see output in realtime you need to call flush after each puts `$stdout.flush` or you can set that for whole script `STDOUT.sync = true`
* [rescue_from](http://api.rubyonrails.org/classes/ActiveSupport/Rescuable/ClassMethods.html) are searched from bootom to top.
* inline rescue can use last return value `rescue $!` [tapas](http://devblog.avdi.org/2012/11/19/rubytapas-022-inline-rescue/)
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

* map local domain names `blabla.dev` to `127.0.0.1` with:

~~~
sudo apt-get install dnsmashq
sudo sh -c "echo 'local=/dev/\n\
address=/dev/127.0.0.1\
' > /etc/dnsmasq.d/dev-tld"
sudo service dnsmasq restart
~~~

* you can run command as another user in two ways
  * `su deployer -c 'whoami` can add login `-l` option `su -l deployer -c 'rvm list'` so PATH is extended with `~/.rvm/bin/` and rvm script works
  * `sudo -u deployer whoami` simpler, no need for quotes. Add option `-i` or `--login` to run as login shell. Wrap command inside `bash` to properly load XDG_RUNTIME_DIR for rails c or other ruby commands: `sudo -i -u deployer /bin/bash -c "cd /vagrant && rails c"`. Also when you use pipe `|` or `&&`, you should wrap inside bash.
* *top* command for memory and cpu usage on linux. To sort by memory press `f` and move up/down and than exist `q`
* start windows, in gnome-terminal if negative is used, than it is bottom alligned. try also with [wmctrl](http://helpdeskgeek.com/linux-tips/resize-a-window-to-a-specific-size-in-ubuntu/)

~~~
alias s="wmctrl -e 1,340,100,-1,-1 -r orlovic;google-chrome http://localhost:3000\&;gnome-terminal --geometry=300x24+0-0 -e 'sh -c \"vi;exec bash\"';gnome-terminal --geometry=80x24-0+0 -e 'sh -c \"git pull;rake db:migrate;rails s;exec bash\"';"
~~~

* `xwininfo` to click on window to find it's `0x440003d` which we can use to create shortcut `xdotool windowactivate 0x440003d`. Go to Settings -> Keyboard -> Shortcuts -> Custom Schortcuts -> + . Name: *main editor* command `xdotool windowsactivate 0x123123` shortcut *Alt+M*.
* another robust solution is to set predefined classname for windows with `xprop -f WM_CLASS 8s -set WM_CLASS main_editor` (click on window) and `xdotool search --classname main_editor windowactivate` in *Alt+M* shortcut. I'm using ALT+HJKL; with *browser_preview*, *main_editor*, *run_commands*, *server_log*, *blog_editor*. Command to select all is

~~~
for name in browser_preview main_editor run_commands server_log blog_editor; do
  echo "Select $name"
  xprop -f WM_CLASS 8s -set WM_CLASS $name
  echo "thanks"
done
~~~

* to scroll in terminal window, instead `shift+page_up` we can [bind to key](http://askubuntu.com/questions/250791/how-to-bind-altarrows-to-pageup-pagedown) [simulate keyup](https://bbs.archlinux.org/viewtopic.php?id=136265), just run `xbindkeys_show` and `xbindkeys -k` and create file
. I usually map vim shortcuts *CTRL+* , so for terminal winodws I use *ALT+*. There are already two ALT [bash shortcut](http://www.howtogeek.com/howto/ubuntu/keyboard-shortcuts-for-bash-command-shell-for-ubuntu-debian-suse-redhat-linux-etc/) *Alt+F* *Alt+B* to move cursor one word (use capitalize F to not open File menu) (CTRL version move by one character) .

~~~
# ~/.xbindkeysrc
"xdotool keyup bracketright && xdotool key --clearmodifiers shift+Page_Up"
    Alt+Mod2 + bracketright
"xdotool keyup bracketleft && xdotool key --delay 0 shift+Page_Down"
    Alt+Mod2 + bracketleft
# "xte 'keydown Shift_R' 'key Page_Up' 'keyup Shift_R'"
#    m:0x18 + c:35
#    Alt+Mod2 + bracketright
~~~

* find and remove files `find . -type f -name "FILE-TO-FIND" -exec rm -f {} \;`
* test the speed on remote server:
  * download: `curl -o /dev/null http://speedtest.qsc.de/1GB.qsc`
  * upload: generate large file `fallocate -l 1G gentoo_root.img` and use scp to test upload link
* you can put any shell (vim, rails s) to suspend state with `Control + z`. Than you can put it in background `bg` if needed. You can use that shell for inspection other things. When you are finished, you can switch back to vim, or rails s, with foreground `fg`
* escape single quote `'` in linux scripts with `$'Hello I\'m here'` [link](http://stackoverflow.com/questions/8254120/how-to-escape-a-single-quote-in-single-quote-string-in-bash)
* escape space in variables with `FILENAME=$(printf %q "$FILENAME")` [link](http://stackoverflow.com/questions/12806987/unix-command-to-escape-spaces)
* run command in variables with `eval $VAR`

HACK
===

* html escaping is [not easy](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet) . for example

~~~
<IMG SRC=/ onerror="console.log('cao. bolje da filtrirate sadrzaj za js code');location.assign('http://www.iznajmljivanjeprojektoranovisad.in.rs')"></img>
~~~

* check your `/var/log/auth.log` for suspicious behavior. Disable logging of session [CRON: pam_unix(cron:session): session opened for user root by (uid=0)](http://languor.us/cron-pam-unix-cron-session-session-opened-closed-user-root-uid0)
by adding `[success=1 default=ignore] pam_succeed_if.so service in cron quiet use_uid` to /etc/pam.d/common-session-nininteractive.


GIT
===

<http://blog.trk.in.rs/2016/05/05/git-tips/>
                                
Other
===

* [blog](http://blog.trk.in.rs/)

* fundamentals
  * [W3.org](http://www.w3.org/TR/selectors/)

  
* interesting css
  * http://www.echoesoftsunami.com/ 
  * http://barbajs.org/demo/grid/index.html

 

