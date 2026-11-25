---
description: Found a security issue in GitBook? Send us a report and we’ll investigate it.
---

# Reporting bugs and vulnerabilities

<a href="mailto:security@gitbook.com?subject=Vulnerability%20Report&#x26;body=Summary%3A%0A%0AAffected%20URL%20or%20feature%3A%0A%0ASteps%20to%20reproduce%3A%0A1.%0A2.%0A%0AImpact%20%28what%20an%20attacker%20could%20do%29%3A%0A%0AProof%20of%20concept%20%28screenshots%2C%20requests%2C%20or%20video%29%3A" class="button primary" data-icon="envelope">Email a vulnerability report</a>

The button opens your email app with the address, subject, and a report template filled in. You can also write to security@gitbook.com with the subject **Vulnerability Report**.

{% hint style="info" %}
For a bug that isn’t a security issue, [contact GitBook support](https://www.gitbook.com/contact) instead.
{% endhint %}

## How to report

{% stepper %}
{% step %}
### Check that it’s in scope

We don’t accept reports for the issues listed under **Out of scope** in [Program details](reporting-bugs-and-vulnerabilities.md#program-details), such as denial of service, missing best practices without a working exploit, or unconfirmed scanner output.
{% endstep %}

{% step %}
### Write it up

Include the steps to reproduce the issue. Copy this template into your email:

```
Summary:

Affected URL or feature:

Steps to reproduce:
1.
2.

Impact (what an attacker could do):

Proof of concept (screenshots, requests, or video):
```
{% endstep %}

{% step %}
### Send it

Email security@gitbook.com with the subject **Vulnerability Report**, or use the button at the top of this page. Before you share anything about your report, read **Disclosure** in [Program details](reporting-bugs-and-vulnerabilities.md#program-details).
{% endstep %}

{% step %}
### We investigate

Our team triages and investigates your report. We confirm we’ve received it, and may ask for more information to understand the scale of the problem. Then we run tests to confirm whether you’ve found a previously unknown issue.
{% endstep %}
{% endstepper %}

## Rewards

We are a small distributed team, which means we are unable to offer financial rewards for reporting vulnerabilities at this stage.

We still would like to show our appreciation for your help in making GitBook better and safer by offering you a **discount on your subscription.**

## Program details

<details>

<summary>Out of scope</summary>

* Denial of service
* Disclosure of server or software version numbers
* Hypothetical subdomain takeovers without supporting evidence
* Issues that are premised on unlikely user interaction
* Missing best practices in SSL/TLS configuration
* Missing email best practices
* Missing HttpOnly or Secure flags on cookies
* Previously known vulnerable libraries without a working Proof-of-Concept
* Public Zero-day vulnerabilities that have had an official patch for less than 1 month will be awarded on a case-by-case basis
* Rate limiting or brute force issues on non-authentication endpoints
* Reports exploiting the behavior of, or vulnerabilities in, outdated browsers
* Reports of spam
* Social engineering
* Tabnabbing
* Unconfirmed reports from automated vulnerability scanners
* Attacks requiring MITM or physical access to a user's device
* Best practice reports without a valid exploit
* Clickjacking on pages with no sensitive actions
* Comma Separated Values (CSV) injection without demonstrating a vulnerability
* Content spoofing and text injection issues without showing an attack vector/without being able to modify HTML/CSS
* Cross-Site Request Forgery (CSRF) on unauthenticated forms or forms with no sensitive actions

</details>

<details>

<summary>Eligibility</summary>

* must be at least 18 years old.
* GitBook employees and contractors, as well as their family members, are strictly prohibited from participating in the Program or sharing information with an external security researcher to bypass this prohibition.

</details>

<details>

<summary>Rules of Engagement</summary>

* Your submission must include a working Reproduction Guide to be considered for a reward.
* Avoid harm to others’ data and privacy. Specifically:
  * If you encounter any personal data or sensitive information in the course of your research, **stop and notify our team immediately so we can investigate**. Please report to us what data was accessed and delete the data. Do not save, copy, download, transfer, disclose, or otherwise use this data. Continuing to access others’ data or otherwise failing to adhere to this requirement will disqualify you from receiving any reward.
  * If your research is designed to identify and demonstrate a vulnerability that could allow unauthorized access to personal data or sensitive information, make sure to take measures to minimize your access to or usage of such data to what is **absolutely necessary** to achieve those purposes (i.e., identification and demonstration of a vulnerability that could allow unauthorized access to personal data or sensitive information). For example, if you are injecting code into GitBook environment to test whether you could exfiltrate data from a GitBook's database, limit the potential exfiltration to the first three rows and five columns of the table rather than the entire database.
  * If, even after taking measures to minimize access to personal data or sensitive information, you ultimately end up encountering such data in the course of your research, follow the mitigation measures described above
* Do not leverage the existence of a vulnerability or access to personal data or sensitive information to make threats or extortionate demands. Do not degrade, interrupt, or deny services to our users or take any actions that can affect the availability or integrity of GitBook's systems and data (e.g., modifying or deleting data). If you notice service degradation or interruption, stop your research and notify us immediately.
* Do not incur a loss of funds that are not your own.
* We consider only the earliest, responsibly-disclosed submission of a vulnerability instance with enough actionable information to identify the issue for a reward. All other reports for a given issue will not be eligible for a reward.
* Your research must not violate any applicable laws or regulations.

</details>

<details>

<summary>Submission Review Process</summary>

After a submission is sent to GitBook in accordance with the Rules of Engagement described above, GitBook engineers will review the submission and validate its eligibility for a reward. The review time could vary depending on the complexity and completeness of your submission, as well as on the number of submissions we receive.

As explained in the Engagement section, GitBook retains sole discretion in determining which submissions are qualified for a reward. If we receive multiple bug reports for the same issue from different parties, the bounty will be granted to the first eligible submission. If a duplicate report provides new information that was previously unknown to GitBook, we may award a differential to the person submitting the duplicate report. GitBook will also reopen and reward any report mistakenly closed as invalid if we later receive and reward the same bug reported by someone else. In these situations, we will reward both researchers.

</details>

<details>

<summary>Disclosure</summary>

By participating in this program, you agree not to publicly or privately disclose the contents of your submission, your findings, your communications with GitBook related to your report, or any facts you have learned about GitBook in the course of this report to any third party without GitBook's prior written approval. There are no exceptions.

</details>

<details>

<summary>Accountability</summary>

GitBook reserves the right to disqualify you from participating if you violate the Rules of Engagement or other rules specified in this program policy, including the rules about disclosure.

</details>
