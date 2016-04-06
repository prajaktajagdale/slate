{
    "swagger": "2.0",
    "info": {
        "title": "IDPS API",
        "description": "Intuit Data Protection System",
        "version": "3"
    },
    "basePath": "/v3", 
    "consumes": [
        "application/json"
    ], 
    "definitions": {
        "ApplianceStatus": {
            "properties": {
                "ca_cert_exists": {
                    "description": "a CA certificate has been entered into the appliance", 
                    "type": "boolean"
                }, 
                "cloud": {
                    "description": "cloud provider", 
                    "enum": [
                        "ec2", 
                        "vmware", 
                        "openstack"
                    ], 
                    "type": "string"
                }, 
                "cloud_creds": {
                    "description": "cloud credentials have been entered for the project", 
                    "type": "boolean"
                }, 
                "instance_id": {
                    "description": "cloud machine instance id", 
                    "type": "string"
                }, 
                "local_config_exists": {
                    "description": "the appliance has been configured", 
                    "type": "boolean"
                }, 
                "master_key_exists": {
                    "description": "the master key has been entered into the appliance", 
                    "type": "boolean"
                }, 
                "max_api_version": {
                    "description": "maximum api version supported by the appliance", 
                    "type": "integer"
                }, 
                "min_api_version": {
                    "description": "minimum api version supported by the appliance", 
                    "type": "integer"
                }, 
                "project_serial": {
                    "description": "serial identifier of the project this instance belongs to (requires authentication)", 
                    "type": "string"
                }, 
                "pvkm_address": {
                    "description": "address of the PVKM that manages this appliance", 
                    "type": "string"
                }, 
                "pvkm_address_is_set": {
                    "description": "the pvkm_address has been set", 
                    "type": "boolean"
                }, 
                "pvkm_reachable": {
                    "description": "the appliance is able to connect to the PVKM", 
                    "type": "boolean"
                }, 
                "region": {
                    "description": "cloud region", 
                    "type": "string"
                }, 
                "time_in_sync": {
                    "description": "time on the appliance is in sync with the PVKM", 
                    "type": "boolean"
                }, 
                "time_skew": {
                    "description": "time skew in seconds between the appliance and the PVKM", 
                    "type": "integer"
                }, 
                "version": {
                    "description": "appliance software version", 
                    "type": "string"
                }, 
                "vkm_credentials_accessible": {
                    "description": "IDPS credentials are accessible at VKM", 
                    "type": "boolean"
                }
            }, 
            "required": [
                "version", 
                "local_config_exists", 
                "master_key_exists", 
                "instance_id", 
                "cloud", 
                "pvkm_address", 
                "pvkm_reachable", 
                "time_in_sync"
            ], 
            "type": "object"
        },
        "ItemInList": {
            "description": "The description includes the name of the item and its type.", 
            "properties": {
                "name": {
                    "description": "The name of the item, optionally, including the path with \"/\" separators, e.g., a/b/c", 
                    "type": "string", 
                    "x-go-name": "ItemName"
                }, 
                "type": {
                    "description": "Type of the returned item, one of: secret, key, or folder", 
                    "type": "string", 
                    "x-go-name": "ItemType"
                }
            }, 
            "title": "The ItemInList object describes an item that is returned as part of an item list.", 
            "type": "object", 
            "x-go-package": "."
        }, 
        "ItemVersion": {
            "description": "IDPS offers clients with an option to version items as a means to simplify key rotation. \nThe ItemVersion field associated with every versioned item indicates a version number and the date of its creation. \nThe IDPS API supports listing of all versions of an item and requesting or deleting a specific version of an item. \nOperations like encrypt and decrypt can be invoked with an explicit key version. ", 
            "properties": {
                "version_create_date": {
                    "description": "Date the version was created", 
                    "type": "string", 
                    "x-go-name": "VersionCreateDate"
                }, 
                "version_number": {
                    "description": "Indicates the version number of the item", 
                    "format": "int32", 
                    "type": "integer", 
                    "x-go-name": "VersionNumber"
                }
            }, 
            "type": "object", 
            "x-go-package": "."
        }, 
        "ItemListResponse": {
            "description": "IDPS clients are provided with an ability to retrieve a list of all items. The ItemListResponse object contains such a list of items\nreturned in a paginated form.", 
            "properties": {
                "list": {
                    "description": "Returned list of items", 
                    "items": {
                        "$ref": "#/definitions/ItemInList"
                    }, 
                    "type": "array", 
                    "x-go-name": "List"
                }, 
                "next": {
                    "description": "The Next field acts as an index into the paginated response and is an indicator of the current page number.\nThe field is omitted for the last page in the response as an indicator that there are no more elements to list.", 
                    "format": "int32", 
                    "type": "integer", 
                    "x-go-name": "Next"
                }
            }, 
            "type": "object", 
            "x-go-package": "."
        }, 
        "ItemVersionsListResponse": {
            "description": "The IDPS API offers clients the ability to list all available versions for a versioned key. The ItemVersionListResponse object \ncontains a list of ItemVersion fields returned as paginated response. ", 
            "properties": {
                "list": {
                    "description": "Returned list of versions", 
                    "items": {
                        "$ref": "#/definitions/ItemVersion"
                    }, 
                    "type": "array", 
                    "x-go-name": "List"
                }, 
                "next": {
                    "description": "The Next field acts as an index into the paginated response and is an indicator of the current page number.\nThe field is omitted for the last page in the response as an indicator that there are no more elements to list.", 
                    "format": "int32", 
                    "type": "integer", 
                    "x-go-name": "Next"
                }
            }, 
            "type": "object", 
            "x-go-package": "."
        }
    }, 
    "host": "$HOST", 
    "info": {
        "description": "provides API to access IDPS protected items", 
        "title": "Intuit Data Protection System", 
        "version": "3"
    }, 
    "paths": {
        "/appliance/status": {
            "get": {
                "operationId": "getApplianceStatus", 
                "responses": {
                    "200": {
                        "description": "Appliance Status", 
                        "schema": {
                            "$ref": "#/definitions/ApplianceStatus"
                        }
                    }
                }, 
                "summary": "Get appliance status"
            }
        }
    }, 
    "produces": [
        "application/json"
    ], 
    "schemes": [
        "https"
    ]
}
