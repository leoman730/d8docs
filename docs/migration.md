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


### Video
Note:
* After discussion, the video content type will not be migrated (95% for sure)
* For the sake of migration, the video field value for some reasons do not migrate.



### Flexslider
Note:
* Everything migrated.

### Menu
Note: 
* Most links were migrate. 
- 34 links failed - Views and other related
- 20 ignored - Admin links, which no need for migrate
```
~/git_repos/nyu-law-d8/web · (migration±)
⟩ fin drush migrate-import  upgrade_d7_menu_links
Processed 4462 items (4408 created, 0 updated, 34 failed, 20 ignored) - done with 'upgrade_d7_menu_links'                                                                                                                  [status]
upgrade_d7_menu_links Migration - 34 failed.                                                                                                                                                                               [error]





~/git_repos/nyu-law-d8/web · (migration±)
⟩ fin drush mmsg  upgrade_d7_menu_links
 source_ids_hash                                                   level   message
 29d2bab6d873450d1187d89170841fdbd5d9de7607ce397c9b9dc874b02e6ce3  1       The path "internal:/aggregator" failed validation.
 e7aad5d001ee00794225748e79a15a428586dcab6315bee28de24925e505620a  1       The path "internal:/ctools_ajax_sample" failed validation.
 f2697de0b770e1961d78ed7e6b6172cd88dbbb6dce5d6375afa9f29c3933ce6f  1       The path "internal:/blog" failed validation.
 ebb421f19738aa44eadc9b25fcbe3920751444168c3c2d077a2eb442d77d722f  1       The path "internal:/mega_menu/1" failed validation.
 20de6002d1f8e607915226d9811fa40db148de4a8d9a13afb7367868f644fd70  1       The path "internal:/press-highlights" failed validation.
 a30bc1ff563489d908e3220d256e46960636c2745bca8fcd0d38deff6bae06a8  1       The path "internal:/announcements" failed validation.
 c2db12edbf17f51cc17300ad58711ee16693ec38d9a07a9f2fa6683ef3415de5  1       The path "internal:/presshightlights" failed validation.
 f223b8e78c3cd1612f6c835cb2103fd1ba638445504f3bfb9a7dfd68f2cdd8a9  1       The path "internal:/news/Press%20Contacts/presscontacts" failed validation.
 f7d4bd88be8b82828e18d881dc4b67cb600442b1f5fea5b08786acbe98553dd5  1       The path "internal:/news/Press%20Contacts/presscontacts" failed validation.
 86532f82132bed200ca21961ca3514200841477b7079fcf70c2ab72cafe1ac8d  1       The path "internal:/news/Press%20Contacts/presscontacts" failed validation.
 37399ff49ae366f50e6f090754563e0c524825e0cee9a69056dbd757c1bfeea8  1       The path "internal:/news/Press%20Contacts/presscontacts" failed validation.
 0be26f44f6e396a0dd6c58084008f5dae1e22fd31160f26d68921e69d31556e8  1       The path "internal:/featured-alumni-view" failed validation.
 562c4b3050ab9f55b1907e76cf4f22127f81ae1a38cbf49d581639af6dce5fa6  1       The path "internal:/aggregator/categories" failed validation.
 cc884b0b7807a909d0663641c264956e5bb2fc83a243c3e1c03d3cec7a8e3679  1       The path "internal:/aggregator/sources" failed validation.
 a6678c6096408964adc595c0edf0431a297290fbbd3efc0514740944bf30ecf3  1       The path "internal:/ctools_ajax_sample/jumped" failed validation.
 aa5eb1a31c0aa8f946d8b7c013dd2829621b52ce5e6b205be8ad18590b4f1d1f  1       The path "internal:/blog/%" failed validation.
 9168cd967017f71606987b2b402dc063e1a07d1bc5f7d43b6995fb13c268f0a6  1       The path "internal:/node/294" failed validation.
 12613bfa414e2508eb70cf4af47e1283071d60144e6b95b97b4d7d8210021e5c  1       The path "internal:/presshighlights" failed validation.
 2e56e78fe884bf6471753179c1ba451b2e2f7dfda56f98bedb25b8b9c6c09e89  1       The path "internal:/news/alumni" failed validation.
 0d6979d68221aae00033393d3b25fb1ea11c9f2ab64935850e2d3e927ac4a1cb  1       The path "internal:/news/centers" failed validation.
 3daca132bb9ddd46c32b39c58d21408f0ad891d43c98ba40d93c0d853ec7fa07  1       The path "internal:/news/faculty" failed validation.
 64e1f55b676184bed00cbc8aea54ec25c0eee58736cea88d3f861e830ccd9ac4  1       The path "internal:/news/global" failed validation.
 95a788d9430dfa7e3366d234dab0c3d87f3338094efce16739d1b25a7c9a42f8  1       The path "internal:/news/students" failed validation.
 c74d0d062d8985b93c69093f4a74f9dfbdd4d27eee525846dd353bb4a2570c38  1       The path "internal:/news-ideas" failed validation.
 7e54fb5d4dc1f71fb71ea70427c483bb1a6d80cb76647c9b78e45f83aa946330  1       The path "internal:/node/269" failed validation.
 9a93537c4a9a846b6cbf688a85a7e2acf0f14273f6adf7cea9e9ec4b3441f384  1       The path "internal:/node/322" failed validation.
 679fca41d8c8b672d8f43e8a3ef8380f59deb096d1df22d679ba883f19685953  1       The path "internal:/node/320" failed validation.
 bde65a4332992b1ff2c3b0abcbeff6be4d59910a80bc476182311a7ea54b91a1  1       The path "internal:/node/308" failed validation.
 a8e6dd7bd7bfb9ce304ec6aeac0c05b41608398ff2e22e895f20f16b38781d53  1       The path "internal:/node/323" failed validation.
 040299cc82da4721e674cf734cdbd33db869865e51d084de0e4ff33006e128e5  1       The path "internal:/node/270" failed validation.
 be48aa213b83876b40c219d4268ea41cccdb77d3982a312f6e72daf172a78d7a  1       The path "internal:/node/325" failed validation.
 e067f1710b30cc3408cf6b319ccfc0bc02e04ce5b2fb75a6f5b17d3496292208  1       The path "internal:/node/288" failed validation.
 59710eaa8e25a5e6b7e9d19ef9fe24966889c3c784d808756b20422db2102e10  1       The path "internal:/node/327" failed validation.
 db3162a1db176c0de98be598bf9167029010951e03c96f8080afde5f99448a2a  1       The path "internal:/node/293" failed validation.



# Following menu link were ignored, because they are admin links
select * from menu_links where mlid in (434,93354,85819,93512,93514,80308,78871,93406,196,68391,93421,79563,491,197,79824,93427,94270,93355,96859,96852);
```





### Custom blocks



### Workbench
Note:
* Content type now need to create a field for access control
* The first level node ("Access control") no longer avaiable for selection

Todo:

* Check if workbench for node set correctly
* Most likely in D8, we need to create the field and then need a custom migration





### MetaTags
Note:
* In D8, in order to enable content to override default metatags settings, the content type needs to create a new field for metatag. See [Metatags per content Drupal8?](https://www.drupal.org/project/metatag/issues/2715395)


Todo:
* Need meta description migrate
* This could be just site config,not migration.


### 404 Redirect
Note:
* Dropping it











