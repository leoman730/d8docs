# Improvement

## Coldefusion Authentication
If cache server is in front of the site, make sure that this will not accidentally serving protected page.
Possible solution: Create a page as a placeholder, ex: /protected_page, any protected content will serve via this page.
Instruct Drupal and cache server do not cache such page.


## Basic page with Hero Image
A new paragraph type for basic page to include a full-width hero image on the top. Similar to the layout for the msltax page.


## News landing page
Right now rely on paginator, would be nice to have auto generate content based on scroll position.

## Single sign on
Leverage sigle sign on that provide by the university for authentication. Match user role from CF/nova core.

## Faculty listing
For performance/stability improvement, it may be better to have a cronjob to pull data nightly and to update the faculty taxonomy list instead.
Then utilize view for the display.

## A better styleguide
Take a look at the github project: [Awesome Design Systems](https://github.com/alexpate/awesome-design-systems)
