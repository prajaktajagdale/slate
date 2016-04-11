---
title: Intuit Data Protection System 3

search: true
---

# Intuit Data Protection System 3
> ### Consumes  
> `application/json`  

> ### Produces
> `application/json`




# Models
## ApplianceDescription
```json
{
    "comments": "string",
    "image_id": "string",
    "instance_id": "string",
    "instance_ip": "string",
    "project_name": "string",
    "public_hostname": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
comments | string | textual comments
image_id | string | appliance image id
instance_id<b title="required">&nbsp;*&nbsp;</b> | string | Cloud-specific instance ID
instance_ip | string | appliance IP address
project_name | string | project name
public_hostname<b title="required">&nbsp;*&nbsp;</b> | string | appliance DNS name

	
## ApplianceList
```json
{
    "instances": [
        {
            "comments": "string",
            "image_id": "string",
            "instance_id": "string",
            "instance_ip": "string",
            "project_name": "string",
            "public_hostname": "string"
        }
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
instances<b title="required">&nbsp;*&nbsp;</b> | array[[ApplianceDescription](#appliancedescription)] | 

	
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

	
## ApplianceTime
```json
{
    "time": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
time<b title="required">&nbsp;*&nbsp;</b> | integer | Unix time, seconds since the epoch

	
## CaCertificate
```json
{
    "ca-cert": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
ca-cert<b title="required">&nbsp;*&nbsp;</b> | string | Project CA certificate in PEM format

	
## DerivedItem
```json
{
    "item": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
item | string | A hex-encoded representation of the derived data.

	
## GetRestrictedKeyByPolicyInput
```json
{
    "identity_document": "string",
    "identity_document_signature": "string",
    "instance_id": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
identity_document | string | AWS provided identity document in JSON format
identity_document_signature | string | base64 encoded signature of the identity document
instance_id | string | cloud instance id

	
## GetRestrictedKeyInput
```json
{
    "instance_id": "string",
    "instance_region": "string",
    "requested_version": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
instance_id<b title="required">&nbsp;*&nbsp;</b> | string | cloud instance id
instance_region | string | cloud region
requested_version | string | requested API key version

	
## GetTempCredsInput
```json
{
    "api_signature": "string",
    "instance_id": "string",
    "instance_region": "string",
    "nonce": "string",
    "time": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
api_signature<b title="required">&nbsp;*&nbsp;</b> | string | api key user signature
instance_id | string | cloud instance id
instance_region | string | cloud region
nonce<b title="required">&nbsp;*&nbsp;</b> | string | random lowercase hex string of 16 bytes
time<b title="required">&nbsp;*&nbsp;</b> | integer | appliance Unix timestamp

	
## ItemInList
```json
{
    "name": "string",
    "type": "string"
}
```

Returned in response to a list item operation. 
The ItemInList object describes an item that is returned as part of an item list.
The description includes the name of the item and its type.

	
### Fields
Name | Type | Description
--- | --- | ---
name | string | The name of the item, optionally
type | string | Type of the returned item, one of secret, key, or folder

	
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

The IDPS API enables clients to retrieve a list of all items. The ItemListResponse object contains such a list of items
returned in a paginated form.

	
### Fields
Name | Type | Description
--- | --- | ---
list | array[[ItemInList](#iteminlist)] | Returned list of items
next | integer | The Next field acts as an index into the paginated response and is an indicator of the current page number. The field is omitted for the last page in the response as an indicator that there are no more elements to list.

	
## ItemRequest
```json
{
    "cache_ttl": "integer",
    "is_enumerable": "boolean",
    "is_versioned": "boolean",
    "item": "string",
    "metadata": "string"
}
```

The ItemRequest object represents all the configurable parameters that can be specified by a client during generation of a new item or storage of an existing item. 
Through ItemRequest, a client can dictate if an item can be cached or whether it&#039;s hidden. 
Clients can also indicate whether mulitple versions of the item need to be managed by IDPS, a feature directed at simplifying key rotation. In addition to storage and 
retrieval of specific versions, IDPS also provides the ability to invoke operations like encrypt and decrypt with specific versions of an item. 
For items derived from a versioned item, changes to the version are propagated transparently to the derived items upon their subsequent retrieval.
Clients also have the option of attaching metadata with each item and its versions.

	
### Fields
Name | Type | Description
--- | --- | ---
cache_ttl | integer | Cache time-to-live in seconds for which the item can be cached by the VA. Caching can be disabled by specifying CacheTtl=0. 
is_enumerable | boolean | An IsEnumerable value of false prevents an item from appearing in item list. Such an item continues to remain directly accessible through a GET request. To make an item in a list visible, set IsEnumerable to true.
is_versioned | boolean | IDPS supports versioning of items as a means to simplify key rotation. An IsVersioned value of true results in a new version of the item being created for each update to the item. 
item | string | Item to store in the IDPS. For item type of secret, the value is a string. For item type of key, the value is a hex-encoded string.
metadata<b title="required">&nbsp;*&nbsp;</b> | string | User-supplied metadata string

	
## ItemResponse
```json
{
    "algorithm": "string",
    "cache_ttl": "integer",
    "is_enumerable": "boolean",
    "is_exportable": "boolean",
    "is_versioned": "boolean",
    "item": "string",
    "last_modified": "string",
    "metadata": "string",
    "name": "string",
    "public_key": "string",
    "type": "string",
    "version": "integer"
}
```

The IDPS API allows clients to retrieve details of the stored items including secrets and keys. When requested, these
details are returned in the ItemResponse object.

	
### Fields
Name | Type | Description
--- | --- | ---
algorithm | string | The encryption algorithm used in the creation of the item. For item type key, one of: AES128, AES256, RSA1024, RSA2048, AES128ECB, AES256ECB, AES128SIV, or AES256SIV
cache_ttl | integer | Items can be configured to be cacheable. The cache time-to-live indicates the time in seconds for which the item can remain cached. A time to live value of 0 prohibits caching.
is_enumerable | boolean | An IsEnumerable value of false prevents an item from appearing in item list. Such an item continues to remain directly accessible through a GET request. A value of true makes the item visible in a list. 
is_exportable | boolean | When set to true, Indicates that a key&#039;s value can be obtained by GET request. Non-exportable keys are used for remote data encryption/decryption
is_versioned | boolean | IDPS supports versioning of items to simplify key rotation. An IsVersioned value of true indicates that the secret or key can have multiple versions
item | string | Value of the item, as retrieved from the database. Value of an item of type secret: string. Value of an item of type key: hex-encoded string. 
last_modified | string | Timestamp of last modification to the item
metadata | string | User defined metadata as printable string
name | string | Name of the item, optionally, including its path with &quot;/&quot; separators, e.g., a/b/c
public_key | string | Indicates the public key For items generated using the RSA asymmetric algorithm. The public key is always returned irrespective of the IsEnumerable and IsExportable values. 
type | string | Type of the returned item, one of: secret, key, or folder
version | integer | For a versioned item, the field indicates the latest or requested version number. For a non-versioned item, the value will always be 1. min: 1. 

	
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
next | integer | The Next field acts as an index into the paginated response and is an indicator of the current page number.The field is omitted for the last page in the response as an indicator that there are no more elements to list.

	
## PolicyRestrictedApiKey
```json
{
    "api_key_id": "string",
    "api_secret_key": "string",
    "expires_after": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
api_key_id<b title="required">&nbsp;*&nbsp;</b> | string | API key id
api_secret_key<b title="required">&nbsp;*&nbsp;</b> | string | API secret key
expires_after | integer | time to expiration, in seconds

	
## ProjectDescription
```json
{
    "project_description": "string",
    "project_name": "string",
    "project_serial": "string",
    "public_hostname": "string",
    "vpc_id": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
project_description | string | long description assigned by user
project_name | string | project name
project_serial<b title="required">&nbsp;*&nbsp;</b> | string | project serial identifier
public_hostname | string | lead appliance DNS name
vpc_id | string | VPC id of the project&#039;s appliances, if specified

	
## ProjectList
```json
{
    "projects": [
        {
            "project_description": "string",
            "project_name": "string",
            "project_serial": "string",
            "public_hostname": "string",
            "vpc_id": "string"
        }
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
projects<b title="required">&nbsp;*&nbsp;</b> | array[[ProjectDescription](#projectdescription)] | 

	
## RandomData
```json
{
    "random": "string"
}
```

Random Data

	
### Fields
Name | Type | Description
--- | --- | ---
random<b title="required">&nbsp;*&nbsp;</b> | string | Returns exactly 256 random bytes, suitable for use in cryptographic operations. The bytes are returned encoded to a base64 string

	
## RestrictedApiKey
```json
{
    "api_key_id": "string",
    "api_secret_key": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
api_key_id<b title="required">&nbsp;*&nbsp;</b> | string | API key id
api_secret_key<b title="required">&nbsp;*&nbsp;</b> | string | API secret key

	
## TempCreds
```json
{
    "credential": "string",
    "expiry": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
credential<b title="required">&nbsp;*&nbsp;</b> | string | base64 encoded temporary credential
expiry<b title="required">&nbsp;*&nbsp;</b> | integer | time to expiration, in seconds

	
