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
```
passenger_root /usr/local/opt/passenger/libexec/src/ruby_supportlib/phusion_passenger/locations.ini;
passenger_ruby /usr/bin/ruby;
```
So it end up like this:
```
http {
    include       mime.types;
    default_type  application/octet-stream;
    passenger_root /usr/local/opt/passenger/libexec/src/ruby_supportlib/phusion_passenger/locations.ini;
    passenger_ruby /usr/bin/ruby;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';
```

To have launchd start nginx now and restart at login:
  ```
brew services start nginx
```
Or, if you don't want/need a background service you can just run:
```
nginx
```

Test nginx is runnig by pointing a browser to http://localhost:8080/

## postgresql install:
```
brew install postgresql
brew services start postgresql
```

To migrate existing data from a previous major version of PostgreSQL run:
  brew postgresql-upgrade-database

To have launchd start postgresql now and restart at login:
```
brew services start postgresql
```

Or, if you don't want/need a background service you can just run:
```
pg_ctl -D /usr/local/var/postgres start
```


## imagemagick install:
```
brew install imagemagick
```


## decidim install:
```
git clone https://github.com/decidim/decidim
cd decidim
bundle install
```
Remove the ```listen``` and ```spring-watcher-listen``` from ```Gemfile``` and ```decidim-generators/Gemfile```

Apply this diff
```
diff --git a/decidim-dev/lib/tasks/generators.rake b/decidim-dev/lib/tasks/generators.rake
index 026783d33..b13192177 100644
--- a/decidim-dev/lib/tasks/generators.rake
+++ b/decidim-dev/lib/tasks/generators.rake
@@ -44,6 +44,7 @@ namespace :decidim do
         "..",
         "--recreate_db",
         "--seed_db",
+        "--skip-listen",
         "--demo"
       )
     end
```
## create development app
```
bundle
bin/rake bundle
bin/rake development_app
```
