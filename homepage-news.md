# Homepage News Endpoints
[Back to the list of all defined endpoints](endpoints.md)

## Main Endpoint
**/api/config/pages**   

Provide access to the list of all static pages (currently home page news only). These are pages not specific to any items. The design of the REST contract should allow it to be extended to e.g. images as well.
Because the XMLUI supports home page news per language, multiple pages can be created here.

Example:
```json
{
  "_embedded": {
    "pages": [
      {
        "id": "004a297e-fd06-4662-ae51-73e4b7c165c8",
        "name": "home-page-news",
        "title": "DSpace Demo Repository",
        "sizeBytes": 234,
        "language": "en",
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/content"
          },
          "format": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/format"
          },
          "dspaceobject": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/sites/f3e266c6-f416-4352-b856-38a1726d573a"
          },
          "self": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8"
          }
        },
        "_embedded": {
          "format": {
            "id": 22,
            "shortDescription": "XHTML",
            "description": "XHTML",
            "mimetype": "text/html; charset=utf-8",
            "supportLevel": 0,
            "internal": false,
            "extensions": null,
            "type": "bitstreamformat",
            "_links": {
              "self": {
                "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/bitstreamformats/22"
              }
            }
          }
        }
      },
      {
        "id": "1054a711-b307-4052-af28-4162d36d2eca",
        "name": "collection-news",
        "title": "News on Open Access",
        "language": "en",
        "sizeBytes": 4131,
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca/content"
          },
          "format": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca/format"
          },
          "dspaceobject": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/collections/16a4b65b-3b3f-4ef5-8058-ef6f5a653ef9"
          },
          "self": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca"
          }
        },
        "_embedded": {
          "format": {
            "id": 22,
            "shortDescription": "XHTML",
            "description": "XHTML",
            "mimetype": "text/html; charset=utf-8",
            "supportLevel": 0,
            "internal": false,
            "extensions": null,
            "type": "bitstreamformat",
            "_links": {
              "self": {
                "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/bitstreamformats/22"
              }
            }
          }
        }
      }
    ]
  }
}
```

## Single page
### View page
**/api/config/pages/<:uuid>**

Provide detailed information about a static page. The JSON response document is as follow
```json
{
  "id": "004a297e-fd06-4662-ae51-73e4b7c165c8",
  "name": "home-page-news",
  "title": "DSpace Demo Repository",
  "sizeBytes": 234,
  "language": "en",
  "type": "page"
}
```

Exposed links:
* format: link to the format resource associated with the file (XHTML, jpeg, etc.). TODO: verify how images can be supported
* content: link to access the actual content of the page
* dspaceobject: link to the community or collection if it's e.g. the collection news. Alternatively link to the site. This can in theory also be used to link to an item

### Edit page: Multipart POST Method
**POST /api/config/pages**

A multipart POST request will result in creating a new file identified by the name.

Send detailed information about a static page, and the actual file. The sizeBytes and uuid is not required, but the other attributes are applicable

```bash
curl --trace-ascii - -X POST "https://dspace7-internal.atmire.com/rest/api/config/pages" \
-H "Authorization: $authorization" \
-F "file=@Downloads/test.html" \
-F 'properties={ "name": "home-page-news", "title": "DSpace Demo Repository", "language": "en" };type=application/json' \
-F "uri-list=https://dspace7-internal.atmire.com/rest/api/core/sites/f3e266c6-f416-4352-b856-38a1726d573a;type=text/uri-list" \
-H 'Content-Type: multipart/form-data'
```

**PUT /api/config/pages/<:uuid>**

A multipart PUT request will result in an update of the file identified by the uuid.

Send detailed information about a static page, and the actual file. The sizeBytes is not required, but the other attributes are applicable

### Delete page
**DELETE /api/config/pages/<:uuid>**

A DELETE request will typically result in deleting the file identified by the uuid. If the file didn't exist yet, the delete will fail

## Linked entities
### Format
**/api/config/pages/<:uuid>/format**

Example: Similar to bitstreams

It returns the format of the resource

### Content
**/api/config/pages/<:uuid>/content**

Example: Similar to bitstreams

It returns the actual content (bits) of the resource

Response Headers:

* **Content-Type**: the mimetype as recorded for the file
* **Content-Length**: the size in bytes of the content

The supported **Request Headers** are:
* If-Modified-Since: 
* If-None-Match: 

### Languages
**/api/config/pages/search/languages?name=<:page-name>**

