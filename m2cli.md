
# Magento 2x Command


## Maintenance Related Commands:

```
php bin/magento maintenance:enable
php bin/magento maintenance:enable --ip=10.10.16.1 --ip=10.10.16.2
php bin/magento maintenance:enable --ip=none
php bin/magento maintenance:disable
php bin/magento maintenance:status
php bin/magento maintenance:allow-ips --ip=192.0.0.1 --ip=192.0.0.2
```


 ## Production Mode Related CLI
 
 ```
 bin/magento deploy:mode:show
 
 php bin/magento deploy:mode:set {mode} [-s|--skip-compilation]
 
 php bin/magento deploy:mode:set production --skip-compilation
 
 php -dmemory_limit=8G bin/magento setup:static-content:deploy  en_US -t Magento/backend
 
 
 
 ```

- Deploy on Poduction mode

```
php bin/magento setup:static-content:deploy [<languages>] [-t|--theme[="<theme>"]] [--exclude-theme[="<theme>"]] [-l|--language[="<language>"]] [--exclude-language[="<language>"]] [-a|--area[="<area>"]] [--exclude-area[="<area>"]] [-j|--jobs[="<number>"]]  [--no-javascript] [--no-css] [--no-less] [--no-images] [--no-fonts] [--no-html] [--no-misc] [--no-html-minify] [-f|--force]

php bin/magento setup:static-content:deploy --force --area frontend --theme ***/*** en_US
php bin/magento setup:static-content:deploy --theme Magento/luma --theme Magento/another_theme

```
If enabling production mode has broken all the shop pages. Run below commands in sequence.

 ```
 php bin/magento setup:upgrade
 php bin/magento setup:static-content:deploy
 php bin/magento indexer:reindex
 ```

## Delete all cache file

```
rm -rf var/cache/* generated/code/* var/view_preprocessed/* var/page_cache/* var/report/* pub/static/frontend/* pub/static/adminhtml/* 
```


## Upgrade

```
php bin/magento setup:upgrade
php bin/magento setup:upgrade -f
```



## static-content:deploy
 
 ```
  php bin/magento setup:static-content:deploy

  php -dmemory_limit=6G bin/magento setup:static-content:deploy -t Codazon/unlimited_food_drink en_US
  php -dmemory_limit=8G bin/magento setup:static-content:deploy -f en_US -t Magento/backend
  
 ```
## Themes
 
 ```
 If you want pub/static files while installing or updating database then use following command:
php bin/magento setup:upgrade --keep-generated
Static Content Deploy(use -f for force deploy on 2.2.x or later):
php bin/magento setup:static-content:deploy
Static Content Deploy For Particular Language:
php bin/magento setup:static-content:deploy en_US
Static Content Deploy For Magento Backend Theme Using Command Line (Working on 2.1.1 or later)
php bin/magento setup:static-content:deploy --theme="Magento/backend"
Static Content Deploy For Specific Themes (Working on 2.1.1 or later)
php bin/magento setup:static-content:deploy --theme Magento/luma --theme Magento/another_theme
Exclude Themes on Static Content Deploy and does not minify HTML files Using Command Line (Working on 2.1.1 or later)
php bin/magento setup:static-content:deploy en_US --exclude-theme Magento/luma --no-html-minify
 ```
 
 
## Cache & Reindex related commands:
```
Cache Clean: php bin/magento cache:clean
Cache Flush: php bin/magento cache:flush
View cache status: php bin/magento cache:status
Enable Cache: php bin/magento cache:enable [cache_type]
Disable Cache: php bin/magento cache:disable [cache_type]

php  bin/magento index:reindex
php -d memory_limit=2G bin/magento index:reindex
```

## Modes related commands:
```
Check Current Mode: php bin/magento deploy:mode:show
Change To Developer Mode: php bin/magento deploy:mode:set developer
Change To Production Mode: php bin/magento deploy:mode:set production
```
  
  
## Module related commands:
```
php bin/magento module:status  [See all modules Status ]
php bin/magento module:enable Namespace_Module [Enable module]
php bin/magento module:disable Namespace_Module [Disable module]
php bin/magento module:uninstall Namespace_Module [Uninstall Module]
```
 
## Other Commands:

```
php bin/magento setup:di:compile [Run the single-tenant Compiler]
php bin/magento admin:user:unlock adminusername [Unlock Admin User]
php bin/magento cron:install --force [Use --force to rewrite an existing Magento crontab.]
crontab -l [view the crontab, enter the following command as the Magento file system owner. ]
php bin/magento cron:remove [Remove Magento crontab]
  
