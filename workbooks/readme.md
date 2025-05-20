Workbook that leverages the following tables:
- DeviceTvmSecureConfigurationAssessment; 
- DeviceEvents (ingested via Defender XDR Data Connector) in Sentinel;


Data from TVMSecureConfigurationAssessment is obtained via KQL Query from Logic APP and then written into a custom table within log analytics workspace from Sentinel. 

![image](https://github.com/user-attachments/assets/24435280-4319-4c58-b22b-d25ea1f11b1d)




![image](https://github.com/user-attachments/assets/6a932950-0f10-4045-9316-0ee6b8607259)



**Workbook screenshots:**

Workbook allows to select from pie chart signature versions or withib the table in dropdown option, to select as well multiple signature versions to get full picture report. It allows to export table data as well.

![image](https://github.com/user-attachments/assets/4cae3dfe-e3f5-472d-a1d1-13388f298b7d)


![image](https://github.com/user-attachments/assets/afa752de-1521-45c9-9e6a-d16a1d1167a6)


![image](https://github.com/user-attachments/assets/c54d978d-5320-453c-ab78-32a807c2c08b)



Custom table is required for **DeviceTvmSecureConfigurationAssessment**.
**Schemma below:**
	
	$tableParams = @'
	{
	"properties": {
	    "schema": {
	        "name": "DeviceTvmSecureConfigurationAssessment_CL",
	        "columns": [
	            {
	                "name": "DeviceId",
	                "type": "string",
	                "description": "Unique identifier for the device in the service"
	            },
	            {
	                "name": "DeviceName",
	                "type": "string",
	                "description": "Fully qualified domain name (FQDN) of the device"
	            },
	            {
	                "name": "OSPlatform",
	                "type": "string",
	                "description": "Platform of the operating system running on the device. Indicates specific operating systems, including variations within the same family, such as Windows 11, Windows 10, and Windows 7."
	            },
	            {
	                "name": "TimeGenerated",
	                "type": "datetime",
	                "isDefaultDisplay": true,
	                "description": "The timestamp (UTC) reflecting the time in which the event was generated."
	            },
	            {
	                "name": "ConfigurationId",
	                "type": "string",
	                "description": "Unique identifier for a specific configuration"
	            },
	            {
	                "name": "ConfigurationCategory",
	                "type": "string",
	                "description": "Category or grouping to which the configuration belongs: Application, OS, Network, Accounts, Security controls"
	            },
	            {
	                "name": "ConfigurationSubcategory",
	                "type": "string",
	                "description": "Subcategory or subgrouping to which the configuration belongs. In many cases, string describes specific capabilities or features."
	            },
	            {
	                "name": "ConfigurationImpact",
	                "type": "string",
	                "description": "Rated impact of the configuration to the overall configuration score (1-10)"
	            },
	            {
	                "name": "IsCompliant",
	                "type": "string",
	                "description": "Indicates whether the configuration or policy is properly configured"
	            },
	            {
	                "name": "IsApplicable",
	                "type": "string",
	                "description": "Indicates whether the configuration or policy applies to the device"
	            },
	            {
	                "name": "Context",
	                "type": "string",
	                "description": "Additional contextual information about the configuration or policy"
	            },
	            {
	                "name": "IsExpectedUseImpact",
	                "type": "string",
	                "description": "Indicates whether there will be user impact if the configuration or policy is applied"
	            },
				{
	                "name": "AVSigVerion",
	                "type": "string",
	                "description": "Indicates AV signature update version"
	            },
				{
	                "name": "AVEngineVersion",
	                "type": "string",
	                "description": "Indicates AV engine version"
	            },
				{
	                "name": "AVSigLastUpdateTime",
	                "type": "string",
	                "description": "Indicates last signature update time"
	            },
				{
	                "name": "AVProductVersion",
	                "type": "string",
	                "description": "Indicates AV Product version"
	            },
				{
	                "name": "AVMode",
	                "type": "string",
	                "description": "Indicates whether AV is active or passive mode"
	            }
	        ]
	    }
	}
	'@
