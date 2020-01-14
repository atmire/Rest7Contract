# WorkspaceItem - upload of files via url (TUS)
[Back to the definition of the workspaceitems endpoint](workspaceitems.md)

To upload large files to workspaceitems you can use a TUS server, where the files get uploaded to, and then introduced into REST via that url.

The section data representing the data about the user uploaded files via tus (accessible via GET /api/submission/workspaceitems/<:id>
                                                                                                                                ):

```json
{
	"tusupload": {
          "files": [
            {
              "uuid": "0a9ebb92-fa89-44b3-afbc-a8535cdb5776",
              "metadata": {
                "dc.source": [
                  {
                    "value": "dstat.map",
                    "language": null,
                    "authority": null,
                    "confidence": -1,
                    "place": 0
                  }
                ],
                "dc.title": [
                  {
                    "value": "dstat.map",
                    "language": null,
                    "authority": null,
                    "confidence": -1,
                    "place": 0
                  }
                ]
              },
              "accessConditions": [],
              "format": {
                "id": 1,
                "shortDescription": "Unknown",
                "description": "Unknown data format",
                "mimetype": "application/octet-stream",
                "supportLevel": "UNKNOWN",
                "internal": false,
                "extensions": [],
                "type": "bitstreamformat"
              },
              "sizeBytes": 3736,
              "checkSum": {
                "checkSumAlgorithm": "MD5",
                "value": "9821c3239bd2780a4b25f0ad661e925d"
              },
              "url": "http://localhost:8080/unsw-7-source/api/core/bitstreams/0a9ebb92-fa89-44b3-afbc-a8535cdb5776/content"
            },
            {
              "uuid": "09a5a352-f301-44c3-9eee-c6983daccee2",
              "metadata": {
                "dc.description": [
                  {
                    "value": "Some description",
                    "language": null,
                    "authority": null,
                    "confidence": -1,
                    "place": 0
                  }
                ],
                "dc.source": [
                  {
                    "value": "/img/svg/logo.svg",
                    "language": null,
                    "authority": null,
                    "confidence": -1,
                    "place": 0
                  }
                ],
                "dc.title": [
                  {
                    "value": "logo.svg",
                    "language": null,
                    "authority": null,
                    "confidence": -1,
                    "place": 0
                  }
                ]
              },
              "accessConditions": [],
              "format": {
                "id": 1,
                "shortDescription": "Unknown",
                "description": "Unknown data format",
                "mimetype": "application/octet-stream",
                "supportLevel": "UNKNOWN",
                "internal": false,
                "extensions": [],
                "type": "bitstreamformat"
              },
              "sizeBytes": 1380,
              "checkSum": {
                "checkSumAlgorithm": "MD5",
                "value": "aa06ed50ec5b86d5b6debc20e8f3bd9e"
              },
              "url": "http://localhost:8080/unsw-7-source/api/core/bitstreams/09a5a352-f301-44c3-9eee-c6983daccee2/content"
            }
          ]
    }
}
```
the files attribute contains the list of user uploaded files via TUS in the section. For each file the following attributes exist
* metadata: the map of the metadata assigned to the specific file with [the same structure](workspaceitem-data-metadata.md) used in the submission-form sectionType for the item metadata
* sizeBytes (**READ-ONLY**): the size of the received file as calculated on the server at the receiving time 
* checkSum (**READ-ONLY**): the checksum details (algorithm and value) of the received file as calculated on the server at the receiving time
* url (**READ-ONLY**): from where the file can be downloaded
* accessConditions: an array of all the policies that has been applied by the user to the file. 

## Patch operations
The PATCH method expects a JSON body according to the [JSON Patch specification RFC6902](https://tools.ietf.org/html/rfc6902)

Each successful Patch operation will return a HTTP 200 CODE with the new workspaceitem as body. See also the [General rules for the Patch operation](patch.md) for more details.

### Add
To add files via TUS during the submission the Add PATCH is used; example:

```
curl -X PATCH \
   ${dspace7-url}/api/submission/workspaceitems/<:id> \
   -H 'Authorization: <:bearer-token>' \
   -H 'Content-Type: application/json' \
   -d '[
   {
     "op": "add",
     "path": "/sections/tusupload/files",
     "value": [
       {
         "file-url": "https://www.atmire.com/cache/img/1e24facc5b38c82c831395f41916cb41-logo-wb-header-en-1.svg"
       },
       
       {
         "file-url": "https://www.atmire.com/cache/img/e80509c0e261278928bed6c75d2d9193-University_of_Cambridge_logo-with_padding_2-01.svg"
       }
     ]
   }
 ]'
 ```

This add patch endpoint can only be used if the TusUploadStep is configured in item-submission.xml

Which links will be accepted as valid for the tus upload is configurable by adding a list of allowed regex in a configurable property.

Bitstreams created by this patch can be removed/moved/metadata added according to the same patches of the regular upload.
These patches are analog to the ones in [Workspaceitem data upload](workspaceitem-data-upload.md). Example:

### Remove
It is possible to remove an uploaded file specifying its index in the path of a remove operation 
`curl --data '{[ { "op": "remove", "path": "/sections/tusupload/files/<:idx-file>"}]' -X PATCH ${dspace7-url}/api/submission/workspaceitems/<:id>>`



