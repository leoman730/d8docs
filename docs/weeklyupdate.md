# Weekly Update

## Project roadmap
- [D8 Project Management Plan](https://cloud.gantter.com/ganttercloud/#fileID=354c8ee02a4a45928c021bce4ac236dd&amode=cloud)

## July 23th, 2018 (week #11)

### Questions/Status
- Update on the testing plan
- ITS Faculty Block >> Are all those blocks active??
- News item, dealing with the edge-to-edge image on the top (to communication)
- Stat box block
- What is the status for protected page clean up, need the report for this?
- How draft works in D8?
- Gallery slider - design improvement for the nav

### Discussion
- Faculty list >> Store in Drupal, pull from coldfusion in a cron job?
- Page header transparent toggle


### To do
- News item, dealing with the edge-to-edge image on the top
- Dealing with Feed



## July 16th, 2018 (week #10)

### Questions/Status
- Luis's latest commit [e457aa1ea15b9ff88811c5dcde78289d9617a057](https://github.com/nyuschooloflaw/nyu-law-d8/commit/e457aa1ea15b9ff88811c5dcde78289d9617a057)
- Update on the testing plan
- ITS Faculty Block >> Are all those blocks active??
- News item, dealing with the edge-to-edge image on the top (to communication)
- Page that with block references
- Stat box block
- What is the status for protected page clean up, need the report for this?
- How draft works in D8?


### Discussion
- Inline Gallery >> in flexslider machanism >> design?
- Faculty list >> Store in Drupal, pull from coldfusion in a cron job?
- Adding alt tag to faculty listing


### To do
- Media browser improvement - better selection experience. Also should this be modified so that one button to do all?
- News item, dealing with the edge-to-edge image on the top
- How to deal with block that looks like a button on the rightside bar
- Adding alt tag to faculty listing
- Make test branch in Pantheon

## July 9th, 2018 (week #9)

### Questions/Status
- Pages that with PHP code
    - Answer: https://docs.google.com/spreadsheets/d/1nCsx8oOyVDd3WjEsO7l9oBeDt-rmhILoQYfk7sqKjb4/edit#gid=0
- Page that with block references
    - Answer: https://docs.google.com/spreadsheets/d/1nCsx8oOyVDd3WjEsO7l9oBeDt-rmhILoQYfk7sqKjb4/edit#gid=2111375419
- What is the status for protected page clean up, need the report for this?
- How draft works in D8?


### Discussion
- Paragraphs type: Full width image (the implementation is too complex)
- Reset all user password, password policy enforcement
- Kevin (How to add "alt text" option for wysiwyg; Big Menu mitigation;)

### To do
- News item, dealing with the edge-to-edge image on the top
- Inline Gallery
- Faculty listing module
- Course block



## July 2nd, 2018 (week #8)

### Questions/Status
- What is the status for protected page clean up, need the report for this?
- How draft works in D8?
- Views cleanup update
- Spec on the edge-to-edge image update


### Discussion
- Paragraphs type: Full width image (the implementation is too complex)
- Reset all user password, password policy enforcement
- Kevin (How to add "alt text" option for wysiwyg; Big Menu mitigation;)
- Related links block
    There are many of them for basic pages (309). 
    Even more if remove exclusion. 

```
select * from field_data_field_related_links
inner join url_alias on url_alias.source = concat('node/', entity_id)
where bundle='basic_page'
and 
(
alias not like 'areasofstudy/%'
and alias not like 'graduateadmissions'
and alias not like 'graduateadmissions/%'
and alias not like 'llmjsd/%')
```

*This used to be created by Views, but now we can just create a block directly thanks for the Field API.*

- Promo block is not longer used

- Block reference
    There a very few numbers of blocks are references(7). Need examine if they still needed. 
    Look at: https://docs.google.com/spreadsheets/d/1nCsx8oOyVDd3WjEsO7l9oBeDt-rmhILoQYfk7sqKjb4/edit#gid=0 

- Image block
    Only 3 pages are using this. Please examine if it really need or we can get rid off it.(17959, 19855, 22280)
    
```
select * from field_data_field_images;
``` 

- Views >> promo >> Public Interest News (Seems not use)
    Answer: This is used on the PILC landing page.

### To do
- Flexslider for homepage. We don't want people update the homepage node everyday.


## June 25th, 2018 (week #7)

### Questions/Status
- What is the status for protected page clean up, need the report for this?
- How draft works in D8?
- Views cleanup update
- Spec on the edge-to-edge image update
    Answer: May need to postone for this. Due to back and forth conversation with communication.


### Discussion
- Paragraphs page layout
    Answer: Improve editorial experience. Including use "Add Paragraphs" button. Create a list of items for this later.
- Related links/promo block for basic page 
    Answer: Get usage reports

### To do
- Views migration
- Flexslider
- Generate block usage report
- Find out if we can control Paragraphs permission by roles

## June 18th, 2018 (week #6)

### Questions/Status
- What is the status for protected page clean up, need the report for this?
- How draft works in D8?
- Views cleanup update
- Menu settings - Currently only basic page allow menu setting, should that be the same.
	Answer: Only keep available for basic page + paragraphs page


### Discussion
- Panel page conversion
	We all agree using paragraphs is the best approach.

- News landing page: Right now rely on paginator, would be nice to have auto generate content based on scroll position.
	A good to have feature, but there maybe some accessibility concern.

- Alt tag in wysiwyg, may need to use the caption field
	- See: [Drupal issue queue](https://www.drupal.org/project/entity_embed/issues/2924391)
	- See: [Add 'alt' and 'title' tokenized text options for image formatters, and a 'title' option for the generic file formatter](https://www.drupal.org/project/drupal/issues/1291262#comment-12302748)
- Testing plan
- Spec for consolidating edge-to-edge images
	Need more work to iron out the spacs. Clayton and Luis will work on it.
 

 
### To do
- Basic page sidebar blocks

## June 11th, 2018 (week #5)

### Questions/Status
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
- Spin up a drupal instant for testing

## June 4th, 2018 (week #4)

### Questions/Status
- What is the status for protected page clean up?
- How draft works in D8?

### Discussion
- The link_attributes module only allow options for class, not for id; therefore, for the footer, we need to convert id to use class 

### To do
- Custom module migration
    - Event Calendar
- Create missing views


## May 28th, 2018 (week #3)

### Questions/Status
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

### Questions/Status
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

### Questions/Status

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
