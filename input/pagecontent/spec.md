This section defines the specific requirements for systems wishing to conform to actors specified in this MedMorph Central Cancer Registry Reporting Content IG.  The specification focuses on using the Health Data Exchange App (HDEA), MedMorph's backend services app, to report cancer data to central cancer registries.

### Context

#### Pre-reading
Before reading this formal specification, implementers should first be familiar with these sections of the specification:

* The [Use Cases](usecases.html) page provides the business context and general process flow enabled by the formal specification.


#### Conventions
This implementation guide uses specific terminology to flag statements that have relevance for the evaluation of conformance with the guide:

* **SHALL** indicates requirements that must be met to be conformant with the specification.

* **SHOULD** indicates behaviors that are strongly recommended (and which may result in interoperability issues or sub-optimal behavior if not adhered to), but which do not, for this version of the specification, affect the determination of specification conformance.

* **MAY** describes optional behaviors that are free to consider but where there is no recommendation for or against adoption.


#### Claiming Conformance 

Actors and Systems asserting conformance to this implementation guide have to implement the requirements outlined in the corresponding capability statements. The following definition of MUST SUPPORT is to be used in the implementation of the requirements.

##### MUST SUPPORT Definition

* Systems **SHALL** be capable of populating data elements as specified by the profiles and data elements are returned using the specified APIs in the capability statement.
* Systems **SHALL** be capable of processing resource instances containing the MUST SUPPORT data elements without generating an error or causing the application to fail. In other words, Systems SHOULD be capable of displaying the data elements for human use or storing it for other purposes.
* In situations where information on a particular data element is not present and the reason for absence is unknown, Systems **SHALL NOT** include the data elements in the resource instance returned from executing the API requests.
* When accessing Central Cancer Registry Reporting data, Systems **SHALL** interpret missing data elements within resource instances returned from API requests as data not present.
* When data is not available for any of the mandatory elements specified in the IG, a data absent reason extension should be added to satisfy the requirement along with an appropriate value from the [data-absent-reason value set](http://hl7.org/fhir/ValueSet/data-absent-reason).


#### Profiles and Other IGs Usage
This specification makes significant use of [FHIR profiles]({{site.data.fhir.path}}profiling.html), search parameter definitions, and terminology artifacts to describe the content to be shared as part of MedMorph Central Cancer Registry Reporting Content IG workflows. The implementation guide is based on [FHIR R4]({{site.data.fhir.path}}) and profiles are listed for each interaction.

The full set of profiles defined in this implementation guide can be found by following the links on the [FHIR Artifacts](artifacts.html) page.


##### MedMorph Reference Architecture (RA) IG Usage

This IG leverages the [MedMorph RA IG]({{site.data.fhir.ver.medmorphIg}}/index.html) defined by HL7 Public Health WG as the reference architecture for automating and implementing the central cancer registry reporting use case.

##### US Core Usage

This IG leverages the [US Core]({{site.data.fhir.ver.uscoreR4}}) set of profiles defined by HL7 for sharing non-veterinary EMR individual health data in the U.S.  Where US Core profiles exist, this IG either leverages them directly or uses them as a base for any additional constraints needed to support the research use cases.  If no constraints are needed, this IG does not define any profiles.


##### US Public Health (PH) library profiles Usage

This IG leverages the [US PH Library Profiles](https://build.fhir.org/ig/HL7/fhir-us-ph-common-library-ig/index.html) as a reference to define the following profile(s) in this IG:

	* USPublicHealthEncounter
	* USPublicHealthPatient


##### mCode FHIR IG Usage

This IG leverages the [mCode FHIR IG]({{site.data.fhir.ver.mcodeIg}}/index.html) for exchanging cancer specific information which includes the following profiles:

	* Primary Cancer Condition
	* Secondary Cancer Condition
	* Cancer Stage Group Information 
	* Cancer Related MedicationRequests 
	* Cancer Related MedicationAdministration
	* TNM Observations 
	* RadiotherapyCourseSummary
	
Implementers **SHOULD** use the [mCode Disease characterization]({{site.data.fhir.ver.mcodeIg}}/group-disease.html) and [mCode Treatment guidance]({{site.data.fhir.ver.mcodeIg}}/group-treatment.html) when using the above profiles.


##### Occupational Data for Health (ODH) IG Usage

This IG leverages the ODH FHIR IG for exchanging occupational data for health which includes the following profile:

	* Usual Work

##### Subscriptions Backport IG Usage

This IG leverages the [Subscriptions Backport IG]({{site.data.fhir.ver.subscriptionsIg}}/index.html) defined by HL7 Infrastructure WG for automating reporting workflows using subscriptions.

##### Bulk Data Access IG Usage

This IG leverages the [FHIR Bulk Data Access IG v1.0.1](http://hl7.org/fhir/uv/bulkdata/STU1.0.1/index.html) defined by HL7 Infrastructure WG for enabling authentication and authorization between various actors involved in the workflows. The Bulk Data Access IG is being referenced to use the SMART on FHIR Backend Services Authorization requirements only. The Bulk Data operations related to exporting data for a cohort (Group) or a patient or system level export is not used for this IG.


#### Implementation Requirements

##### SMART on FHIR Backend Services Authorization Requirements from the Bulk Data Access IG

This section outlines how the SMART on FHIR Backend Services Authorization (from the Bulk Data Access IG) will be used by the Central Cancer Registry (CCR) Reporting Content implementation guide. 

* The system actors namely EHR, backend services app, Trusted Third Party and the Central Cancer Registry are required to use the SMART on FHIR Backend Services Authorization mechanisms as outlined below for the following interactions: 

    * HDEA accessing data from the EHR.
    * HDEA posting data to the Central Cancer Registry data store.
    
* The system actor acting as a server (e.g., EHR, Trusted Third Party, and Central Cancer Registry) **SHALL** advertise conformance to SMART Backend Services by hosting a Well-Known Uniform Resource Identifiers (URIs) as defined in the [Bulk Data Access IG Authorization Section](http://hl7.org/fhir/uv/bulkdata/STU1.0.1/authorization/index.html#advertising-server-conformance-with-smart-backend-services) specification.

* The system actor acting as a server **SHALL** include token_endpoint, scopes_supported, token_endpoint_auth_methods_supported and token_endpoint_auth_signing_alg_values_supported as defined in the [Bulk Data Access IG Authorization Section](http://hl7.org/fhir/uv/bulkdata/STU1.0.1/authorization/index.html) specification.

* When a system actor act as a client (HDEA), they **SHALL** share their JSON Web Key Set (JWKS) with the server System actors (EHRs, Trusted Third Party and Central Cancer Registry) using Uniform Resource Locators (URLs) as defined in the [Bulk Data Access IG Authorization Section](http://hl7.org/fhir/uv/bulkdata/STU1.0.1/authorization/index.html#registering-a-smart-backend-service-communicating-public-keys) specification.

* The system actor acting as a client **SHALL** obtain the access token as defined in the [Bulk Data Access IG Authorization Section](http://hl7.org/fhir/uv/bulkdata/STU1.0.1/authorization/index.html#obtaining-an-access-token) specification.

* For the Central Cancer Registry Reporting use cases, EHRs **SHALL** support the system/*.read scopes. 

* The Central Cancer Registry **SHALL** support the system/*.read and system/*.write scopes. 

* The healthcare organization's existing processes along with the EHRs authorization server **SHALL** verify consent and other policy requirements before allowing the HDEA to access the data to be included in the central cancer registry report. 
 

##### Knowledge Artifact and Knowledge Artifact Repository Requirements 

* The Central Cancer Registry **SHALL** create a Knowledge Artifact following the constraints identified by the [MedMorph Provisioning Requirements]({{site.data.fhir.ver.medmorphIg}}/provisioning.html#creating-knowledge-artifacts).

* The Central Cancer Registry **SHALL** publish the value sets required to trigger a cancer report for a patient with an encounter diagnosis of cancer. This can be published in the Central Cancer Registry FHIR Server or a separate Knowledge Artifact Repository.

* The Central Cancer Registry **SHALL** republish the value sets when the list of concepts comprising the value sets change. 

* The Central Cancer Registry **SHALL** create the Knowledge Artifact following the constraints identified in [ccrr-plandefinition](StructureDefinition-ccrr-plandefinition.html).

* The Central Cancer Registry **SHALL** implement the Knowledge Artifact Repository requirements as outlined in the [MedMorph RA Knowledge Artifact Repository Requirements]({{site.data.fhir.ver.medmorphIg}}/CapabilityStatement-medmorph-knowledge-artifact-repository.html).

##### EHR Requirements

* The EHR **SHALL** support the requirements as outlined in the [EHR Capability Statement](CapabilityStatement-central-cancer-registry-reporting-ehr.html).

###### Authorization requirements 

* EHRs **SHALL** support the [SMART on FHIR Backend Services Authorization](spec.html#smart-on-fhir-backend-services-authorization-requirements) outlined above as a Server. 
 

###### Subscription requirements

* EHRs **SHALL** support the creation of Subscriptions for the [encounter-close Subscription Topic]({{site.data.fhir.ver.medmorphIg}}/StructureDefinition-encounter-close.html).

* EHRs **SHALL** support [``rest-hook``]({{site.data.fhir.path}}subscription.html#2.46.7.1) Subscription channel to notify the HDEA.

* EHRs **SHALL** support Notification Bundles with [``full resource payload``]({{site.data.fhir.ver.subscriptionsIg}}/payloads.html#full-resource) as outlined in the Backport Subscriptions IG. 

* For the Central Cancer Registry Reporting Ig, EHRs **SHALL** include the Encounter resource which was closed as part of the Notification Bundle.

* EHRs **SHALL** support operations and APIs for Subscription, Notification Bundle, and Subscription Status resources as outlined in the [EHR Capability Statement](CapabilityStatement-central-cancer-registry-reporting-ehr.html).


###### Data API requirements

* EHRs **SHALL** support the APIs as outlined in the [EHR Capability Statement](CapabilityStatement-central-cancer-registry-reporting-ehr.html) for the HDEA to access patient data.

 
##### HDEA Requirements 


###### Authorization requirements

* The HDEA **SHALL** support the [SMART on FHIR Backend Services Authorization](spec.html#smart-on-fhir-backend-services-authorization-requirements) outlined above as a client. 


###### Subscription requirements

* The HDEA **SHALL** create Subscriptions for the [encounter-close Subscription Topic]({{site.data.fhir.ver.medmorphIg}}/StructureDefinition-encounter-close.html).

* The HDEA **SHALL** support [``rest-hook``]({{site.data.fhir.path}}subscription.html#2.46.7.1) Subscription channel to receive notifications from the EHR.


###### Subscription Notification API 

* The HDEA **SHALL** support a POST API <BSA Base URL>/receive-notification with a payload of the Subscription Notification Bundle to receive the notifications from the EHR. 


###### Knowledge Artifact processing requirements 

* The HDEA **SHALL** allow the healthcare organization to activate/deactivate a specific Knowledge Artifact. Activation indicates applying the Knowledge Artifact and deactivation indicates not applying the Knowledge Artifact for events occurring within the healthcare organization.

* The HDEA **SHALL** process the MedMorph Central Cancer Registry Reporting Knowledge Artifact and create Subscription resources in the EHR for each trigger event.

* For the Central Cancer Registry Reporting IG, the HDEA **SHALL** create the Subscription for the [encounter-close Subscription Topic]({{site.data.fhir.ver.medmorphIg}}/StructureDefinition-encounter-close.html) trigger event. 

* Upon deactivation of a Knowledge Artifact, The HDEA **SHALL** delete the Subscriptions previously created by the BSA for the Knowledge Artifact (e.g., delete the Subscription created for encounter-close trigger event). 

* The HDEA **SHALL** implement FhirPath expression processing to process the Central Cancer Registry Reporting Knowledge Artifact actions.

* The HDEA **SHALL** use the default queries outlined by the Central Cancer Registry Reporting Knowledge Artifact unless overridden by the healthcare organization.

* The HDEA **SHALL** ensure no duplicate reports are submitted for the same patient and encounter occurring within a healthcare organization.


###### Data API requirements 

* The HDEA acting as a client **SHALL** use the APIs as outlined in the [EHR Capability Statement](CapabilityStatement-central-cancer-registry-reporting-ehr.html) to access patient data from the EHR.


###### Report generation requirements 

* The HDEA **SHALL** create a central cancer registry report following the constraints identified in [Central Cancer Registry Content Bundle](StructureDefinition-ccrr-content-bundle.html).

* The HDEA **SHALL** package the central cancer registry report following the constraints identified in [Central Cancer Registry Reporting Bundle](StructureDefinition-ccrr-reporting-bundle.html).

* The HDEA **SHALL** submit the message containing the central cancer registry report to the endpoint identified in the MedMorph Central Cancer Registry Reporting Knowledge Artifact unless overridden by the healthcare organization.

###### MedMorph RA Requirements 

* The HDEA **SHALL** implement the MedMorph HDEA requirements as outlined in the [MedMorph HDEA requirements]({{site.data.fhir.ver.medmorphIg}}/CapabilityStatement-medmorph-backend-service-app.html).

##### Central Cancer Registry Requirements 


###### Message Receiving and Processing requirements

* The Central Cancer Registry Data Store **SHALL** implement the $process-message operation on the ROOT URL of the FHIR Server to receive reports from the HDEA using the POST operation.

* Upon receipt of the message, the Central Cancer Registry Data Store **SHALL** validate the message before accepting the message.

* When there are validation failures, the Central Cancer Registry Data Store **SHALL** return an Operation Outcome response with the details of the validations as part of the POST response.

* The Central Cancer Registry **SHALL** implement the PHA requirements as outlined in the [MedMorph Data Receiver requirements]({{site.data.fhir.ver.medmorphIg}}/CapabilityStatement-medmorph-public-health-authority.html).

##### Trusted Third Party Requirements


###### Message Receiving and Processing requirements

* Trusted Third Parties **SHALL** implement the $process-message operation on the ROOT URL of the FHIR Server to receive reports from the HDEA using the POST operation.

* Upon receipt of the message, the Trusted Third Parties **MAY** validate the message before accepting the message.

* When the message is validated and there are validation failures, Trusted Third Parties **SHALL** return an Operation Outcome response with the details of the validations as part of the POST response.

* Once a message is accepted by a Trusted Third Party without errors, the Trusted Third Party will have to route the message to the Central Cancer Registry.

* The TTP **SHALL** implement the Trusted Third Party requirements as outlined in the [MedMorph RA TTP requirements]({{site.data.fhir.ver.medmorphIg}}/CapabilityStatement-medmorph-trusted-third-party.html).

