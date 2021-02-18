---
nav_title: "POST: External ID Rename"
page_order: 1

layout: api_page

page_type: reference
platform: API

description: "This article outlines details about the external IDs Rename endpoint."
---
{% api %}
# External ID Rename
{% apimethod post %}
/users/external_ids/rename
{% endapimethod %}

{% alert note %}
For security purposes, this feature is disabled by default. To enable this feature, please reach out to your Success Manager.
{% endalert %}

Use this endpoint to "rename" your users' external IDs. This endpoint sets a new (primary) `external_id` for the user and deprecates their existing `external_id`. This means that the user can be identified by either `external_id` until the deprecated one is removed. The deprecated ID can be removed using the [remove]({{site.baseurl}}/api/endpoints/user_data/external_id_migration/post_external_ids_remove) endpoint. Having multiple external IDs allows for a migration period whereby older versions of your apps still in the wild that use the previous external ID naming schema don’t break. We highly recommend removing deprecated external IDs once your old naming schema is no longer in use.

You can send up to 50 rename objects per request.

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
  "external_id_renames" : (required, array of external ID Renames Object)
  [
    {
      "current_external_id" : (required, string) existing external ID for the user,
      "new_external_id" : (required, string) new external ID for the user, must be unique
    },
    ...
  ]
}
```

### Request Example
```
curl --location --request POST 'https://rest.iad-01.braze.com/users/external_ids/rename' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_REST_API_KEY' \
--data-raw '{
  "external_id_renames" : 
  [
    {
      "current_external_id": "your_existing_external_id",
      "new_external_id" : "your_new_external_id"
    }
  ]
}'
```
{% alert important %}
- The `current_external_id` must be the user’s primary ID, and cannot be a deprecated ID
- The `new_external_id` must not already be in use as either a primary ID or a deprecated ID
- The `current_external_id` and `new_external_id` cannot be the same
{% endalert %}

## Response Body
The response will confirm all successful renames, as well as unsuccessful renames with any associated errors. Error messages in the `rename_errors` field will reference the index of the object in the array of the original request.

```
{

  "message" : (string) status message,
  "external_ids" : (array of successful Rename Operations),
  "rename_errors": (array of any <minor error message>)

}
```

The `message` field will return `success` for any valid request. More specific errors are captured in the `rename_errors` array. The `message` field returns an error in the case of:
- Invalid API key
- Empty `external_id_renames` array
- `external_id_renames` array with more than 50 objects
- Rate limit hit (>1,000 requests/minute)

## Frequently Asked Questions

__Does this impact MAU?__
- No, since the number of users will stay the same, they’ll just have a new `external_id`.

__Does user behavior change historically?__
- No, since the user is still the same user, and all their historical behavior is still connected to them.

__Can it be run on dev/staging app groups?__
- Yes. In fact, we highly recommend running a test migration on a staging or development app group, and ensuring everything has gone smoothly before executing on production data.

__Does this consume data points?__
- This feature does not cost data points.

__What is the recommended deprecation period?__
- We have no hard limit on how long you can keep deprecated external IDs around, but we highly recommend removing them once there is no longer a need to reference users by the deprecated ID.

{% endapi %}
