# WorkspaceItem Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/submission/workspaceitems**   

Provide access to the workspaceitems. It returns the list of existent workspaceitems.

Example: to be provided

## Single Item
**/api/submission/workspaceitems/<:id>**

Provide detailed information about a specific workspaceitem. The JSON response document is as follow
```json
{
  "id": 1911,
  "lastModified": "2017-06-24T00:40:54.970+0000",
  "sections": {
  	 "collection": "05457c63-b392-4629-a373-f2d66ee9ee33",
  	 "traditional-page1": {
  	 	"dc.title" : [{value: "Sample Submission Item"}],
  	 	"dc.contributor.author" : [
  	 		{value: "Bollini, Andrea", authority: "rp00001", confidence: 600}
  	 	]
  	 },
  	 "traditional-page2": {
  	 	"dc.subject" : [{value: "Test"}, {value: "JSON"}, {value: "REST"}],
  	 	"dc.description.abstract" : [
  	 		{value: "This is a long multiline text\n This is a second line of the abstract"}
  	 	]
  	 },
  	 "license": {
  	 	acceptanceDate: "2017-06-24T00:40:54.970+0000",
  	 	url: "http://dspace7.4science.it/api/core/bitstreams/8d33bdfb-e7ba-43e6-a93a-f445b7e8a1e2/content"
  	 },
  	 "uploads": [ 
  	 	{
  	 		metadata: {
  	 			"dc.title" : [{value: "sample_file.pdf"}],
  	 			"dc.description" : [{value: "Description of the sample file"}]
  	 		},
  	 		"sizeBytes": 8528,
			"checkSum": {
			    "checkSumAlgorithm": "MD5",
			    "value": "9d8f0f9e369cf12159d47c146c499cf4"
			},
  	 		"url": "http://dspace7.4science.it/api/core/bitstreams/00001abf-b2e0-477a-99de-104db7cb6469/content",
  	 		"accessConditions": [
  	 			{
  	 				"id": 123,
	  	 			"name": "openaccess",
	  	 			"groupUUID": "uuid-of-the-anonymous-group"
  	 			},
  	 			{
  	 				"id": 126,
	  	 			"name": "administrator",
	  	 			"groupUUID": "uuid-of-the-administrator-group"
  	 			},
  	 			{
  	 				"id": 127,
	  	 			"name": "embargo",
	  	 			"groupUUID": "1faf7c51-2a14-4826-b0b1-f1c1d2d82dd7",
	  	 			"startDate": "2018-06-24T00:40:54.970+0000"
  	 			},
  	 			{
  	 				"id": 128,
	  	 			"name": "lease",
	  	 			"groupUUID": "38ecd5ae-af12-4144-a276-81532e1679f8",
	  	 			"endDate": "2017-12-24T00:40:54.970+0000"
  	 			}
  	 		]
 		}
 	]
  	},
  	 "cclicense": {
  	 	"image-url": "https://i.creativecommons.org/l/by/4.0/88x31.png",
  	 	"license-uri": "https://creativecommons.org/licenses/by/4.0/"
  	 }
  },
  "type": "workspaceitem"
}
```

The actual data of the inprogress submission are arranged in *sections* map following the sections configured in the submissionDefinition. This map is *open for extension*, each type of section will expose a different JSON structure. See the [out-of-box submission section types](submissionsection-types.md) page for details.

Exposed links:
* collection: the collection where the inprogress submission will be created
* item: the item that hold the submission data
* submissionDefinition: the [submission definition](submissiondefinitions.md) used by this inprogress submission


### Linked entities
#### collection
**/api/submission/workspaceitems/<:id>/collection** (READ-ONLY)

Example: to be provided

It returns the collection where the inprogress submission is occuring. This is a **read-only** endpoint, once the inprogress submission is created the collection cannot be changed directly. Specific section, like the enhanced select-collection section planned for DSpace7 will be able to alter the collection manipulating the *sections* data.

#### item
**/api/submission/workspaceitems/<:id>/item** (READ-ONLY)

Example: to be provided

It returns the backend item holds by the submission. See the [item endpoint for more info](items.md). This is a **read-only** endpoint, once the inprogress submission is created the backend item cannot be changed. Update to the backend item will be reflected automatically on the inprogress submission but are not subject to the submission validation, i.e. they correspond to administrative edits

#### submissionDefinition
**/api/submission/workspaceitems/<:id>/submissionDefinition** (READ-ONLY)

Example: to be provided

It returns the submission definition used by the inprogress submission. See the [submission definitions endpoint for more info](submissiondefinitions.md). This is a **read-only** endpoint. 
The submission definition used by the inprogress submission is derived from the inprogress submission attributes. In the default implementation the definition is derived from the collection where the submission is created and is updated if it changes. 
Please note that this endpoint is not strictly necessary as you can currently retrieve the same definition using [/api/config/submissiondefinitions/search/findByCollection?uuid=<:workspaceitem-collection-uuid>](submissiondefinitions.md#findByCollection) but it allows the client to find the submissionDefinition embedded in the workspaceitem without the need to make a separate call. 
In addition, it allows in future to change the 1:1 association between collections and submissionDefinition without breaking the client

### Search methods
#### findBySubmitter
**/api/submission/workspaceitems/search/findBySubmitter?uuid=<:submitter-uuid>**

It returns the workspaceitem created by the specified submitter

## Multipart POST Method
Multipart POST request will typically result in the creation of a new file in the section identified by the name of the variable used for the upload (uploads is the default name of the user uploaded content). The process will be managed by the implementation bind with the identified section.
If succeed a 201 code will be returned and the new state of the workspaceitem serialized in the body.

## Call to request the suggestions
**/api/submission/workspaceitems/<:id>/suggestions**

See [Metadata Suggestions](metadata-suggestions.md) for details about this functionality and the response format

Provide detailed information about the data used for the suggestions. The JSON request document is as follow for a Pubmed live search
```json
{
  "suggestionType": "pubmed",
  "pubmedData": {
    "query": "Digitoxin metabolism by rat liver microsomes."
  }
}
```

This can also be used to request suggestions from the BTE framework, which uses an uploaded bitstream. The JSON request document is as follow for a BTE suggestion
```json
{
  "suggestionType": "bte",
  "bteData": {
    "bitstream": "8d33bdfb-e7ba-43e6-a93a-f445b7e8a1e2"
  }
}
```   