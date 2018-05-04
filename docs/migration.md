* [Upgrading to Drupal 8](https://www.drupal.org/docs/8/upgrade)
* [Upgrade using Drush](https://www.drupal.org/docs/8/upgrade/upgrade-using-drush)

* [Installing Drupal 8 from configuration](https://www.chapterthree.com/blog/installing-drupal-8-from-configuration)
* [Video - Drupal 8 Day: Custom Content Migrations to Drupal 8](https://www.youtube.com/watch?v=J3UDSpwbk7c)
* [Custom Drupal-to-Drupal Migrations](https://drupalize.me/tutorial/custom-drupal-drupal-migrations?p=2578)


## Some useful migration commands
```
# Generate configuration for migration
# Modify settings.php to include db connection string "migrate"
drush migrate-upgrade --configure-only --legacy-db-key=migrate

# Export migrate-status to a file
drush ms > status.txt

# Export configruation files
drush config-export > config.txt
drush config-export --destination=/tmp/migrate

# Show a specific config
drush config-get {config_name}

# Only show migration status related to 'field'
drush ms --group=migrate_drupal_7 --names-only | ag field

# Get a list of Destination plugins
# At the php console:
\Drupal::service('plugin.manager.migrate.destination')->getDefinitions();


fin drush migrate-status --tag=Field
fin drush migrate-import --feedback --execute-dependencies --tag=Field

# To refresh migration in a module
drush config-import --partial --source=module/custom/nyulaw_migrate/config/install




```

## Migration Steps:
Primary migration will divide into 3 phrases: migrate site structures from source site; modify site structure based on new needs; migrate content from source site.

1. Run migration to generate structure based on the Source Site
2. After the structures is generated, modified it base on the need of the new site. For example, news_item content type has an image field, which should be a entity reference field in D8, therefore, it needs to be recreated. Also make sure the machine name is mapped to the old type field name.
3. Make sure to export all the configs as code `drush config-export -y`. This will save all the config in the ../config directory
4. Start content migration

---
Use the [Config Installer](https://www.drupal.org/project/config_installer) to import site profile is the easiest way for manage site structure

1. Once the site structure is ready, use `drush config-export -y` to export entire site configs
2. Install Drupal as usual, but using the minimal profile
3. Run `fin drush site-install --verbose config_installer config_installer_sync_configure_form.sync_directory=../config --yes` to re-install the site based on config files in the sync directory
4. Once it is completed, the srceen will show the user name and password. In case that is not working, Use `fin drush upwd admin --password="admin"` to reset admin password



## Migration Note
To set up a new dev site with content, we could modify the script (migrationclean.sh) to:
1. Install the config profile
2. Then run run-migration.sh to import site content




## Field collection to Paragraphs
Paragraphs has most of the code to migrate field collections. And this is the plan based on the community discussion.

According to @mikelutz

> If you install the latest paragraphs -dev and apply https://www.drupal.org/project/paragraphs/issues/2911244  it
> should migrate through the migrate_drupal_ui

There are couple threads related to this:

* https://www.drupal.org/project/paragraphs/issues/2911244
* https://www.drupal.org/project/paragraphs/issues/2897021



## Basic page migration
benjifisher [2:02 PM]
I think you want the `merge` plugin: https://cgit.drupalcode.org/migrate_plus/tree/src/Plugin/migrate/process/Merge.php

There might be an easier way, but if you want to follow the model in the docblock, then you can create three separate migrations, each of which creates a Paragraph entity from one of the source fields. Then use `migration_lookup` and `merge` as in the sample code in the docblock. Remember that `iterator` is deprecated; use `sub_process` instead. (edited)



## Block reference
Block reference is not support in D8. There are discussions propose how this should work in D8 but there's no agreement
yet. See [Drupal 8 Port](https://www.drupal.org/project/blockreference/issues/2410289)

The [Block Field](https://www.drupal.org/project/block_field) seems work as an alternative.



## CKeditor - Embeded media
Media module is in Drupal core >= 8.5. Ckeditor can work with Media Embed module for embeding many types of media eneity inside a ckeditor. Refer to the [media guide section](/media-guide) for more info.

In order to make legacy embeded string work, some process transformations is needed. This transformation will convert the legacy embeded string into a new string that is regonizabled by the new editor.

```
# Old Embeded String
[[{"fid":"41966","view_mode":"190wide","fields":{"alt":"Alt - Chinese New Year ","title":"Title - Chinese New
Year","style":"float: right;","class":"media-element my_custom_class
file-teaser","data-delta":"1","format":"190wide","field_file_caption[und][0][value]":"Happy Chinese New
Year","field_file_image_alt_text[und][0][value]":"Alt - Chinese New Year
","field_file_image_title_text[und][0][value]":"Title - Chinese New
Year"},"type":"media","field_deltas":{"1":{"alt":"Alt - Chinese New Year ","title":"Title - Chinese New
Year","style":"float: right;","class":"media-element my_custom_class
file-teaser","data-delta":"1","format":"190wide","field_file_caption[und][0][value]":"Happy Chinese New
Year","field_file_image_alt_text[und][0][value]":"Alt - Chinese New Year
","field_file_image_title_text[und][0][value]":"Title - Chinese New Year"}},"attributes":{"alt":"Alt - Chinese New Year
","title":"Title - Chinese New Year","style":"float: left;","class":"media-element my_custom_class
file-190wide","data-delta":"1"}}]]


# New Embeded String
<drupal-entity data-align='left' data-caption='Happy Chinese New Year' data-entity-type='media'
data-entity-uuid='302905a2-3598-433b-9fa2-143fbaac4b98' data-entity-embed-display='entity_reference:media_thumbnail'
data-embed-button='media_browser_button' data-entity-embed-display-settings='{"image_style":"190wide"}'  />

```

Look at the FixMediaTags.php from the nyulaw_migrate module to understand how th process works.


If after migrated content the front end doesn't render html tag correctly. This is due to body_format field value doesn't specified.
The default migration script comes from core does not set soruce for body_format; Therefore, the migration script set a default body_format value to full_html during the migration.


Assuming the body_format value is set, run `drush cr` should resolve this issue.


## Debug migration
```
⟩ drush migrate-import upgrade_d7_menu_links
Processed 4462 items (48 created, 0 updated, 4066 failed, 348 ignored) - done with 'upgrade_d7_menu_links'                                                                                                                 [status]
upgrade_d7_menu_links Migration - 4066 failed.

```

Use drush mmsg upgrade_d7_menu_links

```
drush mmsg upgrade_d7_menu_links

109dbf0220db6b16b80efe7fb1211f97d558d3624372b2b012f745a9ea3b8145  1       The path "internal:/node/19346" failed validation.
```

For reporting purpose, use $migration_executable->saveMessage() to log migration issue.


## Content migration

### Basic Page
* Field_images currently is using paragraph_field_images, because there only a handful of nodes using this field, we may just want to get rid of it.

* Need to find out how many node is using the promo block.

### Landing Page
* There are only 3 handful landing page with no content to it. This may be just convert to a simple basic page.

### News Item
* All items seems migrated

### Press Highlight
* All items seems migrated

### Paragraphs page
* Many pages not migrated, probably due to block references.
* Also, Paragraphs need to be migrated prior to this migration

Todo:
    - We we ignore Paragraphs page that use block reference fields?


### Custom blocks
Todo:

- How many custom blocks do we have, do we have scripts for custom block migration, and how does it looks like


### Views
- If views is created in the admin, it will be managed/tracked by Configuration Mangement

### Node Path/Alias
- All path alias is able to migrated without issue.

### Redirect
Todo:

* There are couple (4) redirect failing, primary because the source url is identical, only the letter cases vary. The easiest fix seems to be re-add those manually after migration.
```
SQLSTATE[23000]: Integrity constraint violation: 1062 Duplicate entry 'JDfYcWeYjq2O0VL70etyNcPOZnQn0DMYpJd_wCMCXcU' for key 'hash': INSERT INTO {redirect} (rid, type, uuid, language, hash, uid, redirect_source__path, redirect_source__query, redirect_redirect__uri, redirect_redirect__title, redirect_redirect__options, status_code, created) VALUES (:db_insert_placeholder_0, :db_insert_placeholder_1, :db_insert_placeholder_2, :db_insert_placeholder_3, :db_insert_placeholder_4, :db_insert_placeholder_5, :db_insert_placeholder_6, :db_insert_placeholder_7, :db_insert_placeholder_8, :db_insert_placeholder_9, :db_insert_placeholder_10, :db_insert_placeholder_11, :db_insert_placeholder_12); Array
(
    [:db_insert_placeholder_0] => 1712
    [:db_insert_placeholder_1] => redirect
    [:db_insert_placeholder_2] => ad68c230-a982-4410-a624-86a3bf4867ce
    [:db_insert_placeholder_3] => und
    [:db_insert_placeholder_4] => JDfYcWeYjq2O0VL70etyNcPOZnQn0DMYpJd_wCMCXcU
    [:db_insert_placeholder_5] => 150
    [:db_insert_placeholder_6] => guarini-global/lawtech
    [:db_insert_placeholder_7] => N;
    [:db_insert_placeholder_8] => internal:/node/29626
    [:db_insert_placeholder_9] =>
    [:db_insert_placeholder_10] => a:0:{}
    [:db_insert_placeholder_11] => 301
    [:db_insert_placeholder_12] => 1525455137
)
 (/var/www/web/core/lib/Drupal/Core/Entity/Sql/SqlContentEntityStorage.php:829)


 27264
 29626
 23299
 23267

```


### Field Collection 
Note: 

* Couple items didn't migrate due to file missing. Not a blocker. 

```
    ⟩ fin drush migrate-import --tag=FieldCollection
Processed 7 items (7 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_field_collection_type'                                                                                                               [status]
Processed 25 items (25 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_field_collection_bm_section'                                                                                                       [status]
Processed 0 items (0 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_field_collection_dynamic_lead_item'                                                                                                  [status]
Processed 7 items (7 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_field_collection_images'                                                                                                             [status]
Processed 49 items (49 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_field_collection_mm_section'                                                                                                       [status]
Missing file with ID 18833. ImageItem.php:327                                                                                                                                                                              [warning]
Missing file with ID 18858. ImageItem.php:327                                                                                                                                                                              [warning]
Processed 12 items (12 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_field_collection_selected_news_item'                                                                                               [status]
Missing file with ID 18866. ImageItem.php:327                                                                                                                                                                              [warning]
Missing file with ID 18867. ImageItem.php:327                                                                                                                                                                              [warning]
Processed 1382 items (1382 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_field_collection_slides'                                                                                                       [status]
Missing file with ID 15901. ImageItem.php:327                                                                                                                                                                              [warning]
Missing file with ID 18883. ImageItem.php:327                                                                                                                                                                              [warning]
Missing file with ID 18884. ImageItem.php:327                                                                                                                                                                              [warning]
Processed 52 items (52 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_field_collection_stat_box_item'                                                                                                    [status]
```

### Gallery 
Note:

* Gallery migrated. 2 missing files is reported. 
```
~/git_repos/nyu-law-d8/web · (migration±)
⟩ fin drush migrate-import --tag=Gallery
Missing file with ID 18866. ImageItem.php:327                                                                                                                                                                              [warning]
Missing file with ID 18867. ImageItem.php:327                                                                                                                                                                              [warning]
Processed 174 items (174 created, 0 updated, 0 failed, 0 ignored) - done with 'upgrade_d7_node_gallery'                                                                                                                    [status]
```


### Menu


### Workbench
Todo:

* Check if workbench for node set correctly


### MetaTags
Todo:

* This could be just site config,not migration.









## Post Migration todo list






