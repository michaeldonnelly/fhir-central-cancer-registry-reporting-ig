### Introduction

This profile is used to represent the PlanDefinition instance which is an integral part of the Central Cancer Registry Reporting Knowledge Artifact.

#### Requirements of the Knowledge Artifact

* The Central Cancer Registry Reporting PlanDefinition is triggered by an encounter-close event.

* The PlanDefinition specifies a mechanism to run scheduled jobs at specified intervals when the reason for the encounter/visit is to diagnose, evaluate, and/or treat an active cancer and create a cancer report.

	* Encounter of ICD-10-CM or SNOMED CT Reportable Codes
	
* The PlanDefinition specifies a mechanism to run scheduled jobs at least every 6 months for the patient and create a cancer report.

* The PlanDefinition specifies a mechanism to run scheduled jobs once every 12 months until the patient is deceased or there is no updates to the record for 24 months and create a cancer report.
