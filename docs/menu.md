Currently, we are using menu_attributes module for providing css class settings for menu link. There's exist a warning complaining about argument data type (array vs string). A custom fix is made to fix this issue. 

This ideally should be package as a patch and submit to the module page.

```
( ! ) Warning: explode() expects parameter 2 to be string, array given in /var/www/web/modules/contrib/menu_attributes/menu_attributes.module on line 374
```


```
# In menu_attributes.module

    // Class attribute needs special handling because it's stored as an array.
    if (isset($attributes[MENU_ATTRIBUTES_LINK]['class'])) {
      $attributes[MENU_ATTRIBUTES_LINK]['class'] = explode(' ', $attributes[MENU_ATTRIBUTES_LINK]['class']);
    }
    if (isset($attributes[MENU_ATTRIBUTES_ITEM]['class'])) {
      $attributes[MENU_ATTRIBUTES_ITEM]['class'] = explode(' ', $attributes[MENU_ATTRIBUTES_ITEM]['class']);
    }


```

Update

The menu_attributes module was removed in favor of the link_attributes module, which has a stable release.


** Todo
* Menu is not scalable and load very slow because of the big menu tree. Big menu module is no longer available, need to find alternative solution.

* Menu select for node also a problem because the big tree make selection very difficult.


