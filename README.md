attachFormValidation
====================
 This is a js plugin that can be use when you need to add validation on your input field and show them in a tipsy, there is attachFormValidation.js you can use.  Example Usage: 
 The following snippet is from a current code I have with one my works.
Note: 
 You need to add the AttachFormValidation.js on your page before you can use it. for example you wanted to validate some input fields:  
 `````javascript
 80                 var $validator = Validator;
 81                 $validator.options.elements_to_validate = 'input';
 82                 $validator.actions.validate(checkErrors, null, '#save');
 83 
 84                 function checkErrors() {
 85                         $('.questions').find('input').each(function() {
 86                                 var $this = $(this);
 87                                 var value = $this.val().replace(/^\s+|\s+$/g,"");
 88                                 var is_rubric = false;
 89                                 if($this.attr('original-title')) {
 90                                         $this.validationNote({is_error : false});
 91                                 }
 92 
 93                                 if($this.hasClass('response')) {
 94                                         is_rubric = $this.closest('td').prev('td.question_rubric').find('input').is(':checked');
 95                                         if(is_rubric) {
 96                                                 if(isNaN(value)) {
 97                                                         $this.validationNote({msg : 'This field should be numeric.'});
 98                                                 }
 99                                                 if($validator.actions.isInteger(value) == false) {
100                                                         $this.validationNote({msg : 'This field should be an integer.'});
101                                                 }
102                                         }
103                                 }
104 
105                                 if($this.hasClass('points')) {
106                                         if(value == '' || typeof(value) == 'undefined') {
107                                                 $this.validationNote({msg : 'This is a required field.'});
108                                         }
109                                         if(isNaN(value)) {
110                                                 $this.validationNote({msg : 'This field should be numeric.'});
111                                         }
112                                 }
113 
114                         }).end();
115                 }
````` 
Line 80-81 instantiate a new Validator and added some option where to validate (elements_to_validate can be a class selector or an id selector) and then added the callback function.  'checkErrors' is the callback function that has the logic that you can set when to show your validation message. Line 89-91 clears all tipsy until the user do something on any of the input fields. (you may need to add this in every start of your callback so that the current and right tipsy will show.) Line 96-98 is an example when to show your tipsy, so, in that code, when the input value is empty and it has a class name 'response' a tipsy is showed with a message 'This is a required field' The rest of the logic has the same purpose with LINE 96-98.  Note: You need not to bother about preventing the submit event since AttachFormValidation already handles that. 
