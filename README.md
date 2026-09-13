# UKG-MMR-Report
For Jupyter Notebooks containing code to work in conjunction with UKG APIs to find MMR users

PLEASE NOTE THAT NOTEBOOKS IN THIS REPOSITORY DO NOT INCLUDE OUTPUTS TO PROTECT PII

First, create a Hyperfind in UKG that meets the conditions: Primary job matches the highest node in Business Structure, as of today (include all jobs from locations below) AND Employee employed and working as of today AND Include only Managers

UKG APIs used: Retrieve Hyperfind profiles GET {tenantURL}/api/v1/commons/hyperfind_profiles Locate the ID of the Hyperfind that was created to find Managers - it will need to be used in the next API call

Execute Hyperfind Query POST {tenantURL}/api/v1/commons/hyperfind/execute In Body of API call: { "dateRange":{ "startDate": start date of Hyperfind range, "endDate": end date of Hyperfind range }, "hyperfind": { "id": ID obtained for Hyperfind in last API call }, "threshold": 35000 }

Use the information obtained from this API to retrieve the IDs of the managers that will be run in the next API call to find the roles assigned to the manager Process information obtained from this API (JSON) in the Jupyter Notebook "PROD MMR Execute Hyperfind Query" The notebook's final cell should give you all the IDs that you will need to put in the body of the next API call in the appropriate format.

Retrieve Manager Role Assignments POST {tenantURL}/api/v1/commons/persons/manager_role_assignments/multi_read In Body of API call: { "where": { "employees" { "key": "personnumber", "values": [ENTER ALL IDS RETRIEVED FROM FINAL CELL IN JUPYTER NOTEBOOK] } } }

Use the response received from the last API call in the Jupyter Notebook "UKG MMR Pull". The final cell should give you the user IDs of the managers that have more than one Manager Role in UKG.
