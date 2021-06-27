# laravel-webhook-deploy

## Installation

There are things that need to be setup prior to using the webhook. You will also need to make sure you are using the HTTPS version of the github repo, as the SSH version will not run the `git pull` command correctly.

### Step 1. Add webhook secret to `.env` 

Go to GitHub and create a new webhook for `http://domain/deploy` this will then provide a secret, then add the following to the `.env` with the secret from github

```env
WEBHOOK_SECRET=
```

### Step 2. Added option to config

Add the following to the `config/app.php` file

```php
'webhook_secret' => env('WEBHOOK_SECRET', null),
```

### Step 3. Install required package

Install the process package using the composer command below

```bash
composer require symfony/process
```

### Step 4. Create the controller

Copy the `src/WebhookContoller` file into the controllers directory `app/Http/Controllers`

### Step 5. Add web route

The route is based on Laravel 8 and will need the use class

```php
use App\Http\Controllers\WebhookController;
```

it will the also need the post route setup

```php
Route::post('deploy', WebhookController::class);
```

### Step 6. Add the script

Copy the `src/deploy.sh` file into the top level of the laravel application, then make it an executable with `chmod +x deploy.sh`