# Development

## Drupal coding standard
- [Drupal Coding Standard](https://www.drupal.org/docs/develop/coding-standards)

## Helpful during development
- [Twig Xdebug](https://www.drupal.org/project/twig_xdebug)
- [Devel](https://www.drupal.org/project/devel)
- [Migrate Devel](https://www.drupal.org/project/migrate_devel)

## Debug within vim

- [vDebug](https://github.com/vim-vdebug/vdebug)


## Module upgrade helper
There's useful module [Drupal Module Upgrader](https://www.drupal.org/documentation/modules/drupalmoduleupgrader) can be used to identify compatibilitiess issue D7 modules.

```
# To generate an issue report
drush dmu-analyze  --skip=info --path=modules/custom/nyulaw_authentication nyulaw_authentication

# To try automatically fix issue
drush dmu-upgrade  --skip=info --path=modules/custom/nyulaw_authentication nyulaw_authentication

```

## Drupal console
Use Drupal console to enable/disable development mode. See [Enable development mode](https://www.drupaleasy.com/quicktips/enabling-development-mode-local-drupal-8-site)
```
drupal site:mode dev
drupal site:mode prod
```

## Cache
[Cache in D8](https://www.adcisolutions.com/knowledge/cache-drupal-8)


## Block 

- [Block API](https://www.drupal.org/docs/8/api/block-api/overview)
- [Transitioning from Drupal 7 to Drupal 8: programmatically creating blocks](http://befused.com/drupal/block-programmatically)
- [Block are now plugins](https://www.drupal.org/node/1880620)
