**Date:** 29 September 2020

**Class:** COSC 69.11: Mobile X

**Team Members:** Manzi, Maria, John, and Abubakar

# Project Proposal

## Background 

In the pandemic era, it is becoming increasingly important to accurately identify nearby users within a specific proximity of one another. Currently, there are a multitude of protocols available for device discovery: bluetooth technology, WiFi technology, AirDrop, and Google Nearby. Unfortunately, no protocol is foolproof. Bluetooth requires users to have Bluetooth constantly enabled, which depends strongly on individual Bluetooth habits. WiFi misses out on users who are in the same radius but are not connected to the same network, which is exacerbated by the growing number of private WiFi networks. As a result, Apple has developed AirDrop, which requires two devices to both have WiFi and Bluetooth enabled, but does not require users to be on the same network. AirDrop, therefore, suffers from the same issues (Bluetooth must be constantly enabled) on top of also restricting its user base to those running a Mac OS. Google’s competitor, Nearby Share, released on August 4th, 2020, automatically determines the best protocol for connection — Bluetooth, Bluetooth Low Energy, WebRTC, or peer-to-peer WiFi — and then allows Android users to establish the connection. The more general use case, Google Nearby Messages API, requires one user to broadcast messages and allows others to subscribe to receiving these messages. Therefore, the unfortunate drawback to Nearby Messages is that it requires two-way permissions for discovery, which isn’t as useful for a user who simply wants to know how many other users they are coming into close contact with. Overall, there is currently no method for a user to easily identify how many users they are physically coming into contact with. 

**Proposed Solution:** We propose using the bluetooth low energy protocol to allow a user to scan and identify other devices with whom they come into close contact throughout the day.

## Timeline: 

**Base Functionality:** Weeks 3-6

The minimum technical requirements are:

1.	The ability to scan for nearby devices
2.	The ability to identify mobile devices from other device types that are less likely to be physically located on a user, such as a laptop or Amazon Alexa. 

### Week 3
We will aim to answer the following questions:

1.	What technology can you use to scan Bluetooth frequencies?

	* Google Nearby or p2pkit- requires an API call
	* Can this be done locally i.e. using the react 		native bluetooth library
	
2.	What technology can you use to differentiate mobile phones from other devices?
3.	What technology can you use to estimate distance between two devices which have been detected?

##### To Dos/ Deliverables

* Read and become familiar with bluetooth low energy technology. (Everyone)
* Develop testing platform (Bakar and John)
* Explore Bluetooth Libraries/APIs of interest (Maria and Manzi)

### Week 4
Develop and write design/implementation specifications

##### To Dos/ Deliverables

* Discuss implementation and project architecture. (Everyone)
* Assign development tasks. (Everyone)

### Week 5 (Thursday)

Mid-Project Presentations — present design/implementation specifications

### Weeks 4-6 
Implementation phase

##### To Dos/ Deliverables

* Develop!

### Weeks 7-10
Achieving Expanded Functionality

### Week 7
Identify places for improvement, research implementation methods, draft improvement specifications

### Week 8 - 9 
Implement improvements phase

### Week 10 (Tuesday)
Final-Project Presentations

## The Proposed Methodology

We envision that achieving minimum functionality will be simple enough. In the next few weeks, we plan to use the React Native Bluetooth Low Energy library, to build a simple Bluetooth scanner application while simultaneously learning how the Bluetooth architecture works. After that we need to achieve “Expanded Functionality”.

## The Expanded Functionality

1.	Can we estimate the distance between the devices?
2.	Can we estimate the likelihood that there are obstacles i.e. walls which are reducing our accuracy
3.	Can we estimate the likelihood that a user has come into contact with an infected person/the virus

We have two ideas in this vein:

To estimate distance we plan on using the following metrics:

1.	A weighted distance metric which uses signal strength to approximate how close devices are
2.	A system which uses the React Native Bluetooth Low Energy library’s RSSI (Received Signal Strength Indicator) in conjunction with other tools to counteract the drawbacks of using RSSI to calculate distance between our users and in-range bluetooth devices
3.	A system which uses technology such as the BatMapper to approximate room geometry and improve our distance metric. 


## Resources

**"Overview  |  Nearby Connections API  |  Google Developers". Google Developers, 2020,** [Link](https://developers.google.com/nearby/connections/overview)	

Google created a way to discover and establish direct communication channels with other devices without having to be connected to the Internet. The communication channel also allows Apple to Android communication.

**"Interact With Apps & People Around You - Google Account Help". Support.Google.Com, 2020,** [Link](https://support.google.com/accounts/answer/6260286?hl=en)

Google gives detailed requirements and instructions on how to use the Nearby app. Some requirements include having both parties install the app on their devices before communication can begin.

**"The Contact Tracing App For Business | Saferme". Safer.Me, 2020,**
[Link](https://www.safer.me/?utm_term=apple%20contact%20tracing%20app&utm_campaign=&utm_source=adwords&utm_medium=ppc&hsa_acc=5288895516&hsa_cam=10500904041&hsa_grp=103118343119&hsa_ad=446996678312&hsa_src=g&hsa_tgt=kwd-912849510893&hsa_kw=apple%20contact%20tracing%20app&hsa_mt=e&hsa_net=adwords&hsa_ver=3&gclid=Cj0KCQjwtsv7BRCmARIsANu-CQd5JF4ElvRn0yBbG4A5gXAmkmWwgQgoivrAcGK6uCEtsG6zPWK7EGgaAucyEALw_wcB)


The company SaferMe developed a contact tracing app for businesses, using bluetooth technology. SaferMe allows companies to keep track of who their employees are interacting with, so that if one employee contracts the virus the company can contain the situation at the source.

**"Apple And Google Partner On COVID-19 Contact Tracing Technology". Apple Newsroom, 2020,** [Link](https://www.apple.com/newsroom/2020/04/apple-and-google-partner-on-covid-19-contact-tracing-technology/)

Google and Apple are joining forces to enable the use of Bluetooth technology to help governments and health agencies reduce the spread of the virus, with user privacy and security central to the design.

**Brown, Bruce. "Wristband Promotes Social Distancing, Aids Contact Tracing". Health Tech Insider, 2020,** [Link](https://healthtechinsider.com/2020/05/14/wristband-promotes-social-distancing-aids-contact-tracing/)  

Canadian company Proxxi developed a wearable wristband called “Halo”. The Halo wristbands have unique IDs and the sensors are always on and use low-energy Bluetooth to detect other units. Each wristband maintains a detailed proximity log of contact with other wristbands. The wristband does not track location and no personally identifiable information is shared between units.

**Becker, Johannes K., David Li, and David Starobinski. "Tracking anonymized bluetooth devices." Proceedings on Privacy Enhancing Technologies 2019.3 (2019): 50-65.** [Link](https://www.researchgate.net/publication/334590931_Tracking_Anonymized_Bluetooth_Devices/fulltext/5d3308db92851cd04675a469/Tracking-Anonymized-Bluetooth-Devices.pdf)


The paper talks about how to use Bluetooth Low Energy (BLE) to anonymously track devices.


