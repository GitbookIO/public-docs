---
description: "GitBook's official Node.js client library."
---

# Client libraries

## Node.js

GitBook provides an official TypeScript/JavaScript client for the API, usable in a browser or Node.js environment.

### Installation

```bash
npm install @gitbook/api
```

### Usage

```typescript
import { GitBookAPI } from '@gitbook/api';

const client = new GitBookAPI({
  authToken: '<your_access_token>'
});
```

With Node.js < v18, pass a custom `fetch` — for example from [`node-fetch`](https://github.com/node-fetch/node-fetch):

```typescript
import { GitBookAPI } from '@gitbook/api';
import fetch from 'node-fetch';

const client = new GitBookAPI({
  customFetch: fetch
});
```

### Method reference

Methods are grouped onto client objects matching the API's resources.

<details>

<summary><code>client.user</code> / <code>client.users</code></summary>

`getAuthenticatedUser()`, `getUserById()`

</details>

<details>

<summary><code>client.spaces</code></summary>

`getSpaceById()`, `updateSpaceById()`, `deleteSpaceById()`, `duplicateSpace()`, `restoreSpace()`, `moveSpace()`, `transferSpace()`, `getEmbedByUrlInSpace()`, `searchSpaceContent()`, `importGitRepository()`, `exportToGitRepository()`, `getSpaceGitInfo()`, `inviteToSpace()`, `updateTeamPermissionInSpace()`, `removeTeamFromSpace()`, `listUserPermissionsInSpace()`, `updateUserPermissionInSpace()`, `removeUserFromSpace()`, `listTeamPermissionsInSpace()`, `getCurrentRevision()`, `importContent()`, `listPages()`, `listFiles()`, `getFileById()`, `listSpaceFileBacklinks()`, `getPageById()`, `listPageLinksInSpace()`, `listSpacePageBacklinks()`, `importContentInPageById()`, `getPageByPath()`, `getReusableContentById()`, `getComputedDocument()`, `getComputedRevision()`, `getDocumentById()`, `createChangeRequest()`, `listChangeRequestsForSpace()`, `getChangeRequestById()`, `updateChangeRequestById()`, `mergeChangeRequest()`, `updateChangeRequest()`, `getReviewsByChangeRequestId()`, `submitChangeRequestReview()`, `getRequestedReviewersByChangeRequestId()`, `requestReviewersForChangeRequest()`, `listChangeRequestLinks()`, `listCommentsInChangeRequest()`, `postCommentInChangeRequest()`, `getCommentInChangeRequest()`, `deleteCommentInChangeRequest()`, `updateCommentInChangeRequest()`, `listCommentRepliesInChangeRequest()`, `postCommentReplyInChangeRequest()`, `getCommentReplyInChangeRequest()`, `updateCommentReplyInChangeRequest()`, `deleteCommentReplyInChangeRequest()`, `getContributorsByChangeRequestId()`, `getRevisionOfChangeRequestById()`, `importContentInChangeRequest()`, `listPagesInChangeRequest()`, `listFilesInChangeRequestById()`, `getFileInChangeRequestById()`, `listChangeRequestFileBacklinks()`, `getPageInChangeRequestById()`, `listPageLinksInChangeRequest()`, `listChangeRequestPageBacklinks()`, `importContentInChangeRequestPageById()`, `getPageInChangeRequestByPath()`, `getReusableContentInChangeRequestById()`, `getChangeRequestPdf()`, `streamBrainstormChangeRequest()`, `streamImplementChangeRequestTask()`, `getRevisionById()`, `getRevisionSemanticChanges()`, `listPagesInRevisionById()`, `listFilesInRevisionById()`, `getFileInRevisionById()`, `getPageInRevisionById()`, `getPageInRevisionByPath()`, `getReusableContentInRevisionById()`, `listCommentsInSpace()`, `postCommentInSpace()`, `getCommentInSpace()`, `deleteCommentInSpace()`, `updateCommentInSpace()`, `listCommentRepliesInSpace()`, `postCommentReplyInSpace()`, `getCommentReplyInSpace()`, `updateCommentReplyInSpace()`, `deleteCommentReplyInSpace()`, `listPermissionsAggregateInSpace()`, `listSpaceIntegrations()`, `listSpaceIntegrationsBlocks()`, `listSpaceIntegrationScripts()`, `getSpaceCustomFields()`, `updateSpaceCustomFields()`, `getSpacePdf()`, `listSpaceLinks()`

</details>

<details>

<summary><code>client.collections</code></summary>

`getCollectionById()`, `updateCollectionById()`, `deleteCollectionById()`, `listSpacesInCollectionById()`, `moveCollection()`, `transferCollection()`, `inviteToCollection()`, `listTeamPermissionsInCollection()`, `updateTeamPermissionInCollection()`, `removeTeamFromCollection()`, `listUserPermissionsInCollection()`, `updateUserPermissionInCollection()`, `removeUserFromCollection()`, `listPermissionsAggregateInCollection()`

</details>

<details>

<summary><code>client.integrations</code></summary>

`listIntegrations()`, `getIntegrationByName()`, `publishIntegration()`, `unpublishIntegration()`, `listIntegrationInstallations()`, `installIntegration()`, `listIntegrationEvents()`, `getIntegrationEvent()`, `listIntegrationSpaceInstallations()`, `setIntegrationDevelopmentMode()`, `disableIntegrationDevelopmentMode()`, `renderIntegrationUiWithGet()`, `renderIntegrationUiWithPost()`, `queueIntegrationTask()`, `getIntegrationInstallationById()`, `updateIntegrationInstallation()`, `uninstallIntegration()`, `createIntegrationInstallationToken()`, `listIntegrationInstallationSpaces()`, `installIntegrationOnSpace()`, `getIntegrationSpaceInstallation()`, `updateIntegrationSpaceInstallation()`, `uninstallIntegrationFromSpace()`, `listIntegrationInstallationSites()`, `installIntegrationOnSite()`, `getIntegrationSiteInstallation()`, `updateIntegrationSiteInstallation()`, `uninstallIntegrationFromSite()`

</details>

<details>

<summary><code>client.orgs</code></summary>

`listOrganizationsForAuthenticatedUser()`, `getOrganizationById()`, `updateOrganizationById()`, `listMembersInOrganizationById()`, `getMemberInOrganizationById()`, `updateMemberInOrganizationById()`, `removeMemberFromOrganizationById()`, `updateOrganizationMemberLastSeenAt()`, `setUserAsSsoMemberForOrganization()`, `listSpacesForOrganizationMember()`, `listTeamsForOrganizationMember()`, `listTeamsInOrganizationById()`, `createOrganizationTeam()`, `getTeamInOrganizationById()`, `updateTeamInOrganizationById()`, `removeTeamFromOrganizationById()`, `updateMembersInOrganizationTeam()`, `listTeamMembersInOrganizationById()`, `addMemberToOrganizationTeamById()`, `deleteMemberFromOrganizationTeamById()`, `inviteUsersToOrganization()`, `joinOrganizationWithInvite()`, `listOrganizationInviteLinks()`, `createOrganizationInvite()`, `updateOrganizationInviteById()`, `deleteOrganizationInviteById()`, `searchOrganizationContent()`, `listSpacesInOrganizationById()`, `createSpace()`, `listCollectionsInOrganizationById()`, `createCollection()`, `listOrganizationCustomFields()`, `createOrganizationCustomField()`, `getOrganizationCustomFieldByName()`, `updateOrganizationCustomField()`, `deleteOrganizationCustomField()`, `listOrganizationIntegrations()`, `getOrganizationIntegrationStatus()`, `listOrganizationInstallations()`, `listOrganizationIntegrationsStatus()`, `listSamlProvidersInOrganizationById()`, `createOrganizationSamlProvider()`, `getOrganizationSamlProviderById()`, `updateOrganizationSamlProvider()`, `deleteOrganizationSamlProvider()`, `listSsoProviderLoginsInOrganization()`, `askInOrganization()`, `getRecommendedQuestionsInOrganization()`, `streamRecommendedQuestionsInOrganization()`, `streamAskInOrganization()`, `listSites()`, `createSite()`, `getSiteById()`, `updateSiteById()`, `deleteSiteById()`, `getPublishedContentSite()`, `publishSite()`, `unpublishSite()`, `listSiteShareLinks()`, `createSiteShareLink()`, `updateSiteShareLinkById()`, `deleteSiteShareLinkById()`, `getSiteStructure()`, `getSitePublishingAuthById()`, `updateSitePublishingAuthById()`, `regenerateSitePublishingAuthById()`, `getSitePublishingPreviewById()`, `getSiteCustomizationById()`, `updateSiteCustomizationById()`, `listSiteIntegrationScripts()`, `listSiteIntegrations()`, `addSpaceToSite()`, `listSiteSpaces()`, `listSiteSectionGroups()`, `addSectionGroupToSite()`, `updateSiteSectionGroupById()`, `deleteSiteSectionGroupById()`, `addSectionToGroup()`, `removeSectionFromGroup()`, `addSectionToSite()`, `listSiteSections()`, `updateSiteSectionById()`, `deleteSiteSectionById()`, `searchSiteContent()`, `streamAskInSite()`, `streamRecommendedQuestionsInSite()`, `updateSiteSpaceById()`, `deleteSiteSpaceById()`, `getSiteSpaceCustomizationById()`, `overrideSiteSpaceCustomizationById()`, `deleteSiteSpaceCustomizationById()`, `moveSiteSectionGroup()`, `moveSiteSection()`, `moveSiteSpace()`, `listPermissionsAggregateInSite()`, `trackEventsInSiteById()`, `aggregateSiteEvents()`, `listSiteVisitorSegments()`, `updateSiteAdsById()`, `createSiteRedirect()`, `listSiteRedirects()`, `updateSiteRedirectById()`, `deleteSiteRedirectById()`, `getSiteRedirectBySource()`, `generateSiteStorageUploadUrl()`, `listOpenApiSpecs()`, `getOpenApiSpecBySlug()`, `createOrUpdateOpenApiSpecBySlug()`, `deleteOpenApiSpecBySlug()`, `listOpenApiSpecVersions()`, `getLatestOpenApiSpecVersion()`, `getLatestOpenApiSpecVersionContent()`, `getOpenApiSpecVersionById()`, `getOpenApiSpecVersionContentById()`

</details>

<details>

<summary><code>client.customHostnames</code></summary>

`getCustomHostname()`, `dnsRevalidateCustomHostname()`, `removeCustomHostname()`

</details>

<details>

<summary><code>client.ads</code></summary>

`adsListSites()`, `adsUpdateSite()`

</details>

<details>

<summary><code>client.urls</code></summary>

`getContentByUrl()`, `getEmbedByUrl()`, `getPublishedContentByUrl()`

</details>

Each method corresponds directly to an endpoint in the [API Reference](api-reference.md) — use that reference for a method's parameters and response shape.
