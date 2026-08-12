---
description: >-
  Capture the network and console information GitBook’s support team needs to
  investigate a bug
---

# Report a bug

Report bugs from the app’s support widget or by emailing [support@gitbook.com](mailto:support@gitbook.com), with as much context as possible on how you encountered the issue.

For some issues, the support team asks for a **HAR capture** (HTTP Archive). It records your browser’s requests and responses with the GitBook app, letting the team investigate further. Capture it alongside a console log:

{% tabs %}
{% tab title="Chrome" %}
1. In Chrome, go to the page in GitBook where you’re experiencing the issue.
2. Click **⋮** at the top right of your browser window, then **More tools → Developer tools**.
3. Click the **Network** tab and check **Preserve log**.
4. Confirm the red circle at the top left of the Network tab is visible — recording has started. If the circle is black, click it to start recording.
5. Refresh the page and reproduce the issue.
6. Click the download icon (↓) in the Network tab toolbar to save all requests as a HAR file.
7. Click the **Console** tab, right-click anywhere in the console, and click **Save as…**. Name the file `Chrome-console.log`.
8. Reply to your case with both files as shared links.
{% endtab %}

{% tab title="Firefox" %}
1. In Firefox, go to the page in GitBook where you’re experiencing the issue.
2. Click the Firefox menu at the top right, then **Web developer → Network**.
3. Click the **Network** tab and check **Persist logs**.
4. Refresh the page and reproduce the issue while the capture is running.
5. Right-click any row of the activity pane and click **Save all as HAR**.
6. Click the **Console** tab, right-click any row, and click **Select all**. Paste the content into a text file named `console-log.txt`.
7. Reply to your case with both files as shared links.
{% endtab %}

{% tab title="Safari" %}
1. In Safari, go to the page in GitBook where you’re experiencing the issue.
2. In the menu bar, click **Develop** and select **Show Web Inspector**.
3. Click the **Console** tab and check **Preserve log**, then go to the **Network** tab.
4. Refresh the page and reproduce the issue while the capture is running.
5. Right-click any row of the activity pane and click **Export HAR**.
6. In the **Console** tab, right-click any row and click **Select all**. Paste the content into a text file named `console-log.txt`.
7. Reply to your case with both files as shared links.
{% endtab %}

{% tab title="Edge" %}
1. In Edge, go to the page in GitBook where you’re experiencing the issue.
2. Click the Edge menu (⋮) at the top right and select **Developer tools**.
3. Click the **Network** tab and clear the **entries on navigate** option (the blue arrow with a red X).
4. Confirm the green play button (**start profiling session**) is selected — the capture is running.
5. Refresh the page and reproduce the issue.
6. Click the **Export as HAR** icon (the floppy disk).
7. In the **Console** tab, right-click any row and click **Copy all**. Paste the content into a text file named `console-log.txt`.
8. Reply to your case with both files as shared links.
{% endtab %}
{% endtabs %}
