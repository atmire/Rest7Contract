# Bitstream Formats Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**GET /api/core/bitstreamformats**   

Provide access to the bitstream formats defined in the registry (DBMS based). It returns the list of existent metadata fields.

Example: <https://dspace7-internal.atmire.com/rest/#https://dspace7-internal.atmire.com/rest/api/core/bitstreamformats>

**POST /api/core/bitstreamformats**   

Create a new bitstream format in the registry (DBMS based). Requires an admin account

The JSON should be similar to:
```json
{
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

## Single Bitstream Format
**GET /api/core/bitstreamformats/<:id>**

Provide detailed information about a specific bitstream format. The JSON response document is as follow
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
  "type": "bitstreamformat",
  "_links": {...}
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

**DELETE /api/core/bitstreamformats/<:id>**

Deletes a specific bitstream format. Requires an admin account. No JSON details are required.
