---
title: Intuit Data Protection System 3

search: true
---

# Intuit Data Protection System 3
> ### Consumes  
> `application/json`  

> ### Produces
> `application/json`



## Get Open API JSON specification

```http
GET /v3/appliance/open-api-schema HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "object"
}
```


## Get random data

```http
GET /v3/appliance/random HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "random": "string"
}
```

### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[RandomData](#randomdata)</td><td>Random Data</td></tr> 
</table>

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
<tr><td>200</td><td>[ApplianceStatus](#appliancestatus)</td><td>Appliance status. See https://wiki.intuit.com/display/IISKM/Monitoring+the+IDPS+Agent</td></tr> 
</table>

## Get appliance time

```http
GET /v3/appliance/time HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "time": "integer"
}
```

### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[ApplianceTime](#appliancetime)</td><td>Appliance Unix Timestamp</td></tr> 
</table>

## Delete restricted api key

```http
DELETE /v3/credentials/{apiKey} HTTP/1.1
```
```http
HTTP/1.1 204 No Content
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
apiKey<b title="required">&nbsp;*&nbsp;</b> | path | string | 
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>204</td><td>no content</td><td>Restricted API key has been deleted.</td></tr> 
</table>

## Get temporary credentials

```http
POST /v3/credentials/{apiKey}?op=get-credentials HTTP/1.1
Content-Type: application/json

{
    "Input": {
        "api_signature": "string",
        "instance_id": "string",
        "instance_region": "string",
        "nonce": "string",
        "time": "integer"
    }
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "credential": "string",
    "expiry": "integer"
}
```

See https://wiki.intuit.com/display/IISKM/API+Authentication+Using+Java


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
apiKey<b title="required">&nbsp;*&nbsp;</b> | path | string | 
Input | body | [GetTempCredsInput](#gettempcredsinput) | 
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[TempCreds](#tempcreds)</td><td>Temporary Credentials</td></tr> 
</table>

## Generate instance-restricted api key

```http
POST /v3/credentials?op=get-restricted-key HTTP/1.1
Content-Type: application/json

{
    "Input": {
        "instance_id": "string",
        "instance_region": "string",
        "requested_version": "string"
    }
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "api_key_id": "string",
    "api_secret_key": "string"
}
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
Input | body | [GetRestrictedKeyInput](#getrestrictedkeyinput) | 
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>201</td><td>[RestrictedApiKey](#restrictedapikey)</td><td>Restricted API Key</td></tr> 
</table>

## Generate instance-restricted api key by policy

```http
POST /v3/credentials?op=get-restricted-key-by-policy&amp;policy_id={policyId} HTTP/1.1
Content-Type: application/json

{
    "Input": {
        "identity_document": "string",
        "identity_document_signature": "string",
        "instance_id": "string"
    }
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "api_key_id": "string",
    "api_secret_key": "string",
    "expires_after": "integer"
}
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
policyId<b title="required">&nbsp;*&nbsp;</b> | path | string | api key access policy id
Input | body | [GetRestrictedKeyByPolicyInput](#getrestrictedkeybypolicyinput) | 
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>201</td><td>[PolicyRestrictedApiKey](#policyrestrictedapikey)</td><td>Restricted API Key</td></tr> 
</table>

## Delete an item

```http
DELETE /v3/items/{name} HTTP/1.1
```

Use the call to delete items of any type from the database.
In the absence of the version parameter, all versions of a secret or key are deleted.
By default, folders are only deleted if empty. 
If the force parameter is set to true, a folder is deleted with any contained items, provided it does not contain sub-folders.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
version | query | integer | Version of the item that acts as the input keying material for the HKDF. If not given or version=0, the latest version will be used.
force | query | boolean | When true, the boolean parameter forces removal of non-empty folders. It, however, will not remove any folder with sub-folders.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
</table>
## Get an item

```http
GET /v3/items/{name} HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

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
```http
HTTP/1.1 default 
```

Use the call to retrieve an item - either a key, a secret or a folder.
Omitting the version parameter when retrieving a key or a secret, returns the latest version of the item.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
version | query | integer | Version of the item that acts as the input keying material for the HKDF. If not given or version=0, the latest version will be used.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[ItemResponse](#itemresponse)</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Decrypt data

```http
POST /v3/items/{name}?op=decrypt HTTP/1.1
Content-Type: application/json

{
    "BinaryBody": "string"
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

"string"
```
```http
HTTP/1.1 default 
```

Use this call for remote decryption by specifying the stored key in the url and the data to decrypt in the request body. The request body contains binary-encoded ciphertext including the 6-byte header with the version information. The header must be excluded when the legacy_data query parameter is set to true. 


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
legacy_data | query | boolean | This boolean parameter indicates whether the encrypted data was generated by legacy API version or an external encryption tool. Legacy data does not include the key version in the encrypted data header.
legacy_version | query | integer | When operating on legacy data (legacy_data=true), the LegacyVersion value indicates the version of the key used to encrypt the data by legacy api version. When omitted, version 1 of the key will be used.
BinaryBody<b title="required">&nbsp;*&nbsp;</b> | body | string | Data to be operated on. For example it indicates cleartext input for all encrypt operations and ciphertext input for all decrypt operation. The data must be transmitted in a binary encoded format.
aad | query | string | Additional Authentication Data for deterministic encryption (SIV). Base64 url-safe, comma-separated.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>string</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Derive data

```http
POST /v3/items/{name}?op=derive HTTP/1.1
```
```http
HTTP/1.1 200 OK
```
```http
HTTP/1.1 default 
```

Key derivation offers an effective strategy when dealing with large number of data objects to be protected. It is used to establish a hierarchy of keys. Use this call to specify the root key and some ancillary information, usually characterizing the client application or an object to be encrypted. IDPS, upon feeding this information to an HMAC-based Key Derivation Function (HKDF) will, deterministically produce a derived key unique to the application or object. 
IDPS will continue to manage the root key, however, the derived key will be generated each time it is needed hence eliminating the need for its storage and management. This enables the IDPS clients to scale to very large number of keys while keeping latency and storage requirements low.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
derivation_data<b title="required">&nbsp;*&nbsp;</b> | query | string | The HKDF function used by IDPS to derive key material, allows the resulting key to be bound to a user-defined application- and context-specific information. A client must specify this information by passing a hex-encoded string in the derivation data parameter.
derived_length<b title="required">&nbsp;*&nbsp;</b> | query | integer | This parameter allows clients to specify the size of the derived data in number of bytes
version | query | integer | Version of the item that acts as the input keying material for the HKDF. If not given or version=0, the latest version will be used.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>no content</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Derive a key and decrypt data

```http
POST /v3/items/{name}?op=derive_and_decrypt HTTP/1.1
Content-Type: application/json

{
    "BinaryBody": "string"
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

"string"
```
```http
HTTP/1.1 default 
```

Derive an encryption key from the specified key and use it for decryption.
Key derivation offers an effective strategy when dealing with large number of data objects to be protected. It is used to establish a hierarchy of keys. Use this call to specify the root key and some ancillary information, usually characterizing the client application or an object to be encrypted. IDPS, upon feeding this information to an HMAC-based Key Derivation Function (HKDF) will, deterministically produce a derived key unique to the application or object. 
IDPS will continue to manage the root key, however, the derived key will be generated each time it is needed hence eliminating the need for its storage and management. This enables the IDPS clients to scale to very large number of keys while keeping latency and storage requirements low.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
derivation_data<b title="required">&nbsp;*&nbsp;</b> | query | string | The HKDF function used by IDPS to derive key material, allows the resulting key to be bound to a user-defined application- and context-specific information. A client must specify this information by passing a hex-encoded string in the derivation data parameter.
legacy_data | query | boolean | This boolean parameter indicates whether the encrypted data was generated by legacy API version or an external encryption tool. Legacy data does not include the key version in the encrypted data header.
legacy_version | query | integer | When operating on legacy data (legacy_data=true), the LegacyVersion value indicates the version of the key used to encrypt the data by legacy api version. When omitted, version 1 of the key will be used.
BinaryBody<b title="required">&nbsp;*&nbsp;</b> | body | string | Data to be operated on. For example it indicates cleartext input for all encrypt operations and ciphertext input for all decrypt operation. The data must be transmitted in a binary encoded format.
aad | query | string | Additional Authentication Data for deterministic encryption (SIV). Base64 url-safe, comma-separated.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>string</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Derive a key and encrypt data

```http
POST /v3/items/{name}?op=derive_and_encrypt HTTP/1.1
Content-Type: application/json

{
    "BinaryBody": "string"
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

"string"
```
```http
HTTP/1.1 default 
```

Derive an encryption key from the specified key and use it for encryption.
Key derivation offers an effective strategy when dealing with large number of data objects to be protected. It is used to establish a hierarchy of keys. Use this call to specify the root key and some ancillary information, usually characterizing the client application or an object to be encrypted. IDPS, upon feeding this information to an HMAC-based Key Derivation Function (HKDF) will, deterministically produce a derived key unique to the application or object. 
IDPS will continue to manage the root key, however, the derived key will be generated each time it is needed hence eliminating the need for its storage and management. This enables the IDPS clients to scale to very large number of keys while keeping latency and storage requirements low.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
derivation_data<b title="required">&nbsp;*&nbsp;</b> | query | string | The HKDF function used by IDPS to derive key material, allows the resulting key to be bound to a user-defined application- and context-specific information. A client must specify this information by passing a hex-encoded string in the derivation data parameter.
version | query | integer | Version of the item that acts as the input keying material for the HKDF. If not given or version=0, the latest version will be used.
BinaryBody<b title="required">&nbsp;*&nbsp;</b> | body | string | Data to be operated on. For example it indicates cleartext input for all encrypt operations and ciphertext input for all decrypt operation. The data must be transmitted in a binary encoded format.
aad | query | string | Additional Authentication Data for deterministic encryption (SIV). Base64 url-safe, comma-separated.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>string</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Encrypt data

```http
POST /v3/items/{name}?op=encrypt HTTP/1.1
Content-Type: application/json

{
    "BinaryBody": "string"
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

"string"
```
```http
HTTP/1.1 default 
```

Clients using IDPS to manage encryption keys can choose to perform the encryption and decryption operations either
locally (i.e. on the client system) or remotely (i.e. on the IDPS appliance). 
Use this call to perform remote encryption. The IDPS appliance will use the algorithm and key indicated by the item
passed in the url to encrypt the cleartext included in the request body. The returned binary response contains the
encrypted data along with the header containing metadata.
IDPS supports symmetric, assymetric and deterministic encryption algorithms - AES128, AES256, RSA1024, RSA2048, 
AES128ECB, AES256ECB, AES128SIV, or AES256SIV.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
version | query | integer | Version of the item that acts as the input keying material for the HKDF. If not given or version=0, the latest version will be used.
BinaryBody<b title="required">&nbsp;*&nbsp;</b> | body | string | Data to be operated on. For example it indicates cleartext input for all encrypt operations and ciphertext input for all decrypt operation. The data must be transmitted in a binary encoded format.
aad | query | string | Additional Authentication Data for deterministic encryption (SIV). Base64 url-safe, comma-separated.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>string</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## List items in a folder

```http
GET /v3/items/{name}?op=list HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

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
```http
HTTP/1.1 default 
```

List items - keys, secrets and folders - contained in the specified folder name.
The requested list of items is returned as a paginated response with each page consisting of up to 100 items. The request parameter start can be used to advance the list to the next page. For example, pass the value start=100 to retrieve the next set of 100 items.
The &quot;next&quot; parameter will be omitted from the response for the last response as an indicator that there are no more elements to list.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
start | query | integer | The parameter allows traversal of paginated list responses. It points to the index of the first page element of a paginated response.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[ItemListResponse](#itemlistresponse)</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## List versions
key versioning allows idps to simplify key rotation.

```http
GET /v3/items/{name}?op=list-versions HTTP/1.1
```
```http
HTTP/1.1 200 OK
```
```http
HTTP/1.1 default 
```

Use this call to retrieve all versions of a secret or key
The requested list of versions is returned as a paginated response with each page consisting maximum 100 versions. The request parameter start can be used to advance the list to the next page. For example, pass the value start=100 to retrieve the next set of 100 items.
The &quot;next&quot; parameter will be omitted from the response for the last response as an indicator that there are no more elements to list.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
start | query | integer | The parameter allows traversal of paginated list responses. It points to the index of the first page element of a paginated response.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>no content</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Reencrypt data

```http
POST /v3/items/{name}?op=reencrypt HTTP/1.1
Content-Type: application/json

{
    "BinaryBody": "string"
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

"string"
```
```http
HTTP/1.1 default 
```

Any update to a key is followed by re-encryption of the data encrypted using the updated key. This call helps clients to seamlessly perform this operation by passing the name of the updated key and other parameters in the url. 
Alternatively, the call can be used any time the client wishes to encrypt data using a version of the key different from the one previously used for encryption. The key version to use is specified either in the header of the ciphertext or using the legacy_version parameter when legacy_data=true.
Always use latest version of the key to encrypt.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
legacy_data | query | boolean | This boolean parameter indicates whether the encrypted data was generated by legacy API version or an external encryption tool. Legacy data does not include the key version in the encrypted data header.
legacy_version | query | integer | When operating on legacy data (legacy_data=true), the LegacyVersion value indicates the version of the key used to encrypt the data by legacy api version. When omitted, version 1 of the key will be used.
BinaryBody<b title="required">&nbsp;*&nbsp;</b> | body | string | Data to be operated on. For example it indicates cleartext input for all encrypt operations and ciphertext input for all decrypt operation. The data must be transmitted in a binary encoded format.
aad | query | string | Additional Authentication Data for deterministic encryption (SIV). Base64 url-safe, comma-separated.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>string</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Create a folder

```http
POST /v3/items/{name}?type=folder HTTP/1.1
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

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
```http
HTTP/1.1 default 
```

IDPS supports a hierarchical namespace for organizing stored items. Thus clients can group 
and scope items using a hierarchical folder structure. IDPS treats a folder as a type of item. 
So the item name &#039;A/B/C&#039; represents an item or folder &#039;C&#039; residing in folder &#039;B&#039; under folder &#039;A&#039;. 
It is important to note that to create item &#039;C&#039;, folder &#039;A/B&#039; should already exist. 
The hierarchy allows items with same name to exist within a project as long as they reside in different folders.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>201</td><td>[ItemResponse](#itemresponse)</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Create an encryption key

```http
POST /v3/items/{name}?type=key HTTP/1.1
Content-Type: application/json

{
    "body": {
        "cache_ttl": "integer",
        "is_enumerable": "boolean",
        "is_versioned": "boolean",
        "item": "string",
        "metadata": "string"
    }
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

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
```http
HTTP/1.1 default 
```

Generating cryptographically strong keying material is at the core of any encryption subsystem. IDPS supports creation of keys with an adequate source of entropy, designed to be version-able to support key rotation and configureable to be hidden and/or inaccessible to everyone except the IDPS appliance.
Use this call to create a key with the specified name and parameters.
Instead of relying on IDPS for key generation, clients may choose to use the service to store and manage an already generated key. This can be achieved by passing the key in the request body. Omit the item in the body for the key to be randomly generated.
Similarly, clients can instruct IDPS to generate a random name for the key being generated by setting the generate_name parameter to true. The name in the url, in this case, must be set to the parent folder.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
body<b title="required">&nbsp;*&nbsp;</b> | body | [ItemRequest](#itemrequest) | Item data for create and update operations
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
generate_name | query | boolean | A boolean parameter which when set to true will have IDPS generate a random name for the secret or key item
algorithm<b title="required">&nbsp;*&nbsp;</b> | query | string | Encryption algorithm for which the key is being generated or updated.
is_exportable | query | boolean | Tag the key to be exportable. For RSA algorithms, the private key will be exported on &#039;true&#039;, while the public key is always returned as a separate parameter.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>201</td><td>[ItemResponse](#itemresponse)</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>
## Update an encryption key

```http
PUT /v3/items/{name}?type=key HTTP/1.1
Content-Type: application/json

{
    "body": {
        "cache_ttl": "integer",
        "is_enumerable": "boolean",
        "is_versioned": "boolean",
        "item": "string",
        "metadata": "string"
    }
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

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
```http
HTTP/1.1 default 
```

It is recommended that keys have limited lifespans and are rotated periodically to minimize risk. Clients may also need to generate newer versions of keys in case of suspected compromise or as part of disaster recovery strategies. The update call allows a key with the specified name and parameters to be updated to a newer version.
The key can be randomly generated by omitting the item in the body.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
body<b title="required">&nbsp;*&nbsp;</b> | body | [ItemRequest](#itemrequest) | Item data for create and update operations
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
algorithm<b title="required">&nbsp;*&nbsp;</b> | query | string | Encryption algorithm for which the key is being generated or updated.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>201</td><td>[ItemResponse](#itemresponse)</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Create a secret

```http
POST /v3/items/{name}?type=secret HTTP/1.1
Content-Type: application/json

{
    "body": {
        "cache_ttl": "integer",
        "is_enumerable": "boolean",
        "is_versioned": "boolean",
        "item": "string",
        "metadata": "string"
    }
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

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
```http
HTTP/1.1 default 
```

Create a secret with the specified name and parameters.
Secrets are opaque data objects that IDPS manages. Examples of secrets include database passwords, TLS certificates, 
API keys (such as a Services Gateway PrivateAuth key), or even encryption keys that that an application or a 
third-party has generated. Although the last example of a kind of secret is encryption keys, it must not be confused 
with the IDPS item type of &#039;key&#039; - the distinction being that IDPS did not generate the encryption key and will simply 
treat it as an arbitrary string of bytes that needs to be securely stored and managed.
Clients can also use this call to generate a random secret, which, the application can then use as an keying material 
for cryptographic algorithms not supported by IDPS. Such a secret can be generated by passing an empty string in the 
&#039;item&#039; field of the ItemRequest parameter object.
Additionally, by setting the generate_name parameter to true, the client can instruct IDPS to generate a random name 
for the secret. The &#039;name&#039; in the url, in this case, must be set to the parent folder.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
body<b title="required">&nbsp;*&nbsp;</b> | body | [ItemRequest](#itemrequest) | Item data for create and update operations
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
size | query | integer | Size of the generated secret in bytes. The returned secret will be a hex-encoded string of length twice the size specified by Size parameter (since 1 byte represents 2 hexadecimal characters)
generate_name | query | boolean | A boolean parameter which when set to true will have IDPS generate a random name for the secret or key item
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>201</td><td>[ItemResponse](#itemresponse)</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>
## Update a secret

```http
PUT /v3/items/{name}?type=secret HTTP/1.1
Content-Type: application/json

{
    "body": {
        "cache_ttl": "integer",
        "is_enumerable": "boolean",
        "is_versioned": "boolean",
        "item": "string",
        "metadata": "string"
    }
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

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
```http
HTTP/1.1 default 
```

Update a secret with the specified name and parameters


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
body<b title="required">&nbsp;*&nbsp;</b> | body | [ItemRequest](#itemrequest) | Item data for create and update operations
name<b title="required">&nbsp;*&nbsp;</b> | path | string | Name of the item, optionally including the path with &quot;/&quot; separators, e.g., a/b/c
size | query | integer | Size of the generated secret in bytes. The returned secret will be a hex-encoded string of length twice the size specified by Size parameter (since 1 byte represents 2 hexadecimal characters)
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>201</td><td>[ItemResponse](#itemresponse)</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Batch encryption operations

```http
POST /v3/items?op=batch HTTP/1.1
Content-Type: application/json

{
    "BinaryBody": "string"
}
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

"string"
```
```http
HTTP/1.1 default 
```

Supports invocation of a single API call to perform multiple operations on a set of data objects in a batch. The output of all operations is return in a binary encoded response.
The list of items to be used in the operations and the list of data objects to be operated on is sent via the request body using the encoding format detailed at https://wiki.intuit.com/display/IISKM/Binary+Batch.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
BinaryBody<b title="required">&nbsp;*&nbsp;</b> | body | string | Data to be operated on. For example it indicates cleartext input for all encrypt operations and ciphertext input for all decrypt operation. The data must be transmitted in a binary encoded format.
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>string</td><td></td></tr> 
<tr><td>default</td><td>no content</td><td></td></tr> 
</table>

## Get project ca certificate

```http
GET /v3/project/ca-cert HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "ca-cert": "string"
}
```

### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[CaCertificate](#cacertificate)</td><td>Project CA Certificate</td></tr> 
</table>

## Get list of projects for the user

```http
GET /v3/projects HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

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

### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[ProjectList](#projectlist)</td><td>User Projects</td></tr> 
</table>

## Get list of appliances for the project

```http
GET /v3/projects/{projectSerial}/appliances HTTP/1.1
```
```http
HTTP/1.1 200 OK
Content-Type: application/json

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

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
projectSerial<b title="required">&nbsp;*&nbsp;</b> | path | string | 
//todo: migrate to html tables. after cool looking nested table
### Responses
<span comment="workaround for markdown processing in table"></span>
<table>
<tr><th>Http code</th><th>Type</th><th>Description</th></tr>
<tr><td>200</td><td>[ApplianceList](#appliancelist)</td><td>Project Appliances</td></tr> 
</table>


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

	
