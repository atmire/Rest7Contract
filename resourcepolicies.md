# Resource Policies Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/authz/resourcepolicies**   

As we don't have yet an use case to iterate over all the existent resource policies the main endpoint is not implemented and a 405 error code is returned according to our [general error response codes](README.md#Error codes).

## Retrieve Single Resource Policy
**GET /api/authz/resourcepolicies/<:id>**

Provide detailed information about a specific resource policy. The JSON response document is as follow
```json
{
  "id": 2844,
  "name": null,
  "description": null,
  "policyType": "TYPE_SUBMISSION",
  "action": "READ",
  "type": "resourcePolicy",
  "start-date": null,
  "end-date": null
}
```

Exposed links:
* eperson: link to the eperson that have permission grant by the policy
* group: link to the group that have permission grant by the policy
* resource: link to the resource subject to the policy

## Linked entities
### EPerson
**/api/authz/resourcepolicies/<:id>/eperson**

Should be an object of https://github.com/DSpace/DSpace/blob/master/dspace-spring-rest/src/main/java/org/dspace/app/rest/repository/EPersonRestRepository.java

### Group
**/api/authz/resourcepolicies/<:id>/group**

Should be an object of https://github.com/DSpace/DSpace/blob/master/dspace-spring-rest/src/main/java/org/dspace/app/rest/repository/GroupRestRepository.java

### Resource
**/api/authz/resourcepolicies/<:id>/resource**

Should be the DSO
