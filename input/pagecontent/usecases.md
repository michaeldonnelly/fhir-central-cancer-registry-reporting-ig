### Business Need and User Stories
The section identifies the business needs and specific user stories outlining the central cancer registry reporting data exchange needs.

#### Use Case Goals
The purpose of the use case is to transmit cancer case information to state Central Cancer Registries. The intent is to provide access to data not currently available, or available through non-standard and/or manual methods; it will not replace hospital registry reporting methods that are working well. The cancer use case will help assess how to address the gaps in workflow and triggers, and the ability to leverage MedMorph RA IG along with other existing HL7 FHIR Implementation Guides to address the public health information needs.

#### Problem Statement
Cancer is a mandatory reportable disease; every state has public health law/regulation requiring information to be reported to a central cancer registry about all cancers diagnosed or treated within that state. Central cancer registries are population-based cancer registries that collect data on all cancer cases in a defined population.  The main sources of information include information from treatment facilities (e.g., hospitals, clinics/physician offices), diagnostic services (e.g., pathology laboratories) and vital statistics (e.g., death certificates). Central cancer registries have an emphasis on epidemiology and public health to determine patterns among various populations, monitor cancer trends over time, guide planning and evaluation of cancer control efforts, help prioritize health resource allocations and to advance clinical, epidemiologic and health services research.[1]  Even with reporting requirements, cancer surveillance is complex given the heterogeneous nature of the disease, numerous diagnostic and prognostic factors, and multiple medical encounters that produce data from a variety of non-harmonized data sources.

Challenges include:
* Issues with data flow (Need to identify more specifics)
* Delays in data availability (Need to identify existing timeliness and impact of delays)
* A lack of standardized systems for cancer data collection and reporting (in some cases) --- What about existing CDA approaches ? 


These challenges make it difficult for registries to synthesize information in a timely and actionable way.

In Central Cancer Registry Reporting Content IG, MedMorph RA IG and other existing FHIR infrastructure is leveraged to transmit cancer case information primarily from ambulatory care practices to state cancer registries. The intent is to automate and provide access to data not currently available to public health and research. This will not replace hospital registry reporting methods which are working well. Automation of cancer case registry reporting will reduce the burden of manual or other non-standardized data collection processes that currently exist.

#### Goals of the Use Case
The goal of this use case is to capture cases of cancer and cancer treatment information not reported by other sources and provide incidence data faster for research and public health. Additionally, this use case aims to identify data standards that allow for the collection, transmission, and aggregation of these data electronically from EHRs automatically rather than relying on labor-intensive manual processes and duplications of effort.

##### Scope of the Use Case

**In-Scope**

* Collect standardized data on all types of reportable cancers diagnosed and/or treated
* Define under what circumstances an EHR system must create and transmit a cancer report to the central cancer registry
* Identify the data elements to be retrieved from the EHR to produce the cancer report
* Use NAACCR Volume II data dictionary for standardized data collection
* Include data collection along the longitudinal spectrum (Diagnosis -> Staging -> Initial Treatment -> Death)

**Out-of-Scope**

* Validation of the EHR data
* Data captured outside the EHR and communicated directly to registries
* Changes to existing provider workflow or existing data entry
* Policies of the clinical care setting to collect consent for data sharing
* Integrating claims data into the trigger event to send a report to the cancer registries

 
#### **User Story #1: Cancer Diagnosis and Treatment Reporting based on Specific Criteria** 
A patient visits her primary care provider (PCP) because of a lump in her breast. The provider orders a mammogram and then a biopsy that is sent to the pathology laboratory for testing. The laboratory analyzes the biopsy specimen which indicates the patient has breast cancer. The pathology report is sent to the provider who ordered the biopsy. The provider confirms the diagnosis of breast cancer. This information is integrated into the patient's clinical record. The patient is informed of her test results. The PCP’s clinic EHR system determines that the patient has been diagnosed with a cancer that meets the criteria for reporting to the central cancer registry, as defined by the national standard Cancer Reportability List. A standard report with the required data elements is sent to the central cancer registry where the patient resides, as required by state law. The PCP orders a further workup and clinically stages the patient’s cancer. The EHR system determines that staging information has not been previously submitted to the central cancer registry and meets the criteria for reporting. A standard report with the required data elements is sent to the central cancer registry where the patient resides, as required by state law.

