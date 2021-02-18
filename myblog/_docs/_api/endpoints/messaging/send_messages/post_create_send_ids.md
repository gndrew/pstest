---
nav_title: "POST: Create Send IDs"
page_order: 4

layout: api_page

page_type: reference
platform: API
tool:
  - Canvas
  - Campaigns

description: "This article outlines details about the Create Send IDs Braze endpoint."
---
{% api %}
# Create Send IDs For Message Send Tracking
{% apimethod post %}
/sends/id/create
{% endapimethod %}

Braze’s Send Identifier adds the ability to send messages and track message performance entirely programmatically, without campaign creation for each send. Using the Send Identifier to track and send messages is useful if you are planning to programmatically generate and send content.

The daily maximum number of custom send identifiers that can be created via this endpoint for a given app group is 100. Each send id - campaign id combination that you create will count towards your daily limit. The response headers for any valid request include the current rate limit status, see [API Limits]({{site.baseurl}}/api/basics/#api-limits).


{% apiref swagger %}https://www.braze.com/docs/api/interactive/#/Messaging/CreateSendIdsForMessageSendTracking {% endapiref %}
{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#74a04e53-659f-4473-abc5-0f6f735550ff {% endapiref %}

{% alert important %}
__Looking for the `api_key` parameter?__<br>As of May 2020, Braze has changed how we read API keys to be more secure. Now API keys must be passed as a request header, please see `YOUR_REST_API_KEY` within the __Example Request__ below.<br><br>Braze will continue to support the `api_key` being passed through the request body and URL parameters, but will eventually be sunset. Please update your API calls accordingly.
{% endalert %}


## Request Body

```
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
```

```json
{
  "campaign_id": (required, string) see Campaign Identifier,
  "send_id": (required, string) see Send Identifier
}
```

### Request Parameters

| Parameter | Required | Data Type | Description |
| --------- | ---------| --------- | ----------- |
|`campaign_id`|Required|String|See Campaign Identifier|
|`send_id`| Optional | String | See Send Identifier |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

### Request Components
- [Campaign Identifier]({{site.baseurl}}/api/identifier_types/)

### Example Request
```
curl --location --request POST 'https://rest.iad-01.braze.com/sends/id/create' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_REST_API_KEY' \
--data-raw '{
"campaign_id": "",
"send_id": ""
}'
```

## Response

```json
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
{
  "message": "success",
  "send_id" : "example_send_id"
}
```

{% endapi %}
