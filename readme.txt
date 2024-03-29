* USPS RateV4 Intl RateV2 - September 7, 2014 Version K6

This module requires that you have CURL installed on your server.

If you do not already have a USPS Web Tools account ...

Registering and Creating a customer account for USPS realtime shipping quotes ...

If you do not already have a USPS Web Tools account ...

1. Register and create a USPS Web Tools account:
https://www.usps.com/business/webtools.htm

2. Fill in your customer information details and click Submit

3. You will receive an email containing your USPS rate-quote Web Tools User ID

4. Insert the Web Tools User ID in the Zen Cart USPS shipping module.

5. Telephone USPS 1-800-344-7779 and ask them to move your account to the Production Server or email them at icustomercare@usps.com, quoting your Web Tools User ID.

6. They will send another confirmation email. Set the Zen Cart module into Production mode (instead of Test mode) to finish activation.


To install this code ...

1 go to your Zen Cart Admin to the Modules ... Shipping ...

2 If USPS exists, Click on USPS and edit then save all your settings to NotePad as they will be lost

3 Go to your Zen Cart Admin and to the Modules ... Shipping ...

4 If USPS exists, Click on USPS and then click REMOVE to uninstall the current version of USPS

5 Load the new files with your FTP program they go in the same directories so you can copy the directory
/includes

to your server and overwrite the old files:
/includes/modules/shipping/usps.php
/includes/languages/english/modules/shipping/usps.php

6 Go to your Zen Cart Admin and to the Modules ... Shipping ...

7 Click on USPS shipping modules and click INSTALL

8 Configure your USPS shipping module


=====

NOTE: 2014-10-30

Updates to the USPS Production Server should include the missing quotes for: First-Class Mail Large Envelope

This version removes the CURLOPT_SSLVERSION setting in response to the POODLE bug.

This USPS module will also update the table: orders field: shipping_method to manage larger USPS shipping method names.

For Online quotes, and addition for: First-ClassTM Package Service has been added. This is ONLY available for Online quotes.

Also added is $usps_insurance_charge
          $methods[] = array('id' => $type_rebuilt,
                             'title' => $title . $show_hiddenCost,
                             'cost' => $cost,
                             'insurance' => $usps_insurance_charge,
                            );


which could be used for creating an Order Total module to offer an optional insurance opt-out by customers.


=====

NOTES:

Rates are quoted ONLY for those methods that are checked.

USPS minimum Length, Width and Height are only included for obtaining International Rate Quotes. Dimensions are NOT supported by this shipping module.
There are now separate settings for Domestic and International.

Minimum Weight and Maximum Weight per shipping method will enable/disable the methods based on the total weight.

Handling has both Global National and International fees per Box or per Order. In addition, individual Handling Fees per order can be added for each shipping method.

Extra Service charges for National and International are available where applicable.

Quotes can be obtained based on Retail or Online pricing.

Debug logs can be saved to the /logs directory, when enabled to review quote request sent to USPS and quote received back from USPS.

For US shipping, First Class has a filter to help prevent multiple First Class quotes from being displayed, due to the way USPS responds back to quote requests for multiple First Class methods.

Enable USPS First-Class filter for US shipping
This will use the 1st quote from USPS for First-Class and skip other First-Class methods to help avoid duplicate display quotes
note: using weight minimum/maximum is usually a better method to control this

USPS Options for the Display Transit Times may slow down quotes

USPS Domestic Transit Time Calculation Mode
a) NEW: uses whatever the new option "ShipDate" returns. This is something new added by USPS on July 28, and the way this Version J5 module implements it causes it to 
ask USPS to quote based on "ship this item today if quoting before 2pm, else ship tomorrow". 
This may affect the number of days you see, and maybe that's why you were confused about the meaning of this "NEW" option. 


b) OLD: uses the older legacy APIs (multiple separate calls to each Service) to get dates. This is how it worked before July 28. 
At this point there is no indicator whether this option will still be supported by USPS for much longer.

Note: If blank from USPS, uses CUSTOM values from parseDomesticLegacyAPITransitTimeResults() in usps.php

c) 
CUSTOM: uses only what's hard-coded into usps.php in the parseDomesticTransitTimeResults() function. Completely ignores whatever USPS provides.
NOTE: Ignored for International destinations.


