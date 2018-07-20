# Changes from Drupal 7

## Field collection

Fields in field collection have converted to Paragraphs type in D8. 

In Basic page type, the sidebar field collection now are in Paragraphs sidebar blocks.


## Menu link attributs
* Menu attributs modules is no longer use and in favor of link attributes module.


## Access Control
- In D7, there's opion to allow the vacaburary be one of the active editorial section (admin/structure/taxonomy/access_control/edit). This option is not longer available in D8.

## Node clone module
- There's no D8 version of this, and will not be migrated. 


## Page class
- In D7, the context module add a classname to the body tag based on the path. This no longer the case in D8. There's a custom implementation to accomplish the same. Look at the add_classname_based_on_path() in nyulaw.theme.


## Related link/Super header block
- This used to be created by Views, but now we can just create a block directly thanks for the Field API.

