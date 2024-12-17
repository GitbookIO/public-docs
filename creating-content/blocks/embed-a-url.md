---
description: Embed videos, music and more directly into your page with a URL
---

# Embedded URLs

To add an embedbed URL, simply paste the link of the content you want to embed and hit `Enter`.

{% hint style="info" %}
**Note:** The content you want to embed must be publicly available in order for GitBook to access the file. For example, when embedding a Google doc the share settings must be set to _Anyone with the link_.
{% endhint %}

### Videos

{% embed url="https://www.youtube.com/watch?v=D_uLM5i0Z4c" %}

{% hint style="info" %}
**Note:** You can choose to auto-play and loop YouTube and Vimeo embeds by adding `?autoplay=1&_loop=1` to the end of your video’s URL.
{% endhint %}

### Codepen

{% embed url="https://codepen.io/davidkpiano/pen/wMqXea" %}

### Spotify

{% embed url="https://open.spotify.com/track/4FmiciU3ZmfgABlbCSXcWw?si=65zMAhStT2ivTit-kZISWg" %}

### Representation in Markdown

```markdown
{% raw %}
{% embed url="URL_HERE" %}
{% endraw %}
```
