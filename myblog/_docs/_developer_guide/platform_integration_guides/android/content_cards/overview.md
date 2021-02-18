---
nav_title: Overview
page_order: 0

platform: Android
---

# Content Cards 

{% include video.html id="4FUPxkIq2xc" align="right" %}

With **Content Cards**, you can send a highly targeted, dynamic stream of rich content to your customers right within the apps they love, without interrupting their experience. Also, Content Cards support more personalized features, including card pinning, card dismissal, API-based delivery, custom card expiration times, card analytics, and easy coordination with push notifications. <br><br>Note that Content Cards are __not__ available out-of-the-box and must be purchased. To get started with Content Cards, reach out to your Customer Success Manager for more information.

{% alert note %}
Braze recommends that customers who use our News Feed tool, move over to our Content Cards messaging channel - it is more flexible, customizable, and reliable. It is also easier to find and use in the Braze product. Contact your Braze account manager for more information.
{% endalert %}

## When to Use Content Cards

Content Cards typically sit in a feed of sorts (but not necessarily) and help you take advantage of the visual space by incorporating images and graphics that stand out. You can personalize the cards based on user actions, onboard your customers with a checklist, and much more!

### Great Use Cases

- Showcase new content.
- Coordinate with push messages to illustrate a persistent record of promotions.
- Give customers without push enabled access to promotions.
- Trigger order confirmations or other personalized communication with your customer.
- Develop and deliver an onboarding schedule.

## Content Cards & Feed

This is what it looks like for your users to open a basic Content Card feed. As you can see, three basic types of cards can sit in the feed - __a Banner Card, a Captioned Content Card, and a Classic Content Card__. Note that the Classic Content Card includes two types of sub cards, a Text Announcement Card (a classic card without text) and a Short News Card (a classic card with text and an image). Visit our Content Card [data models article]({{site.baseurl}}/developer_guide/platform_integration_guides/android/content_cards/data_models/) to learn more.

![Content Cards Feed]({% image_buster /assets/img/sample-torchy-feed-content-cards-braze.png %}){: style="max-width:40%;"}

{% alert note %}
Content Cards have a maximum size of **2kb** (including images, links, and all content) - exceeding that amount will prevent the card from sending.
{% endalert %}

## Content Cards Integration Overview {#content-cards-integration-for-android}

In Android, the Content Cards feed is implemented as a [Fragment][2] that are available in the Braze Android UI project. View [Google's documentation on Fragments][3] for information on how to add a Fragment to an Activity.

The [`AppboyContentCardsFragment`][4] class will automatically refresh and display the contents of the Content Cards and log usage analytics. The cards that can appear in a user's ContentCards are created on the Braze dashboard.

[2]: http://developer.android.com/guide/components/fragments.html
[3]: http://developer.android.com/guide/components/fragments.html#Adding "Android Documentation: Fragments"
[4]: https://appboy.github.io/appboy-android-sdk/javadocs/com/appboy/ui/AppboyContentCardsFragment.html
