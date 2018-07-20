# API
[Drupal APIs documentation](https://www.drupal.org/docs/8/api)

## Entity Type
To list all entity type defined in a site:
```
⟩ fin drupal shell
Psy Shell v0.9.3 (PHP 7.1.15 — cli) by Justin Hileman
>>> \Drupal::entityTypeManager()->getDefinitions()
=> [
     "block" => Drupal\Core\Config\Entity\ConfigEntityType {#5804},
     "block_content" => Drupal\Core\Entity\ContentEntityType {#5522},
     "base_field_override" => Drupal\Core\Config\Entity\ConfigEntityType {#2616},
   ]
```

* [Entity API Documentation](https://www.drupal.org/docs/8/api/entity-api/working-with-the-entity-api)
* [Drupal 8 Entity API cheat sheet](https://www.metaltoad.com/blog/drupal-8-entity-api-cheat-sheet)


## Caching
```
# Reference: https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Cache%21CacheBackendInterface.php/interface/CacheBackendInterface/8.2.x
\Drupal::cache('page')->get('http://d8.law.nyu.edu/academics/colloquia/legalhistory:html')
\Drupal::cache('page')->delete('http://d8.law.nyu.edu/academics/colloquia/legalhistory:html')


```


## Event subscription
The [CacheExclude](https://www.drupal.org/project/cacheexclude) module is a small module that show how to create event subscription in Drupal 8.



