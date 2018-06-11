# Weekly Update

## June 11th, 2018 (week #5)

### Questions
- What is the status for protected page clean up?
- How draft works in D8?


### Discussion
- View: docket >> Current broken on the live site 
- View: Featured Blog Post >> Broken
- View: /editweb
- View: Feeds view >> Are we still using it? Seems like most of those blocks are disabled
- View: Field Blocks >> Related to field collection, need verify if this still use
- View: /gac >> Google analytics counter?
- View: Recent and Promoted >> Some of the blocks seems unused, can we disabled those



- The link_attributes module only allow options for class, not for id; therefore, for the footer, we need to convert id to use class 
- Event calendar module upgraded with more admin options
 
### To do
- Update drupal core + modules
- Create missing views
	- Faculty FlexSlider Service View
    - Faculty Service View
	- Featured Alumni
	- FlexSlider Views (Flexslider block, New Magazine Flexslider)
	- Ideas Story Grid
	- News/Press Highlights
	- Recent and Promoted



- Works on template for the news_items
- Basic page - work on sidebar items
- Homepage 


## June 4th, 2018 (week #4)

### Questions
- What is the status for protected page clean up?
- How draft works in D8?

### Discussion
- The link_attributes module only allow options for class, not for id; therefore, for the footer, we need to convert id to use class 

### To do
- Custom module migration
    - Event Calendar
- Create missing views


## May 28th, 2018 (week #3)

### Questions
- What is the status for protected page clean up?
- What is the status for the invalid menu items?
    - Invalid menu deleted from live site? [Status](https://docs.google.com/spreadsheets/d/1hRQsA26YvzzE_rXdJCr-O0Xp8cH_fZo8iI27VrJvSl8/edit#gid=0)
- How draft works in D8?
- List of different news item page
    - [Page type](https://docs.google.com/spreadsheets/d/16T4ns_7iqVucMoRRzhWW_boSfYlc1jobmYZV4I39pBs/edit#gid=529093495)


### Discussion
- Drupal 8 Page caching. 
    - How protected page can be secured even with anonymous user caching turn on.
    - Varnish may bring issue for protected page.



### To do
- Custom module migration
    - Protected Page for CF
    - Event Calendar



## May 21th, 2018 (week #2)

### Questions
- What is the status for protected page clean up?
- What is the status for the invalid menu items?
- Are all users in the system active?
    - Need content purge
- Should workbench assignment manually migrate?

### Discussion
- Workbench node access: The toppest root level 'Access Control' is no longer available in D8
- In D7, there's opion to allow the vacaburary be one of the active editorial section (admin/structure/taxonomy/access_control/edit). This option is not longer available in D8.
- Node Clone module, communication should know that this module will not be avaiabled in D8. There's may be a draft feature in D8 so it may worth of time to find out.


### To do




## May 14th, 2018 (week #1)

### Questions

Protected page

- There are 22 protected pages that are managed by protected page module. Do this page still valid or can be deleted.
- If they need, probably need manually migrated


### To do
- Finishing up migration for workbench (node access + editor role)
- Recreate views (clayton will work on this later in the d8 instance)
- Solution for custom blocks
- Custom module - protected page via coldfusion
- Protected page migration
- Clayton to re-examine the list of menu-items, which didn't migrate
```
 The path "internal:/aggregator" failed validation.
 The path "internal:/ctools_ajax_sample" failed validation.
 The path "internal:/blog" failed validation.
 The path "internal:/mega_menu/1" failed validation.
 The path "internal:/press-highlights" failed validation.
 The path "internal:/announcements" failed validation.
 The path "internal:/presshightlights" failed validation.
 The path "internal:/news/Press%20Contacts/presscontacts" failed validation.
 The path "internal:/news/Press%20Contacts/presscontacts" failed validation.
 The path "internal:/news/Press%20Contacts/presscontacts" failed validation.
 The path "internal:/news/Press%20Contacts/presscontacts" failed validation.
 The path "internal:/featured-alumni-view" failed validation.
 The path "internal:/aggregator/categories" failed validation.
 The path "internal:/aggregator/sources" failed validation.
 The path "internal:/ctools_ajax_sample/jumped" failed validation.
 The path "internal:/blog/%" failed validation.
 The path "internal:/node/294" failed validation.
 The path "internal:/presshighlights" failed validation.
 The path "internal:/news/alumni" failed validation.
 The path "internal:/news/centers" failed validation.
 The path "internal:/news/faculty" failed validation.
 The path "internal:/news/global" failed validation.
 The path "internal:/news/students" failed validation.
 The path "internal:/news-ideas" failed validation.
 The path "internal:/node/269" failed validation.
 The path "internal:/node/322" failed validation.
 The path "internal:/node/320" failed validation.
 The path "internal:/node/308" failed validation.
 The path "internal:/node/323" failed validation.
 The path "internal:/node/270" failed validation.
 The path "internal:/node/325" failed validation.
 The path "internal:/node/288" failed validation.
 The path "internal:/node/327" failed validation.
 The path "internal:/node/293" failed validation.
```
