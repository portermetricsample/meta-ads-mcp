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

One line per asset. A video also reports its length and both processing stages. Ids below are made up.

```
image   hash 4f2c…            uploaded
video   id 46200000000000     length 4.083s, uploading complete, processing complete
```

| Asset | Type | Reference to reuse |
|---|---|---|
| `<image file name>` | image | image hash |
| `<video file name>` | video | video id |

## How to read it

Two stages matter for video: **uploading** moves the bytes, **processing** makes the file usable in an ad. Both must say complete. A video that finished uploading but is still processing will fail when you try to build an ad from it — wait and ask again.

Source can be a public URL or the raw bytes of a file sitting on your machine. The bytes path is what lets an assistant take a file from your desktop into the account with no manual upload step in between.

Keep the hash (images) or id (videos) that comes back. That reference is what the ad build uses, and asking for the account's uploaded assets later gets it back for you.

> [!NOTE]
> Uploaded images and videos **cannot be deleted** through this connector. Removing an asset from the account is an Ads Manager job. Name files carefully, because clutter accumulates.

## The trap

> [!WARNING]
> **A Google Drive or Dropbox share link is not a file link.** It serves a web page, so the upload receives HTML instead of an image or a video and fails with a message about the URL serving a web page. Use a direct-download link that returns the file itself, or hand over the local file and let the bytes be uploaded instead. This is the single most common failure here, and the error text does not look like it is about the link.

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

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
