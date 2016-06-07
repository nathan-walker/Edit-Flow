# edit_flow.php

Actions
------

#### editflow_after_setup_actions

**Description**

Fires after setup of all edit_flow actions.

Plugin authors can hook into this action to manipulate the edit_flow class after initial actions have been registered.

**Examples**

```
add_action( 'editflow_after_setup_actions', 'my_callback' );

function my_other_callback() {
	//Do something here
}

function my_callback( $arg ) {
	//Will only register this callback if Edit Flow is active and after edit_flow
	//has setup all it's actions
	add_action( 'init', 'my_other_callback' );
}
```

#### ef_module_registered

**Description**

Fires after edit_flow has registered a module.

Plugin authors can hook into this action to trigger functionaltiy after a module has been loaded.

**Examples**

```
add_action( 'ef_module_registered', 'my_callback' );

function my_callback( $module_name ) {
	if ( $module_name === 'calendar' ) {
		//Do something after the Calendar module is registered
	}
}
```

#### ef_modules_loaded

**Description**

Fires after edit_flow has loaded all Edit Flow internal modules. 

Plugin authors can hook into this action to add their own modules to the $edit_flow global object.

**Examples**

Create a custom module for Edit Flow and add it to the $edit_flow global object.

```
add_action( 'ef_modules_loaded', 'my_callback' );

function my_callback() {
	global $edit_flow;

	class MyCustomModule extends EF_Module {}

	$edit_flow->mycustommodule = new MyCustomModule();
}
```

#### ef_module_options_loaded

**Description**

Fires after edit_flow has loaded all of the module options from the database.

Plugin authors can hook into this action to read and manipulate module settings.

**Examples**

```
add_action( 'ef_module_options_loaded', 'my_callback' );

function my_callback() {
	global $edit_flow;
	
	if ( $edit_flow->calendar->module->options->enabled && $edit_flow->calendar->module->options->enabled === 'on' ) {
		//Do something if the Calendar module is enabled
	}
}
```

#### ef_init

**Description**

Fires after edit_flow has loaded all modules and module options.

Plugin authors can hook into this action to trigger functionaltiy after all Edit Flow module's have been loaded.

**Examples**

```
add_action( 'ef_init', 'my_callback' );

function my_callback() {
	global $edit_flow;
	
	if( $edit_flow->calendar->create_post_cap == 'edit_posts' ) {
		//If the create_post_cap for calendar is edit_posts, do something here
	}
}
```

Methods
------

#### get_module_by

**Description**
Get's a module by a given $key and $value


**Usage**
```<?php $edit_flow->get_module_by( $key, $value ); ?>```

**Parameters**
$key 
(__string__) (__required__) Any of the [parameters found on a module](https://github.com/Automattic/Edit-Flow/blob/master/edit_flow.php#L216). 
Examples: 'slug', 'name', 'title'

$value
(__string|int|array__) (__required__) A value of a [parameter found on a module](https://github.com/Automattic/Edit-Flow/blob/master/edit_flow.php#L216)