---
title: View Search Results by Page
description: Learn how to view search results page by page and include totals.
topics:
  - users
  - user-management
  - search
contentType: how-to 
useCase:
  - manage-users
---
# View Search Results by Page

To page the user search results, use the `page`, `per_page`, and `include_totals` parameters at your request.

Parameter | Description
----------|------------
`page` | The page number, zero based. When this is not set, we return a maximum of 50 records, regardless of how many records exist.
`per_page` | The amount of users per page.
`include_totals` | Set to `true` to include a query summary as part of the result.

## Sample request

```har
{
    "method": "GET",
    "url": "https://${account.namespace}/api/v2/users",
    "httpVersion": "HTTP/1.1",
    "headers": [{
        "name": "Authorization",
        "value": "Bearer YOUR_MGMT_API_ACCESS_TOKEN"
    }],
    "queryString":  [
        {
          "name": "q",
          "value": "logins_count:[100 TO 200]"
        },
        {
          "name": "page",
          "value": "2"
        },
        {
          "name": "per_page",
          "value": "10"
        },
        {
          "name": "include_totals",
          "value": "true"
        },
        {
          "name": "search_engine",
          "value": "v3"
        }
    ]
}
```

## Sample response

A sample response body for the values set in the above sample request is as follows:

```json
{
    "start": 20,
    "limit": 10,
    "length": 10,
    "users": [
        {
            ...
        }
    ],
    "total": 79
}
```

Paramater | Description
----------|------------
`start`   | Record position from which the page starts.
`limit`   | Maximum number of records that can be shown on the page.
`length`  | Number of records shown on the page.
`total`   | Total number of records found.

## Limitation

Auth0 limits the total number of users you can retrieve to 1000 (for example, 100 users per page for 10 pages). When the `page` parameter is not set, we return a maximum of 50 records, regardless of how many records exist.

## Keep reading

For more information on the `page`, `per_page` and other parameters, see the [Management API Explorer](/api/management/v2#!/Users/get_users) documentation.
