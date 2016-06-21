## WordPress custom fields - tips and tricks
###What are WordPress custom fields?

Custom fields are a kind of meta-data, that is data about data. Each post can have any number of custom fields. they are stored in the WordPress database as key/value pairs. The key is the name of the item while the value represents the content that will be displayed in the post, this can be text or a URL. The value is saved for each specific post .You can use the same key multiple times, for example a key of "fruit" can have the values of "apple" and "orange" stored via the post's back end form.

![ admin ](https://raw.githubusercontent.com/geoffwhittaker/wordpress-custom-fields/master/custom-fields.png)
Custom fields are a quick way to add extra functionality to a WordPress site with the minimal amount of code.

Next we look at three examples of using custom fields to add content to your posts in a more efficient and fun way!
###Simple example
>Add a list of items with the same custom field name, in this case a list of favourite fruits.

To add the content of a custom field to a post use this code in the WordPress loop.
`<?php the_meta(); ?>`
This will add all the custom fields at once.
To add a specific key use the "get-post-meta" function. replace the "key" with your actual key for example fruit.
`<?php echo get_post_meta($post->ID, 'key', true); ?>`

![Fruits display](https://raw.githubusercontent.com/geoffwhittaker/wordpress-custom-fields/master/fruits_display.png)
The frontend display is shown here.

To display multiple items with the same key you can use a for each loop.

       <?php $Fruits = get_post_meta($post->ID, 'Fruits', false); ?>
	 <h3>Today's fruits are:</h3>
          <ul>
		<?php foreach($Fruits as $fruit) {
			echo '<li>'.$fruit.'</li>';
	         	} ?>
          </ul>
      

###Display content depending on the key value
>Add a link to a detail page depending  on the subject of a post.

![Custom field for post subject](https://raw.githubusercontent.com/geoffwhittaker/wordpress-custom-fields/master/post_subject.png)
Condtional statements can be used to test for a particular value and dsiplay diiferent content. In the code shown below an "elseif" loop checks for the stored custom field value and displays a link dependant on  the value of the custom field. If no value is found a link to the home page is shown.
The key in this case is "tech" and has the values of PHP, JavaScript and WordPress.
![ back end custom field entry](https://raw.githubusercontent.com/geoffwhittaker/wordpress-custom-fields/master/back-end-tech-field.png)
```
<?php /** custom field for post subject, display*/   ?
<?php $value = get_post_meta($post->ID, 'tech', true); 
echo 'Find out more about...';
 if($value == 'php') { 
 echo '<a http://php.net/">PHP.net</a>'; 
 } elseif($value == 'javascript') { 
 echo '<a href="https://www.javascript.com/">Javascript docs</a>'; 
 } elseif($value == 'wordpress') { 
 	echo '<a href="https://en-gb.wordpress.org/">WordPress</a>'; 
 } else { 
    	echo '<a http://www.smallbusinesswebdesignnorthwest.co.uk/">This site</a>'; 
 	} 
	?> 
```

The code is placed in your themes single.php file where you want the link to appear. 

###Use a short code with custom fields
>Easily add widgets, iframes and social media apps to a post using custom fields and short codes. The weather widget shown below was added using a short code.

![Weather app](https://raw.githubusercontent.com/geoffwhittaker/wordpress-custom-fields/master/weather_app.png)

If you have ever worked with HTML blocks in WordPress you will find that the text editor does not save HTML in the case of switching between text mode and visual mode. To obviate this problem you can add a block of code such as a widget or iframe to a custom field. A short code can then be used to place it in the post.
 Add the code below to your functions.php file.
 
`function field_func($atts){
			global $post;
			$name = $atts ['name'];
			if (empty($name)) return;
			return get_post_meta($post->ID, $name, true);
			};
        add_shortcode('field', 'field_func');`
        
 Then go to the location in the post where you want to place the content and add the shorcode in the format:
 
 [field name=key]
 
The key should be the name of the custom field. The saved content will then be displayed.
>**How it works**- the Add_shortcode() function has two parameters, the first is the name to use as a "tag" (in this case "field") ,this is used to reference the added content in the post. the second is the function to run when the shotcode is called. The format of the shortcode is  [field name=weather]
The  function is passed an array of key/value pairs, this is placed into the variable $name by getting the value of the "name" attribute, which is in this case "weather".
The get_post_meta() function is then called to get the value of the key and display it in the post.

As an example a weather widget was added to a post, any number of widgets or iframes can be added by changing the "name" attrbute to match a custom field.
###where next?
Hopefully these techniques will help you to get a feel for using custom fields. looping is a useful way of handling multiple key values. 
Using conditional expressions to find a particular custom field's value and do something specific with it is a powerful technique for customising your content.
The abilty of custom fields to store code as well as text can be used as a quick way to add weather and other widgest to a post with the  minimum of hasstle. There is more to explore with custom fields so have a go!
###References

WordPress beginner article[ custom fields](https://github.com/geoffwhittaker/wordpress-custom-fields/blob/master/custom-fields.png)
Perishable Press [custom fields- the basics](https://perishablepress.com/wordpress-custom-fields-tutorial/)
Custom fields [tutorial video](https://www.youtube.com/watch?v=UBMFOQWD0vw)
