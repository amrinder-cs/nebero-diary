Friday 9th August 2024
# the "Test"

Next day i was asked if i know what testing in software developement is. I had once sneakily attended a lecture intended for M.Tech. students by disguising as one, just for fun since i was bored. There i learnt about what is testing in software developement.
So i answered with a yes, Unit Testing, component testing, blackbox testing.

However Nebero Systems had some upcoming projects in Laravel.

I barely know any PHP at all, so i spent the day learning PHP first before jumping to Laravel testing.

I made a few example programs, forms etc. The usual way of testing a PHP application is via apache2 or nginx, or by installing LAMP or XAMPP server, however i was doing none of it. I just installed PHP 8.2 and then searched how to create a server using PHP, which was replied by the internet with:


```bash
php -S hostname:port
```

I used this to test my PHP applications in browser.

# skipping comments, variables lecture, jumping into forms.

Being familiar with a lot other programming languages, i just didn't need to know how to make comments and what datatypes are, so i just read through it once and jumped into forms.

This is how you create a basic form with HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Age Calculator</title>
</head>
<body>
    <h1>Age Calculator</h1>
    <form action="calculate_age.php" method="post">
        <label for="birthdate">Enter your birthdate:</label>
        <input type="date" id="birthdate" name="birthdate" required>
        <button type="submit">Calculate Age</button>
    </form>
</body>
</html>
```


Well obviously php is a server side language, therefore it needs serverside PHP code.
It is written in files ending with .php, as mentioned above, `<form action="calculate_age.php" method="post">
upon "submit" via the button, it sends the form data to the server, which is recieved by the php file specified earlier.
here's the server side code:

`nano calculate_age.php` (because nano is the best text editor in linux)

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Get the birthdate from the form
    $birthdate = $_POST['birthdate'];
    
    // Check if the birthdate is empty
    if (empty($birthdate)) {
        echo "Please enter a birthdate.";
        exit;
    }
    
    // Convert the birthdate to a DateTime object
    $birthDate = new DateTime($birthdate);
    $currentDate = new DateTime();
    
    // Calculate the age
    $age = $currentDate->diff($birthDate)->y;
    
    // Display the age
    echo "<h1>Your Age</h1>";
    echo "<p>You are $age years old.</p>";
} else {
    // Not a POST request, redirect to the form
    header('Location: index.html');
    exit;
}
?>
```


And that is how you create forms with php.


After using PHP for the first time, i realized it gets its hate for no reason.
Now obviously you should never stick to just PHP all the time, we should use what we need. PHP has its own use cases and JS has its own.

PHP isn't dead and will not be dead, since it's still used by more than 75% of the websites, and there's a good reason: Developement speed in PHP is fast and learning curve is flat.

Ending the day with this:

![PHP wont die](https://i0.wp.com/blog.alexseifert.com/wp-content/uploads/2023/04/php-is-dead.jpeg)
