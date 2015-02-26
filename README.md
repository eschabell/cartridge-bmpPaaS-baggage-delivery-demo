Cartridge for bpmPaaS with Baggage Deliver Demo
===============================================
This cartridge provides the **_Red Hat JBoss BPM Suite_** for easy deployment to OpenShift based bpmPaaS with pre-loaded Baggage
Delivery Demo.


Install with one click in xPaaS (bpmPaaS)
-----------------------------------------
After clicking button, ensure `Gear` size is set to `medium`:

[![Click to install OpenShift](http://launch-shifter.rhcloud.com/launch/light/Install bpmPaaS.svg)](https://openshift.redhat.com/app/console/application_type/custom?&cartridges[]=https://raw.githubusercontent.com/jbossdemocentral/cartridge-bpmPaaS-baggage-delivery-demo/master/metadata/manifest.yml&name=baggagedelivery&gear_profile=medium&initial_git_url=)

Once installed you can use the JBoss BPM Suite logins: 

   * u:erics   p: bpmsuite  (admin)

   * u: alan   p: bpmsuite  (analyst)

   * u: daniel p: bpmsuite (developer)

   * u: ursla  p: bpmsuite (user)

   * u: mary   p: bpmsuite (manager)


Running the demo
----------------
Build the project then kick off the process. An initial form will show for first name, last name, 
flyer status {None, Bronze, Silver, Gold}, Country Code, Zip if in US and number of bags lost.  

If in US, will pass in zip code to zip code web service. Only the following zip codes will return 
states. Any other zip will return Texas.

	  //Park Ridge, IL
		zipCodes.put("60068", "IL");
		
		//Honolulu, HI
		zipCodes.put("96801", "HI");
		
		//New York, NY
		zipCodes.put("10001", "NY");
		
		//Bethel, AK
		zipCodes.put("99559", "AK");

After zip code service is called, the state field on passenger is used in web decision table to 
determine the cost of shipping.  Next, a DSL is used to figure out a surcharge for AK and HI.  

If not in US, county code is looked up in spreadsheet decision table and sets shipping and surcharge.

Finally, DSL is used to apply a promotion of free shipping and surcharge if passenger is of status Gold. 
You are then shown the route the process took and the variables to confirm shipping and surcharges are correct.

Note: this is a fully automated Straight Through Process (STP), so to view outuput of logs in the Cloud you need
to use the following OpenShift CLI command from a console:

    ```
    $ rhc tail baggagedelivery
    ```


Important Note
--------------
You need the ability to setup MEDIUM gears, which is freely available if you [upgrade your account to Bronze here] (https://www.openshift.com/products/pricing). 


Manual setup on OpenShift
-------------------------
Or if you want to use the [rhc command line](https://www.openshift.com/developers/rhc-client-tools-install) type:

    rhc app create -g medium <APP NAME> https://raw.githubusercontent.com/jbossdemocentral/cartridge-bpmPaaS-baggage-delivery-demo/master/metadata/manifest.yml

For more information on the [JBoss BPM Baggage Delivery Demo see here] (https://github.com/jbossdemocentral/bpms-baggage-delivery-demo).

Supporting Articles
-------------------
None yet...


Released versions
-----------------
See the tagged releases for the following versions of the product:

- v1.0 - bpmPaaS on OpenShift cartridge, JBoss BPM Suite 6.0.2 and JBoss BPM Baggage Delivery demo installed.

![Digital Sign Annoucement](https://github.com/jbossdemocentral/bpms-baggage-delivery-demo/blob/master/docs/demo-images/cloud-sign.jpg?raw=true)
