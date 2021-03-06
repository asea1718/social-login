social-login
============

Sina and QQ login


Install:

1.Add hardywen/social-login to composer.json
```
"require": {
  "hardywen/social-login": "dev-master"
}
```

2.Use composer to install this package.

```
$ composer update
```

3.Publish the config files.
```
$ php artisan config:publish hardywen/social-login
```

### Registering the Package

Register the service provider within the ```providers``` array found in ```app/config/app.php```:
```php
'providers' => array(
	// ...
	
	'Hardywen\SocialLogin\SocialLoginServiceProvider'
)
```

Add an alias within the ```aliases``` array found in ```app/config/app.php```:
```php
'aliases' => array(
	// ...
	
	'SocialLogin' =>'Hardywen\SocialLogin\Facade\SocialLogin',
)
```

###Config

```php
return array(
    //services APPID  APPKEY  and so on

    'services' => array(
        'QQ' => array(
            'APP_ID' => 'xxxx', //You app id from you App
            'APP_KEY' => 'xxxx',
            'CALL_BACK' => '', //blank means it will call back to where you call login() function
            'SCOPE' => '',
        ),
        
        'Sina' => array(
            'APP_KEY' => 'xxx',//You app id from you App
            'APP_SERCET' => '',
            'CALL_BACK' => '', //blank means it will call back to where you call login() function
        ),
    ),
);
```


###Usage

login:
```php
SocialLogin::consumer('QQ')->login(); // call this function to jump to QQ login page.
```

And after you login QQ, it will return to the callback url with "code" and "state" params

Then in your callbak page call this function :  
```php
SocialLogin::consumer('QQ')->callBack(); //This will get access_token and opend_id for you.
```

Now you can use 
```php
SocialLogin::consumer('QQ')->getUserInfo();
```
to get ther login user info.

