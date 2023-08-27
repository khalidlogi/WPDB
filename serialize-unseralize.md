## retrieve unserialized data from db

```php
$heading_row = $wpforms->get_results("SELECT form_id, form_value, form_date FROM $table_name
                WHERE form_post_id = '$fid' ORDER BY form_id DESC LIMIT 1",OBJECT);

            $heading_row = reset( $heading_row );
            $heading_row = unserialize( $heading_row->form_value );
            $heading_key = array_keys( $heading_row );

```
