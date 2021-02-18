---
nav_title: "GET: List Upcoming Scheduled Campaigns and Canvases"
page_order: 4

layout: api_page

page_type: reference
platform: API
tool:
  - Canvas
  - Campaigns

description: "This article outlines details about the Get Scheduled Messages Braze endpoint."
---
{% api %}
# Get Upcoming Scheduled Campaigns and Canvases
{% apimethod get %}
/messages/scheduled_broadcasts
{% endapimethod %}

You can view a JSON list of upcoming and scheduled Campaigns and Canvases using the following information and parameters. The endpoint will return information about scheduled Campaigns and entry Canvases between now and the designated `end_time` specified in the request. Daily, recurring messages will only appear once with their next occurrence. Results returned in this endpoint are only for Campaigns and Canvases created and scheduled in Braze.

{% apiref swagger %}https://www.braze.com/docs/api/interactive/#/Messaging/GetUpcomingScheduledCampaignsAndCanvases {% endapiref %}
{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#6f623cc3-383b-4bf7-b14d-7c56fc5562f5 {% endapiref %}

{% alert important %}
__Looking for the `api_key` parameter?__<br>As of May 2020, Braze has changed how we read API keys to be more secure. Now API keys must be passed as a request header, please see `YOUR_REST_API_KEY` within the __Example Request__ below.<br><br>Braze will continue to support the `api_key` being passed through the request body and URL parameters, but will eventually be sunset. Please update your API calls accordingly.
{% endalert %}

## Request Parameters

| Parameter | Required | Data Type | Description |
| --------- | -------- | --------- | ----------- |
| `end_time` | Yes | String in ISO 8601 format | End date of the range to retrieve upcoming scheduled Campaigns and Canvases. This is treated as midnight in UTC time by the API. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

### Example URL

`https://rest.iad-01.braze.com/messages/scheduled_broadcasts?end_time=2018-09-01T00:00:00-04:00`

### Example Request
```
curl --location --request GET 'https://rest.iad-01.braze.com/messages/scheduled_broadcasts?end_time=2018-09-01T00:00:00-04:00' \
--header 'Authorization: Bearer YOUR_REST_API_KEY'
```

## Response

```json
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
{
    "scheduled_broadcasts": [
      # Example Canvas
      {
        "name" => String,
        "id" => String,
        "type" => "Canvas",
        "tags" => [String tag names],
        "next_send_time" => "YYYY-MM-DD HH:mm:ss" (may also include time zone if not local/intelligent delivery)
        "schedule_type" => one of "local_time_zones", "intelligent_delivery", or the name of your company's time zone
      },
      # Example Campaign
      {
        "name" => String,
        "id" => String,
        "type" => "Campaign",
        "tags" => [String tag names],
        "next_send_time" => "YYYY-MM-DD HH:mm:ss" (may also include time zone if not local/intelligent delivery)
        "schedule_type" => one of "local_time_zones", "intelligent_delivery", or the name of your company's time zone
      },
    ]
}
```

{% endapi %}
