[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | Service Agreement | [Accessibility](Accessibility)  

# CHEFS Service Agreement  (DRAFT)
  
## Our responsibilities  
For your responsibilities read the CHEFS [Terms of Use](Terms-of-Use)  

### CHEFS Overview
* Software as a Service (SaaS) system operated by the Office of the Chief Information Officer (OCIO)  
* Private Cloud-hosted system using Openshift Container Platform (OCP). OCP hosts on their services an instance of CHEFS at Submit.digital.gov.bc.ca     
* Able to support the need for medium integrity, and medium availability services
* Urgent and emergency use cases requiring higher levels of integrity or availability may be considered on a case by case basis, with best efforts 

### Is CHEFS really free?  
#### Licences or Fees  
The teams that develop and support the CHEFS software are funded through the OCIO. The Licence for the software is free. There are no plans to ever switch to another funding model.  

#### What does the CHEFS team not pay for?  
* CHEF's clients using the product accept the cost of designing, testing, publishing, marketing, reviewing submissions, or exporting data for or from the individual forms that are built with CHEFS  
* In some cases there are Ministry teams who are contributing code to the CHEFS product. The OCIO welcomes these contributions but these contributions are not compensated. If you want to contribute code to improve CHEFS, you will need to pay your own staff or contractors to developer those new features or fixes.  

### You’re a CHEFS client if you’re
* An employee or contractor of the BC Government using **submit.digital.gov.bc.ca**  
* Staff who use CHEFS’s [interface](https://submit.digital.gov.bc.ca/) or [API](https://submit.digital.gov.bc.ca/app/api/v1/docs)  
* Services on CHEFS that are created by these staff  

### This agreement covers OCIO responsibilities for the CHEFS system  
**exceptions**:
* Devices such as computers or mobile phones  
* Other services or infrastructure, such as internet or email service providers   
* Services that form submitters need to submit forms, such as mobile phone carriers, internet or email service providers   

### OCIO CHEFS team will provide, operate and support  
* Patching security vulnerabilities in a timely manner, based on our determination of the level of threat  
* Priority bug fixes for all [CHEFS Capabilities](Capabilities) that are not listed as experimental
* Restoration of the system to operation if there’s unplanned downtime
     * Downtime is an interruption in which you experience a reduction in the existing quality of service or an event that will impact the existing service   
     * The CHEFS service is setup for [High Availability](Architecture), notwithstanding; unplanned downtime will trigger automated alarms to the CHEFS Team  
* Support your use of CHEFS, including requests submitted through our MS Teams channel or via email:  

(a) Non-urgent requests: We are working towards having shorter response times, usually in 1-2 business days, Monday to Friday between 9am-5pm Pacific Time  
(b) Urgent requests: We do not yet have funding for 24/7 support.  Response time is best efforts. Please include the phrase “this is urgent” in all caps in the request, and if we happen to be up for a midnight snack and happen to see the "URGENT REQUEST", we might go back to sleep pretending like we didn't see it, but likely someone will see it and start making a plan for the morning when the staff get back online   

### Maintain timely operations  
* Ensure Submit.digital.gov.bc.ca is available for use, We aim for an uptime of 99.95%   
* Excluding any downtime experienced by  
     * Openshift Container Platform   
     * Keycloak Login Services 
     * External APIs (Email Services, Document Generation Services, Address Lookups, and Business Name Search)   
* Utilize zero downtime deployments so that we can enhance and patch the product without service interruptions  

#### View the history of Uptime for various services: 
> [CHEFS Uptime Statistics Dashboard](https://stats.uptimerobot.com/vpjoZUE6YE)  
> [OCP Silver Cluster Uptime](https://status.developer.gov.bc.ca/statuspage/platform-service-status-page/1388599?start=20220101&end=20221231)       
> [Keycloak Login service on Gold Cluster](https://status.loginproxy.gov.bc.ca/)  


***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)