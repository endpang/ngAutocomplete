ngAutocomplete
==============





A simple directive for adding google places autocomplete to a textbox element.

Texbox will be invalidated with a property name `parse` (see example below) if user fails to pick one of the suggestions.
As a result of the selection `$scope.details` will hold a bit modified version of "google place" object that is ready to be sent to the server/database.

You can specifying short_name or long_name for each component. Currently to do so you need to change `componentForm` variable in the `ngAutocomplete.js`. In time changing this will be allowed on the dirrective using attributes. `formattedAddress` still returns the long_name route version but the individual component is returned as specified.

Requirements
-------------
* AngularJs 1.3
* Reference to google maps api

Installation:
-------------
*Reference module in your app*
```
angular.module('app', ['ngAutocomplete']);
```

Example
-------------
```
<form name="formAddress" novalidate>
    <input ng-model="vm.address.formattedAddress" required
        ng-autocomplete details="vm.address"
        placeholder="Start typing your address" id="address" name="address" type="text" />
    
    <div ng-messages for="formAddress['address'].$error" class="help-block error">
        <div ng-message when="required">Please provide your address</div>
        <div ng-message when="parse">Please select one of the suggested options</div>
    </div>
</form>
```

**Demo:** [**Plunker Example**](http://plnkr.co/edit/2Ct5RSJIypBUHqB9NY9U?p=preview)

Credits
-------------
This is a heavily modified version of [Will Palahnuk](https://github.com/wpalahnuk)'s version of [ngAutocomplete](https://github.com/wpalahnuk/ngAutocomplete). Kudos, Will!

**Major differences/features are:**
* Directive does not use isolate scope.
* Details are stored as a modified version of Google Place object that's ready to be stored in DB.
* `<input>` requires `ng-model` attribute for built-in validation.
* included default validation that requires user to actually select one of the suggested options.
* Because of the [bug in Google Api](https://code.google.com/p/gmaps-api-issues/issues/detail?id=7627&thanks=7627&ts=1423588307), input disables validation described above when Google Service is not available (occurs when used in China)
* optional attribute `validate-fn` which can be used to provide additional validation function that'll run when user selects something from the list of suggestions.
