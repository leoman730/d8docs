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
     "block_content_type" => Drupal\Core\Config\Entity\ConfigEntityType {#5227},
     "comment_type" => Drupal\Core\Config\Entity\ConfigEntityType {#4830},
     "comment" => Drupal\Core\Entity\ContentEntityType {#5532},
     "editor" => Drupal\Core\Config\Entity\ConfigEntityType {#5463},
     "embed_button" => Drupal\Core\Config\Entity\ConfigEntityType {#3650},
     "entity_browser" => Drupal\Core\Config\Entity\ConfigEntityType {#5346},
     "field_config" => Drupal\Core\Config\Entity\ConfigEntityType {#4754},
     "field_storage_config" => Drupal\Core\Config\Entity\ConfigEntityType {#4537},
     "field_collection" => Drupal\Core\Config\Entity\ConfigEntityType {#3300},
     "field_collection_item" => Drupal\Core\Entity\ContentEntityType {#4408},
     "file" => Drupal\Core\Entity\ContentEntityType {#5844},
     "filter_format" => Drupal\Core\Config\Entity\ConfigEntityType {#4009},
     "flexslider" => Drupal\Core\Config\Entity\ConfigEntityType {#5761},
     "image_style" => Drupal\Core\Config\Entity\ConfigEntityType {#5676},
     "media_type" => Drupal\Core\Config\Entity\ConfigEntityType {#5496},
     "media" => Drupal\Core\Entity\ContentEntityType {#5064},
     "metatag_defaults" => Drupal\Core\Config\Entity\ConfigEntityType {#4583},
     "migration_group" => Drupal\Core\Config\Entity\ConfigEntityType {#4250},
     "migration" => Drupal\Core\Config\Entity\ConfigEntityType {#4987},
     "node_type" => Drupal\Core\Config\Entity\ConfigEntityType {#4008},
     "node" => Drupal\Core\Entity\ContentEntityType {#4481},
     "rdf_mapping" => Drupal\Core\Config\Entity\ConfigEntityType {#3654},
     "redirect" => Drupal\Core\Entity\ContentEntityType {#4261},
     "search_page" => Drupal\Core\Config\Entity\ConfigEntityType {#5178},
     "shortcut_set" => Drupal\Core\Config\Entity\ConfigEntityType {#5084},
     "shortcut" => Drupal\Core\Entity\ContentEntityType {#4967},
     "simple_block" => Drupal\Core\Config\Entity\ConfigEntityType {#4908},
     "action" => Drupal\Core\Config\Entity\ConfigEntityType {#5005},
     "menu" => Drupal\Core\Config\Entity\ConfigEntityType {#4861},
     "taxonomy_term" => Drupal\Core\Entity\ContentEntityType {#4834},
     "taxonomy_vocabulary" => Drupal\Core\Config\Entity\ConfigEntityType {#4943},
     "tour" => Drupal\Core\Config\Entity\ConfigEntityType {#3760},
     "user" => Drupal\Core\Entity\ContentEntityType {#4354},
     "user_role" => Drupal\Core\Config\Entity\ConfigEntityType {#4341},
     "section_association" => Drupal\Core\Entity\ContentEntityType {#3622},
     "access_scheme" => Drupal\Core\Config\Entity\ConfigEntityType {#5545},
     "menu_link_content" => Drupal\Core\Entity\ContentEntityType {#4691},
     "view" => Drupal\Core\Config\Entity\ConfigEntityType {#5728},
     "paragraph" => Drupal\Core\Entity\ContentEntityType {#5040},
     "paragraphs_type" => Drupal\Core\Config\Entity\ConfigEntityType {#4687},
     "date_format" => Drupal\Core\Config\Entity\ConfigEntityType {#2723},
     "entity_form_mode" => Drupal\Core\Config\Entity\ConfigEntityType {#6008},
     "entity_view_display" => Drupal\Core\Config\Entity\ConfigEntityType {#5861},
     "entity_form_display" => Drupal\Core\Config\Entity\ConfigEntityType {#5833},
     "entity_view_mode" => Drupal\Core\Config\Entity\ConfigEntityType {#6052},
     "base_field_override" => Drupal\Core\Config\Entity\ConfigEntityType {#2616},
   ]
```


## Caching
```
# Reference: https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Cache%21CacheBackendInterface.php/interface/CacheBackendInterface/8.2.x
\Drupal::cache('page')->get('http://d8.law.nyu.edu/academics/colloquia/legalhistory:html')
\Drupal::cache('page')->delete('http://d8.law.nyu.edu/academics/colloquia/legalhistory:html')


```


## Event subscription
The [CacheExclude](https://www.drupal.org/project/cacheexclude) module is a small module that show how to create event subscription in Drupal 8.



