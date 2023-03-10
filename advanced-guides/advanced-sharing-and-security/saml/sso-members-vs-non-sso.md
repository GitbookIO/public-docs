# SSO Members vs non-SSO

Users who have created a GitBook account with an email used in your SAML Identity Provider, or joined your organization prior to the configuration of SAML, might see their login with SSO being blocked with a message prompting them to "_Log in with your existing credentials_":

<figure><img src="../../../.gitbook/assets/sso_login_issue.png" alt=""><figcaption></figcaption></figure>

## Origin of the message and security considerations

The first principle of our SAML SSO implementation is security.

If a user account has been created using an email address `bob@company.com`, and later on Bob attempts to log in with the company SAML, **GitBook cannot verify the integrity of the email address returned by the identity provider** and thus cannot authenticate them as the current account `bob@company.com`.&#x20;

To prevent the creation of two accounts associated with the `bob@company.com` email address, **GitBook indicates to the user that they should log in with their original account. The organization administrator, later on, decides how to handle the case**:

By enabling SSO on a user account, an organization administrator indicates to GitBook that the relationship between the email address of the account and the profile in your SAML Identity Provider can be trusted.

## Remediations

When a user sees their SSO login not succeeding with the message "Log in with your existing credentials", actions can be taken by the organization administrator to authorize them.

#### If the user account is already a member of the organization:

* An organization administrator can enable SSO on your organization membership from the administration dashboard. Next time, the user account will be authorized to login into the organization using the SSO flow.

or

* The user can log in to their account using the credentials initially used to create the account. For example, by clicking on "Continue with email" to receive an email sign-in link.
* :information\_source: SSO login will not be automatically enabled for this user, and an organization administrator has to enable it explicitly from the admin dashboard.

#### If the user account is not yet a member of the organization:

* An organization administrator should add the user account to the organization by inviting their email address from the admin dashboard. The user account can then directly be enabled for SSO login.

## Enabling SSO login for members

Organization administrators can enable SSO login for members by linking their accounts to SSO. Doing this indicates GitBook that the user account can be trusted as being connected to the identity in your provider.

<figure><img src="../../../.gitbook/assets/sso.gif" alt=""><figcaption></figcaption></figure>
