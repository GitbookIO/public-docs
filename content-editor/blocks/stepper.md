# Stepper

Stepper blocks let you break down a tutorial or guide into separate, but clearly linked steps. Each step can contain multiple different blocks, allowing you to add detailed information.

### Example

{% stepper %}
{% step %}
### Add a stepper block

To add a stepper block, hit `/` on an empty line or click the `+` on the left of the editor and select **Stepper** from the insert menu.
{% endstep %}

{% step %}
### Add some content

Once you’ve inserted your stepper block, you can start adding content to it — including code blocks, drawings, images and much more.
{% endstep %}

{% step %}
### Add more steps

Click the `+` below the step numbers or hit `Enter` twice to add another step to your stepper block. You can remove or change the style of the step header or step body if you wish.
{% endstep %}
{% endstepper %}

## Representation in Markdown

<pre class="language-markdown"><code class="lang-markdown"><strong>## Example
</strong><strong>
</strong><strong>{% stepper %}
</strong>{% step %}
### Step 1 title
Step 1 text
{% endstep %}
{% step %}
### Step 2 title
Step 2 text
{% endstep %}
{% endstepper %}
</code></pre>

### Limitations

There are some limitations on which blocks you can create inside of a stepper block — for example, you cannot add expandable blocks or another stepper block. See all the blocks you can add by starting a new line within a stepper block and pressing `/` to bring up the insert palette.
