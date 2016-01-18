The sample portal is, while useful by itself, written in a way that it
demonstrates most features in the simplest format.

# directory structure
index.html    : the main landing page
bundle/messages.properties: for localization and hotspot package specification
payment.html  : for credit card information submission. requires https, also 
                served as an example of additional .html page
fail.html     : default page when there's error handling guest login

supporting files: 
images/
js/
reset-min.css
styles.css


===== unifi tags =====

====== <unifi var="name" /> ======
a few vars are populated where you can use <unifi var="varnames" /> to render it in the HTML page

* auth:            none | password | hotspot
* auth_none:       false | true
* auth_password:   false | true
* auth_hotspot:    false | true

* voucher_enabled: false | true
* payment_enabled: false | true

* package:         the package id (from POST or GET)
* mac:             guest's MAC address
* ap_mac:          AP's MAC address 
* ap_name:         AP's name
* map_name:        AP's location (name of the map)
* ssid:            the SSID of the wireless network

* error:           error message
* has_error:       false | true


====== <unifi include="header.html" /> ======
to include another HTML page


====== <unifi if="name" eq="value"> ... <unifi else="var" /> ... </unifi> ======
the simple if/then/else logic to determine if a section of the page should be shown
use <unifi if="!name" eq="value" > ...</unifi>


====== <unifi txt="InvalidPassword" /> ======
text localization, see bundle/messages.properties


====== <unifi url="payment.html" https="true" /> ======
generates the URL (and possibly change it to HTTPs) relatively


====== /guest/login ======
this is the URL the user will POST to get authorized, it takes the following parameters:

* by:               type of authentication (for hotspot): voucher | credit | paypal
* package:          package id (for hotspot)
* voucher:          voucher code (for hotspot/voucher)
* cc_xxxxx:         credit card information (for hotspot/credit):
* landing_url:      use a dynamic landing URL (which can be constructed by using vars)
* page_error:       relative URI when error occurs (fail.html is the default)


credit card related fields: 
cc_firstname, cc_lastname, cc_number, cc_year, cc_month, cc_ccv2
cc_addr1, cc_addr2, cc_city, cc_state, cc_zip, cc_country, cc_email
