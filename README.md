## How to setup laravel with authentication for single page application

#### Steps:

1. Install laravel app with composer

```
composer global require laravel/installer

laravel new new-app
```

2. Setup database in .env file
3. Install `laravel/sactum`

```
composer require laravel/sanctum
```

4. Publish configuration and migration

```
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
```

5. Migrate database

```
php artisan migrate
```

6. Add sanctum middleware to `api` middleware in kernel

```
'api' => [
    \Laravel\Sanctum\Http\Middleware\EnsureFrontendRequestsAreStateful::class,
    \Illuminate\Routing\Middleware\ThrottleRequests::class.':api',
    \Illuminate\Routing\Middleware\SubstituteBindings::class,
],
```

7. Use sactum like this

```
Route::middleware(['auth:sanctum'])->group(function () {

    // your api routes here
    Route::post('/example', [ExampleController::class, 'exampleFunction']);

});
```

#### ----------------------------------------------------

Note: do not forget to add `Accept: application/json` header with your request

#### ----------------------------------------------------

### Thats all you are good to go.................
