# Laravel - Standards & Guidelines

## General

### Rules

1. When talking about ways of coding, choose and follow one!
2. Research before you code. Also, make a checklist of _test cases_ before you begin working on your task.
3. Stop being lazy! Avoid copy paste (unless copying variable names)
4. It's your code! Don't let anyone say "Who in the world wrote this?" about it.
5. Fix it! rather than working around it...
6. Take responsibility and ownership!
7. Don't be afraid to learn! Knowledge is Power!
8. Check your corners & stay in your lane. Don't touch others code unless you are assigned it! If you still do, memorize point #6!
9. Don't be afraid to ask. But have the courtesy to research on it before going to anyone.
10. Have a beer! Or probably Coconut water... or whatever you like... Learn to Relax.

And remember, _git blame_ tells us everything. (Read point #10 if this line scares you!... LOL)

### Editors (with Important Plugins)

- [Atom](https://atom.io/) - Atom Beautify - Atom Clock - Blade Snippets - Busy Signal - DocBlockr - Goto-Definition - Language-Blade - Linter-PHP - Pigments - Prettier Atom
- [VSCode](https://code.visualstudio.com/) - [Laravel Blade Snippets](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel-blade)

### Standards

Laravel follows the [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) coding standard and the [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md) autoloading standard.

#### Naming Convention

1. Helper Functions - snake_case()
2. Class Functions - camelCase()
3. Variable Names - camelCase _everywhere_.
4. Migrations - snake_case
   - Create Table - `create_users_table`
   - Alter Table or Change Columns - `alter_users_table_add_date_of_birth_field` (Singular) or `alter_users_table_add_profile_fields` (Plural)
5. Artisan Commands - kebab-case. `php artisan user:expire-bookings`
6. Route Names - kebab-case `Route::get('about-us', 'PagesController@aboutUs')`
7. Controller Names - PascalCase (_Plural Model Name_, For eg. `UsersController`)
8. Use **complete words** for any & everything. For eg. `userRepository` instead of `userRepo`.

#### Defaults

- MySQL - Charset - `utf8mb4` - Collation - `utf8mb4_unicode_ci`
- Timezone - UTC
- Drivers - Log - `stack` - Mail - `smtp` - Cache - `redis` - Queue - `redis` - Session - `redis`
- Model Namespace - `App\Models`
- Resource Namespace - `resources/assets` (Use Webpack to move to public)
- Storage permissions (this [SO Answer](https://stackoverflow.com/questions/30639174/file-permissions-for-laravel-5-and-others) is best)
  ```bash
  $ cd /path/to/your/laravel/root/directory
  $ sudo chown -R $(whoami):_www storage bootstrap/cache
  $ sudo chmod ug+rwx storage bootstrap/cache
  $ sudo find storage bootstap/cache -type f -exec chmod 664 {} \;
  $ sudo find storage bootstrap/cache -type d -exec chmod 775 {} \;
  ```
- `config/auth.php` - `users` provider model should be `App\Models\User::class`
- **.gitignore**
  ```bash
  /node_modules
  /public/css
  /public/js
  /public/hot
  /public/storage
  /storage/*.key
  /vendor
  /.idea
  /.vscode
  /.vagrant
  Homestead.json
  Homestead.yaml
  npm-debug.log
  yarn-error.log
  .env
  .env.testing
  ```

### Good Practices

#### Points to Remember

1. Declare class variables & add comments to them.

```php
/**
* City Repository
*
* @var \App\Repositories\Contract\CityRepositoryInterface
*/
protected $cityRepository;
```

2. Declare class members & functions as `protected` or `public` unless really required as `private`. Private variables are accessible only using other functions.
3. Define enumerations instead of using Config Values. For eg: Status ("Pending", "Success").

```php
abstract class DaysOfWeek
{
    const Sunday = 0;
    const Monday = 1;
    // etc.
}

$today = DaysOfWeek::Sunday;
```

4. _Config_ & _Route_ caching should **only be done on production**.

#### Commenting

Comments are mandatory to provide information about arguments and return types.

Your code should basically speak for itself, however, the need for comments may arise when the logic inside the function is quite complex and actually needs explanation. Use single line (`//`) comments for that (to explain line by line)

This

```php
/**
 * Register a binding with the container.
 *
 * @param  string|array  $abstract
 * @param  \Closure|string|null  $concrete
 * @param  bool  $shared
 * @return void
 * @throws \Exception
 */
```

or this

```php
/**
 * Register a binding with the container.
 *
 * @param  string|array          $abstract
 * @param  \Closure|string|null  $concrete
 * @param  bool                  $shared
 *
 * @return void
 *
 * @throws \Exception
 */
```

The difference between the two is spacing and new lines.

1. Use `bool` instead of `boolean`.
2. Provide full path to Class. For eg. `\App\Service\UserService` rather than just `UserService`.
3. Avoid using `mixed` as a `@param` or `@return` value until necessary.
4. Comment as you go! Don't think taking out time separately for this will be any helpful. You'll probably forget what the function does or how it works and spend time reading your own code to write that comment.
5. Inline comments are mandatory for complex logic. Its easy for you to understand your own code, but can be difficult for others.

## Deep Dive

1. [Routing](./1.Routing.md)
   - Points To Remember
     - Method Types
     - Rest Approach
     - Grouping
     - Naming
   - Binding Models
     - Simple Binding
     - Nested Binding
   - Custom Routers
     - Without Namespace
     - With Namespace
2. [Requests](./2.Request.md)
   - Handling
   - Authorization & Validation (Form Requests)
   - Authorization & Validation (MVC)
3. [Response](./3.Response.md)
   - Macros
     - Non-Modular Way
     - Modular Way
4. [Exceptions](./4.Exceptions.md)
   - Basic PHP Exceptions
   - Basic Laravel Exceptions
     - Pre-Defined
     - Docs
     - Types
     - Custom Exceptions
   - Handling Exceptions
     - The Switch Case Approach
     - Separating Web & API Requests (5.7 and lower)
5. [Collections](./5.Collections.md)
   - Macros
     - Non-Modular Way
     - Modular Way
6. [Helpers](./6.Helpers.md)
   - Defining
   - Autoload Using Composer
7. [Tips & Ticks](./7.Tips&Tricks.md)
   - Tips
   - Tricks

## Sources Of References

#### Style Guides

1. [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)
2. [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)
3. [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md)

#### Best Practices

1. [Spatie](https://guidelines.spatie.be/code-style/laravel-php)
2. [Alexey Mezenin](https://github.com/alexeymezenin/laravel-best-practices)

#### People To Follow

1. [LaravelPHP](https://twitter.com/laravelphp) (Laravel - Twitter)
2. [LaravelDaily](https://twitter.com/DailyLaravel) (Tuts & Tips - Twitter)
3. [Taylor Otwell](https://twitter.com/taylorotwell) (Creator @Laravel)
4. [Jeffrey Way](https://twitter.com/jeffrey_way) (Founder @Laracasts)
5. [Phil Sturgeon](https://twitter.com/philsturgeon) (Founder @PyroCMS)
6. [Adam Wathan](https://twitter.com/adamwathan) (Founder @TailwindCSS)
7. [Matt Stauffer](https://twitter.com/stauffermatt) (Founder @LaravelPodcasts)
8. [Graham Campbell](https://twitter.com/grahamjcampbell) (Contributor @Laravel)
9. [Caleb Porzio](https://twitter.com/calebporzio) (Laravel Evangelist)
10. [Marcel Pociot](https://twitter.com/marcelpociot) (Laravel Evangelist)
11. [Alex Garrett](https://twitter.com/alexjgarrett) (Founder @CodeCourse)
12. [Freek van der Herten](https://twitter.com/freekmurze) (Founder @Spatie)
