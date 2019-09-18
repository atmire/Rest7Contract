# Admin Scripts Endpoints
[Back to the list of all defined endpoints](endpoints.md)

DSpace has functionality to import and export items in CSV and ZIP format, to start a collection harvest run, to run or schedule curation tasks, …. Each of these functionalities also map on a DSpace CLI script. While we could implement each of these operations as a separate endpoint, this contract tries to describe a generic endpoint that allows administrators to explore, run or schedule DSpace CLI scripts from the REST API.

## Scripts Endpoint
**GET /api/system/scripts**

This endpoint will list all (REST supported) scripts defined in `dspace/config/spring/rest/scripts.xml`. The script entries are embedded with a name, description and a self link. By "REST supported" we mean all scripts that have been updated to allow invocations from the REST API.

The JSON response document is as follows
```json
{
  "page": {
      	"size": 5,
      	"totalElements": 14,
      	"totalPages": 3,
      	"number": 0
  },
  "_embedded" : {
    "scripts" : [
      {
        "id" : "import",
        "name" : "import",
        "type" : "script",
        "parameters" : [
            {
              "name" : "-a",  
              "nameLong": "--add",
              "description" : "add items to DSpace",
              "type" : "boolean"
            },
            {
              "name" : "-b",         
              "nameLong": "--add-bte",
              "description" : "add items to DSpace via Biblio-Transformation-Engine (BTE)",
              "type" : "boolean"
            },
            {
              "name" : "-c",  
              "nameLong": "--collection",
              "description" : "destination collection(s) database ID",
              "type" : "id"
            },
            {
              "name" : "-d",      
              "nameLong": "--delete",
              "description" : "delete items listed in mapfile",
              "type" : "file"
            },
            {
              "name" : "-e",       
              "nameLong": "--eperson",
              "description" : "email of eperson doing importing",
              "type" : "string"
            },
            {
              "name" : "-i",      
              "nameLong": "--inputtype",
              "description" : "input type in case of BTE import",
              "type" : "string"
            },
            {
              "name" : "-n",     
              "nameLong": "--notify",
              "description" : "if sending submissions through the workflow, send notification emails",
              "type" : "boolean"
            },
            {
              "name" : "-p",        
              "nameLong": "--template",
              "description" : "apply template",
              "type" : "string"
            },
            {
              "name" : "-q",         
              "nameLong": "--quiet",
              "description" : "don't display metadata",
              "type" : "boolean"
            },
            {
              "name" : "-m",     
              "nameLong": "--mapfile",
              "description" : "mapfile items in mapfile",
              "type" : "file"
            },
            {
              "name" : "-r",    
              "nameLong": "--replace",
              "description" : "replace items in mapfile",
              "type" : "boolean"
            },
            {
              "name" : "-R",     
              "nameLong": "--resume",
              "description" : "resume a failed import (add only)",
              "type" : "boolean"
            },
            {
              "name" : "-t",   
              "nameLong": "--test",
              "description" : "test run - do not actually import items",
              "type" : "boolean"
            },
            {
              "name" : "-w",            
              "nameLong": "--workflow",
              "description" : "send submission through collection's workflow",
              "type" : "boolean"
            },
            {
              "name" : "-z",      
              "nameLong": "--zip",
              "description" : "zip file containing the import",
              "type" : "file"
            }
           ],
        "description" : "Import items into DSpace",
        "_links" : {
          "self" : {
            "href" : "/api/system/scripts/import"
          }
        }
      },
      {
        "name" : "metadata-import",
        "type" : "script",   
        "parameters": [
            {
              "name": "-f",
              "nameLong": "--file",
              "description": "source file",
              "type": "InputStream",
              "mandatory": true
            },
            {
              "name": "-e",
              "nameLong": "--email",
              "description": "email address or user id of user (required if adding new items)",
              "type": "String",
              "mandatory": true
            },
            {
              "name": "-s",
              "nameLong": "--silent",
              "description": "silent operation - doesn't request confirmation of changes USE WITH CAUTION",
              "type": "boolean",
              "mandatory": false
            },
            {
              "name": "-w",
              "nameLong": "--workflow",
              "description": "workflow - when adding new items, use collection workflow",
              "type": "boolean",
              "mandatory": false
            },
            {
              "name": "-n",
              "nameLong": "--notify",
              "description": "notify - when adding new items using a workflow, send notification emails",
              "type": "boolean",
              "mandatory": false
            },
            {
              "name": "-t",
              "nameLong": "--template",
              "description": "template - when adding new items, use the collection template (if it exists)",
              "type": "boolean",
              "mandatory": false
            },
            {
              "name": "-h",
              "nameLong": "--help",
              "description": "help",
              "type": "boolean",
              "mandatory": false
            }
          ],
        "description" : "Import metadata after batch editing",
        "_links" : {
          "self" : {
            "href" : "/api/system/scripts/metadata-import"
          }
        }
      }
    ]
  }
}
```

