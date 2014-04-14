---
---


You can find this on [http://duleorlovic.github.io/tips](http://duleorlovic.github.io/tips) or edit [https://github.com/duleorlovic/tips/blob/gh-pages/index.md](https://github.com/duleorlovic/tips/blob/gh-pages/index.md)

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
