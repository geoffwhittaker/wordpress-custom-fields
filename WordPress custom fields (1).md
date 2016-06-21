## WordPress custom fields
What are WordPress custom fields?
Custom fields are a Kind of meta-data, that is data about data. Each post can have any number of custom fields. they are stored in the WordPress database as key/value pairs. The key is the name of the item while the value represents the content that will be displayed in the post, this can be text or a URL. The value is saved for each specific post .You can use the same key multiple times, for example a key of "fruit" can have the values of "apple" and "orange" stored via the post's back end form.

![ admin ](https://raw.githubusercontent.com/geoffwhittaker/wordpress-custom-fields/master/custom-fields.png)
###Simple example
To add the content to a post use this code in the WordPress loop.
`<?php the_meta(); ?>`
This will add all the custom fields at once.
To add a specific key use the "get-post-meta" function. replace the "key" with your actual key for example fruit.
`<?php echo get_post_meta($post->ID, 'key', true); ?>`

>blockquote paragraph

###References

wp beginner article[ custom fields](https://github.com/geoffwhittaker/wordpress-custom-fields/blob/master/custom-fields.png)
perishable press [custom fields- the basics](https://perishablepress.com/wordpress-custom-fields-tutorial/)