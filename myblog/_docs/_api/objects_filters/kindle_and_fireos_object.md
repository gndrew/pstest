---
nav_title: "Kindle and FireOS Push Object"
page_order: 7

page_type: reference

channel: Push
platform:
  - API
  - Android
  - FireOS
  - Kindle

tool:
  - Campaigns
  - Canvas

description: "This article explains the different components of Braze's Kindle or FireOS Object."
---

# Kindle and FireOS Push Object

```json
{
   "alert": (required, string) the notification message,
   "title": (required, string) the title that appears in the notification drawer,
   "extra": (optional, object) additional keys and values to be sent in the push,
   "message_variation_id": (optional, string) used when providing a campaign_id to specify which message variation this message should be tracked under (must be an Kindle/FireOS Push Message),
   "priority": (optional, integer) the notification priority value,
   "collapse_key": (optional, string) the collapse key for this message,
   // Specifying "default" in the sound field will play the standard notification sound
   "sound": (optional, string) the location of a custom notification sound within the app,
   "custom_uri": (optional, string) a web URL, or Deep Link URI
}
```

The `priority` parameter will accept values from `-2` to `2`, where `-2` represents "MIN" priority and `2` represents "MAX". `0` is the "DEFAULT" value. Any values sent that outside of that integer range will default to `0`.
