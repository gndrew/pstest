---
nav_title: "POST: Update Email Template"
page_order: 4

layout: api_page

page_type: reference
platform: API
channel:
  - Email
tool:
  - Canvas
  - Campaigns

description: "This article outlines details about the Update Email Template Braze endpoint."
---
{% api %}
# Update Existing Email Templates
{% apimethod post %}
/templates/email/update
{% endapimethod %}

Use the Template REST APIs to programmatically manage the email templates that you have stored on the Braze dashboard, on the Templates & Media page. Braze provides two endpoints for creating and updating your email templates.

Use the endpoints below to update email templates on the Braze dashboard. You can access an email template's `email_template_id` by navigating to it on the Templates and Media page. The email template creation API endpoint will also return an `email_template_id` reference.

All fields other than the `email_template_id` are optional, but you must specify at least one field to update.

{% apiref swagger %}https://www.braze.com/docs/api/interactive/#/Email%20Templates/UpdateEmailTemplate {% endapiref %}
{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#680315e8-32d4-4a3d-81b6-0085a91b9cdc {% endapiref %}

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
  "email_template_id": (required, string) your email template's API Identifier,
  "template_name": (optional, string) the name of your email template,
  "subject": (optional, string) the email template subject line,
  "body": (optional, string) the email template body that may include HTML,
  "plaintext_body": (optional, string) a plaintext version of the email template body,
  "preheader": (optional, string) the email preheader used to generate previews in some clients,
  "tags": (optional, array of Strings) Tags must already exist
  "should_inline_css": (optional, Boolean) One of 'true' or 'false' is expected
}
```

### Request Parameters

| Parameter | Required | Data Type | Description |
| --------- | ---------| --------- | ----------- |
|`email_template_id`| Required |String|Your email template's API Identifier.|
|`template_name`|Optional|String|The name of your email template|
|`subject`|Optional|String|The email template subject line|
|`body`|Optional|String|The email template body that may include HTML|
|`plaintext_body`|Optional|String|A plaintext version of the email template body|
|`preheader`|Optional|String|The email preheader used to generate previews in some clients|
|`should_inline_css`|Optional|Boolean|Enables or disables the 'inline_css' feature per template.  If  not provided, Braze will use the default setting for the AppGroup.  One of 'true' or 'false' is expected|
|`tags`|Optional|String|Tags must already exist|
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

### Request Components
- [Template Identifier]({{site.baseurl}}/api/identifier_types/)

### Request Example
```
curl --location --request POST 'https://rest.iad-01.braze.com/templates/email/update' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_REST_API_KEY' \
--data-raw '{
  "email_template_id": "ab1cde55-fg47-4h3i-8297-158jk3l2466m",
  "template_name": "Weekly Newsletter",
  "subject": "This Week'\''s Styles",
  "body": "Check out this week'\''s digital lookbook to inspire your outfits. Take a look at https://www.braze.com/",
  "plaintext_body": "This is the updated text within my email body and here is a link to https://www.braze.com/.",
  "preheader": "We want you to have the best looks this Summer",
  "tags": ["Tag1", "Tag2"],
  "should_inline_css": false
}'
```

### Possible Errors
- `Template Name is required`

- `Tags must be an array.`

- `All Tags must be Strings.`

- `Some Tags could not be found.`

- `"Invalid value for 'should_inline_css'.  One of 'true' or 'false' was expected"` - 'should_inline_css' accepts boolean characters only.  The error likely is being shown as the value is being sent as a 'string'.


{% endapi %}
