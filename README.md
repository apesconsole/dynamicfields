# dynamicfields

The Component generates HTML from a JSON input. It handles the complexities of event handling between 2 fields and basic operations,

##Features
1. Label to identify the field
2. Types of fields
    * Text
    * Password
    * Hidden
    * Radio
    * Checkbox
    * Textarea
    * Drop Down/Select Box
    * Multiple Selection Box
    * Single Selection Drop Downs
3. Add any desired attributes
4. Add Listeners
5. Display Default Values/Selections
6. Load options for the Drop Downs
    * From a Provided list
    * From a remote server/REST API
7. Resolve Dependencies between 2 Drop Downs 

##Initialization

##HTML Code
```
<html lang="en-US">
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.8/angular.min.js"></script>
<script src="dynamic-fields-module.js"></script>
<div ng-app="dynamicfields1" ng-controller="some-contoller">
    <form>
        <h2>Dynamic Field</h2>
        <-- Custom directive and custom attributes -->
        <dynamicsection 
               datasource="my_field_input" 
               model="my_model">
        </dynamicsection>    
    </form>
</div>
</script>
</body>
</html>
```

##Script
```
var app = angular.module("dynamicfields1", ['dynamic-fields'])
  .controller('some-contoller', ['$scope', function($scope) {
		$scope.my_model = {};
    $scope.my_field_input = [	
    {  
          // Configure Text Box
					   id: '_userId',
					model: 'userName',
					label: {text: 'Text Field', css: 'label'},
					field: 'input', 
			   attributes: [
						{name: 'id', value : '_userId'},
						{name: 'type', value : 'text'}, 
						{name: 'class', value : 'field-class'}, 
						{name: 'maxlength', value : 15}, 
						{name: 'value', value : 'User Name'}
					]		
			}, 	{       
      // Configure Text Box - Type Password
					   id: '_pwd',
					model: 'password',
					label: {text: 'Password Field', css: 'label'},
					field: 'input', 
			   attributes: [
						{name: 'id', value : '_pwd'},
						{name: 'type', value : 'password'}, 
						{name: 'class', value : 'field-class'}, 
						{name: 'maxlength', value : 8}, 
						{name: 'value', value : 'password'}
					]		
			}, 	{       
       // Configure Radio Button
					   id: '_radio1',
					model: 'group',					   
					label: {text: 'Radio A', css: 'label'},
					field: 'input', 
			   attributes: [
						{name: 'name', value : 'group'},
						{name: 'type', value : 'radio'}, 
						{name: 'value', value : 'A'},
						{name: 'class', value : 'field-class'}
					]		
			}, 	{       
					   id: '_radio2',	
					model: 'userName',					   
					label: {text: 'Radio B', css: 'label'},
					field: 'input', 
			   attributes: [
						{name: 'name', value : 'group'},			   
						{name: 'type', value : 'radio'}, 
						{name: 'value', value : 'B'},
            //Pre-Selected
						{name: 'checked', value : 'true'},
						{name: 'class', value : 'field-class'}
					]		
			}, 	{       
        // Configure Check Box
					   id: '_chkbx',
					model: '_chkbx',					   
					label: {text: 'Check Box', css: 'label'},
					field: 'input', 
			   attributes: [
						{name: 'id', value : '_chkbx'},			   
						{name: 'type', value : 'checkbox'}, 
						{name: 'value', value : 'C'},
            // Pre-Selected
						{name: 'checked', value : 'true'},						
						{name: 'class', value : 'field-class'}
					]		
			}, 	{       
      // Configure Test Area
					   id: '_txtarea',
					model: '_txtarea',					   
					label: {text: 'Text Area', css: 'label'},
					field: 'textarea',
					value: 'Some thing long!',	
			   attributes: [
						{name: 'id', value : '_txtarea'},				   
						{name: 'class', value : 'field-class'}
					]		
			}, 	{      
      // Configure Multiple Selection Box
					   id: '_mltslct',	
					model: '_mltslct',					   
					label: {text: 'Multiple Selection', css: 'label'},
					field: 'select',
				  options: {
					    value: ['option1', 'option4'],
			  remote_data_set: null,
        //Pre Loaded Data
			   local_data_set: [
              //Pre-Selection
							{value: 'option1', text: 'Option 1', defaultSelect: true}, 
							{value: 'option2', text: 'Option 2', defaultSelect: false}, 
              //Pre-Selection
							{value: 'option3', text: 'Option 3', defaultSelect: true}, 
							{value: 'option4', text: 'Option 4', defaultSelect: false}
						]},
			   attributes: [
						{name: 'id', value : '_mltslct'},				   
						{name: 'class', value : 'field-class'},
						{name: 'multiple', value : 'multiple'}
					]		
			}, 	{       
      // Configure Drop Down Box
					   id: '_slct_lcl',	
					model: '_slct_lcl',					   
					label: {text: 'Local Drop Down', css: 'label'},
					field: 'select',
				  options: {
            //Final Selected Value
						value: ['option1'],
			  remote_data_set: null,
        //Pre-Loaded Data
			   local_data_set: [
							{value: '', text: '--Select--', defaultSelect: false}, 
							{value: 'option1', text: 'Option 1', defaultSelect: false}, 
							{value: 'option2', text: 'Option 2', defaultSelect: false}, 
              //Pre-Selection
							{value: 'option3', text: 'Option 3', defaultSelect: true}, 
							{value: 'option4', text: 'Option 4', defaultSelect: false}
						]},
			   attributes: [
						{name: 'id', value : '_slct_lcl'},			   
						{name: 'class', value : 'field-class'}
					]		
			}, 	{       
					   id: '_slct_rmt',	
					model: '_slct_rmt',					   
					label: {text: 'Remote Drop Down', css: 'label'},
					field: 'select',
				  options: {
				  	    value: ['INDIA'],
			  remote_data_set: {
              //Remote Server Data Loading - Sample REST service 'loaddata1'
							service: 'http://localhost:8080/loaddata1',
               //Pre-Loading Parameters if any
							 params: { forKey: null}
					   },
			   local_data_set: null
					    },
			   attributes: [
						{name: 'id', value : '_slct_rmt'},			   
						{name: 'class', value : 'field-class'}
					]		
			}
    ];
  }]);

```

##Dependency Management:
A typical scenario of Country, Sate, Zip relations. At any point of time we might not be sure what the user selects on the Country which has to load the corresponding States which again will dictate the zipcodes
```
		$scope.my_field_input = [
			{       
					   id: '_cntry',
					model: '_cntry',					   
					label: {text: 'Country', css: 'label'},
					field: 'select',
				   parent: null,
              //Child Link - This is Stop Default Data load calls of States without a Country Selection
			        child: '_ste',
				  options: {
						value: ['USA'],				  
			  remote_data_set: {
							service: 'http://localhost:8080/loadcountry',
							 params: null
					   },
			   local_data_set: null
					    },
			   attributes: [
						{name: 'id', value : '_cntry'},			   
						{name: 'class', value : 'field-class'}
					]		
			}, 	{       
					   id: '_ste',	
					model: '_ste',					   
					label: {text: 'State', css: 'label'},
					field: 'select',
             //Parent Link - This is force the data load for a Selected Country
			       parent: '_cntry',
				    child: null,
				  options: {
						value: null,				  
			  remote_data_set: {
							service: 'http://localhost:8080/loadstate',
							 params: { forKey: null}
					   },
			   local_data_set: null
					    },
			   attributes: [
						{name: 'id', value : '_ste'},			   
						{name: 'class', value : 'field-class'}
					]		
			}];
```
