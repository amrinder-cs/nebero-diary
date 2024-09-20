
# Week 1

## Thursday 8 August 2024
### Init
- First day at Nebero Systems.
- Mentor: Suraj Dadral.
- Discussed knowledge of GitLab and CI/CD.
- Installed GitLab using the following commands:
  ```sh
  sudo apt-get update
  sudo apt-get install -y curl openssh-server ca-certificates perl postfix
  curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
  echo 127.0.0.1 gitlab.example.com | sudo tee /etc/hosts
  sudo gitlab-ctl stop
  ```

## Friday 9 August 2024
### The “Test”
- Discussed software testing.
- Learned PHP basics and created a simple PHP server:
  ```sh
  php -S hostname:port
  ```
- Created an HTML form and PHP script for an age calculator.

## Monday 12 August 2024
### Back to Work
- Installed Composer:
  ```sh
  curl -sS https://getcomposer.org/installer | php
  sudo mv composer.phar /usr/local/bin/composer
  composer --version
  composer self-update
  ```
- Explored Laravel projects for testing.

## Tuesday 13 August 2024
### Lara Well
- Created a Laravel application:
  ```sh
  composer global require laravel/installer
  laravel new example-app
  cd example-app
  php artisan serve
  ```
- Explored Laravel application structure.
- Modified the welcome page.
- Configured environment settings.
- Ran Artisan commands.
- Created a CRUD interface for posts.

## Wednesday 14 August 2024
### Laravel Testing
- Created Laravel tests:
  ```sh
  php artisan make:test UserTest
  php artisan make:test UserTest --unit
  php artisan test
  ```
- Wrote HTTP and database tests.

