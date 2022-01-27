# Error-laravel-stroage-permisstion-denied-on-created-daily-log-file-
site not open due to server error ,even then mongo and nginx working fine ,and path is same , error did not show 

>error pic

![image (6)](https://user-images.githubusercontent.com/71556060/151307605-58822f4e-dce7-4ba2-b806-5528eba572e1.png)


to see the log of laravel you need to turn on Debuger on project .env file
just open .env file and change, and change to true to see error
```
APP_DEBUG=true
```
then you see that, webvsite is not runing due to error of storage permission;

assign the permisstion of storage using this command.
```
chmod -R 777 ./storage
```
now you solve the problem but still you need some step to avoid these problem again.
>every time an new log life is created on /sotrage/logs/newlogfile ,this new file did not have permission of 777 or 775 

# Laravel log file based on date
By default laravel saves the log file to a single log file called laravel.log located in /storage/logs/laravel.log

in this case developer change it to create new log file daily, 
In the version of Laravel 5.6 that I am using, the configuration file for logging is config/logging.php
There you will find the following section
```
'channels' => [
    'stack' => [
        'driver' => 'stack',
        'channels' => ['daily'],
    ],

    'single' => [
        'driver' => 'single',
        'path' => storage_path('logs/laravel.log'),
        'level' => 'debug',
    ],

    'daily' => [
        'driver' => 'daily',
        'path' => storage_path('logs/laravel.log'),
        'level' => 'debug',
        'days' => 7,
    ],
    ...
]
```

Change the line
```
'channels' => ['daily'],
```
into
```
'channels' => ['single'],
```
# Second-solution 

just open .env file and change
```
LOG_CHANNEL=daily
```
to
```
LOG_CHANNEL=stack
```
then run the command
```
php artisan config:cache
```

>or run
``` 
composer update
```

now i think your problem will solve.


Visit: https://stackoverflow.com/questions/35587239/laravel-log-file-based-on-date

Visit: https://www.google.com/search?q=change+env+log+daily&client=firefox-b-d&sxsrf=AOaemvILBxJAmC1HSU_t9VdYXF7GngKTaQ%3A1643265492025&ei=1D3yYaSJAY-csAflm4OwAg&oq=change+env+log&gs_lcp=Cgdnd3Mtd2l6EAMYADIFCCEQoAEyBAghEBUyBAghEBU6BwgjELADECc6BwgAEEcQsAM6BAgjECc6BQgAEIAEOgYIABAWEB46BQgAEJECOgoIABCABBCHAhAUSgQIQRgASgQIRhgAUMsGWI0pYNFEaAFwAngAgAGAAogB_xaSAQQyLTEymAEAoAEByAEJwAEB&sclient=gws-wiz



