---
title: Intuit Data Protection System 3

search: true
---

# Intuit Data Protection System 3
> ### Consumes  
> `application/json`  

> ### Produces
> `application/json`



## Get appliance status

```http
GET /v3/appliance/status HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "ca_cert_exists": "boolean",
    "cloud": "string",
    "cloud_creds": "boolean",
    "instance_id": "string",
    "local_config_exists": "boolean",
    "master_key_exists": "boolean",
    "max_api_version": "integer",
    "min_api_version": "integer",
    "project_serial": "string",
    "pvkm_address": "string",
    "pvkm_address_is_set": "boolean",
    "pvkm_reachable": "boolean",
    "region": "string",
    "time_in_sync": "boolean",
    "time_skew": "integer",
    "version": "string",
    "vkm_credentials_accessible": "boolean"
}
```

### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[ApplianceStatus](#appliancestatus)</td><td>Appliance Status</td></tr> 
</table>


# Models
## ApplianceStatus
```json
{
    "ca_cert_exists": "boolean",
    "cloud": "string",
    "cloud_creds": "boolean",
    "instance_id": "string",
    "local_config_exists": "boolean",
    "master_key_exists": "boolean",
    "max_api_version": "integer",
    "min_api_version": "integer",
    "project_serial": "string",
    "pvkm_address": "string",
    "pvkm_address_is_set": "boolean",
    "pvkm_reachable": "boolean",
    "region": "string",
    "time_in_sync": "boolean",
    "time_skew": "integer",
    "version": "string",
    "vkm_credentials_accessible": "boolean"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
ca_cert_exists | boolean | a CA certificate has been entered into the appliance
cloud<b title="required">&nbsp;*&nbsp;</b> | string | cloud provider
cloud_creds | boolean | cloud credentials have been entered for the project
instance_id<b title="required">&nbsp;*&nbsp;</b> | string | cloud machine instance id
local_config_exists<b title="required">&nbsp;*&nbsp;</b> | boolean | the appliance has been configured
master_key_exists<b title="required">&nbsp;*&nbsp;</b> | boolean | the master key has been entered into the appliance
max_api_version | integer | maximum api version supported by the appliance
min_api_version | integer | minimum api version supported by the appliance
project_serial | string | serial identifier of the project this instance belongs to (requires authentication)
pvkm_address<b title="required">&nbsp;*&nbsp;</b> | string | address of the PVKM that manages this appliance
pvkm_address_is_set | boolean | the pvkm_address has been set
pvkm_reachable<b title="required">&nbsp;*&nbsp;</b> | boolean | the appliance is able to connect to the PVKM
region | string | cloud region
time_in_sync<b title="required">&nbsp;*&nbsp;</b> | boolean | time on the appliance is in sync with the PVKM
time_skew | integer | time skew in seconds between the appliance and the PVKM
version<b title="required">&nbsp;*&nbsp;</b> | string | appliance software version
vkm_credentials_accessible | boolean | IDPS credentials are accessible at VKM

	