The patient has surgery (not covered in this user story) and then PCP refers her to a medical oncologist in the same clinic for further treatment. The medical oncologist sends the patient to the radiation therapy department to initiate radiation therapy as part of the first course of treatment for her breast cancer. Radiation therapy is given and is documented in the EHR as the reason for the encounter/visit. The EHR system determines that the patient was seen for treatment of a cancer that meets the criteria for reporting to the central cancer registry and that this patient has not previously received this category* of treatment. A standard report with the required data elements is sent to the central cancer registry where the patient resides, as required by state law. As directed by the treatment plan, the patient returns to the cancer treatment center to receive the next radiation treatment session. Radiation is given and is documented in the EHR as the reason for the encounter/visit. The EHR system determines that this patient has received this category(NOTE 1) of treatment and a report was already sent to the registry based on this category. Therefore, it does not generate a new report to send to the cancer registry.

After radiation, the medical oncologist initiates the chemotherapy regimen as part of the first course of treatment for her breast cancer. The chemotherapy drugs are infused, and the chemotherapy treatment is documented in the EHR as the reason for the encounter/visit. The EHR system determines that the patient was seen for treatment of a cancer that meets the criteria for reporting to the central cancer registry and that this patient has not previously received this category of treatment. A standard report with the required data elements is sent to the central cancer registry where the patient resides, as required by state law. As directed by the treatment plan, the patient returns to the cancer treatment center to receive the next chemotherapy cycle. The intravenous chemotherapy drugs are infused, and the chemotherapy treatment is documented in the EHR as the reason for the encounter/visit. The EHR system determines that this patient has received this category of treatment and a report was already sent to the registry based on this category. Therefore, it does not generate a new report to send to the cancer registry.
 
The medical oncologist prescribes hormone therapy for the patient, which is documented in the EHR. The EHR system determines that the patient was prescribed a treatment that meets the criteria for reporting to the central cancer registry and that this patient has not previously received this category of treatment. A standard report with the required data elements is sent to the central cancer registry where the patient resides, as required by state law. As directed by the treatment plan, the patient gets prescribed the next dose of hormone therapy. The prescription is documented in the EHR. The EHR system determines that this patient has received this category of treatment and a report was already sent to the registry based on this category. Therefore, it does not generate a new report to send to the cancer registry.

After a certain period of time from a specified starting point (to be determined by the cancer registry), the EHR generates and sends a standard report with data elements (to be identified) to the central cancer registry where the patient resides.

**NOTE 1** Category of treatment: Cancer-directed Procedures, Radiation, Chemotherapy, Hormone Therapy, Immunotherapy (Biological Response Modifier (BRM)), Refusal for Treatment, Watchful Waiting, Other cancer-directed therapy. (Note: These can all be provided in one or more value sets).
 

#### Central Cancer Registry Reporting Workflow 

The following is a diagram of the workflow based on the above user story used for Central Cancer Registry Reporting


{% include img.html img="central-cancer-registry-reporting-workflow.png" caption="Figure 2.1 - Central Cancer Registry Reporting Workflow" %}

<br/>


<br/>


#### MedMorph Central Cancer Registry Reporting Actors and Definitions

The following actors and definitions from the [MedMorph RA IG]({{site.data.fhir.ver.medmorphIg}}/usecases.html#medmorph-actors-and-definitions) are used by the Central Cancer Registry Reporting use cases. 

* EHR 
* Backend Service App (BSA)
* Central Cancer Registry (PHA)
* Knowledge Artifact Repository (KAR)
* Trusted Third Party (TTP)
