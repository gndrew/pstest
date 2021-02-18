---
nav_title: "GET: Canvas Details"
page_order: 4

layout: api_page

page_type: reference
platform: API
tool: Canvas
description: "This article outlines details about the Canvas Details Endpoint."
---
{% api %}
# Canvas Details Endpoint
{% apimethod get %}
/canvas/details
{% endapimethod %}

This endpoint allows you to export metadata about a Canvas, such as its name, when it was created, its current status, and more.

{% apiref swagger %}https://www.braze.com/docs/api/interactive/#/Export/Canvas%20export%20%20details%20example {% endapiref %}
{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#5188873c-13a3-4aaf-a54b-9fa1daeac5f8 {% endapiref %}

{% alert important %}
__Looking for the `api_key` parameter?__<br>As of May 2020, Braze has changed how we read API keys to be more secure. Now API keys must be passed as a request header, please see `YOUR_REST_API_KEY` within the __Example Request__ below.<br><br>Braze will continue to support the `api_key` being passed through the request body and URL parameters, but will eventually be sunset. Please update your API calls accordingly.
{% endalert %}

## Request Parameters

| Parameter   | Required | Data Type | Description            |
| ----------- | -------- | --------- | ---------------------- |
| `canvas_id` | Yes      | String    | Canvas API Identifier  |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

### Request Components
- [Canvas Identifier]({{site.baseurl}}/api/identifier_types/)

## Example Request
```
curl --location --request GET 'https://rest.iad-01.braze.com/canvas/details?canvas_id=3bbc4555-8fa0-4c9b-a5c0-4505edf3e064' \
--header 'Authorization: Bearer YOUR_REST_API_KEY'
```

## Response

```json
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
{
  "created_at": (string) date created as ISO 8601 date,
  "updated_at": (string) date updated as ISO 8601 date,
  "name": (string) Canvas name,
  "description": (string) Canvas description,
  "archived": (boolean) whether this Canvas is archived,
  "draft": (boolean) whether this Canvas is a draft,
  "schedule_type": (string) type of scheduling action,
  "first_entry": (string) date of first entry as ISO 8601 date,
  "last_entry": (string) date of last entry as ISO 8601 date,
  "channels": (array of strings) step channels used with Canvas,
  "variants": [
    {
      "name": (string) name of variant,
      "id": (string) API identifier of the variant,
      "first_step_ids": (array of strings) API identifiers for first steps in variant,
      "first_step_id": (string) API identifier of first step in variant (deprecated in November 2017, only included if the variant has only one first step)
    },
    ... (more variations)
  ],
  "tags": (array of strings) tag names associated with the Canvas,
  "steps": [
    {
      "name": (string) name of step,
      "id": (string) API identifier of the step,
      "next_step_ids": (array of strings) API identifiers of steps following step,
      "channels": (array of strings) channels used in step,
      "messages": {
          "message_variation_id": (string) {  // <=This is the actual id
              "channel": (string) channel type of the message (eg., "email"),
              ... channel-specific fields for this message, see Campaign Details Endpoint API Response for example message responses ...
          }
      }
    },
    ... (more steps)
  ],
  "message": (required, string) the status of the export, returns 'success' when completed without errors
}
```
{% alert tip %}
For help with CSV and API exports, visit our troubleshooting article [here]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
