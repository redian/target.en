---
description: Information about Target Server Side delivery APIs, Recommendations APIs, and the NodeJS SDK.
keywords: server side;server-side;api;sdk;nodejs;node js;recommendations api
seo-description: Information about Target Server Side delivery APIs, Recommendations APIs, and the NodeJS SDK.
seo-title: Server Side  implement Target
solution: Target
title: Server Side  implement Target
topic: Recommendations
uuid: 21d321c7-3da4-44a2-a04f-1807cc2a893b
---

# Server Side: implement Target{#server-side-implement-target}

Information about Target Server Side delivery APIs, Server Side Batch Delivery APIs, NodeJS SDK, Target Recommendations APIs, and Target Classic APIs (decommissioned).

The following section lists the various APIs and the NodeJS SDK and provides additional information:

## Server Side Delivery APIs

Link: [Server Side Delivery APIs](https://developers.adobetarget.com/api/#server-side-delivery)

`/rest/v1/mbox`

Adobe Target lets your application make mbox calls from any browser, mobile device, or even another server. The Server Side delivery API is specifically designed to integrate Adobe Target with any server-side platform that makes HTTP/HTTPS calls.

You can use the API to integrate your custom application with Target. This is especially valuable for organizations that want to deliver targeting to a non-browser based IoT device, such as a connected TV, kiosk, or in-store digital screen.

This endpoint can return offers for ordinary mboxes only. You can also fetch content for a single mbox only.

This API implements existing mbox features in a RESTful manner.

This API does not process cookies or redirect calls.

## Server Side Batch Delivery APIs

Link: [Server Side Batch Delivery APIs](https://developers.adobetarget.com/api/#server-side-batch-delivery)

`/rest/v2/batchmbox`

The Batch Delivery API lets your application request content for multiple mboxes in a single call. It also has a prefetch mode that enables clients like mobile apps, servers, and so forth to fetch content for multiple mboxes in one request, cache it locally, and later notify Target when the user visits those mboxes.

This endpoint can return offers for ordinary mboxes only. Because you can fetch content for multiple mboxes, for performance, it makes more sense to use batch the mbox API. It lets you avoid executing multiple HTTP requests, which can be expensive.

## NodeJS SDK

Link: [NodeJS SDK](https://www.npmjs.com/package/@adobe/target-node-client)

In terms of SDKs, currently we have just one SDK, the NodeJS SDK.

The NodeJS SDK is a thin wrapper around the NodeJS core HTTP/HTTPS module. Behind the scenes, the NodeJS SDK APIs use the same Server Side Delivery APIs.

Here is the mapping:

* `MarketingCloudClient.getOffer() \*- invokes \*/res/v1/mbox endpoint`
* `MarketingCloudClient.getOffers() \*- invokes \*/res/v2/batchmbox endpoint`

## Target Recommendations APIs

Link: [Target Recommendations APIs](https://developers.adobetarget.com/api/recommendations)

The Recommendations APIs enable you to programmatically interact with Target's recommendations servers. These APIs can be integrated with a range of application stacks to perform functions that you would typically do via the user interface.

## Target Classic APIs

The Target Classic UI and APIs have been decommissioned. For information about switching to Target’s modern APIs, see [Transitioning from Target Legacy APIs to Adobe I/O](../../c-implementing-target/c-api-and-sdk-overview/target-api-documentation.md#concept_3A31E26C8FAF49598152ACFE088BD4D2).

>[!NOTE]
>Authoring APIs (in which you create activities, offers, audiences, and so forth) do not support Cross Origin Resource Sharing (CORS).

## Differences Between Server Side Delivery APIs and the NodeJS SDK {#section_10336B7934F54CE98E35907A4748A4A4}

Many customers are confused about the differences between the Server Side delivery APIs and the NodeJS SDK. This is especially true when it comes to performance.

The following FAQs should help you decide which to use:

**When should you use "raw" Server Side APIs versus the NodeJS SDK?**

Ideally if you are using NodeJS as your backend technology, NodeJS SDK is a natural choice. The SDK handles a lot of details, such as cookies, headers, payload, and so forth. This lets you focus on the core of your application.

**Should I gain any performance improvements by using the NodeJS SDK?**

Unfortunately, we don't have any performance numbers. However, in general, the NodeJS SDK should have good performance, thanks to the NodeJS event-driven architecture. Be aware that most of the time is spent on the Target backend. The NodeJS SDK does very little processing. The SDK is basically responsible for packaging a Target request and parsing a Target response. 
