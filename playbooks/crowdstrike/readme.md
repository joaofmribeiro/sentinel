
**Playbook: CrowdStrikeAlertAPI-Pull AlertEntities**

Logic App Flow:
- Acquire access token to CrowdStrike API;
- Get Alert ID's from CrowdStrike Alert API;
- Pear each Alert ID get all alert entities via CrowdStrike AlertEntities API.
- Write to a custom table in Log Analytics (short version of entities) and write into Events Hub for ADX integration for a full entities version.


![image](https://github.com/user-attachments/assets/f795e8ed-6a50-4e41-9bcc-50e99fe261ce)




  Logic App must be subject to modifications / change of scope if required to fit your needs.

**Table Structure:**

  $tableParams = @'
{
    "properties": {
        "schema": {
            "name": "CrowdstrikeAlertEntities_CL",
            "columns": [
								
				{
					"name":"Confidence",
					"type":"string"
				},
				{
					"name":"Description",
					"type":"string"
				},
				{
					"name":"Display_name",
					"type":"string"
				},
				{
					"name":"Name",
					"type":"string"
				},
				{
					"name":"Product",
					"type":"string"
				},
				{
					"name":"AlertSeverity",
					"type":"int"
				},
				{
					"name":"Source_account_domain",
					"type":"string"
				},
				{
					"name":"Source_account_name",
					"type":"string"
				},
				{
					"name":"Source_endpoint_host_name",
					"type":"string"
				},
				{
					"name":"Tactic",
					"type":"string"
				},
				{
					"name":"Technique",
					"type":"string"
				},
				{
					"name":"TimeGenerated",
					"type":"datetime"
				},
				{
					"name":"Status",
					"type":"string"
				},
				{
					"name":"Source_endpoint_ip_address",
					"type":"string"
				},
				{
					"name":"Target_account_name",
					"type":"string"
				},
				{
					"name":"Target_endpoint_host_name",
					"type":"string"
				},
				{
					"name":"Cmdline",
					"type":"string"
				},
				{
					"name":"Device_id",
					"type":"string"
				},
				{
					"name":"Hostname",
					"type":"string"
				},
				{
					"name":"Local_ip",
					"type":"string"
				},
				{
					"name":"OS_version",
					"type":"string"
				},
				{
					"name":"Filename",
					"type":"string"
				},
				{
					"name":"Filepath",
					"type":"string"
				},
				{
					"name":"Global_prevalence",
					"type":"string"
				},
				{
					"name":"Md5",
					"type":"string"
				},
				{
					"name":"Sha256",
					"type":"string"
				},
				{
					"name":"Indicator_id",
					"type":"string"
				},
				{
					"name":"Local_prevalence",
					"type":"string"
				},
				{
					"name":"Logon_domain",
					"type":"string"
				},
				{
					"name":"Falcon_host_link",
					"type":"string"
				}
            ]
        }
    }
}

