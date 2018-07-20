# Things need to do after migration

## Metatag migration

There are about 48 metatags need to be migrate manually.

```
select entity_id from metatag group by entity_id;

```

## Views
- This can be done in an earlier stage, and use configuration management to export configs into code.



## Crazyeggs
- Migrate crazyeggs snippet. https://jira.law.nyu.edu/browse/DRP-923


## From migrate-later branch
Migrate everything from the migrate-later branch in D7 project


## Https
- If we want to turn on https when site goes live, we need to make sure that the web fonts from typography is pointing to https not http


## Web services
- Need to modify coldfusion to point to the new service links:
	- http://d8.law.nyu.edu/faculty_flexslider_service_view?facultyid=20315&items_per_page=1&_format=json
	- http://d8.law.nyu.edu/faculty_service_view?facultyid=20315&items_per_page=1&_format=json

| Comparision | D8 | D7 |
|---|---|---|
|Flexslider View| {host_name}/faculty_flexslider_service_view?facultyid=20315&items_per_page=1&_format=json| {host_name}/api/v1/views/faculty_flexslider_service_view?facultyid=20315&limit=1	
|Faculty View|{host_name}/faculty_service_view?facultyid=20315&items_per_page=1&_format=json|{hostname}/api/v1/views/faculty_service_view?facultyid=20315&limit=1


## Media
- Make sure all users can view media assets (Set permission for allow all user for view)

## Security
- Reset all user password, make sure password is strong.
