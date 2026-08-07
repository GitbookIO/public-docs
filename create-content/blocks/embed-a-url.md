---
description: Embed videos, music and more directly into your page with a URL
---

# Embedded URLs

To add an embedbed URL, simply paste the link of the content you want to embed and hit `Enter`.

{% hint style="info" %}
**Note:** The content you want to embed must be publicly available in order for GitBook to access the file. For example, when embedding a Google doc the share settings must be set to _Anyone with the link_.
{% endhint %}

{% hint style="info" %}
GitBook doesn't support embedding external content with an HTML `<iframe>`, due to its content security policy. If the content is publicly available, use the embed block instead.
{% endhint %}

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
