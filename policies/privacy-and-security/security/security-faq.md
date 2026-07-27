# Security FAQ

## What is GitBook?

GitBook is a tech startup, incorporated in the U.S as `GitBook Inc`, with a French subsidiary `GitBook SAS`

## Where is GitBook hosted?

We are hosted on [Google Cloud](https://cloud.google.com/security/overview/), which is backed by the same infrastructure and security that Google uses for its own services.

Customer data is stored in U.S. data centers. Some data (HTML pages & assets) may be cached in other geographies by our CDN. Access to private content through our CDN is always validated through our application servers using a complex permissions system.

Google follows or even leads most of the industry's best-practices and is compliant with most major security [standards and certifications](https://cloud.google.com/security/compliance/).

## Is customer data encrypted?

Yes, all customer data is encrypted at rest and in-transit:

* In transit, we use HTTPS to encrypt all traffic served to end-users.
  * Even user-provided custom domains are covered, thanks to [LetsEncrypt](https://letsencrypt.org/) and Cloudflare.
* At rest on Google Cloud Platform, using [multiple layers of AES256-AES128](https://cloud.google.com/security/encryption-at-rest/default-encryption/resources/encryption-whitepaper.pdf).

## How are users authenticated?

By default, all customer data, unless explicitly public, can only be accessed by authenticated users with valid permissions.

You can control and restrict access through our [Teams feature](https://docs.gitbook.com/organization-management/setting-up-permissions#teams), allowing you to invite external members to join your organization and collaborate, whilst restricting their access to a chosen subset of your projects.

## Which user/company data is required to operate on GitBook?

The only required piece of information to sign up and start using GitBook is an email address.

Depending on the risk evaluation performed using the [Clearbit Risk API](https://clearbit.com/risk), a phone number may be necessary for new users. The risk evaluation is based on a combination of the provided email address and the visitor's IP address.

When subscribing to a plan, the user will be asked for credit card information. This information never reaches our servers and is processed by [Stripe](https://stripe.com) only.

[Stripe](https://stripe.com) gives us access to the expiration date, the brand and the last 4 digits of the credit card only, which are stored in our database for convenience. The user can opt-in to provide us with a billing address, which is also stored in our database. As for the credit card partial information, the billing address is private and only accessible by the GitBook organization's and the application's administrators.

## What other 3rd-party services process data?

GitBook leverages the following 3rd-party services and APIs:

* [Turbopuffer](https://turbopuffer.com/) for Search
* [Stripe](https://stripe.com/) for Payments
* [Intercom](https://www.intercom.com/) for Support
* [Clearbit](https://clearbit.com/) for Sign up risk evaluation
* [Amplitude](https://amplitude.com/) and [Google Analytics](https://www.google.com/analytics/) for Analytics
* [Google Cloud](https://cloud.google.com/), [Cloudflare](https://www.cloudflare.com/) and [Vercel](https://vercel.com/) for hosting (data & compute)
* [Planetscale](https://planetscale.com/) for data (database)

Since these services provide the highest standards and are regularly externally audited, GitBook does not audit them by its own means.

## How are role-based permissions applied on GitBook?

Each user on GitBook is assigned a unique identifier when her/his account is created. When creating or joining a GitBook organization, each user is then assigned a role: reader, editor, admin... This role is then used to derivate a set of permissions for each member of the organization. Thanks to this design, each organization's data is logically isolated from other tenants across the whole application, and the user's access to an organization's content is automatically revoked when they are removed from the said organization

These permissions are then applied at the GitBook API level, which is the only entrypoint to our database. For each request, based on the user's unique identifier and the set of permissions associated with its role at the time of the request, our API will either accept or reject the request.

## How well is GitBook protected against common web application vulnerabilities?

Google Cloud Functions, that are used to serve our application, live behind the Google Frontend. They are protected against brute force/DDoS attacks the same way that [google.com](https://google.com) protects itself.

In addition, since Firebase Authentication is the gateway to many of our backend services and security rules, many of our quotas are protected by per-IP limits to give an extra layer of protection against a localized attack.

## Is GitBook SOC2 certified?

Yes, we are. You can read more about [security as our company](security-as-a-company-value.md#soc-2-type-2) value and our certification on the next page.
