---
nav_title: "POST: External ID Remove"
page_order: 2

layout: api_page

page_type: reference
platform: API

description: "This article outlines details about the external IDs Remove endpoint."
---
{% api %}
# External ID Remove
{% apimethod post %}
/users/external_ids/remove
{% endapimethod %}

{% alert note %}
For security purposes, this feature is disabled by default. To enable this feature, please reach out to your Success Manager.
{% endalert %}

Use this endpoint to remove your users' old deprecated external IDs. This endpoint completely removes the deprecated ID and cannot be undone.

You can send up to 50 external IDs per request.

You will need to create a new [API key]({{site.baseurl}}/api/api_key/) with permissions for this endpoint.

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
  "external_ids" : (required, array of external IDs to remove)
}
```

### Request Example
```
curl --location --request POST 'https://rest.iad-01.braze.com/users/external_ids/remove' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_REST_API_KEY' \
--data-raw '{
  "external_ids" : 
    [
      "your_existing_deprecated_external_id_string",
      ...
    ]
}'
```
{% alert important %}
Only deprecated IDs can be removed; attempting to remove a primary external ID will result in an error.
{% endalert %}

## Response Body
The response will confirm all successful removals, as well as unsuccessful removals with the associated errors. Error messages in the `removal_errors` field will reference the index in the array of the original request.

```
{

  "message" : (string) status message,
  "removed_ids" : (array of successful Remove Operations),
  "removal_errors": (array of any <minor error message>)

}
```

The `message` field will return `success` for any valid request. More specific errors are captured in the `removal_errors` array. The `message` field returns an error in the case of:
- Invalid API key
- Empty `external_ids` array
- `external_ids` array with more than 50 items
- Rate limit hit (>1,000 requests/minute)

{% endapi %}