Example:
```json
{
  "_embedded": {
    "pages": [
      {
        "id": "004a297e-fd06-4662-ae51-73e4b7c165c8",
        "name": "home-page-news",
        "title": "DSpace Demo Repository",
        "sizeBytes": 234,
        "language": "en",
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/content"
          },
          "format": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/format"
          },
          "dspaceobject": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/sites/f3e266c6-f416-4352-b856-38a1726d573a"
          },
          "self": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8"
          }
        },
        "_embedded": {
          "format": {
            "id": 22,
            "shortDescription": "XHTML",
            "description": "XHTML",
            "mimetype": "text/html; charset=utf-8",
            "supportLevel": 0,
            "internal": false,
            "extensions": null,
            "type": "bitstreamformat",
            "_links": {
              "self": {
                "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/bitstreamformats/22"
              }
            }
          }
        }
      },
      {
        "id": "1054a711-b307-4052-af28-4162d36d2eca",
        "name": "home-page-news",
        "title": "DSpace Démo Dépôt",
        "language": "fr",
        "sizeBytes": 0,
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca/content"
          },
          "format": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca/format"
          },
          "dspaceobject": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/sites/f3e266c6-f416-4352-b856-38a1726d573a"
          },
          "self": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca"
          }
        },
        "_embedded": {
          "format": {
            "id": 22,
            "shortDescription": "XHTML",
            "description": "XHTML",
            "mimetype": "text/html; charset=utf-8",
            "supportLevel": 0,
            "internal": false,
            "extensions": null,
            "type": "bitstreamformat",
            "_links": {
              "self": {
                "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/bitstreamformats/22"
              }
            }
          }
        }
      }
    ],
    "_links": {
      "self": {
        "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/search/languages"
      }
    }
  }
}
```

It returns all the language variants of the resource

Parameters:
* The name parameter is mandatory

### DSpace Objects
**/api/config/pages/search/dso?uuid=<:dspaceobject-uuid>**

Example:
```json
{
  "_embedded": {
    "pages": [
      {
        "id": "004a297e-fd06-4662-ae51-73e4b7c165c8",
        "name": "home-page-news",
        "title": "DSpace Demo Repository",
        "sizeBytes": 234,
        "language": "en",
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/content"
          },
          "format": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8/format"
          },
          "dspaceobject": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/sites/f3e266c6-f416-4352-b856-38a1726d573a"
          },
          "self": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/004a297e-fd06-4662-ae51-73e4b7c165c8"
          }
        },
        "_embedded": {
          "format": {
            "id": 22,
            "shortDescription": "XHTML",
            "description": "XHTML",
            "mimetype": "text/html; charset=utf-8",
            "supportLevel": 0,
            "internal": false,
            "extensions": null,
            "type": "bitstreamformat",
            "_links": {
              "self": {
                "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/bitstreamformats/22"
              }
            }
          }
        }
      },
      {
        "id": "1054a711-b307-4052-af28-4162d36d2eca",
        "name": "home-page-news",
        "title": "DSpace Démo Dépôt",
        "language": "fr",
        "sizeBytes": 0,
        "type": "page",
        "_links": {
          "content": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca/content"
          },
          "format": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca/format"
          },
          "dspaceobject": {
            "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/sites/f3e266c6-f416-4352-b856-38a1726d573a"
          },
          "self": {
            "href": "https://dspace7-internal.atmire.com/rest/api/config/pages/1054a711-b307-4052-af28-4162d36d2eca"
          }
        },
        "_embedded": {
          "format": {
            "id": 22,
            "shortDescription": "XHTML",
            "description": "XHTML",
            "mimetype": "text/html; charset=utf-8",
            "supportLevel": 0,
            "internal": false,
            "extensions": null,
            "type": "bitstreamformat",
            "_links": {
              "self": {
                "href": "https://dspace7.4science.it/dspace-spring-rest/api/core/bitstreamformats/22"
              }
            }
          }
        }
      }
    ],
    "_links": {
      "self": {
        "href": "https://dspace7.4science.it/dspace-spring-rest/api/config/pages/search/dso"
      }
    }
  }
}
```

It returns all the pages linked to the DSpace Object

Parameters:
* The uuid parameter is mandatory
* The name parameter is optional
* The language parameter is optional and overrides the preferred language. It can be either a single language or "all"

The preferred language can be defined in the "Accept-Language" header

