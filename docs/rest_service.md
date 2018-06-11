# Rest Services

Drupal 8 now has REST service out of the box, meaning we don't need to rely on the Services module to 
create service API. With build in REST module and the Serilization module enable, Views can export service
directly. 

The only thing I see need to change it the Service API URL.
For example: http://d8.law.nyu.edu/faculty_service_view?_format=json
Notice that the _format={} is required, otherwise "client error" may occured. 

In additional, in order to be able to control number of items to display, there some odd settings need to
be make to the view:
- The pager has to be set "Full pager".
- In the full pager setting, the expose options value has to be 'whitelist'.


See:
- [Your First RESTful View in Drupal 8](https://drupalize.me/blog/201402/your-first-restful-view-drupal-8)
- [Insights and Useful Snippets for the D8 Rest
  Module](https://www.mediacurrent.com/blog/8-insights-and-useful-snippets-d8-rest-module/)
