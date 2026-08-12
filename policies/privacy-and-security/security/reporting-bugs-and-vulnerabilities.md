---
description: Learn about how you can report suspected vulnerabilities or security concerns
---

# Reporting bugs and vulnerabilities

Occasionally we are contacted about suspected vulnerabilities or security concerns. Please note that we do take those extremely seriously and investigate each report.&#x20;

## How to report suspected vulnerabilities or security concerns?

To report vulnerabilities, please contact us at support@gitbook.com with a title 'Vulnerability Report'. For all other bugs please provide a specific title relating to the are where the bug occured. To help us respond to you faster, please share the steps to reproduce the behaviour. Our team will triage your report and respond to you with next steps.&#x20;

### What happens after I report my concern?

When we receive your report our team will triage and investigate it. We will confirm the receipt of your report and may also ask you for additional information to help us understand the scale of the problem. Next, our team will run tests and confirm if you have identified a previously unknown issue.

### Which vulnerabilities should I not report?

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

## Do you offer any rewards or bug bounties for reporting a vulnerability?&#x20;

We are a small distributed team which means we are unable to offer financial rewards for reporting vulnerabilities at this stage.&#x20;

We still would like to show our appreciation for your help in making GitBook better and safer by offering you a **discount on your subscription.**&#x20;

#### Eligibility <a href="#user-content-program-eligibility" id="user-content-program-eligibility"></a>

* must be at least 18 years old.
* GitBook employees and contractors, as well as their family members, are strictly prohibited from participating in the Program or sharing information with an external security researcher to bypass this prohibition.

#### Rules of Engagement

* Your submission must include a working Reproduction Guide to be considered for a reward.
* Avoid harm to others’ data and privacy. Specifically:
  * If you encounter any personal data or sensitive information in the course of your research, **stop and notify our team immediately so we can investigate**. Please report to us what data was accessed and delete the data. Do not save, copy, download, transfer, disclose, or otherwise use this data. Continuing to access others’ data or otherwise failing to adhere to this requirement will disqualify you from receiving any reward.&#x20;
  * If your research is designed to identify and demonstrate a vulnerability that could allow unauthorized access to personal data or sensitive information, make sure to take measures to minimize your access to or usage of such data to what is **absolutely necessary** to achieve those purposes (i.e., identification and demonstration of a vulnerability that could allow unauthorized access to personal data or sensitive information). For example, if you are injecting code into GitBook environment to test whether you could exfiltrate data from a GitBook's database, limit the potential exfiltration to the first three rows and five columns of the table rather than the entire database.
  * If, even after taking measures to minimize access to personal data or sensitive information, you ultimately end up encountering such data in the course of your research, follow the mitigation measures described above
* Do not leverage the existence of a vulnerability or access to personal data or sensitive information to make threats or extortionate demands. Do not degrade, interrupt, or deny services to our users or take any actions that can affect the availability or integrity of GitBook's systems and data (e.g., modifying or deleting data). If you notice service degradation or interruption, stop your research and notify us immediately.
* Do not incur a loss of funds that are not your own.
* We consider only the earliest, responsibly-disclosed submission of a vulnerability instance with enough actionable information to identify the issue for a reward. All other reports for a given issue will not be eligible for a reward.
* Your research must not violate any applicable laws or regulations.

#### Submission Review Process <a href="#user-content-submission-review-process" id="user-content-submission-review-process"></a>

After a submission is sent to GitBook in accordance with the Rules of Engagement described above, GitBook engineers will review the submission and validate its eligibility for a reward. The review time could vary depending on the complexity and completeness of your submission, as well as on the number of submissions we receive. \
\
As explained in the Engagement section, GitBook retains sole discretion in determining which submissions are qualified for a reward. If we receive multiple bug reports for the same issue from different parties, the bounty will be granted to the first eligible submission. If a duplicate report provides new information that was previously unknown to GitBook, we may award a differential to the person submitting the duplicate report. GItBook will also reopen and reward any report mistakenly closed as invalid if we later receive and reward the same bug reported by someone else. In these situations, we will reward both researchers.

#### Disclosure

By participating in this program, you agree not to publicly or privately disclose the contents of your submission, your findings, your communications with GitBook related to your report, or any facts you have learned about GitBook in the course of this report to any third party without GitBook's prior written approval. There are no exceptions.

#### Accountability <a href="#user-content-accountability" id="user-content-accountability"></a>

GitBook reserves the right to disqualify you from participating if you violate the Rules of Engagement or other rules specified in this program policy, including the rules about disclosure.
