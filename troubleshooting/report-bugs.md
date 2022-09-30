---
description: >-
  Encountered a bug? Find out how to provide all the essential information for
  speedy resolution.
---

# How do I report bugs?

Bugs should be reported using the messaging widget available from your dashboard or by sending an email to [support@gitbook.com](mailto:support@gitbook.com). In order to get the best help possible, please provide as much context on how you encountered the bug.

## **Generate Network Captures for Troubleshooting**

**HAR**

A HAR capture (HTTP Archives) records the requests and responses that your browser makes with the GitBook Application.

### **Chrome**

1. In Chrome, go to the page within GitBook where you are experiencing trouble.
2. At the top-right of your browser window, click the Chrome menu (⋮).
3. Select **Tools > Developer Tools**. The Developer Tools window opens as a docked panel at the side or bottom of Chrome.
4. Click the **Network** tab.
5. Select **Preserve log**.
6. You will see a red circle at the top left of the Network tab. This means the capture has started. If the circle is black, click the **black circle** to start recording activity in your browser.
7. **Refresh the page** and reproduce the problem while the capture is running.
8. After you successfully reproduce the issue, right click on any row of the activity pane and select **Save as HAR with Content**.
9. Select the **Console** tab
10. Right-click anywhere in the console and select **Save as...**.
11. Name the log file **Chrome-console.log**.
12. Send both files as shared links in a reply to your case.

### **Firefox**

1. In Firefox, go to the page within GitBook where you are experiencing trouble.
2. Click the Firefox menu (Three horizontal parallel lines) at the top-right of your browser window.
3. Select **Web Developer > Network**.
4. The Developer Tools window opens as a docked panel at the side or bottom of Firefox.
5. Click the **Network** tab.
6. Select **Persist logs**.
7. **Refresh the page** and reproduce the problem while the capture is running.
8. After you successfully reproduce the issue, right-click any row of the activity pane and select **Save all as HAR**.
9. Select the **Console** tab.
10. Right-click any row and select **Select all**.
11. Paste the content in a text file and name it **console-log.txt**.
12. Send both files as shared links in a reply to your case.

### **Safari**

1. In Safari, go to the page within GitBook where you are experiencing trouble.
2. In the menu bar at the top, click **Develop** and select **Show Web Inspector**.
3. Click the **Console** tab and select **Preserve Log**.
4. Go back to the **Network** tab.
5. **Refresh the page** and reproduce the problem while the capture is running.
6. After you successfully reproduce the issue, right-click any row of the activity pane and select **Export HAR**.
7. Click the **Console** tab.
8. Right-click any row and select **Select all**.
9. Paste the content in a text file and name it **console-log.txt**.
10. Send both files as shared links in a reply to your case.

### **Internet Explorer (IE11)**

1. In Internet Explorer, go to the page within GitBook where you are experiencing trouble.
2. Click the gear icon in the top right.
3. Select **F12 Developer** Tools.
4. Click the **Network** tab.
5. Clear the **Clear entries on navigate** option, which is selected by default. The icon looks like blue arrow with a red X.
6. The green play button (**Start Profiling Session**), should be selected by default. This means the capture function is running.
7. Refresh the the page and reproduce the problem while the capture is running.
8. Once you have reproduced the issue, click the **Export as HAR** icon. The icon looks like a floppy disk.
9. Click the **Console** tab.
10. Right-click any row and select **Copy all.**
11. Paste the content in a text file and name it **console-log.txt**.
12. Send both files as shared links in a reply to your case.

### **Edge**

1. In Edge, go to the page within GitBook where you are experiencing trouble.
2. At the top-right of your browser window, click the Edge menu (⋮)
3. Select **Developer Tools**.
4. Click the **Network** tab.
5. Clear the **Clear entries on navigate** option, which is selected by default. The icon looks like blue arrow with a red X.
6. The green play button (**Start Profiling Session**), should be selected by default. This means the capture function is running.
7. Refresh the the page and reproduce the problem while the capture is running.
8. Once you have reproduced the issue, click the **Export as HAR** icon. The icon looks like a floppy disk.
9. Click the **Console** tab.
10. Right-click any row and select **Copy all.**
11. Paste the content in a text file and name it **console-log.txt**.
12. Send both files as shared links in a reply to your case.
