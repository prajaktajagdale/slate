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

	
## ItemInList
```json
{
    "name": "string",
    "type": "string"
}
```

The description includes the name of the item and its type.

	
### Fields
Name | Type | Description
--- | --- | ---
name | string | The name of the item, optionally, including the path with &quot;/&quot; separators, e.g., a/b/c
type | string | Type of the returned item, one of: secret, key, or folder

	
## ItemVersion
```json
{
    "version_create_date": "string",
    "version_number": "integer"
}
```

IDPS offers clients with an option to version items as a means to simplify key rotation. 
The ItemVersion field associated with every versioned item indicates a version number and the date of its creation. 
The IDPS API supports listing of all versions of an item and requesting or deleting a specific version of an item. 
Operations like encrypt and decrypt can be invoked with an explicit key version. 

	
### Fields
Name | Type | Description
--- | --- | ---
version_create_date | string | Date the version was created
version_number | integer | Indicates the version number of the item

	
## ItemListResponse
```json
{
    "list": [
        {
            "name": "string",
            "type": "string"
        }
    ],
    "next": "integer"
}
```

IDPS clients are provided with an ability to retrieve a list of all items. The ItemListResponse object contains such a list of items
returned in a paginated form.

	
### Fields
Name | Type | Description
--- | --- | ---
list | array[The ItemInList object describes an item that is returned as part of an item list.] | Returned list of items
next | integer | The Next field acts as an index into the paginated response and is an indicator of the current page number.
The field is omitted for the last page in the response as an indicator that there are no more elements to list.

	
## ItemVersionsListResponse
```json
{
    "list": [
        {
            "version_create_date": "string",
            "version_number": "integer"
        }
    ],
    "next": "integer"
}
```

The IDPS API offers clients the ability to list all available versions for a versioned key. The ItemVersionListResponse object 
contains a list of ItemVersion fields returned as paginated response. 

	
### Fields
Name | Type | Description
--- | --- | ---
list | array[[ItemVersion](#itemversion)] | Returned list of versions
next | integer | The Next field acts as an index into the paginated response and is an indicator of the current page number.
The field is omitted for the last page in the response as an indicator that there are no more elements to list.

	
