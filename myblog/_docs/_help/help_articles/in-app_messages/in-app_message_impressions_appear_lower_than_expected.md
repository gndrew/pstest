---
nav_title: In-App Message Impressions Appear Lower Than Expected
page_order: 1
---
# In-App Message Impressions Appear Lower Than Expected

If your impressions are lower than you'd like them to be, we recommend you...

* [Check Segment](#segment-size)
* [Check Changelogs](#segment-changelogs)
* [Run Tests](#run-tests)
* [Check Event Triggers](#event-triggers)
* [Check Message Impressions](#message-impressions)

## Segment Size

It’s important to ensure that your Segment size in the Campaign reflects your intended audience. Perhaps there are filters applied limiting your audience and causing your campaign to have fewer impressions.

## Segment Changelogs

If the impression count is low compared to where it once was, make sure no one unintentionally altered the Segment or Campaign since launch. Our Segment and Campaign changelogs will give you insight into changes that have been made, who made the change, and when it happened.

![trouble4][10]

## Run Tests

A quick way to identify any obvious issues is to clone the Campaign and target your own userid/email and launch the Campaign. Once you perform the message trigger (Session Start, Custom Event, etc.), verify that you receive the message correctly. Then, navigate to the dashboard and refresh the page to see if your impression is logged correctly. If it is not, then the problem is likely within your implementation.


## Event Triggers

If the campaign is triggered by a Session Start or a Custom Event, you will want to ensure that this event or session is happening frequently enough to actually trigger the message. You can check this data on the App Usage (for session data) or Custom Events pages:


![trouble5][11]

## Message Impressions

Customization of the In-App Message UI or delivery mechanisms within the SDK may require your developers to utilize our methods to manually log In-App message impressions. Check with your developers to see if you use In-App message customization.

You can read more about this:
  * [iOS][12] In-app message documentation
  * [Android][13] In-app message documentation

Still need help? [Open a support ticket]({{site.baseurl}}/support_contact/).


[10]: {% image_buster /assets/img_archive/trouble4.png %}
[11]: {% image_buster /assets/img_archive/trouble5.png %}
[12]: {{site.baseurl}}/developer_guide/platform_integration_guides/ios/in-app_messaging/customization/#logging-impressions-and-clicks
[13]: {{site.baseurl}}/developer_guide/platform_integration_guides/android/in-app_messaging/customization/#setting-custom-listeners
