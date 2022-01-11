# Overview
This guide describes the various functions provided in the Home page of the reference UI implementation of the registration client.

## Registration client reference UI implementation
Below is the image of the reference UI implementation of the registration client.
![](_images/reg-client-orig.png)

### Menu bar
The registration client menu bar displays the following:

     * MOSIP logo
     * Home button
     * Logged in username
     * Center name
     * Machine name
     * Server connection status symbol(shows if the client is online or offline)
     * Breadcrumbs (User Guide/Reser Password/Logout)
    
![](_images/reg-client-menu.png)

### Operational Tasks
      
* **Synchronize Data**: Synchronize data is the data required to make the registration client functional. Full sync is performed initially during the launch of the registration client for the first time. Post this, the registration client syncs only the changes from sever and this is called as the delta sync. Synchronize data is automated and can be triggered manually. 
This happens automatically while launching the registration client and is also manually initiated by the operator.
 
   1. **Configuration sync**: Sync of properties which drives in deciding the registration client UI functionality. For example: Invalid login attempts, idle timeout, thresholds, etc
   1. **Masterdata sync** : As a part of this sync, supporting information like Dynamic fields data, templates, locations, screen authorization, block listed words, etc are pulled in.
   1. **UserDetails sync**: userID, user roles along witrh their status is synced. Only the user details belonging to machine mapped center will be synced. 
   1. **Certificate sync**: Certificates used to validate the server signatures, device CA certificates, public key used to encrypt the registartion packet will be synced.
   1. **Packet sync**: 
         * All the approved/rejected Registration IDs(RIDs) will be synced to the server.
         * All the synced RID packets will be uploaded to the server.
         * All the uploaded packet status will be synced from server.
          
* **Download Pre-Registration Data**: An operator can download the pre-registration data of a machine mapped center while being online and store it locally in the registration machine for offline use. Now when the system is offline and the pre-registration data is already downloaded, the operator can enter the pre-registration ID to auto-populate the registration form. Provided the machine is online, any pre-registration application can be downloaded irrespective of the center booked by the resident.
     
  **Note** - Date Range of pre-registration data to be downloaded and storage location of pre-registration data in the registration machine is configurable. Also, this is synced as a part of configuration sync.       
       
* **Update Operator Biometrics**:  Using this option, the operator can onboard themselves anytime.  
For more details, refer to [operator onboarding](operator_onboarding.md)

  ![](_images/reg-client-biometric-page.png)

 * **Application Upload**: Application upload refers to upload of supervisor reviewed registration packets(approved and rejected). From this page, the operator can export the packets to any location on their machine. 
      - Upload of registration packet from this page internally performs two operations in sequence:
          * Sync registration metadata to server
          * On successful sync of metadata, actual registration packets are uploaded to the server.
      
   **Client Status** : This column displays the status of a registration packet based on the above mentioned operation.
      
       * APPROVED
       * REJECTED
       * SYNCED
       * EXPORTED
 
   **Server Status** :
      
     On success,
     
       * PUSHED
       * PROCESSED 
       * ACCEPTED
      
    On failure,
      
       * REREGISTER
       * REJECTED
       * RESEND
        
  **Registration Type**: This column displays the type of registration packet(New packet, Lost packet, Update packet, Correction packet)
      
* **Center Remap Sync**:
      
* **Check Updates**:
   
   
### Registration Tasks
The operator can initiate any task from amongst- New registrations, Update UIN, Lost UIN, Correction flow. To get started, the operator needs to select a language for data entry. The number of languages displayed in the UI is configurable and depends on the country.
   
## New registration
An operator can initiate the process of registering a new applicant in the MOSIP ecosystem by filling the new registration form with the resident.

![](_images/reg-client-new-registration.png)

Below are few of the processes that needs to be completed for a new registration.
1. **Capture consent**- For every registration, the registration client provides an option for the operator to mark an individual's consent for data storage and utilization. 

2. **Enter demographic data and upload documents**
If the resident has a pre-registration application ID, the operator can auto-populate the demographic data and the documents by entering the pre-registration ID.
If the resident does not have a pre-registration ID, the operator can enter the resident’s demographic details (such as Name, Gender, DOB, Residential Address, etc.) and upload the documents (such as Proof of Address, Proof of Identity, Proof of Birth) based on the [ID Object defined](MOSIP-ID-Object-Definition.md) by the country.

3. **Capture biometrics of a resident**
The capture of biometrics is governed by the country, i.e. capture of each modality (fingerprint, iris or face) can be controlled by the country using the global configuration.
When the operator clicks on the **capture** button and tries to capture the biometrics of the resident, the device needs to make the capture when the quality of the biometrics is more than the threshold configured by the country. The device will try to capture the biometrics until the quality threshold has crossed or the device capture timeout has crossed which is also configurable. 

After the timeout has occurred and the captured quality of biometrics is less than the threshold, registration client provides an option to re-try capture of biometrics but for a particular number of times which is also configurable.
If the resident has a biometric exception (resident is missing a finger/iris or quality of finger/iris is very poor) the operator can mark that particular biometrics as **exception** but the operator has to capture the resident's exception photo.

 What is the difference between an adult' and an infant' biometric capture?
 * For an adult, all the configured biometrics can be captured.
 * For an infant, by default, only the face biometrics is allowed to be captured.   
     
## Update UIN
When a resident visits the registration center to update their demographic or biometric details, the operator captures the updated data as provided by the resident in the registration client. The resident needs to give their UIN and also select the field(s) that needs an update.
The image below gives an idea of the update UIN process Flow in the registration client.

![](_images/reg-client-update-uin.png)

{% hint style="info" %}
*The UIN update feature is configurable by a country. The Admin can turn ON or OFF, the UIN update feature using the configuration.*
{% endhint %}

## Lost UIN
There might be a situation when a resident might have lost his UIN and visits the registration center for retrieving the same. The operator then captures the biometrics and the demographic details of the individual and processes a request to retrieve the lost UIN. As biometrics play a crucial in identifying a person' indentity, it is mandated to provide the biometrics as a part of the Lost UIN flow. Other details like demographic data, documents are optional.
![](_images/reg-client-lost-uin.png)
   
## Correction process
For a resident whose UIN is yet not generated, they can get a request intimation to re-provide their details with a RequestId.
The same *AddtionalInfo RequestId* must be provided to the operator during the correction flow. 

![](_images/reg-client-lost-uin.png)

**Note**- The above mentioned Registration tasks are completely configurable through UI Specs<<link>>
   
## Preview and operator' packet authentication
   
* The operator can preview the data filled and navigate back to the respective tabs in case of corrections.
* Once the resident and the operator are satisfied with the data being captured, the operator can proceed to the authentication tab and provide his valid credentials to mark the complete of the registration task.

{% hint style="info" %}
Mode of authentication is configurable by a country. The Admin can turn ON or OFF the UIN update feature using the configuration.
{% endhint %}
   
## Acknowledgement receipt and printing
Once the registration process (new registration, UIN update or lost UIN, correction) is completed, the registration client generates an acknowledgement receipt.
This receipt contains a QR code of the Registration application ID, captured demographic data in the selected language, photograph of the resident and ranking of each finger from 1 to 10 (1 being the finger with the best quality). This receipt is print friendly and can be used for printing using any printer.

### End of day processes

* Pending Approval:
* Re-registrations:
 
  
### Dashboard:
      
### News and Updates: 