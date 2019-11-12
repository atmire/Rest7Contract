# Workflow Steps Endpoints
[Back to the list of all defined endpoints](endpoints.md)

A workflow step represents a single step in the reviewing process, e.g. the accept/reject step.  
Depending on its type or action, it may include additional details for rendering.  
Not all steps currently required additional configuration. If each action represents a simple button and the chosen action should be sent to REST, no additional configuration is required.  

All endpoints mentioned here require authentication

## Main Endpoint
**/api/config/workflowsteps**   

Provide access to the configured workflow steps. It returns the list of existent workflow-steps.

## Single Workflow Step Definition
**/api/config/workflowsteps/<:step-name>**

Provide detailed information about a specific workflow step. An example JSON response document:
```json
{
  	"id": "editstep",
    "actions": [
        "approve",
        "reject",
        "edit_metadata"
    ],
  	"type": "workflowstep",
  	"_links": {
  		"elements" : "<dspace-url>/config/workflowsteps/<:step-name>/elements", 
  		"action-reject" : "<dspace-url>/config/submissionforms/<:id-of-the-submission-form-page>" 
  	}
}
```

The **actions** property contains the list of actions the user is authorized to perform in this step:
* The **edit_metadata** action implies the user can use the PATCH on the workflow item's submission sections to edit the metadata.
* Other actions are considered to be buttons with an action sent to REST using a POST to the claimed task

Reject:
```sh
curl 'https://dspace7.4science.cloud/server/api/workflow/claimedtasks/29' \
-H 'Connection: keep-alive' \
-H 'Accept: application/json, text/plain, */*' \
-H 'authorization: Bearer eyJhbGci...' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data 'submit_reject=true&reason=test'
```
Edit metadata:
```sh
curl 'https://dspace7.4science.cloud/server/api/workflow/workflowitems/102' \
-XPATCH \
-H 'Accept: application/json, text/plain, */*' \
-H 'Content-Type: application/json; charset=utf-8' \
-H 'Authorization: Bearer eyJhbGciOi...' \
--data-binary '[{"op":"replace","path":"/sections/traditionalpageone/dc.title/0","value":{"value":"test item","language":null,"authority":null,"display":"test item","confidence":-1,"place":0,"otherInformation":null}}]'
```

## Linked Entities
### elements

It returns the endpoint to use to access a detailed, workflow step dependent, configuration to be used on the task execution page:
* In the scoreReview workflow, this can be used to inform the UI to display the current score
* In the selectReviewerStep, this can be used to inform the UI to display a search for a reviewer, and a list of matches

Samples can be found in [workflowstep-additional-config.md](workflowstep-additional-config.md).

## Linked Entities
### action-<:action-name>

It returns the endpoint to use to access a detailed, action dependent, configuration to be used on the task execution page:
* For the reject action, it can be used to detail that the reject action requires a reject message
* For the scoreReviewStep's evaluationStep, it can be used to detail that a score selection should be displayed

Samples can be found in [workflowstep-additional-config.md](workflowstep-additional-config.md).