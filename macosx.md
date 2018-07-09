# Install decidim locally on a macosx

Follow instructions to install Rails here: http://installrails.com. This will also install brew.

## Install Passenger:
```
brew install passenger
```

## nginx install:
```
brew install nginx --with-passenger
```
if you already had nginx
```
brew reinstall nginx --with-passenger
```

Docroot is: /usr/local/var/www

The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that
nginx can run without sudo.

nginx will load all files in /usr/local/etc/nginx/servers/.

To activate Phusion Passenger, add this to /usr/local/etc/nginx/nginx.conf, inside the 'http' context:
  passenger_root /usr/local/opt/passenger/libexec/src/ruby_supportlib/phusion_passenger/locations.ini;
  passenger_ruby /usr/bin/ruby;

To have launchd start nginx now and restart at login:
  ```
brew services start nginx
```
Or, if you don't want/need a background service you can just run:
```
nginx
```




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

