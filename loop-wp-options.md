```php
global $wpdb;
                $table_name = $wpdb->prefix . 'options';
                $data = $wpdb->get_row("SELECT * FROM $table_name WHERE option_name = 'wpretro'");
                $option_value = $data->option_value;

                $unserialized_data = unserialize($option_value);

                echo "<table>";
                foreach ($unserialized_data as $key => $value) {
                    echo "<tr><td>$key</td>";

                    // Check if the value is an array
                    if (is_array($value)) {
                        echo "<td><ul>";

                        // Loop through the subarray
                        foreach ($value as $subkey => $subvalue) {
                            echo "<li>$subkey: $subvalue</li>";
                        }

                        echo "</ul></td>";
                    } else {
                        echo "<td>$value</td>";
                    }

                    echo "</tr>";
                }
                echo "</table>";
                break;
```
