### Background to Cancer Reporting in the USA

Population-based cancer surveillance is critical in North America for cancer control activities aimed at reducing the morbidity and mortality of cancer, the second leading cause of death in the United States (U.S.).  Population-based public health central cancer registries across the U.S. are mandated to collect complete and timely cancer diagnostic, treatment, and outcome data from hospitals, physician offices, treatment centers, clinics, laboratories, and other sources. Recent shifts in cancer treatment away from hospital settings and towards ambulatory healthcare settings are increasing the importance of ambulatory (non-hospital) healthcare providers (e.g., non-hospital, non-laboratory health care practitioner, physician or dental office, ambulatory surgery center, cancer treatment center, etc.) authorized/required to report a cancer case to the public health central cancer registry for cancer surveillance.

Regional, state and territorial public health central cancer registries collect, manage, and analyze data about cancer cases and cancer deaths. Cancer surveillance is a complex system that captures longitudinal data from multiple data sources using a variety of methods. In addition to recording the occurrence of each reportable cancer (or tumor), the reporters provide information to public health central cancer registries on the diagnosis, treatment and vital status. Reporting requirements may vary by hospital, state, district, territory, or province. Please note for the purposes of this implementation guide the term, “reportable cancer” is inclusive of all tumors reportable to a public health central cancer registry. The [North American Association of Central Cancer Registries (NAACCR) Standards for Cancer Registries, Volume II, Data Standards and Data Dictionary](http://datadictionary.naaccr.org/default.aspx?c=10&Version=22), describes the standards of tumor reportability for national standard-setting organizations in North America.

Public health central cancer registry data are used for surveillance, development of comprehensive cancer control programs, and healthcare planning and interventions. Improved accuracy and completeness of cancer surveillance data impacts all areas of public health interventions. Data also provides baseline and performance measures for cancer-related interventions designed to reduce cancer incidence or improve early detection. Identification of disparities among various population subgroups in stage at diagnosis or in treatment received can inform interventions to reduce these disparities and reduce the cancer morbidity and mortality in minority or disadvantaged populations.

The National Program of Cancer Registries (NPCR), established in 1992 by the U.S. Congress with enactment of the Cancer Registries Amendment Act (Public Law 202-515), is funded and managed by the Centers for Disease Control and Prevention’s (CDC) Cancer Surveillance Branch (CSB) in the Division of Cancer Prevention and Control (DCPC). The Surveillance Epidemiology and End Results (SEER) Program of the National Cancer Institute (NCI), initiated by the National Cancer Act of 1971 (PL 92-218), began collecting population-based cancer incidence data in 1973. Together, NPCR and SEER programs collect data for the entire U.S. population and produce the annual United States Cancer Statistics (USCS). CDC and NCI monitor the burden of cancer, including disparities among various population subgroups and provide data for research, evaluation of cancer control activities, and planning for future healthcare needs at both the state and national levels. Complete and high-quality cancer reporting traditionally relies primarily on data from acute care hospitals and, more recently, pathology laboratories.  

Advances in medicine and changes in the healthcare delivery system now allow patients to obtain their care outside the acute care hospital setting. Data collection systems from ambulatory healthcare providers such as physician offices and radiation therapy centers are not as standardized or complete with respect to reporting of cancer occurrences and treatment. When reporting does occur, it may be through a manual process of identifying reportable cases and submitting paper copies of the medical record, or the central registry may send certified tumor registrars (CTRs) to ambulatory healthcare provider offices to abstract the information manually or electronically from the paper-based medical records. The [Health Level 7 (HL7) Clinical Document Architecture (CDA®) Release 2 Implementation Guide (IG): Reporting to Public Health Cancer Registries from Ambulatory Healthcare Providers, Release 1, DSTU Release 1.1 – US Realm](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=398) is the first standard for ambulatory care to use when electronically transmitting cancer cases to the central cancer registry. The CDA IG is part of the Office of the National Coordinator (ONC) Meaningful Use and identifies the content and structure for reporting from physician electronic health records (EHRs) to central cancer registries (CCRs), but it does not use HL7 Fast Healthcare Interoperability Resources (FHIR®). These processes are very resource intensive, time-consuming, prone to errors in transcription, and inherently less secure. This leads to under-reporting of certain types of cancers, especially those now diagnosed and treated primarily outside of hospitals, such as in dermatology, urology, and hematology, as well as under-reporting of treatment information across most types of cancer.

Standards specifications provided in this document are designed to facilitate the implementation of an automated electronic process for the identification and reporting of cancer cases, treatment, and outcomes using ambulatory healthcare provider EHR systems to create a cancer event report and submit it to public health central cancer registries. Automated electronic reporting is expected to reduce labor (for the ambulatory healthcare providers and public health central cancer registries), and increase the security, completeness, timeliness and accuracy of cancer surveillance data.


### Legal Mandate for Cancer Reporting 

Cancer reporting from all healthcare providers (e.g., hospital, laboratory and ambulatory) for public health surveillance is mandated at the state and territory level. Legislation requiring cancer reporting by healthcare providers exists in all states with some variation in specific requirements. United States federal law Public Health Service Act (42 USC 280e-280e-4; Public Law 102-515), as amended.), authorizing the National Program of Cancer Registries, specifies that each federally-funded registry must have a legislative "means for the statewide cancer registry to access all records of physicians and surgeons, hospitals, outpatient clinics, nursing homes, and all other facilities…”. The [National Cancer Act of 1971 (Public Law 92-218)](https://www.congress.gov/92/statute/STATUTE-85/STATUTE-85-Pg778-3.pdf) gives the Director of NCI the authority to “collect, analyze, and disseminate all data useful in the prevention, diagnosis and treatment of cancer.”

