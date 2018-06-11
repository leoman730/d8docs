# Improvement

## Authentication
If cache server is in front of the site, make sure that this will not accidentally serving protected page.
Possible solution: Create a page as a placeholder, ex: /protected_page, any protected content will serve via this page.
Instruct Drupal and cache server do not cache such page.
