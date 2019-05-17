# Bitstream Formats Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**GET /api/core/bitstreamformats**   

Provide access to the bitstream formats defined in the registry (DBMS based). It returns the list of existent metadata fields.

Example: <https://dspace7.4science.cloud/dspace-spring-rest/#https://dspace7.4science.cloud/dspace-spring-rest/api/core/bitstreamformats>

**POST /api/core/bitstreamformats**   

Create a new bitstream format in the registry (DBMS based). Requires an admin account

The JSON should be similar to:
```json
{
  "shortDescription": "XML",
  "description": "Extensible Markup Language",
  "mimetype": "text/xml",
  "supportLevel": 1,
  "internal": false,
  "extensions": [
    {
      "xml"
    }
  ],
  "type": "bitstreamformat"
}
```

Status codes:
* 201 Created - if the operation succeed
* 401 Forbidden - if you are not authenticated
* 403 Unauthorized - if you are not logged in with sufficient permissions

## Single Bitstream Format
**GET /api/core/bitstreamformats/<:id>**

Provide detailed information about a specific bitstream format. The JSON response document is as follow
```json
{
  "id": "8",
  "shortDescription": "XML",
  "description": "Extensible Markup Language",
  "mimetype": "text/xml",
  "supportLevel": 1,
  "internal": false,
  "extensions": [
    {
      "xml"
    }
  ],
  "type": "bitstreamformat",
  "_links": {
    "self": {
      "href": "https://dspace7.4science.cloud/dspace-spring-rest/api/core/bitstreamformats/5"
    }
  }
}
```

Exposed links:
* self

**PUT /api/core/bitstreamformats/<:id>**

Updates a specific bitstream format. Requires an admin account. The JSON should be similar to:
```json
{
  "id": "8",
  "shortDescription": "XML",
  "description": "Extensible Markup Language",
  "mimetype": "text/xml",
  "supportLevel": 0,
  "internal": false,
  "extensions": [
    {
      "xml"
    }
  ],
  "type": "bitstreamformat"
}
```

Status codes:
* 201 Created - if the operation succeed
* 401 Forbidden - if you are not authenticated
* 403 Unauthorized - if you are not logged in with sufficient permissions
* 404 Not found - if the bitstream format doesn't exist

**DELETE /api/core/bitstreamformats/<:id>**

Deletes a specific bitstream format. Requires an admin account. No JSON details are required.

Status codes:
* 204 No content - if the operation succeed
* 401 Forbidden - if you are not authenticated
* 403 Unauthorized - if you are not logged in with sufficient permissions
* 404 Not found - if the bitstream format doesn't exist (or was already deleted)
