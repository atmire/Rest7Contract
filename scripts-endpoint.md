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
        "name" : "import",
        "type" : "script",
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
   "name" : "import",
   "description" : "Import items into DSpace",
   "type" : "script",
   "parameters" : [
    {
      "name" : "-a",
      "description" : "add items to DSpace",
      "type" : "boolean",
      "mandatory": false
    },
    {
      "name" : "-b",
      "description" : "add items to DSpace via Biblio-Transformation-Engine (BTE)",
      "type" : "boolean",
      "mandatory": false
    },
    {
      "name" : "-c",
      "description" : "destination collection(s) database ID",
      "type" : "id",
      "mandatory": true
,
    },
    {
      "name" : "-d",
      "description" : "delete items listed in mapfile",
      "type" : "file",
      "mandatory": false
    },
    {
      "name" : "-e",
      "description" : "email of eperson doing importing",
      "type" : "string",
      "mandatory": true
    },
    {
      "name" : "-i",
      "description" : "input type in case of BTE import",
      "type" : "string",
      "mandatory": false
    },
    {
      "name" : "-n",
      "description" : "if sending submissions through the workflow, send notification emails",
      "type" : "boolean",
      "mandatory": false
    },
    {
      "name" : "-p",
      "description" : "apply template",
      "type" : "string",
      "mandatory": false
    },
    {
      "name" : "-q",
      "description" : "don't display metadata",
      "type" : "boolean",
      "mandatory": false
    },
    {
      "name" : "-m",
      "description" : "mapfile items in mapfile",
      "type" : "file",
      "mandatory": true
    },
    {
      "name" : "-r",
      "description" : "replace items in mapfile",
      "type" : "boolean",
      "mandatory": false
    },
    {
      "name" : "-R",
      "description" : "resume a failed import (add only)",
      "type" : "boolean",
      "mandatory": false
    },
    {
      "name" : "-t",
      "description" : "test run - do not actually import items",
      "type" : "boolean",
      "mandatory": false
    },
    {
      "name" : "-w",
      "description" : "send submission through collection's workflow",
      "type" : "boolean",
      "mandatory": false
    },
    {
      "name" : "-z",
      "description" : "zip file containing the import",
      "type" : "file",
      "mandatory": true
    }
   ]
}
```

Following parameter types are available:
* `String`: A regular string value
* `Date`: A string that has a valid date pattern
* `Boolean`: true or false
* `InputStream`: For parameters with this type, the user has to provide a file. This would be a multipart POST request using the same filename
* `OutputStream`: Parameters with this type define the name of the output file. This name can be used later to download the the output file (e.g. when running `export` or `metadata-export`).
