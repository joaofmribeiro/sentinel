
Symantec BlueCoat Proxy solution in Sentinel Content Hub expects logs being ingested as SYSLOG format into Log Analytics workspace. However, if you area already sending more data as CEF formatted logs and want to keep using the same log forwarder and ingest data via data connector AMA via CEF logs, then this custom parser which you can save as function might work for you. 

Solution in content hub, expecting syslog: 

![image](https://github.com/user-attachments/assets/09ec03c0-fd07-4251-a38e-9d756c952d71)

Parser defined in this solution (syslog):

let forwarder_host_names = dynamic(["datasource"]);
let datasource = union isfuzzy=true  (datatable(Source: string)[]), (_GetWatchlist('ASimSourceType') | where SearchKey == 'SymantecProxySG' | project Source);
Syslog
| where CollectorHostName in (forwarder_host_names) or Computer in (forwarder_host_names) or CollectorHostName in (datasource) or Computer in (datasource)
| where Facility == "local0"
| parse SyslogMessage with logTime:datetime " " time_taken:long " " c_ip:string " " cs_userdn:string " " cs_auth_groups:string " " exception_id " " sc_filter_result:string ' "' cs_categories:string '" "' cs_referrer:string '" ' sc_status:string " " s_action:string " " cs_method:string ' "' content_type:string '" ' cs_uri_scheme:string " " cs_host:string " " cs_uri_port:string " " cs_uri_path:string " " cs_uri_query:string " " cs_uri_extension:string ' '  Part2:string
| extend cs_categories = split(cs_categories,";") 
| extend content_type = split(replace(@"%20",@'',tostring(content_type)),";")
| parse Part2 with '"' UserAgent '" ' Part3
| extend cs_user_agent = iff(Part2 startswith "-", "-", UserAgent),
     Part3 = iff(Part2 startswith "-", substring(Part2,2), Part3)
| parse Part3 with s_ip:string " " sent_bytes:long " " received_bytes:long " " virus_id:string  ' "' app_name:string  '" "' app_operation:string '" ' src_port:string ' "' country:string '" ' cs_threat_risk:string "#015"
| project-away Part2, Part3, UserAgent


Then both analytic rules need to be updated to support the CEF formatted logs:
- User Accessed Suspicious URL Categories
- Excessive Denied Proxy
--> Updated versions of these Analytic Rules via CEF Parser: https://github.com/joaofmribeiro/sentinel/tree/main/analytic%20rules

Parser KQL via CEF within this current folder "Symantec Blye Coat (CEF).yaml

Sure these can be maybe updated or edited to fill the needs, however can be a good start :)

