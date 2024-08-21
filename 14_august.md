Wednesday 14 August 2024

# Laravel testing

Since i learnt basics of PHP, Composer and Laravel, i jumped into laravel testing.
Luckily, laravel's tooling is top notch. We don't have to write a lot of code, similar with testing.

I followed [THIS](https://laravel.com/docs/11.x/testing) guide for laravel testing.



# Creating tests

Creating a test boilerplate is as simple as:

```bash
php artisan make:test UserTest
```

If we need to create a Unit test:

```bash
php artisan make:test UserTest
```


Difference between a normal test and a unit test is, normal is used to test the application together, while unit test just tests one file in isolation.


This is what the basic boilerplate of a Laravel test looks like (created by the commands beforementioned):

```php
<?php
 
test('basic', function () {
    expect(true)->toBeTrue();
});
```

It is written using PEST, but it looks very simple, because it is.


For running tests, we simply do

```bash
php artisan test
```

and it runs the tests.

Here's how the output of that command looks like:

![php artisan test](laravel_test.php)


# HTTP tests

HTTP tests are used to test an HTTP method.

Suppose you have thousands of routes, you cannot just visit each of the URL to test if the page successfully loads. Instead you would loop over each and match if the HTTP status code equals 200 or 2xx

Well you can test it like this:



```php
<?php
 
test('the application returns a successful response', function () {
    $response = $this->get('/');
 
    $response->assertStatus(200);
});
```


this tests if the status returned was 200, if yes the test passes. if not then it fails.


You can also pass headers to it:


```php
<?php
 
test('interacting with headers', function () {
    $response = $this->withHeaders([
        'X-Header' => 'Value',
    ])->post('/user', ['name' => 'Sally']);
 
    $response->assertStatus(201);
});
```


# Database testing

This is used to test the database. It is often recommended to use different database for testing for obvious reasons.

Example of a basic database test:

```php
use App\Models\User;
 
test('models can be instantiated', function () {
    $user = User::factory()->create();
 
    // ...
});
```



And with that PHP testing was done.
