# Add GraphQL support for new ACF field

## Example 01 - [ACF-Unique-ID-Field](https://github.com/philipnewcomer/ACF-Unique-ID-Field)

```
add_filter('wpgraphql_acf_supported_fields', function ($supported_fields) {
	array_push($supported_fields, 'unique_id');
	return $supported_fields;
});

add_filter('wpgraphql_acf_register_graphql_field', function($field_config, $type_name, $field_name, $config) {
	$acf_field = isset( $config['acf_field'] ) ? $config['acf_field'] : null;
	$acf_type  = isset( $acf_field['type'] ) ? $acf_field['type'] : null;
	if($acf_type == 'unique_id')
	  $field_config['type'] = 'String';
	return $field_config;
}, 10, 4);
```



## Example 02 - [ACF Medium Editor](https://github.com/Hube2/acf-medium-editor/)

```
add_filter('wpgraphql_acf_supported_fields', function ($supported_fields) {
  array_push($supported_fields, 'medium_editor');
  return $supported_fields;
});

add_filter('wpgraphql_acf_register_graphql_field', function($field_config, $type_name, $field_name, $config) {
  $acf_field = isset( $config['acf_field'] ) ? $config['acf_field'] : null;
  $acf_type  = isset( $acf_field['type'] ) ? $acf_field['type'] : null;
  if($acf_type == 'medium_editor')
    $field_config['type'] = 'String';
  return $field_config;
}, 10, 4);
```
