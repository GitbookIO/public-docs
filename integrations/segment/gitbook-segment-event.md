# GitBook Segment event

Once the Segment integration has been installed and configured on a Space, anytime a visitor access a page in your GitBook Published content, the integration will send `[GitBook] space_view` events to the Segment Source you've chosen to use.

This event includes various information on the visitor and the page they've accessed.

It should have the following shape:

```json
{
  "anonymousId": "<visitor_anonymous_id>",
  "context": {
    "ip": "<visitor_ip_address>",
    "library": {
      "name": "GitBook",
      "version": "0.0.0"
    },
    "page": {
      "path": "/path/of/the/visited/page",
      "referrer": "<referrer_url>",
      "search": "<page_url_query_string>",
      "url": "<full_page_url>"
    },
    "userAgent": "<visitor_user_agent>"
  },
  "event": "[GitBook] space_view",
  "integrations": {},
  "messageId": "api-2CIZxqhowyXWX1IR7XD3ku0Wtdm",
  "properties": {
    "pageId": "<gitbook_page_id>",
    "spaceId": "<gitbook_space_id>"
  },
  "receivedAt": "2022-07-22T12:18:27.692Z",
  "timestamp": "2022-07-22T12:18:27.692Z",
  "type": "track"
}
```
