# Get images and video into the ad account

The designer sent three new statics and a 15-second cut this morning, and they need to be in the account before the ad can be built.

## Ask this

```
Upload these to my Meta ad account and give me back the id or hash for each:
- the image at <public image URL>
- the video file at <path to the file on my machine>
Then show me the account's uploaded images and videos so I can confirm they landed.
```

## What comes back

One line per asset, carrying the reference you will reuse. Ids below are made up.

```
image   hash 4f2c…            uploaded
video   id 46200000000000     uploaded
```

| Asset | Type | Reference to reuse |
|---|---|---|
| `<image file name>` | image | image hash |
| `<video file name>` | video | video id |

## How to read it

Keep the hash (images) or the id (videos) that comes back. That reference is what the ad build uses, and asking for the account's uploaded assets later gets it back for you.

Two sources work: a public URL, or the file's own bytes sent as base64 from your machine. The bytes route is what lets an assistant take a file off your desktop into the account with no manual upload step in between. If you pass a URL, it has to be one that returns the file itself — a share link from a cloud drive returns a web page, and a web page is not an image.

Ask for the account's uploaded images and videos as a second step and check yours is in the list before you build an ad from it.

## The trap

> [!WARNING]
> **Uploaded images and videos cannot be deleted through this connector, so every mistake is permanent.** There is no delete for assets — removing one is an Ads Manager job — even though campaigns, ad sets and ads can all be deleted here. Name files properly on the way in, upload the final cut rather than the review copy, and expect the asset list to only ever grow.

## Go deeper

- Show me every image and video already uploaded to this account, newest first.
- Build a paused ad from the image I just uploaded, with headline `<headline>` and a Shop Now button.
- Upload every file in this folder and give me a table of file name against its hash or id.
- Show me my current ads with a preview link for each, so I can see how the new creative will look.
- Which of my running ads use this same image, so I know what I am about to replace?

## Fields this uses

- [`facebook_ads_image_asset_hash`](../06-reference/all-fields.md) · [`facebook_ads_image_asset_url`](../06-reference/all-fields.md) · [`facebook_ads_image_thumbnail`](../06-reference/all-fields.md)
- [`facebook_ads_video_asset`](../06-reference/all-fields.md) · [`facebook_ads_video_asset_thumbnail_url`](../06-reference/all-fields.md)
- [`facebook_ads_ad_format_asset`](../06-reference/all-fields.md) · [`facebook_ads_call_to_action_asset_name`](../06-reference/all-fields.md) · [`facebook_ads_link_url_asset_website_url`](../06-reference/all-fields.md)
- [`facebook_ads_ad_mobile_feed_preview_url`](../06-reference/all-fields.md) · [`facebook_ads_ad_instagram_preview_url`](../06-reference/all-fields.md)

An ad must be built from uploaded assets. Promoting a post that already exists on the page is not available here — see [what it cannot do](../06-reference/what-it-cannot-do.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
