# Development

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


## Block 

- [Block API](https://www.drupal.org/docs/8/api/block-api/overview)
- [Transitioning from Drupal 7 to Drupal 8: programmatically creating blocks](http://befused.com/drupal/block-programmatically)
- [Block are now plugins](https://www.drupal.org/node/1880620)
