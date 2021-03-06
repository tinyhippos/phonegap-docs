contacts.find
=============

Queries the device contacts database and returns one or more `Contact` objects, each containing the fields specified.

    navigator.service.contacts.find(contactFields, contactSuccess, contactError, contactFindOptions);

Description
-----------

contacts.find is an asynchronous function that queries the device contacts database and returns an array of `Contact` objects.  The resulting objects are passed to the `contactSuccess` callback function specified by the __contactSuccess__ parameter.  

Users must specify the contact fields to be used as a search qualifier in the __contactFields__ parameter.  Only the fields specified in the __contactFields__ parameter will be returned as properties of the `Contact` objects that are passed to the __contactSuccess__ callback function.  A zero-length __contactFields__ parameter will result in an array of empty `Contact` objects.

The __contactFindOptions.filter__ string can be used as a search filter when querying the contacts database.  If provided, a case-insensitive, partial value match is applied to each field specified in the __contactFields__ parameter.  If a match is found in a comparison with _any_ of the specified fields, the contact is returned.

Parameters
----------

- __contactFields:__ Contact fields to be used as search qualifier. Only these fields will have values in the resulting `Contact` objects. _(DOMString[])_ [Required]
- __contactSuccess:__ Success callback function that is invoked with the contacts returned from the contacts database. [Required]
- __contactError:__ Error callback function. Invoked when error occurs. [Optional]
- __contactFindOptions:__ Search options to limit and/or filter contacts. [Optional]

Supported Platforms
-------------------

- Android
- BlackBerry Widgets (OS 5.0 and higher)
- iOS

Quick Example
-------------

    function onSuccess(contacts) {
        alert('Found ' + contacts.length + ' contacts.');
    };

    function onError() {
        alert('onError!');
    };

    // find all contacts with 'Bob' in any name field
    var options = new ContactFindOptions();
	options.filter="Bob"; 
	var fields = ["displayName", "name"];
    navigator.service.contacts.find(fields, onSuccess, onError, options);

Full Example
------------

    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
                          "http://www.w3.org/TR/html4/strict.dtd">
    <html>
      <head>
        <title>Contact Example</title>

        <script type="text/javascript" charset="utf-8" src="phonegap.js"></script>
        <script type="text/javascript" charset="utf-8">

        // Wait for PhoneGap to load
        //
        function onLoad() {
            document.addEventListener("deviceready", onDeviceReady, false);
        }

        // PhoneGap is ready
        //
        function onDeviceReady() {
		    // find all contacts with 'Bob' in any name field
		    var options = new ContactFindOptions();
			options.filter="Bob"; 
			var fields = ["displayName", "name"];
		    navigator.service.contacts.find(fields, onSuccess, onError, options);
        }
    
        // onSuccess: Get a snapshot of the current contacts
        //
        function onSuccess(contacts) {
			for (var i=0; i<contacts.length; i++) {
				console.log("Display Name = " + contacts[i].displayName);
			}
        }
    
        // onError: Failed to get the contacts
        //
        function onError() {
            alert('onError!');
        }

        </script>
      </head>
      <body onload="onLoad()">
        <h1>Example</h1>
        <p>Find Contacts</p>
      </body>
    </html>
    
iOS Quirks
----------
- iOS currently only supports searching by name.
