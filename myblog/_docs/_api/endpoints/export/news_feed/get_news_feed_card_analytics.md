---
nav_title: "GET: News Feed Card Analytics"
page_order: 4

layout: api_page

page_type: reference
channel: News Feed
platform: API
tool: Segments
description: "This article outlines details about and using the Segments List endpoint to export a list of available Segments."
---
{% api %}
# News Feed Card Analytics Endpoint
{% apimethod get %}
/feed/data_series
{% endapimethod %}

This endpoint allows you to retrieve a daily series of engagement stats for a card over time.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#9cdc3b1e-641e-4d62-b9e8-42d04ee9d4d8 {% endapiref %}

{% alert important %}
__Looking for the `api_key` parameter?__<br>As of May 2020, Braze has changed how we read API keys to be more secure. Now API keys must be passed as a request header, please see `YOUR_REST_API_KEY` within the __Example Request__ below.<br><br>Braze will continue to support the `api_key` being passed through the request body and URL parameters, but will eventually be sunset. Please update your API calls accordingly.
{% endalert %}

## Request Parameters

| Parameter   | Required | Data Type | Description |
| ----------- | -------- | --------- | ----------- |
| `card_id`   | Yes      | String    | Card API Identifier |
| `length`    | Yes      | Integer   | Max number of units (days or hours) before ending_at to include in the returned series - must be between 1 and 100 inclusive |
| `unit`      | No       | String   | Unit of time between data points - can be "day" or "hour" (defaults to "day")  |
| `ending_at` | No       | DateTime (ISO 8601 string) | Date on which the data series should end - defaults to time of the request |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

### Request Components
- [Card ID]({{site.baseurl}}/api/identifier_types/)
- [News Feed List]({{site.baseurl}}/api/endpoints/export/news_feed/get_news_feed_cards/)
<br><br>
The `card_id` for a given card can be found in the Developer Console page and on the card details page within your dashboard or you can use the [News Feed List Endpoint](#news-feed-list).

### Example URL
`https://rest.iad-01.braze.com/feed/data_series?card_id=3bbc4555-8fa0-4c9b-a5c0-4505edf3e064&length=14&unit=day&ending_at=2018-06-28T23:59:59-5:00`

### Example Request
```
curl --location --request GET 'https://rest.iad-01.braze.com/feed/data_series?card_id=3bbc4555-8fa0-4c9b-a5c0-4505edf3e064&length=14&unit=day&ending_at=2018-06-28T23:59:59-5:00' \
--header 'Authorization: Bearer YOUR_REST_API_KEY'
```

## Response

```json
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "data" : [
        {
            "time" : (string) point in time - as ISO 8601 extended when unit is "hour" and as ISO 8601 date when unit is "day",
            "clicks" : (int) ,
            "impressions" : (int),
            "unique_clicks" : (int),
            "unique_impressions" : (int)
        },
        ...
    ]
}
```
{% alert tip %}
For help with CSV and API exports, visit our troubleshooting article [here]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
