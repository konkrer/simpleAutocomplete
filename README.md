# simpleAutocomplete  
---

## Dead simple autocomplete suggestions display and selection.  
<br>


simpleAutocomplete is a vanilla JavaScript utility class and some CSS used to display auto-complete suggestions to the user. Setup and use is very simplistic and minimalistic. As the user selects a suggestion the value is put in the corresponding text input element and a callback is called if provided. This utility is so simple it should be no problem for JavaScript developers of nearly any skill level to quickly understand and/or alter the code to their needs. Customize the CSS file to your needs.

The developer is responsible for watching for text being typed in inputs, obtaining the auto-complete suggestions they wish to display, and for the simple preparation for display. See below section: ***Preparing Suggestions for Display*** 

###Setup:

1. Load `simpleAutocomp.css` and `simpleAutocomp.js` files on the page you want to have auto-complete functionality. For example:  
		
		<link rel="stylesheet" href="/static/css/simpleAutocomp.css" />  

		<script src="/static/js/simpleAutocomp.js"></script>

  
2.	For each HTML text input you wish to have auto-complete display functionality prepare the HTML by putting a datalist element directly after each text input with the proper sequential id as below: 

		<!-- First input with simpleAutocomplete functionality on page -->  

		<input type="text" name="..." id="...">
		<datalist id="datalist-autocomplete">

		<!-- Second input with simpleAutocomplete functionality on page -->  

		<input type="text" name="..." id="...">
		<datalist id="datalist-autocomplete-1">

		<!-- Third input with simpleAutocomplete functionality on page -->  

		<input type="text" name="..." id="...">
		<datalist id="datalist-autocomplete-2">

3.	Instantiate a simpleAutocomplete object for each text input autocomplete functionality you need. There needs to be an corresponding datalist element properly labeled with sequential id for each new simpleAutocomplete object created (as above).

		// This instance has a callback and will be associated with the first input and datalist with id "datalist-autocomplete".
		const autocomp0 = new simpleAutocomp(callback);

		// This instance has a callback and will be associated with the second input and datalist with id "datalist-autocomplete-1".
		const autocomp1 = new simpleAutocomp(callback, 1);

		// This instance has no callback and will be associated with the third input and datalist with id "datalist-autocomplete-2".
		const autocomp2 = new simpleAutocomp(null, 2);

4. Write code to watch for the user typing in the auto-complete inputs, get the suggestions, and prepare the results as a HTML string or array of elements. See ***Preparing Suggestions for Display*** below. (For example add "keyup" event listener on the text input, call an API with the text input value for suggestions, then prepare the HTML string or array of elements to be added to the datalist for display.)

5. Next, in that code after preparing suggestions for display set the datalist or datalistElements property on the simpleAutocomplete object to equal the the HTML string or array of elements to display the results.

		// Display the prepared HTML string.
		autocomp0.datalist = htmlString;

		// Display the prepared array of DOM elements.
		autocomp0.datalistElements = arrayOfElements;

6. Your Done! If the user selects a suggestion it will be made the value of the associated input and the callback will be called if provided.

7.	If you need the value of the last suggestion the user selected in the callback function it is available as the value property on the class instance.

		autocomp0.value // The last value the user selected.

    If you need to programmatically hide the datalist of suggestions call closeDatalist.

		autocomp0.closeDatalist()

<br>


###Preparing Suggestions for Display:

The suggestions need to be put inside of HTML option elements. If we had suggestions of "A" and "B", this would be the HTML string preparation and display:


		const htmlString = "<option value="A">A</option><option value="B">B</option>";
		autocomp0.datalist = htmlString;

This could be the preparation of an array of elements and the display of those elements:

		const array = [];

		const el1 = document.createElement("option");
		el1.value = "A";
		el1.innerText = "A";
		const el2 = document.createElement("option");
		el2.value = "B";
		el2.innerText = "B";

		array.push(el1, el2);
		autocomp0.datalistElements = array;

<br>
###Options:  

		SimpleAutocomplete(callback, multiAutoCompID, fontAwesome, marginTop, fixed)

  Callback --> Function. (default: null)  

  Optional function to be called after user suggestion selection.

----------


  multiAutoCompID --> Number. (default: 0)  

Id differentiator for when there are multiple SimpleAutocomplete instances.
Leave the first one default or set to 0. Set the next one to one, then increment for each
additional SimpleAutocomplete added (i.e. - 1, 2, 3...).


----------


  fontAwesome --> Boolean. (default: false)  

If font awesome icons are available and desired for the close button.


----------


  marginTop --> String. (default: null)  

String setting for CSS margin-top to adjust datalist position to input.


----------


  fixed --> Boolean. (default: false)  

Set to true to make datalist have a position: fixed instead of absolute.
Use as necessary to ensure the entirety of the datalist is visible when the
containing div is too small to allow full datalist to be visible.