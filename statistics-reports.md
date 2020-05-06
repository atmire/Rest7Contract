# Displaying usage statistics
[Back to the list of all defined endpoints](endpoints.md)

## Statistics for a DSpaceObject
**GET /api/statistics/reports**

This endpoint provides a paginated list of statistics for a DSpaceObject. 

The DSpaceObject is given through the following parameters:
- `scope` The UUID of the DSpaceObject
- `scopeType` The string type of the DSpaceObject 

The usual parameters for paginated lists are supported as well:
- `page` The page number 
- `size` The number of statistics in a page

An example JSON response document to `/api/statistics/reports?page=0&size=2&scopeType=site&scope=6d65c6a2-3fe7-44dd-bacb-79271257c35d`:

```json
{
    "_embedded": {
        "reports": [
            {
                "id": "TotalVisits",
                "type": "report",
                "report-type": "TotalVisits",
                "points": [
                    {
                        "label": "cad835c8-0cae-4769-a08a-857f0f814020",
                        "type": "item",
                        "id": "cad835c8-0cae-4769-a08a-857f0f814020",
                        "values": {
                            "views": 3313
                        }
                    },
                    {
                        "label": "6759d5e0-3915-4864-917c-1940bdb75fbd",
                        "type": "item",
                        "id": "6759d5e0-3915-4864-917c-1940bdb75fbd",
                        "values": {
                            "views": 3308
                        }
                    },
                    {
                        "label": "b0f6ce54-2ed8-4b67-a075-64794abb4e82",
                        "type": "item",
                        "id": "6759d5e0-3915-4864-917c-1940bdb75fbd",
                        "values": {
                            "views": 1800
                        }
                    }
                ]
            }
        ]
    }
}
```

An example JSON response document to `/api/statistics/reports?scopeType=item&scope=1911e8a4-6939-490c-b58b-a5d70f8d91fb`:

```json
{
    "_embedded": {
        "reports": [
            {
                "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalVisits",
                "points": [
                    {
                        "label": "1911e8a4-6939-490c-b58b-a5d70f8d91fb",
                        "type": "item",
                        "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb",
                        "values": {
                            "views": 3
                        }
                    }
                ]
            },
            {
                "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalVisitsPerMonth",
                "points": [
                    {
                        "label": "March 2020",
                        "type": "date",
                        "id": "2020-03",
                        "values": {
                            "views": 0
                        }
                    },
                    {
                        "label": "April 2020",
                        "type": "date",
                        "id": "2020-04",
                        "values": {
                            "views": 0
                        }
                    },
                    {
                        "label": "May 2020",
                        "type": "date",
                        "id": "2020-05",
                        "values": {
                            "views": 3
                        }
                    }
                ]
            },
            {
                "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TotalDownloads",
                "points": [
                    {
                        "label": "8d33bdfb-e7ba-43e6-a93a-f445b7e8a1e2",
                        "type": "bitstream",
                        "id": "8d33bdfb-e7ba-43e6-a93a-f445b7e8a1e2",
                        "values": {
                            "downloads": 8
                        }
                    }
                ]
            },
            {
                "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries",
                "points": [
                    {
                        "label": "United States",
                        "type": "country",
                        "id": "US",
                        "values": {
                            "views": 2
                        }
                    },
                    {
                        "label": "China",
                        "type": "country",
                        "id": "CN",
                        "values": {
                            "views": 1
                        }
                    }
                ]
            }
        ]
    }
}
```

Possible response status:
* 200 OK - The DSpaceObject was found, and the data has been properly returned.
* 400 Bad Request - The scope or scopeType parameter format is incorrect

## Single statistic
**GET /api/statistics/reports/<:id>**

This endpoint provides a specific statistic

An example JSON response document to `/api/statistics/reports/1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries`:
```
{
    "id": "1911e8a4-6939-490c-b58b-a5d70f8d91fb_TopCountries",
    "points": [
        {
            "label": "United States",
            "type": "country",
            "id": "US",
            "values": {
                "views": 2
            }
        },
        {
            "label": "China",
            "type": "country",
            "id": "CN",
            "values": {
                "views": 1
            }
        }
    ]
}
```

Possible response status

- 200 OK - The specific statistics data was found, and the data has been properly returned.
- 404 Not Found - The specified ID was not found