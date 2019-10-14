# Harvesting metadata configuration Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/config/harvestermetadata**   

Provide access to the list of harvesting metadata configurations (config based).

Example: <http://dspace7.4science.it/dspace-spring-rest/#/dspace-spring-rest/api/config/harvestermetadata>


A sample json response:

```json
{
  "configs": [
    {
       "id": "dc",
       "label": "Simple Dublin Core",
       "nameSpace": "http://www.openarchives.org/OAI/2.0/oai_dc/"
    },
    {
       "id": "qdc",
       "label": "Qualified Dublin Core",
       "nameSpace": "http://purl.org/dc/terms/"
    },
    {
       "id": "dim",
       "label": "DSpace Intermediate Metadata",
       "nameSpace": "http://www.dspace.org/xmlns/dspace/dim"
    }
  ],
  "_links": {
    "self": {
      "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/harvestermetadata"
    }
  }
}
```
