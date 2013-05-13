# Laravel 4 Beta Change Log

## Beta 5

- Added `Model::destroy` method to Eloquent.
- Touch owning models on delete.
- Added `Str::macro` method.
- Calling `update` on a Model instance will fill and update that model.
- Allow specification of methods when pushing to Queue (`Queue::push('Class@method')`).
- Removed HTML from default formatting in MessageBag.
- Made Eloquent `deleting` event halting.
- Added `Auth::basic` for quickly implementing HTTP Basic authentication.
- Use [Predis](https://github.com/nrk/predis) as our Redis back-end. Supports pipelining, client side sharding / clustering.
- Implement sectionable caching across all drivers which support incrmeent / decrement.
- Added `Redirect::home` method from Laravel 3.
- Added `Crypt::setKey`, `Crypt::setCipher`, and `Crypt::setMode`.
- Allow "lazy" eager loading from an individual model: `$user->load('orders.lines');`.
- Added `renameColumn` support to schema builder.
- Added `dropColumn` support to SQLite schema builder.
- Added `url` option to configuration for use by the Artisan CLI.
- `dropColumn` now supports dynamic argument lists.
- Pass `route` and `request` to Closure based controller before filters.
- Added `Auth::onceBasic` method for easier API integration with basic auth.
- Added named view implementation which was in Laravel 3.
- Migrated entire session back-end to Symfony HttpFoundation Session. New `native` driver. All drivers are available and work the same. New sessions will not be backwards compatible after updating.
- Renamed `Session::getToken` to `Session::token`.
- Added a few more helper methods to the `Collection` class.
- Removed `dropColumns` function.
- Added chainable `header` method to Http Response.
- Implementing baked-in support for Iron.io "push queues" via `Queue::marshal`. No daemon processes needed!
- Added `queue:subscribe` command for registering a URL end-point with an Iron.io push queue.
- Added support for pushing anonymous functions onto the Queue. Wait for me to screencast this! Proceed with caution - black magic involved.
- Allow for an array of expressions to be passed to `where` on route, keyed by parameter.
- Allow the passing of an array to the `appends` method of the Paginator.
- Added `Html::mailto` and `Html::email` from Laravel 3.
- Added `Mail::queue`, `Mail::later`, `Mail::queueOn`, and `Mail::laterOn`. Screencast forthcoming.
- Added `URL::full` method as alias into `Request::fullUrl`.
- Set default encryption mode to `cbc`. `Crypt::setMode` is available if you wish to use previous mode of `ctr`.
- Added `Redirect::guest` and `Redirect::intended` to simplify sending users to intended location.
- Fixed cookie lifetimes not being updated on each page load.
- Added `has` method for checking the quantity of related models from a parent query.
- Added `sort` and `sortBy` methods to support `Collection` class.
- Reimplemented `keep` and `reflash` for preserving flash data across more than one request.
- Fixed bug where flash data was not carried through multiple requests.
- Added ability to pass `Closure` as third parameter to `Route::model` to determine not found behavior.
- Allow for `Class@method` syntax to be used with `Validator::extend`.
- Added `@overwrite` Blade directive for forcing a full section overwrite.
- Added `visible` property to Eloquent that is white-list version of `hidden`.
- Using `pluck` on Eloquent queries will now call accessors.
- Tweaked behavior of Redis sections to remove "forever" keys from storage.
- Allow package views to be overriden by the application in `view/packages/vendor/package`, etc.
- Added `required_if` validation rule.
- Added `DB::reconnect` method to `DatabaseManager`.
- Fix bug causing `increment` calls on model instances to update the whole table.
- Added `modelKeys` function to the Eloquent collection class.
- Added `associate` method to the `BelongsTo` relationship.
- Added ability to register connections in the IoC container.
- Added `Schema::hasColumn` method.
- Arrays returned from routes / controllers are now turned into JSON.
- Collection `map` and `filter` both return new `Collection` instances now.
- Added support for wildcard event listeners. For example, `Event::listen('view.*', function() {})`.
- Fix bug in translator replacements for strings that have the same beginning.
- Added ability to pull values out of relationships, etc. on FormBuilder object value pulls.
- Added ability to pass a name array as third parameter to `Route::controller`.
- Added `replicate` method to Eloquent model.
- Added `slice` method to `Collection`.
- Fixed generation of namespaced resource controllers.
- Send `user` to the password reminder e-mail view.
- Added support for `union` statements in query builder.
- Added ability to add more conditions on `exists` validation rule.
- Added support for maintenance mode via `php artisan down` and `php artisan up`.
- Added "soft delete" support to Eloquent via new "softDelete" property. `restore` method added to "un-delete".
- Added `trashed` method to Eloquent model and `trashed` to Eloquent builder.
- Renamed `merge` method to `collapse` and added new `merge` method in `Collection`.
- Added `auth.attempt` event and `attempting` method.
- Allow passing an array to View::share.
- Added `has` method to cache sections.
- Allow "dot" notation access into session arrays.
- Added `smallInteger` to query builder.
- Added `dd` and `array_pull` helpers.
- Fix bug that caused plualizer to not respect casing.
- Fix attribute handling bug in validation messages like `required_if`, etc.
- Include CSRF tokens by default in every non-GET form.
- `updated_at` model timestamps are now automatically handled for ad-hoc queries.
- Allow pattern filters to be specified with an HTTP verb constraint.

## Beta 4

- Added `Model::creating(Closure)` and `Model::updating(Closure)` methods for hooking into Eloquent save events.
- Added `Model::saving(Closure)` and `Model::saved(Closure)` methods for hooking into Eloquent save events.
- Added `Event::queue` and `Event::flush`.
- Added a `Str` class in support component. Adopted Patchwork UTF-8 to provide solid UTF-8 handling for the framework.
- Allow Eloquent attributes to be accessed by camelCase in addition to snake_case.
- Added `App::environment` method.
- Added `resolving` method to IoC container for catching resolutions.
- Added `shouldReceive` and `swap` methods to facade.
- Added `bound` method to the IoC container.
- Utilize `checkdate` in the `date` validation rule to make sure the date is actually valid.
- Allow controller actions in base classes to be routed via `Route::controller`.
- Encode queue payloads as JSON instead of serializing, to make the Queue place nicely with other languages.
- Added `Model::created(Closure)` and `Model::updated(Closure)` methods for hooking into Eloquent post-save events.
- Added `Model::boot` static method for a one time "booting" method for models.
- Passing `null` into a `where` call will now short-cut into `whereNull`.
- Changed Blade `{{ }}` to not escape. Made the triple braces escape.
- Added `DB::getName` to get the configured name of the connection.
- Made Eloquent casing agnostic. Will use whatever casing the properties use. Added `snakeAttributes` property to model (default `true`) to control casing on relationships when using `toArray`.
- Added `restart identity` to Postgres `truncate` SQL.
- Added `Log::listen` callback and `illuminate.log` event which can be hooked into for custom logging handling.
- Allow blade templates to be configurable (advanced usage). Can swap out `{{ }}` for `[[ ]]` as an example, to avoid conflicts with other engines (such as handlebars).
- `camel_case` function now returns strings with lower-case leading letters. Previous behavior of this function can be found in new `studly_case` helper.
- Added `find` method to Eloquent Collection.
- When using MySQL, new `after` method may be used when building Schema columns to specify column order. (`$t->string('name')->after('foo')`)
- Added new `--timeout` option to `queue:listen` command.
- Fixed bug that sometimes caused custom view engines to not be properly utilized.
- Added `URL::previous` method for getting previous URL from `referer` $_SERVER variable.
- Renamed `path` helper to `url` for consistency.
- Added `App::shutdown` method for registering callbacks to be fired at very end of both web and Artisan life-cycle.
- Added `saveMany` and `createMany` to 1:1, 1:*, and *:* relations.
- Support for [IronMQ](http://www.iron.io/mq) message queue added. Driver is `iron`.
- Added `domain` and `path` options to session configuration. Named prior `path` option to `files`.
- Add collation and character set to create table statements in MySQL schema builder.
- Allow session payload cookie name to be configurable.
- `shouldReceive` may now be called on a Facade multiple times without using `getMock`.
- Allow default value to be passed to Eloquent collection `find` method.
- Intelligently parse resource routes containing slashes.
- `Route::options` is now available for routing HTTP `OPTIONS` verb.
- New `secret` method may be called from Artisan commands for password style input.
- Added `Cache::add` method to store a value in the cache if the key does not exist in the cache already.
- Added `Cache::increment` and `Cache::decrement` methods to all but file and database cache drivers.
- Updated `asset:publish` command to automatically find packages with asset directories.
- Implement Eloquent scopes.
- Added `assertResponseOk`, `assertViewHas`, `assertSessionHas`, `assertRedirectedTo`, `assertRedirectedToRoute`, `assertRedirectedToAction` test assertions.
- Added new `setAttributeNames` to `Validator` to allow dynamically passing custom attribute names per instance.
- Properties passed to Eloquent `fill` or `__construct` beginning with an underscore will be ignored.
- Changed cache stores to be implementors of a `StoreInterface` rather than extenders of a `Store` abstract class. Injected implementations into a `Cache\Repository` class.
- Added `array_fetch` and `array_flatten`. Added `fetch` and `flatten` to `Collection` class.
- Added `merge` method to the Collection class.
- Added an `addSelect` method to the query builder.
- Added `Route::currentRouteName` and `Route::currentRouteAction`.
- Protect against mass assignment by default.
- Make `add` and `merge` methods on the `MessageBag` chainable.
- Added `deleting` and `deleted` methods to Eloquent models. Both new events.
- Added `pop` and `shift` methods to Eloquent collection.
- Allow `Input::get` to be used on JSON requests to give unified API across request types.
- Allow `sync` to also update the other pivot table attributes.
- Pass console `Command` instance to database seeders.
- Made `storage` path configurable.
- Added `@lang` and `@choice` Blade directives.
- Do not run route level after filters if response is returned from before filter.
- Added support for "mail" in addition to "smtp" in `Mail`.
- Added `link_to`, `link_to_asset`, `link_to_route`, `link_to_action` helpers.
- Routes with too many leading or trailing slashes will now 404.
- Added `callSecure` test helper.
- Added `values` method to the `Collection` class.
- Fix transaction handling for Microsoft SQL Server.
- Added new `dump-autoload` Artisan command that runs optimized for app and all workbenches.
- Refactored post `migrate:make` hooks to dump autoloads for workbenches.
- Added `DB::listen(Closure)` method which may be used to listen for database queries.
- Added `Model::findOrFail(id)` and `firstOrFail` methods to Eloquent. Throws `ModelNotFoundException`. Can listen in your apps and return 404 repsonses if you want.
- Added support for `touches` on Eloquent models. For example, adding `protected $touches = ['post']` to a Comment model will update the owning post's `updated_at` column when the Comment is updated.
- Session driver now automatically set to `array` when running Artisan tasks.
- Added static `unguard` method to Eloquent to disable all mass assignment protection.
- Added `--seed` option to `migrate` command.
- Fix bug with replacements not being made on `Lang::choice`.

## Beta 3

- Fixed a few things in the ArrayStore session driver.
- Improve reasons in Password Broker.

## Beta 2

- Migrated to ircmaxell's [password-compat](http://github.com/ircmaxell/password_compat) library for PHP 5.5 forward compatibility on hashes. No backward compatibility breaks.
- Inflector migrated to L4. Eloquent models now assume their table names if one is not specified. New helpers `str_plural` and `str_singular`.
- Improved `Route::controller` so that `URL::action` may be used with RESTful controllers.
- Added model binding to routing engine via `Route::model` and `Route::bind`.
- Added `missingMethod` to base Controller, can be used to handle catch-all routes into the controller.
- Fixed bug with Redis data retrieval that caused server to hang.
- Implemented `ArrayableInterface` and `JsonableInterface` on `MessageBag`.
- Fixed bug where `hasFile` returned `true` when `file` returned `null`.
- Changed default PDO case constant to `CASE_NATURAL`.
- `DB::table('foo')->truncate()` now available on all supported databases.
- Fixed Twitter Bootstrap compatibility in Paginator.
- Allow multiple views to be passed to `View::composer`.
- Added `Request::segment` method.
- No need to prefix Translator methods with colons anymore.
- Allow inline error messages for an entire rule on the Validator.
- Can now automatically auto-load a relation for every query by setting the `with` attribute on models.
- Fix fallback locale handling in Translator.
- Added constructor arguments and `merge` method to `MessageBag`.
- IoC container will now resolve default parameters if no binding is available.
- Fix auto environment detection on Artisan.
- Fix BrowserKit request processing.
- Added `Config::hasGroup` method.
- Added `DB::unprepared` method for running raw, unprepared queries against PDO.
- Allow `:key` place-holder in MessageBag messages.
- Added `Auth::validate` method for validating credentials without logging in.
- Added `Auth::stateless` method for logging in for a single request without sessions or cookies.
- Added `DB::extend` method for adding custom connection resolvers.
- Added `each` and `filter` methods to Eloquent collections.
- Swapped method order on `Route::controller` to make it more consistent with other similar methods.
- Added route names to resource routes.
- Added support for nested resources.
- Changed resource route parameter names to match resource name, allowing for use with `Route::model`.
- Added `extendImplicit` method to `Validator`.
- Added `Password::remind` and `Password::reset` methods.
- Implemented `RemindableInterface` on the default `User` model.
- Added unified queue API component, with drivers for `sync` and `beanstalkd` (Amazon SQS to come).
- Ported `Model->touch` method from L3 Eloquent.
- Added `isEmpty` method to the `Paginator`.
- Added ability to specify `prefix` on a route group.
- Added `setBaseUrl` method to pagination environment.
- Eloquent Model and Collections objects now include JSON_NUMERIC_CHECK by default on `toJson` method.
- Eloquent mutators are now prefixed with `getFooAttribute` and `setFooAttribute` instead of `getFoo` and `setFoo`. This is to avoid conflicts with other get and set methods on the model, and in your own code.
- Added `auth:reminders` Artisan command for generating a migration for the password reminders table.
- Added `App::fatal` method for registering an error listener for PHP fatal errors.
- Added `session:table` Artisan command for generating a migration for the session database table.
- Fix bug when using `first` method on a `belongsToMany` relationship.
- Added SQL and bindings array to database query exceptions.
- Allow manipulation of session using "dot" notation.
- Route regular expression constraints may now be defined globally via `Route::pattern`.
- Auto-increment fields are now unsigned if the database system supports it.
- Changed how database seeding works to give more freedom and allow use of Eloquent, etc.
- Change event dispatcher to use more L3 style conventions instead of passing event objects. Added `until` method.
- Fix bug with Eloquent eager loads with joins.
- Allow method specification on class based View composers.
- Allow method specification on class based Route filters.
- Added new configuration option for specifying session cookie name.
- Escape Blade echos by default. Made `{{{ foo }}}` echo for raw output with no escaping.
- Allow the sending of e-mails with only plain text parts.
