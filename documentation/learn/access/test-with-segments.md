---
description: Preview your site as different visitor segments to validate adaptive content.
---

# Test with segments

Segments let you test [content conditions](write-content-conditions.md) by defining claims on a mock user — for example, a segment representing a beta user, to check which pages would be visible to them.

### Create a segment

In the condition editor, click the settings icon next to an existing segment in the segment dropdown. Define the data that should appear on a mock user — since this data represents the visitor, the `visitor.claims` key is omitted.

For example, to create a segment for beta users:

```json
{
  "isBetaUser": true
}
```

Back in the condition editor, selecting the beta segment shows whether the page you're viewing would be accessible to that test user.

### Detected segments

Detected segments show the kinds of claims you're actually receiving from visitors to your site. They aren't editable, but you can copy claims from them to build your own segments.

### Testing segments in the preview

You can also apply segments in real time from the preview when viewing changes to your site — use the dropdown in the upper-left corner of preview mode to choose a segment and see how your site looks for it.
