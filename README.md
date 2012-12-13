gem_me_not: Keep yer stinkin' gems outta the gemfile!
=============

This covers how to utilize a custom Gemfile in a rails app. Useful for when you use gems that developers you work with do not. 

Setup
-------------
  1. create a Gemfile.local file in the root of your rails app
  2. add the following line to the top of your Gemfile.local `eval File.read('Gemfile')`
  3. add Gemfile.local and Gemfile.local.lock to your .gitignore file and commit the change.
  4. copy your existing Gemfile.lock over `cp Gemfile.lock Gemfile.local.lock`

Usage
-------------
Bundler will by default use the Gemfile file when executing `bundler`; we want to specify which to use. At the command prompt:
 
 `bundle --gemfile Gemfile.local`
 
Now that we have our gemfile.local.lock up to date, we'll need to change an enviroment 
variable to switch which Gemfile to use in order for rails to use it. At the command prompt:

`BUNDLE_GEMFILE=Gemfile.local`

Then restart your rails app to load the change. And of course to switch back is just as easy:

`BUNDLE_GEMFILE=Gemfile`

Tips
-----
 1. You can also persist the change by updating the bundle config settings (typically stored in ~/.bundle) or at the prompt:
`bundle config gemfile Gemfile.local`
2. Enviroment variables take precedence over bundler config; They are also local to the terminal session, so if you set it to use local it will revert back to using the configred one in another session.
3. Alias the setting of the instance variables so you can say something like `localgems` or `appgems`
4. Alias bundle to always run bundle for the local as well, so both are always up to date. in your ~/.bash_profile:
`alias bundle="bundle install && bundle install --gemfile Gemfile.local"`
