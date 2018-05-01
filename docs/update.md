# Core/Module update

The site uses composer as package manger to manage core/module update. Generally, you will use the following commands:

```
# To find out what are out-of-date
composer outdate

# To update a module
composer update [module_name]

or

composer update [module_name]:[specific version using sematnic versioning syntax]


# Run update script
cd [drupal_root]
drush updatedb

```


## Update Drupal Core
```
composer update drupal/core --with-dependencies

# Sometimes drupal/core update is not update, use following to check what is blocking the update.
composer prohibits drupal/core:8.5.0 // version number
```

To learn more about composer with syntax for versioning, take a look at [Drupal 8 Composer Best Practices](https://www.lullabot.com/articles/drupal-8-composer-best-practices).


## Composer install vs. Composer update
Never run composer update in production. Correct workflow should be: 
1. Run Composer update in dev to generate the composer.lock file 
2. Run composer install in prod based on composer.lock


![Composer install vs update](/assets/composer_workflow.png)



See: ["composer update" vs "composer install"](https://adamcod.es/2013/03/07/composer-install-vs-composer-update.html)
