# Get images and video into the ad account

The designer sent three new statics and a 15-second cut this morning, and they need to be in the account before the ad can be built.

> [!NOTE]
> **What on this page has actually been run.** Uploading an **image from a public URL** was executed against a live ad account on 2026-09-07, and the response shape below is the one that came back. **Video upload and uploading a file from your own machine were not run.** They are listed as supported by the connector, but nobody on this repo has seen their responses — read your own result back before you build an ad on top of one.

## Ask this

```
Upload the image at <public image URL> to my Meta ad account
and give me back the hash it returns.

```

## What comes back — image from a URL, verified

The upload action is `facebook_ads.image_upload`. It answers with an `images` object, and **the key inside it is a file name the connector derives from the last segment of the URL you gave it**:

```
images
  └─ <file name derived from your URL>
       └─ hash   <the reference you reuse>
```

In the run behind this page the URL ended in `.../1200/628` and the key came back as `628.jpg`. Your URL will produce a different key.

> [!WARNING]
> **Do not hardcode that key, and do not let a script look for the file name you think you uploaded.** The connector invents it from the URL, so a URL with no file name in it still produces one. Read the **first value inside `images`** and take its `hash`. Anything that reaches for a fixed key breaks the moment the URL shape changes.

## How to read it

Keep the hash. That is the reference the ad build uses, and nothing lists the account's uploaded assets afterwards, so keep it.

**Two upload routes exist.** A public URL, or the file's own bytes sent as `image_base64` / `video_base64` from your machine — the base64 route is what lets an assistant take a file off your desktop into the account with no manual step in between. **Only the URL route for images has been run here.**

If you pass a URL it has to be one that returns the file itself. A share link from a cloud drive returns a web page, and a web page is not an image.


## The traps

> [!WARNING]
> **Uploaded images and videos cannot be deleted through this connector, so every mistake is permanent.** There is no delete for assets — removing one is an Ads Manager job — even though campaigns, ad sets and ads can all be deleted here. Name files properly on the way in, upload the final cut rather than the review copy, and expect the asset list to only ever grow.

> [!WARNING]
> **Building the ad afterwards has its own naming traps, and these were hit in the live run.** The headline parameter is **`headline`** — pass `title` and it is silently dropped, so the ad is created without the headline you wrote. **`link` is required** even when the destination is inside an app. The button is a restricted list: **`LEARN_MORE` works, `GET_STARTED` is rejected**. And the ad needs a `page_id`, which you get from `facebook_ads.page_list`.

## Go deeper

- Build a paused ad from the image I just uploaded, with headline `<headline>` and a Learn More button, pointing at `<your URL>`.
- Upload each of these URLs and give me a table of the returned key against its hash.
- Show me my current ads with a preview link for each, so I can see how the new creative will look.
- Which of my running ads use this same image, so I know what I am about to replace?

## Fields this uses

- [`facebook_ads_image_asset_hash`](../../reference/all-fields.md) · [`facebook_ads_image_asset_url`](../../reference/all-fields.md) · [`facebook_ads_image_thumbnail`](../../reference/all-fields.md)
- [`facebook_ads_video_asset`](../../reference/all-fields.md) · [`facebook_ads_video_asset_thumbnail_url`](../../reference/all-fields.md)
- [`facebook_ads_ad_format_asset`](../../reference/all-fields.md) · [`facebook_ads_call_to_action_asset_name`](../../reference/all-fields.md) · [`facebook_ads_link_url_asset_website_url`](../../reference/all-fields.md)
- [`facebook_ads_ad_mobile_feed_preview_url`](../../reference/all-fields.md) · [`facebook_ads_ad_instagram_preview_url`](../../reference/all-fields.md)

An ad must be built from uploaded assets. Promoting a post that already exists on the page is not available here — see [what it cannot do](../../reference/what-it-cannot-do.md).

---

*Not affiliated with, endorsed by, or sponsored by Meta Platforms, Inc.*
