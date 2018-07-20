# Testing

## Testing list from Clayton
* [Drupal Migration Compoenents](https://airtable.com/tblt9O2o7jXcmc5D6/viwshisSFAGbVbW4O)


## Access control
* Make sure a user who doesn't has access right can not edit the piece of the content
* If a user has 'full access control' priviledge, she should be able to access all content for editing


## Protected Page (module)
* Make sure page that is passwd protected still working

## Calendar Block
* Calendar Homepage block should only display 'Ping to homepage event'
* Cache durarion setting in the admin should reflect in the calendar block.
    * Make sure drupal page load not hitting Coldfusion everytime


## Coldfusion Authentication
* Make sure only login user can view the content
* Make sure once user logout, content viewing need to be re-authenticated


## Faculty Services
* Faculty profile could pull data from Faculty service (faculty view, faculty flexslider view)
	* http://d8.law.nyu.edu/faculty_flexslider_service_view?facultyid=20315&items_per_page=1&_format=json
	* http://d8.law.nyu.edu/faculty_service_view?facultyid=20315&items_per_page=1&_format=json


## News/Press highlight
* There should be a redirect icon for news/press highlight that link to external page.

## Basic Page
* Sidebar blocks
	* When the node has sidebar block content, it should show on the right sidebar. (http://d8.law.nyu.edu/academics)
	* When the node doesn't have sidebar block content, it should not show on the right sidebar.
	  (http://d8.law.nyu.edu/academics/lawyeringprogram), and the page content should have full width on the right.
	
## Metatag
    * Make sure metatag is set correctly (meta description, title etc...)
