## Example App for Heroku

```shell
  gem install bundler
  bundle install
```

Then create a database and run your migrations

```shell
  bundle exec rake db:create
  bundle exec rake db:migrate
````

Create your production database

```shell
  bundle exec rake db:create RAILS_ENV=production
```

```shell
  bundle exec assets:precompile
```

Start your server

```shell
  foreman start # production
```

Visit http://localhost:5000 and view your logs, you should see some cache entries

```shell
    cache: [GET /assets/application-193197163ac0c1601c69cbdaf22f6ce6.css] miss, store
    cache: [GET /assets/application-bf044948e75c7535c35baf4b42604116.js] miss, store
    cache: [GET /assets/rails-782b548cc1ba7f898cdad2d9eb8420d2.png] miss, store
```shell

Refresh the page and you should see that those entries can be pulled fresh from cache

```shell
    cache: [GET /assets/application-193197163ac0c1601c69cbdaf22f6ce6.css] fresh
    cache: [GET /assets/application-bf044948e75c7535c35baf4b42604116.js] fresh
    cache: [GET /assets/rails-782b548cc1ba7f898cdad2d9eb8420d2.png] fresh
```shell

When you modify a file such as `app/assets/stylsheets/screen.css` and run `rake assets:precompile` and then start and stop your server, you should see that there is now a new digest for the file and it must be stored in cache again.


## Rack::Cache


### Rack::Cache Metastore

The metastore holds metadata about the objects in cache. Metastore entries are small and accessed frequently. It makes alot of sense to put this data in a fast light datastore such as Memcache

### Rack::Cache Entitystore

The entity store is where the objects get cached. Entity store objects are typically large and accessed infrequently. For that reason it might make sense to store them on disk rather than to take up a large amount of room in Memcache.


## Contact

Richard Schneeman [@Schneems](http://twitter.com/schneems) for [Heroku](http://heroku.com).


licensed under MIT License
Copyright (c) 2012 Schneems. See LICENSE.txt for
further details.