## Script Name Endpoint

### Script Details
**GET /api/system/scripts/<:script-name>**

This endpoint will return information on all the parameters that are required to invoke the script. This depends on the parameters defined in the implementation of the script.

The JSON response document is as follows
```json
{
   "id" : "import",
   "name" : "import",
   "description" : "Import items into DSpace",
   "type" : "script",
   "parameters" : [
    {
      "name" : "-a",  
      "nameLong": "--add",
      "description" : "add items to DSpace",
      "type" : "boolean"
    },
    {
      "name" : "-b",         
      "nameLong": "--add-bte",
      "description" : "add items to DSpace via Biblio-Transformation-Engine (BTE)",
      "type" : "boolean"
    },
    {
      "name" : "-c",  
      "nameLong": "--collection",
      "description" : "destination collection(s) database ID",
      "type" : "id"
    },
    {
      "name" : "-d",      
      "nameLong": "--delete",
      "description" : "delete items listed in mapfile",
      "type" : "file"
    },
    {
      "name" : "-e",       
      "nameLong": "--eperson",
      "description" : "email of eperson doing importing",
      "type" : "string"
    },
    {
      "name" : "-i",      
      "nameLong": "--inputtype",
      "description" : "input type in case of BTE import",
      "type" : "string"
    },
    {
      "name" : "-n",     
      "nameLong": "--notify",
      "description" : "if sending submissions through the workflow, send notification emails",
      "type" : "boolean"
    },
    {
      "name" : "-p",        
      "nameLong": "--template",
      "description" : "apply template",
      "type" : "string"
    },
    {
      "name" : "-q",         
      "nameLong": "--quiet",
      "description" : "don't display metadata",
      "type" : "boolean"
    },
    {
      "name" : "-m",     
      "nameLong": "--mapfile",
      "description" : "mapfile items in mapfile",
      "type" : "file"
    },
    {
      "name" : "-r",    
      "nameLong": "--replace",
      "description" : "replace items in mapfile",
      "type" : "boolean"
    },
    {
      "name" : "-R",     
      "nameLong": "--resume",
      "description" : "resume a failed import (add only)",
      "type" : "boolean"
    },
    {
      "name" : "-t",   
      "nameLong": "--test",
      "description" : "test run - do not actually import items",
      "type" : "boolean"
    },
    {
      "name" : "-w",            
      "nameLong": "--workflow",
      "description" : "send submission through collection's workflow",
      "type" : "boolean"
    },
    {
      "name" : "-z",      
      "nameLong": "--zip",
      "description" : "zip file containing the import",
      "type" : "file"
    }
   ]
}
```

Following parameter types are available:
* `string`: A regular string value
* `date`: A string that has a valid date pattern
* `boolean`: true or false
* `file`: For parameters with this type, the user has to provide a file. This would be a multipart POST request using the same filename
* `output`: Parameters with this type define the name of the output file. This name can be used later to download the the output file (e.g. when running `export` or `metadata-export`).