#### HIPAA:
The Health Insurance Portability and Accountability Act (HIPAA, or the Act), P.L. 104-191, enacted on August 21, 1996, includes provisions related to insurance coverage and a section that is relevant to electronic reporting of healthcare information. The regulation implementing the HIPAA privacy provisions allows public health exemptions for disclosure without patient consent of individually identifiable health information.
A [discussion of HIPAA as it relates to reporting to Cancer Registries](https://www.naaccr.org/?s=HIPAA) outlines details relating to HIPAA and cancer reporting.


### Business Need and User Stories
The section identifies the business needs and specific user stories outlining the central cancer registry reporting data exchange needs.

#### Use Case Goals
The purpose of the use case is to transmit cancer case information to state central cancer registries. The intent is to provide access to data not currently available, or available through non-standard and/or manual methods; it will not replace hospital registry reporting methods that are working well. The cancer use case will help assess how to address the gaps in workflow and triggers, and the ability to leverage MedMorph RA IG along with other existing HL7 FHIR® Implementation Guides to address the public health information needs.

#### Problem Statement
Cancer is a mandatory reportable disease; every state has public health law/regulation requiring information to be reported to a central cancer registry about all cancers diagnosed or treated within that state. Central cancer registries are population-based cancer registries that collect data on all cancer diagnosed in residents in a defined geographic area.  The main sources of information include information from treatment facilities (e.g., hospitals, clinics/physician offices), diagnostic services (e.g., pathology laboratories) and vital statistics (e.g., death certificates). Central cancer registries have an emphasis on epidemiology and public health to determine patterns among various populations, monitor cancer trends over time, guide planning and evaluation of cancer control efforts, help prioritize health resource allocations and to advance clinical, epidemiologic and health services research <sup>1</sup>. Even with reporting requirements, cancer surveillance is complex given the heterogeneous nature of the disease, numerous diagnostic and prognostic factors, and multiple medical encounters that produce data from a variety of non-harmonized data sources.

Challenges include:
* Inability to identify which patient diagnoses and encounters require reporting
* A lack of data in discrete fields (e.g., narrative blob text fields, PDF documents)
* Issues with data flow 
* Delays in data availability 
* Managing proper timing of creating and transmitting reports
* A lack of standardized systems for cancer data collection and reporting (in some cases)


These challenges make it difficult for registries to synthesize information in a timely and actionable way. Automation of cancer case registry reporting will reduce the burden of manual or other non-standardized data collection processes that currently exist.


#### Goals of the Use Case

The goal of the Central Cancer Registry Reporting Content IG is to automate the capture of cancer cases and cancer treatment information not reported by other sources and provide incidence data faster for research and public health. It will leverage the Making Electronic Data More Available for Research and Public Health (MedMorph) Reference Architecture (RA) IG and other existing FHIR® infrastructure to transmit cancer case information primarily from ambulatory care practices to central cancer registries. This Use case will not replace hospital registry reporting methods which are working well.  Additionally, this use case aims to identify data standards that allow for the collection and transmission of these data electronically from EHRs automatically rather than relying on labor-intensive manual processes and duplications of effort.

##### Scope of the Use Case

**In-Scope**

* Collect standardized data on all types of reportable cancers diagnosed and/or treated
* Define under what circumstances an EHR system must create and transmit a cancer report to the central cancer registry
* Identify the data elements to be retrieved from the EHR to produce the cancer report


**Out-of-Scope**

* Validation of the EHR data
* Data captured outside the EHR and communicated directly to registries
* Changes to existing provider workflow or existing data entry
* Policies of the clinical care setting to collect consent for data sharing
* Integrating claims data into the trigger event to send a report to the cancer registries

 
#### **User Story: Cancer Diagnosis and Treatment Reporting based on Specific Criteria** 
A patient visits her primary care provider (PCP) because of a lump in her breast. The provider orders a mammogram and then a biopsy that is sent to the pathology laboratory for testing. The laboratory analyzes the biopsy specimen which indicates the patient has breast cancer. The pathology report is sent to the provider who ordered the biopsy. On January 20, 2022, the provider confirms the diagnosis of breast cancer. This information is integrated into the patient's EHR. The patient is informed of her test results. The PCP clinic's electronic reporting system determines that the patient has been diagnosed with a cancer that meets the criteria for reporting to the central cancer registry, as defined by the national standard Cancer Reportability List. These lists and other reportability criteria are contained in the Health Data Exchange App (HDEA), MedMorph's backend services app. The HDEA handles all the trigger events for exchanging a patient's EHR information across systems and is notified when the encounter is closed. The HDEA creates a standard report with the required data elements and sends it to the central cancer registry in the state where the patient resides, as required by state law. On February 2, 2022, the PCP orders a further workup and clinically stages the patient’s cancer. This information is also included in the patient’s EHR. The HDEA recognizes that this initial staging information does not meet the criteria for reporting because the information has been added within six months of the initial report transmitted to the central cancer registry (i.e., the initial report was sent January 20, 2022, and the staging information was done February 2, 2022). Thus, the staging information is in the EHR, but does not yet trigger the HDEA to report or exchange this information. 

The patient has surgery on February 9, 2022, and the PCP refers her to a medical oncologist in the same clinic for further treatment. The medical oncologist sends the patient to the radiation therapy department to initiate radiation therapy as part of the first course of treatment for her breast cancer. Radiation therapy is given through September 29, 2022 and is documented in the EHR as the reason for the encounter/visit. The HDEA is notified of this update by the patient's EHR and determines that the patient was seen for treatment of a cancer that meets the criteria for reporting to the central cancer registry and is more than six months after the initial diagnosis was transmitted to the central cancer registry. Thus, the HDEA creates a standard report with the required data elements and securely sends it to the central cancer registry in the state where the patient resides, as required by state law.

After radiation was completed on September 29, 2022, the medical oncologist initiates the chemotherapy regimen on October 10, 2022, as part of the first course of treatment for her breast cancer. The chemotherapy drugs are infused, and the chemotherapy treatment is documented in the EHR as the reason for the encounter/visit. The HDEA determines that the patient was seen for treatment of a cancer that meets the criteria for reporting to the central cancer registry; however, it does not meet the criteria for transmitting to the central registry because it has been added to the EHR between 6 months and 12 months of the initial diagnosis and transmission of a cancer report. 
 
After 12 months from the initial diagnosis and transmission of a cancer report to the central cancer registry, the HDEA generates and sends a standard report with essential data elements to the central cancer registry in the state where the patient resides. At every subsequent 12 months after the initial diagnosis and transmission of a cancer report to the central cancer registry, the HDEA generates and sends a standard report with essential data elements to the central cancer registry in the state where the patient resides, until the patient is recorded as deceased or there have been no updates to the patient’s EHR record. These timed exchanges of a patient’s EHR information are triggered by criteria set up in the HDEA and run seamlessly in the background without human intervention, which eases mandatory reporting requirements. 


#### Central Cancer Registry Reporting Workflow 

The following is a diagram of the workflow based on the above user story used for Central Cancer Registry Reporting


{% include img.html img="central-cancer-registry-reporting-workflow.png" caption="Figure 2.1 - Central Cancer Registry Reporting Workflow" %}

<br/>


<br/>


#### Central Cancer Registry Reporting Actors and Definitions

The following actors and definitions from the [MedMorph RA IG]({{site.data.fhir.ver.medmorphIg}}/usecases.html#medmorph-actors-and-definitions) are used by the Central Cancer Registry Reporting use cases. 

* Data Source (e.g., EHR, HIE)
* Health Data Exchange App (HDEA) (MedMorph's backend services app)
* Central Cancer Registry (Data Receiver)
* Knowledge Artifact Repository (KAR)
* Trusted Third Party (TTP)

##### Interactions between MedMorph RA Actors and Systems for Central Cancer Registry Reporting 
This section outlines the high-level interactions between the various MedMorph Actors and Systems listed above. These interactions are shown in Figure 2.2 below along with the descriptions for each step.

{% include img.html img="cancer-actors-and-systems.png" caption="Figure 2.2 - Central Cancer Registry Reporting Actors and Systems" %}

The descriptions for each step in the above diagram include:
* Step 1: A Central Cancer Registry (e.g., Data Receiver ) creates a Knowledge Artifact and makes it available via the Knowledge Artifact Repository.
     * Step 1a: Knowledge Artifact Repositories which implement notifications, can optionally notify the subscribers (EHRs, Backend System App, Administrators) of changes in the Knowledge Artifacts. 
* Step 2: The Health Data Exchange App (HDEA) queries the Knowledge Artifact Repository to retrieve a Knowledge Artifact. 
     * Step 2a: HDEA receives the Knowledge Artifact as a response to the query in Step 2.     
* Step 3: The HDEA processes the Knowledge Artifact and creates subscriptions in the Data Source’s (e.g., EHR) FHIR Server so that it can be notified when specific events occur in clinical workflows.
* Step 4: Providers as part of their clinical workflows update the data in the Data Source’s patient chart.
* Step 5: The Data Source notifies the HDEA based on subscriptions that have been created in Step 3.
* Step 6: The HDEA queries the Data Source for patient’s data.
     * Step 6a: HDEA receives the response from the Data Source with the patient’s data.
* Step 7: The HDEA submits the created report to the TTP. (Central Cancer Registries require Trusted Third Parties (TTPs) to act as intermediaries to receive reports from clinical organizations.) 
     * Step 7a: The TTP receives a submitted report from the HDEA and forwards the report to the Central Cancer Registry.
* Step 8: A Central Cancer Registry requires a TTP to act as an intermediary to submit reports to clinical organizations and submits a response back to the TTP based on the submitted report. The Response transaction can be synchronous or asynchronous (after a period of time).
     * Step 8a: The TTP receives the submitted response from the Central Cancer Registry and forwards the response to the HDEA which is part of the healthcare organization.
* Step 9: The HDEA writes back the response from the Central Cancer Registry to the Data Source as appropriate. Note: The Response may have to be re-identified in some scenarios using Trust Services before it is written back to the EHR.
 
- - - -


<sup>1</sup>  Menck, H., Gress, D. and Griffin, A., 2011. Cancer Registry Management Principles and Practices for Hospitals and Central Registries. 3rd ed. Dubuque, IA: Kendall Hunt.  ISBN: 978-0-7575-6900-5.
