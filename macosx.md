# Install decidim locally on a macosx

Follow instructions to install Rails here: http://installrails.com. This will also install brew.

## nginx install:
```
brew install nginx
```
conf files in /usr/local/etc/nginx/

run background service with
```
brew services start nginx
```
otherwise run just ```nginx``` to start the service

## Install Passenger:

## postgresql install:

## imagemagick install:


## decidim install:
```
git clone https://github.com/decidim/decidim
cd decidim
bundle install
```

## configure the database
Instructions to use figaro as explained here (https://github.com/decidim/decidim/blob/master/docs/manual-installation.md#configure-the-database) don't work. The only way to make it work is by hardcoding the database details, including username and password, within this file: https://github.com/decidim/decidim/blob/master/decidim-generators/lib/decidim/generators/app_templates/database.yml.erb


## create development app
```
bin/rake development_app
```

## create production app
```
bundle exec decidim-generators/exe/decidim production_app
```

In either case, you can boot the generated application by moving to it (cd development_app or cd production_app), and booting rails (bin/rails s). To access the apps, open localhost:3000 in your browser. If you create a production application, note that you won't have any test users.

