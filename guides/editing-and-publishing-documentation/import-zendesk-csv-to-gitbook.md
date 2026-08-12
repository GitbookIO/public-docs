---
description: "Learn how to add data from Zendesk —\_or any other CSV file — into GitBook"
---

# Import content from a CSV file into GitBook

This guide explains how to import HTML content stored in a CSV file into GitBook.&#x20;

This process is useful for migrating content from various sources, such as help centers like Zendesk, documentation databases, or any application that exports HTML data to CSV.

{% hint style="info" %}
Scroll to the bottom of this page to see a video version of this guide.
{% endhint %}

{% stepper %}
{% step %}
### **Connect GitBook to your Git repository**

You can follow [our import/migration guide](import-or-migrate-your-content-to-gitbook-with-git-sync.md) to add your content from a GitHub or GitLab repository into to a new GitBook space. Read more about Git Sync in [our documentation](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync)
{% endstep %}

{% step %}
### **Preparing your CSV file**

Before you import your CSV content, you should first make sure it’s in the right format for import:

* Open your CSV file in a spreadsheet editor (e.g., Google Sheets, Microsoft Excel).
* Ensure your CSV file has the following essential columns:
  * **Section:** This column will determine the organization of your content in GitBook. It represents the section or category the HTML content belongs to. If your data does not contain sections, you can create a single section name for all rows.
  * **Article Title:** The title of each page.
  * **Article Body:** The HTML content itself.
* **Zendesk example:** If you’re migrating from Zendesk, you’ll typically export a CSV that includes columns like “Section”, “Article Title”, and “Article Body” (which contains the HTML).
{% endstep %}

{% step %}
### **Converting CSV to Markdown**

To import your CSV data into GitBook, you first need to convert it into Markdown so GitBook can interpret it correctly. Here’s how:

* Go to [https://csv-to-md.streamlit.app/](https://csv-to-md.streamlit.app/)
* Upload your prepared CSV file.
* Review the preview to ensure the data is displayed correctly.
* Click the **Convert to Markdown and Download** button.
* Download the resulting ZIP file. This file will contain Markdown files for each article and a `SUMMARY.md` file.
{% endstep %}

{% step %}
### **Adding files to your Git repository**

* Unzip the downloaded ZIP file.
* If your upload is small (less than 100 pages) you can drag and drop the extracted Markdown files into your repository. Alternatively you can use the command line to push from your machine to [GitHub](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository#adding-a-file-to-a-repository-using-the-command-line) and [GitLab](https://docs.gitlab.com/topics/git/add_files/). If you are not familiar with the command line, GitHub’s desktop app is also a user friendly way to add large folders to your repository.
* Commit and push the changes.
{% endstep %}

{% step %}
### **GitBook sync and verification**

* Because you’ve set up Git Sync, GitBook will automatically detect the changes in your Git repository and sync the content to your GitBook space.
* Verify that your articles and sections are displayed correctly in your GitBook space.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
The CSV-to-Markdown converter creates a `SUMMARY.md` file that GitBook uses for navigation. Ensure this file is added to your repository. If you encounter issues with page display, review the `SUMMARY.md` to confirm the correct page order and inclusion. For reference, [this](https://github.com/GitbookIO/public-docs/blob/main/SUMMARY.md) is how a GitBook `SUMMARY.md` file looks.
{% endhint %}

{% embed url="https://www.loom.com/share/2b4a574a4ad54586b5d486cb6ad3735b?sid=75e4ec94-4188-4223-baf0-3e9bd3d8cb60" %}
A video guide explaining how to import a CSV file from Zendesk into GitBook
{% endembed %}
