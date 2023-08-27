## retrieve unserialized data from db

```php
$heading_row = $wpforms->get_results("SELECT form_id, form_value, form_date FROM $table_name
                WHERE form_post_id = '$fid' ORDER BY form_id DESC LIMIT 1",OBJECT);

            $heading_row = reset( $heading_row );
            $heading_row = unserialize( $heading_row->form_value );
            $heading_key = array_keys( $heading_row );

```
## example

```php
$serializedData = 'a:3:{s:4:"name";s:5:"John";s:5:"email";s:15:"john@example.com";s:7:"message";s:20:"This is a message.";}' ;

$unserializedData = unserialize($serializedData);

## result
array(
    'name' => 'John',
    'email' => 'john@example.com',
    'message' => 'This is a message.'
)
//This allows you to access the individual values by their corresponding keys, such as $unserializedData['name'], $unserializedData['email'], and //$unserializedData['message'].
```
