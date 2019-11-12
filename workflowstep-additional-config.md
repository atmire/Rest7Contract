# Workflow step additional configuration
[Back to the definition of the workflowsteps endpoint](workflowsteps.md)

## selectReviewerStep Definition
**/api/config/workflowsteps/selectReviewerStep**

Provide detailed information about the selectReviewerStep workflow step. An example JSON response document:
```json
{
  	"id": "selectReviewerStep",
    "actions": [
        "query",
        "select_reviewer"
    ],
  	"type": "workflowstep",
  	"_links": {
  		"elements" : "<dspace-url>/config/workflowsteps/selectReviewerStep/elements", 
  		"action-query" : "<dspace-url>/config/workflowsteps/selectReviewerStep/action-query" 
  	}
}
```

### selectReviewerStep elements Definition
**/api/config/workflowsteps/selectReviewerStep/elements**

Provide detailed information about the UI elements selectReviewerStep workflow step. An example JSON response document:
```json
{
    "elements": [
        {
          "element-type": "query"
        }
    ],
  	"type": "workflowstep-element"
}
```

This specifies a query field should be rendered

### selectReviewerStep query action Definition
**/api/config/workflowsteps/selectReviewerStep/action-query**

Provide detailed information about the query action in the selectReviewerStep workflow step. An example JSON response document:
```json
{
    "elements": [
        {
          "select-action": "single"
        }
    ],
  	"type": "workflowstep-element"
}
```

This specifies a single value can be selected from the search results

## scoreReviewStep Definition
**/api/config/workflowsteps/scoreReviewStep**

Provide detailed information about the scoreReviewStep workflow step. An example JSON response document:
```json
{
  	"id": "scoreReviewStep",
    "actions": [
        "submit_score"
    ],
  	"type": "workflowstep",
  	"_links": {
  		"elements" : "<dspace-url>/config/workflowsteps/scoreReviewStep/elements" 
  	}
}
```

### scoreReviewStep elements Definition
**/api/config/workflowsteps/scoreReviewStep/elements**

Provide detailed information about the UI elements scoreReviewStep workflow step. An example JSON response document:
```json
{
    "elements": [
        {
          "element-type": "select",
          "values": [
            "0%",
            "25%",
            "50%",
            "75%",
            "100%"
          ]
        }
    ],
  	"type": "workflowstep-element"
}
```

This specifies a select box should be rendered with the given values