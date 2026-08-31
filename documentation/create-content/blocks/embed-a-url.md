---
description: Embed videos, music and more directly into your page with a URL
---

# Embedded URLs

To add an embedded URL, paste the link of the content you want to embed and press `Enter`.

### Videos

{% embed url="https://www.youtube.com/watch?v=D_uLM5i0Z4c" %}

{% hint style="info" %}
**Note:** You can choose to auto-play and loop YouTube and Vimeo embeds by adding `?autoplay=1&loop=1` to the end of your video’s URL.
{% endhint %}

#### Video files

Uploaded video files — such as MP4s — don't play inline; they appear as links that visitors can click to open or download. To show a playable video on your page, upload the video to a publicly accessible platform such as YouTube or Google Drive, then paste the link into an embed block. Private URLs won't display on your page.

### Codepen

{% embed url="https://codepen.io/davidkpiano/pen/wMqXea" %}

### Spotify

{% embed url="https://open.spotify.com/track/4FmiciU3ZmfgABlbCSXcWw?si=65zMAhStT2ivTit-kZISWg" %}

### Representation in Markdown

```markdown
{% embed url="URL_HERE" %}
```

### FAQ

<details>

<summary>Why isn't my URL working?</summary>

Your content must be publicly available. For Google Docs, select the _Anyone with the link_ sharing setting.

GitBook embeds URLs through [Iframely](https://iframely.com/domains). Confirm that Iframely supports your provider, then [test your URL with Iframely](https://iframely.com/try).

GitBook can't embed external HTML `<iframe>` tags because of its content security policy. Use an embed block instead.

</details>
