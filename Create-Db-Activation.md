# WPDB

```php
  register_activation_hook(__FILE__, array($this, 'create_custom_table_on_activation'));
  register_deactivation_hook(__FILE__, array($this, 'delete_table_plugin'));
public static function create_db() {

    global $wpdb;
    $table_name = $wpdb->prefix . "custom_table_name";
    $plugin_name_db_version = get_option( 'plugin-name_db_version', '1.0' );

    if( $wpdb->get_var( "show tables like '{$table_name}'" ) != $table_name ||
        version_compare( $version, '1.0' ) < 0 ) {

        $charset_collate = $wpdb->get_charset_collate();

        $sql[] = "CREATE TABLE " . $wpdb->prefix . "database_table (
            id mediumint(9) NOT NULL AUTO_INCREMENT,
            db_field_tinytext tinytext,
            db_field_datetime DEFAULT '0000-00-00 00:00:00',
            db_field_varchar varchar(128) DEFAULT '',
            db_field_mediumint mediumint,
            db_field_text text,
            PRIMARY KEY  (id)
        ) $charset_collate;";

        require_once( ABSPATH . 'wp-admin/includes/upgrade.php' );

        /**
         * It seems IF NOT EXISTS isn't needed if you're using dbDelta - if the table already exists it'll
         * compare the schema and update it instead of overwriting the whole table.
         *
         * @link https://code.tutsplus.com/tutorials/custom-database-tables-maintaining-the-database--wp-28455
         */
        dbDelta( $sql );

        add_option( 'plugin-name_db_version', $plugin_name_db_version );

    }

}
```

### delete table on deactivation
```php 
 public function delete_table_plugin()
        {
            global $wpdb;
            // Get the table name
            $table_name = $wpdb->prefix . 'kh_contact2';

            // Check if the table exists
            if ($wpdb->get_var("SHOW TABLES LIKE '$table_name'") !== $table_name) {
                return;
            }

            // Drop the table
            $wpdb->query("DROP TABLE $table_name");
        }
