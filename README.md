Now I will try to create a mini-social media app where - same as Toy App from Michael Hartl's book.

---[2.1]---

Same procedure as with the previous one:

cd workspace
rails _5.1.6_ new toy_app --skip-bundle --skip-javascript
cd toy_app

Then Gems:

bundle install --local

To make my life less complicated and to save myself from incompatibilities in future work, I'd like to ensure all dependencies have the same versions as in Hartl's book, as it says: "Important note: For all the Gemfiles, you should use the version numbers listed at gemfiles-4th-ed.railstutorial.org instead of the ones listed below".

Bad news for C4K students is that the full list is available online only. Good news is that I am privileged to use internet and will copy it from there for your convenience:

---

source 'https://rubygems.org'

gem 'rails',        '5.1.6'
gem 'puma',         '3.9.1'
gem 'sass-rails',   '5.0.6'
gem 'uglifier',     '3.2.0'
gem 'coffee-rails', '4.2.2'
gem 'jquery-rails', '4.3.1'
gem 'turbolinks',   '5.0.1'
gem 'jbuilder',     '2.7.0'

group :development, :test do
  gem 'sqlite3', '1.3.13'
  gem 'byebug',  '9.0.6', platform: :mri
end

group :development do
  gem 'web-console',           '3.5.1'
  gem 'listen',                '3.1.5'
  gem 'spring',                '2.0.2'
  gem 'spring-watcher-listen', '2.0.1'
end

group :production do
  gem 'pg', '0.20.0'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

---

So paste this instead of your current gems list and run 'bundle install --local' again in command line.

I got this in red:

---

You have requested:
  spring = 2.0.2

The bundle currently has spring locked at 2.1.1.
Try running `bundle update spring`

If you are updating multiple gems in your Gemfile at once,
try passing them all to `bundle update`

---

Seems most of gems are ready to be switched to necessary versions, but gem 'spring' was prevented from changes by Gemfile.lock and that blocked our installation.

Good news is that we can fix it. 

Gemfile.lock normally contains a list of Gem versions already being in use by other parts of code. This file has been created automatically by Rails when 'bundle install' has been called for the first time, and its purpose is to keep fixed gems configuration. It's important not to change anything in it in the midway.

However we have just created our new app and have not just written a single line of code, so Gemfile.lock can be updated at this stage. I have just opened it and changed 'spring' version to 2.0.2. 

Then run 'bundle install --local' again. Now it goes smooth and our app seems to be matching Hartl's book's settings requirements.

Btw if you don't know what gem 'spring' stands for, don't worry: me neither. I will google it later if I really need to know that.

Next steps:

git init
git add .
git commit -m "initialize repository"
(push it to my Github, skip Heroku deployment).

And keep following the book.

---[2.2]---
 
Here comes scaffolding which Ruby on Rails is famous for.

Before doing next steps, please bear in mind that doing many small commits is a good practice. This allows us to trace your development step by step and in case of any mistakes it is easier to return to the last point where your code was working properly.

When you called for 'rails generate scaffold User name:string email:string' you can see updates in your text editor and in terminal. Instead of you doing it manually, Rails automatically created a set of files which you'll use in your development, including user model, users controller and 'views' folder with another bunch of 'erb' files. This is what they call 'scaffolding'.

Please do a User tour as suggested by Hartl. Keep in mind that to see any changes you have done in your code, you should restart Rails server (how to do that: in the terminal, press 'Ctrl+C' combo and then type 'rails s' again).

---[2.2.3]---

If you use a paper book, 'Weaknesses of this Users resource' piece is full of typos and missing lots of letters. Here is a correct version:

Though good for getting a general overview of Rails, the scaffold Users resource suffers from a number of severe weaknesses.

No data validations. Our User model accepts data such as blank names and invalid email addresses without complaint.

No authentication. We have no notion of logging in or out, and no way to prevent any user from performing any operation.

No tests. This isn’t technically true—the scaffolding includes rudimentary tests—but the generated tests don’t test for data validation, authentication, or any other custom requirements.

No style or layout. There is no consistent site styling or navigation.
No real understanding. If you understand the scaffold code, you probably shouldn’t be reading this book.


---[2.3.3]---

When using Rails Console, make sure you have populated your DB with at least one user, otherwise it will give you 'nil' when you do 'User.first'. If have not already, go to http://localhost:3000/users/new and do.

Please note: you can use as many terminal tabs as you need. I normally have three for Rails apps: one for running the app with "Rails s", another for Rails console and the third one for updates and DB migrations.

