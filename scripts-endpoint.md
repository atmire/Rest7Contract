# Admin Scripts Endpoints
[Back to the list of all defined endpoints](endpoints.md)

DSpace (6) has admin functionality to import and export items in CSV and ZIP format, to start a collection harvest run, to run or schedule curation tasks. Each of these functionalities also map on a DSpace CLI script. While we could implement each of these operations as a separate endpoint, this contract tries to describe a generic endpoint that allows administrators to explore, run or schedule DSpace CLI scripts from the REST API.

## Scripts Endpoint
**GET /api/admin/scripts**

This endpoint will list all (REST supported) scripts defined in `dspace/config/launcher.xml`. The script entries are embedded with a name, description and a self link. By "REST supported" we mean all scripts that have been updated to allow invocations from the REST API.

The JSON response document is as follows
```
{
  "page": {
      	"size": 5,
      	"totalElements": 14,
      	"totalPages": 3,
      	"number": 0
  },
  "sort" : {
    "by" : "name",
    "order" : "asc"
  },
  "_embedded" : {
    "scripts" [
      {
        "name" : "import",
        "description" : "Import items into DSpace"
        "_links" : {
          "self" : {
            "href" : "/api/admin/scripts/import"
          }
        }
      },
      {
        "name" : "metadata-import",
        "description" : "Import metadata after batch editing"
        "_links" : {
          "self" : {
            "href" : "/api/admin/scripts/metadata-import"
          }
        }
      },
      ...
    ]
  }
```

## Script Name Endpoint

### Script Details
**GET /api/admin/scripts/<:script-name>**

This endpoint will return information on all the parameters that are required to invoke the script. This dependens on the parameters defined in the implementation of the script.

The JSON response document is as follows
```
{
   "name" : "import",
   "description" : "Import items into DSpace",
   "parameters" : [
    {
      "name" : "a",
      "description" : "add items to DSpace"
      "type" : "boolean"
    },
    {
      "name" : "b",
      "description" : "add items to DSpace via Biblio-Transformation-Engine (BTE)"
      "type" : "boolean"
    },
    {
      "name" : "c",
      "description" : "destination collection(s) database ID"
      "type" : "id"
    },
    {
      "name" : "d",
      "description" : "delete items listed in mapfile"
      "type" : "file"
    },
    {
      "name" : "e",
      "description" : "email of eperson doing importing"
      "type" : "string"
    },
    {
      "name" : "i",
      "description" : "input type in case of BTE import"
      "type" : "string"
    },
    {
      "name" : "n",
      "description" : "if sending submissions through the workflow, send notification emails"
      "type" : "boolean"
    },
    {
      "name" : "p",
      "description" : "apply template"
      "type" : "string"
    },
    {
      "name" : "q",
      "description" : "don't display metadata"
      "type" : "boolean"
    },
    {
      "name" : "m",
      "description" : "mapfile items in mapfile"
      "type" : "file"
    },
    {
      "name" : "r",
      "description" : "replace items in mapfile"
      "type" : "boolean"
    },
    {
      "name" : "R",
      "description" : "resume a failed import (add only)"
      "type" : "boolean"
    },
    {
      "name" : "t",
      "description" : "test run - do not actually import items"
      "type" : "boolean"
    },
    {
      "name" : "w",
      "description" : "send submission through collection's workflow"
      "type" : "boolean"
    },
    {
      "name" : "z",
      "description" : "zip file containig the import"
      "type" : "file"
    }
   ]
}
```

Following parameter types are available:
* `string`: A regular string value
* `date`: A string that has a valid date pattern
* `boolean`: true or false
* `file`: For parameters with this type, the user has to provide a file
* `output`: Parameters with this type define the name of the output file. This name can be used later to download the the output file (e.g. when running `export` or `metadata-export`).

### Script Invocation
**POST /api/admin/scripts/<:script-name>**

POST requests to this endpoint will start the corresponding script with the provided parameters. All parameter values should be provided in the body that has to use the `multipart/form-data` content type. Once the upload is complete and the script was started successfully, this endpoint will return details on the scripts execution

The POST request body can contain the optional parameter `startTime`. When this parameter contains a valid timestamp, the script will start at that timestamp.

```
{
  "processId" : "000003f1-a850-49de-af03-997272d834c9",
  "scriptName" : "import",
  "startTime" : "2017-11-22T10:29:11Z",
  "status" : "RUNNING",
  "_links" : {
    "self" : {
      "href" : "/api/admin/processes/000003f1-a850-49de-af03-997272d834c9"
    }
  }
}
```

The possible `status` values are `RUNNING`, `STOPPED`, `FAILED` and `SCHEDULED`.