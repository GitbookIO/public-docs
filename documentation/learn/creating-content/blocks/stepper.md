---
description: "The Stepper block: what it does and how to use it."
---

# Stepper

Stepper blocks break a tutorial or guide into separate, clearly linked steps. Each step can hold multiple other blocks.

### Example

{% stepper %}
{% step %}
#### Add a stepper block

Hit `/` on an empty line, or click the `+` on the left of the editor, and select **Stepper**.
{% endstep %}

{% step %}
#### Add some content

Add content to each step — code blocks, drawings, images, and more.
{% endstep %}

{% step %}
#### Add more steps

Click the `+` below the step numbers, or hit `Enter` twice, to add another step. Change or remove the step header or body style as needed.
{% endstep %}
{% endstepper %}

### Limitations

Some block types can't be created inside a stepper block — for example, expandable blocks or another stepper. Start a new line inside one and press `/` to see the full list available.
