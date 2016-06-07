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
	
	//Always turn the calendar off regardless of site option setting
	$edit_flow->calendar->module->options->enabled = 'off';
}
```


