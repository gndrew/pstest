---
nav_title: Logging Purchases
platform: React Native
subplatform: iOS
page_order: 3
---
## Logging Purchases

See [the iOS integration instructions][1] for in depth discussion of revenue tracking best practices and interfaces.

```javascript
var properties = {};
properties["KeyOne"] = "ValueOne";
ReactAppboy.logPurchase("testPurchaseWithNullCurrency", 10, null, 5, properties);
```

[1]: {{site.baseurl}}/developer_guide/platform_integration_guides/ios/analytics/logging_purchases/
