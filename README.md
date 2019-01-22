
[![License: CC BY-NC-ND 4.0](https://licensebuttons.net/l/by-nc-nd/4.0/80x15.png)](https://creativecommons.org/licenses/by-nc-nd/4.0/)


YDigital Media Client Side Libraries
====

This set of libraries makes integration to YDigital Media systems a breeze.



## Conversion Lib
This library is intended to be used to track conversions in landing pages of campaigns developed by YDigital Media and will allow clients to notify YDigital Media about a conversion. To start using the library you'll need to.

1. [Include the library in your page](#include-the-library-in-your-page);
2. [Change some configuration options (optional)](#configuration-options);
3. [Learn how to notify YDigital Media about a conversion](#make-a-conversion).

**Note:** This documentation assumes that you have basic knowledge of JavaScript and HTML.



#### Include the library in your page
The script you're about to include will look for all relevant parameters and save them for future use, that is, when a conversion takes place.
Include the script (at cdn.jsdelivr.net/gh/ydigitalmedia/conversion@4/yd-conversion.js) at the end of the body tag of your HTML document, ie:
```
        ...
        <div>Some content</div>
        <script type="text/javascript" src="//cdn.jsdelivr.net/gh/ydigitalmedia/conversion@4/yd-conversion.js"></script>
    </body>
</html>
```
After inserting the script tag inside the HTML document, there's some options you can use to change the default behavior of the script, please see the next section for details about this.



#### Configuration Options
Almost every part of the lib can be configured. Bellow there's a list of all the configurations you can change and how.

##### By declaring the YD variable
List of available configuration directives:

* **logging** (Boolean, false)
	Console logging switch. In test hosts it defaults to true.


* **testHosts** (Array, ['localhost', '10.0.0.169'])
	Array with a list of the test hosts.


* **conversion.ydUrlParameter** (string, 'yd')
	Expected YD URL parameter name on input


* **conversion.clickIdUrlParameter** (string, 'ydClick')
	Expected click id URL parameter name on input


* **conversion.formClassName** (string, 'yd-conversion')
	The CSS class name used to find the form that is "convertible"

Example:
```
        ...
        <div>Some content</div>
        <script type="text/javascript">
            window.YD = {
                logging: true,
                conversion: {
                    ydUrlParameter: 'yd',
                    clickIdUrlParameter: 'ydClick',
                    formClassName: 'yd-conversion'
                }
            };
        </script>
        <script type="text/javascript" src="//cdn.jsdelivr.net/gh/ydigitalmedia/conversion@4/yd-conversion.js"></script>
    </body>
</html>
```



##### By passing parameters in the URL
List of available configuration directives:

* **logging** (boolean, false)
	Console logging switch. In test hosts it defaults to true.


* **ydParam** (string, 'yd')
	Expected YD URL parameter name on input


* **clickParam** (string, 'ydClick')
	Expected click id URL parameter name on input


* **formClass** (string, 'yd-conversion')
	The CSS class name used to find the form that is "convertible"

Example:
```
<script type="text/javascript" src="//cdn.jsdelivr.net/gh/ydigitalmedia/conversion@4/yd-conversion.js?logging=1"></script>
```
You can also pass any of this configuration parameters in the top link of the page.



#### Make a conversion
This function will notify YDigital about a conversion, but only if yd parameters where found in the URL (or previously found and saved in a cookie or local data).
```
YD.trackConversion(action = null, payout = null, allowMultiple = false)
```
###### Parameters
* **action**         - Optional string convertion type, ie: purchase, install, etc. Can be any value and the default is null
* **payout**         - Optional float purchase value, usually when a purchase occurs
* **allowMultiple**  - Optional Boolean, the default is false, but if true will allow clients to make multiple conversions with the same yd and ydClick, usually only one is allowed.

###### Returns
Returns a Promise object. Read more about promises in here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

###### Examples
```
// Simple example
YD.trackConversion();

// Complete example
YD.trackConversion('purchase', 0.50, true);

// example with a callback
YD.trackConversion().then(function(event){
    window.alert('Success!');
});
```



#### Track events
This function will send events to clicks.ydigitalmedia.com. Use this method if you need to track events that the user performed in the client LP.
```
YD.trackEvent(eventName, action = 'click', useDOM = false)
```
###### Parameters
* **eventName** - This is the name / label of the event performed by the user.
* **action**    - Optional, the name of the action performed by the user, available options are: *click*, *shake*, *share* and *swipe*. The default is *click*.
* **useDOM**    - Optional, this parameter is *false* by default and in case it's true, a real HTML image tag will be written to the document, otherwise (the default) the Image object will be used to make the server call.

###### Returns
Returns a Promise object. Read more about promises in here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

###### Examples
```
// Simple example
YD.trackEvent('Know More');

// Complete example
YD.trackEvent('Know More', click, false);

// example with a callback
YD.trackEvent().then(function(event){
    window.alert('Success!');
});
```



#### Get tracking-code
Obtain the current tracking-code
```
YD.getTrackingCode()
```
###### Returns
Returns the detected tracking-code or null if none was detected.



#### Get click ID
Obtain the current click ID
```
YD.getClickId()
```
###### Returns
Returns the detected click ID or null if none was detected.




## License
#### Attribution-NonCommercial-NoDerivatives 4.0 International
[creativecommons.org/licenses/by-nc-nd/4.0/](https://creativecommons.org/licenses/by-nc-nd/4.0/)
