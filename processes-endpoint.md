# Admin Processes Endpoints
[Back to the list of all defined endpoints](endpoints.md)

This endpoint allows users to list and manipulate script processes created by the [Scripts endpoint](scripts-endpoint.md).

## Execution List
**GET /api/system/processes**

This endpoint will return a list of all created processes. The JSON response document is as follows:

```json
{
  "page": {
      	"size": 5,
      	"totalElements": 14,
      	"totalPages": 3,
      	"number": 0
  },
  "sort" : {
    "by" : "script",
    "order" : "asc"
  },
  "_embedded" : {
    "processes" : [
      {
        "processId" : "000003f1-a850-49de-af03-997272d834c9",
        "userId" : "aa0263e2-b90a-4528-89fa-116ea4859de1",
        "startTime" : "2017-11-22T10:29:11Z",
        "status" : "RUNNING",
        "parameters" : [
          {
            "name" : "c",
            "value" : "954e5cfa-6990-4c85-ae42-f30d8c7888e2"
          },
          {
            "name" : "n",
            "value" : "true"
          }
        ],
        "_links" : {
          "self" : {
            "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9"
          },
          "script" : {
            "href" : "/api/system/scripts/import"
          },
          "output" : {
            "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/output"
          },
          "files" : {
            "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/files"
          }
        }
      },
      {
        "processId" : "d3007ea8-1cc0-481d-914a-06720a200edf",
        "userId" : "c7d85e7f-63e5-4bc0-96cb-5d80be48d62e",
        "startTime" : "2017-11-20T10:29:11Z",
        "status" : "FAILED",
        "parameters" : [
          {
            "name" : "i",
            "value" : "c70893a6-ac55-48c7-9447-61e026b62929"
          }
        ],
        "_links" : {
          "self" : {
            "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9"
          },
          "script" : {
            "href" : "/api/system/scripts/metadata-export"
          },
          "output" : {
            "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/output"
          },
          "files" : {
            "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/files"
          }
        }
      }
    ]
  }
}
```

Optional parameters to query the processes:
* `script`: The name of the script (e.g. import)
* `userId`: The UUID of the person who created the process (only admins can retrieve processes they didn't start)
* `status`: The status of the script
* `parameter.xyz`: Which parameters have been used, and their value

Sort options should support:
* `script`
* `startTime`

## Execution Details
**GET /api/system/processes/<:process-id>**

This endpoint will return details on the requested process.

```json
{
  "processId" : "000003f1-a850-49de-af03-997272d834c9",
  "userId" : "aa0263e2-b90a-4528-89fa-116ea4859de1",
  "startTime" : "2017-11-22T10:29:11Z",
  "status" : "RUNNING",
  "parameters" : [
    {
    "name" : "c",
    "value" : "954e5cfa-6990-4c85-ae42-f30d8c7888e2"
    },
    {
    "name" : "n",
    "value" : "true"
    }
  ],
  "_links" : {
    "self" : {
      "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9"
    },
    "script" : {
      "href" : "/api/system/scripts/import"
    },
    "output" : {
      "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/output"
    },
    "files" : {
      "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/files"
    }
  }
}
```

The possible `status` values are `RUNNING`, `STOPPED`, `FAILED` and `SCHEDULED`.

## Execution Console Output
**GET /api/system/processes/<:process-id>/output**

This endpoint will return the console output of the script, if any, in a JSON format annotated with timestamps.

The endpoint supports the following optional parameters:
* `fromTime`: A timestamp starting starting from which the console output entries have to be returned
* `toTime`: A timestamp up until which the console output entries have to be returned

```json
[
{ "time" : "2017-11-21T11:32:52Z", "line" : "Adding items from directory: /Users/tom/Development/dspaces/dspace7/imports/saf.zip" },
{ "time" : "2017-11-21T11:32:54Z", "line" : "Generating mapfile: temp" },
{ "time" : "2017-11-21T11:32:56Z", "line" : "Adding item from directory item_1" },
{ "time" : "2017-11-21T11:32:58Z", "line" : "	Loading dublin core from /Users/tom/Development/dspaces/dspace7/imports/saf.zip/item_1/dublin_core.xml" },
{ "time" : "2017-11-21T11:33:00Z", "line" : "	Schema: dc Element: title Qualifier:  Value: Bunny Video" },
{ "time" : "2017-11-21T11:33:02Z", "line" : "	Processing contents file: /Users/tom/Development/dspaces/dspace7/imports/saf.zip/item_1/contents" },
{ "time" : "2017-11-21T11:33:04Z", "line" : "	Bitstream: mp4test.mp4" },
{ "time" : "2017-11-21T11:33:06Z", "line" : "Processing handle file: handle" },
{ "time" : "2017-11-21T11:33:08Z", "line" : "It appears there is no handle file -- generating one" },
{ "time" : "2017-11-21T11:33:10Z", "line" : "0 item_1" }
]
```

## Execution File Output List
**GET /api/system/processes/<:process-id>/files**

This endpoint will let an administrator download an output file created by a process. If the file is found, it will be presented as a download. This endpoint will support "Range" HTTP headers so that downloads can be paused and resumed.

```json
{
  "processId" : "000003f1-a850-49de-af03-997272d834c9",
  "_links" : {
    "self" : {
      "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/files"
    },
    "mapfile" : {
      "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/files/mapfile"
    },
    "zipfile" : {
      "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/files/zipfile"
    }
  }
}
```

## Execution File Output
**GET /api/system/processes/<:process-id>/files/<:file-name>**

This endpoint will let an administrator download an output file created by a process. If the file is found, it will be presented as a download. This endpoint will support "Range" HTTP headers so that downloads can be paused and resumed.

Required parameters:
* `file-name`: The name of the output file to retrieve

## Execution Deletion
**DELETE /api/system/processes/<:process-id>**

If the process is still in a `RUNNING` or `SCHEDULED` status, a best-effort attempt will be made to stop the process. Then the process information will be removed.

### Script Invocation
**POST /api/system/scripts/<:script-name>/processes**

POST requests to this endpoint will start the corresponding script with the provided parameters. All parameter values should be provided in the body that has to use the `multipart/form-data` content type. Once the upload is complete and the script was started successfully, this endpoint will return details on the scripts execution

The POST request body can contain the optional parameter `startTime`. When this parameter contains a valid timestamp, the script will start at that timestamp.

```json
{
  "processId" : "000003f1-a850-49de-af03-997272d834c9",
  "userId" : "aa0263e2-b90a-4528-89fa-116ea4859de1",
  "startTime" : "2017-11-22T10:29:11Z",
  "status" : "RUNNING",
  "parameters" : [
    {
    "name" : "c",
    "value" : "954e5cfa-6990-4c85-ae42-f30d8c7888e2"
    },
    {
    "name" : "n",
    "value" : "true"
    }
  ],
  "_links" : {
    "self" : {
      "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9"
    },
    "script" : {
      "href" : "/api/system/scripts/import"
    },
    "output" : {
      "href" : "/api/system/processes/000003f1-a850-49de-af03-997272d834c9/output"
    }
  }
}
```

The possible `status` values are `RUNNING`, `STOPPED`, `FAILED` and `SCHEDULED`.
