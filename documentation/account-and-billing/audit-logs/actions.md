---
description: >-
  Every action GitBook audit logs can record, with the action ID to use in the
  API and the label shown in the app.
---

# Audit log actions

Each audit event has an action ID, such as `site.redirect.created`, and a label, such as **Created site redirect**. The app shows the label in the **Action** column and filter. API responses return the action ID in the `action` field. CSV exports include both.

To get the current list for your organization programmatically, use the [List organization audit event actions](https://gitbook.com/docs/developers/gitbook-api/api-reference/organizations/list-organization-audit-event-actions) endpoint.

Coverage may expand as GitBook adds more actions. For what audit logs don’t record, see [What audit logs record](./#what-audit-logs-record).

## Organization administration

| Action ID | Label |
| --- | --- |
| `organization.agent-instructions.updated` | Updated organization agent instructions |
| `organization.custom-font.created` | Created custom font |
| `organization.custom-font.deleted` | Deleted custom font |
| `organization.custom-font.updated` | Updated custom font |
| `organization.link-invite.created` | Created organization invite link |
| `organization.link-invite.deleted` | Deleted organization invite link |
| `organization.link-invite.updated` | Updated organization invite link |
| `organization.settings.updated` | Updated organization settings |
| `organization.team.created` | Created organization team |
| `organization.team.deleted` | Deleted organization team |
| `organization.team.member-added` | Added organization team member |
| `organization.team.member-removed` | Removed organization team member |
| `organization.team.member-updated` | Updated organization team member |
| `organization.team.members-replaced` | Replaced organization team members |
| `organization.team.updated` | Updated organization team |
| `translation.configuration.created` | Created translation configuration |
| `translation.configuration.deleted` | Deleted translation configuration |
| `translation.configuration.updated` | Updated translation instructions |
| `translation.glossary.updated` | Updated translation glossary |

## Members

| Action ID | Label |
| --- | --- |
| `organization.member.access-updated` | Updated organization member access |
| `organization.member.joined` | Added organization member |
| `organization.member.removed` | Removed organization member |
| `organization.member.sso-enforced` | Enforced SSO for organization member |
| `organization.member.sso-released` | Released organization member from SSO |
| `organization.member.updated` | Updated organization member |

## SSO and SCIM

| Action ID | Label |
| --- | --- |
| `organization.sso-enforcement.updated` | Updated SSO enforcement |
| `sso.email-migration.completed` | Completed SSO email migration |
| `sso.email-migration.failed` | Failed SSO email migration |
| `sso.email-migration.started` | Started SSO email migration |
| `sso.saml-provider.created` | Created SAML provider |
| `sso.saml-provider.deleted` | Deleted SAML provider |
| `sso.saml-provider.updated` | Updated SAML provider |
| `sso.scim-connection.created` | Created SCIM connection |
| `sso.scim-connection.deleted` | Deleted SCIM connection |
| `sso.scim-connection.token-rotated` | Rotated SCIM connection token |
| `sso.scim-connection.updated` | Updated SCIM connection |

## Billing and plans

| Action ID | Label |
| --- | --- |
| `billing.credits-bundle.updated` | Updated AI credit bundle |
| `billing.meter.disabled` | Disabled billing usage add-on |
| `billing.meter.enabled` | Enabled billing usage add-on |
| `billing.overrides.updated` | Updated billing overrides |
| `billing.plan.migrated` | Migrated organization billing plan |
| `billing.plan.updated` | Updated organization billing plan |
| `billing.settings.updated` | Updated billing settings |
| `billing.trial.started` | Started organization trial |
| `billing.trial.updated` | Updated organization trial |

## Sites

| Action ID | Label |
| --- | --- |
| `site.customization.updated` | Updated site customization |
| `site.default-section.updated` | Updated default section |
| `site.default-space.updated` | Updated default space |
| `site.external-link.added` | Added external link |
| `site.external-link.deleted` | Deleted external link |
| `site.external-link.moved` | Moved external link |
| `site.external-link.reordered` | Reordered external link |
| `site.external-link.updated` | Updated external link |
| `site.lifecycle.created` | Created site |
| `site.lifecycle.deleted` | Deleted site |
| `site.lifecycle.published` | Published site |
| `site.lifecycle.unpublished` | Unpublished site |
| `site.plan.updated` | Updated site plan |
| `site.section-group.added` | Added section group |
| `site.section-group.deleted` | Deleted section group |
| `site.section-group.moved` | Moved section group |
| `site.section-group.reordered` | Reordered section group |
| `site.section-group.updated` | Updated section group |
| `site.section.added` | Added section |
| `site.section.deleted` | Deleted section |
| `site.section.moved` | Moved section |
| `site.section.reordered` | Reordered section |
| `site.section.updated` | Updated section |
| `site.settings.updated` | Updated site |
| `site.space-customization.created` | Created space customization |
| `site.space-customization.reset` | Reset space customization |
| `site.space-customization.updated` | Updated space customization |
| `site.space.added` | Added space |
| `site.space.deleted` | Deleted space |
| `site.space.moved` | Moved space |
| `site.space.reordered` | Reordered space |
| `site.space.updated` | Updated space |
| `site.structure.reordered` | Reordered site structure |
| `site.structure.sorted` | Sorted site structure |
| `site.team-permission.granted` | Granted team access to site |
| `site.team-permission.revoked` | Revoked team access to site |
| `site.team-permission.updated` | Updated team access to site |
| `site.user-permission.granted` | Granted user access to site |
| `site.user-permission.revoked` | Revoked user access to site |
| `site.user-permission.updated` | Updated user access to site |

## Site AI and context

| Action ID | Label |
| --- | --- |
| `site.adaptive-schema.updated` | Updated site adaptive schema |
| `site.agent-settings.updated` | Updated site agent settings |
| `site.channel.created` | Created site channel |
| `site.channel.deleted` | Deleted site channel |
| `site.channel.updated` | Updated site channel |
| `site.context-connection.created` | Created site context connection |
| `site.context-connection.deleted` | Deleted site context connection |
| `site.context-connection.sync-completed` | Completed context sync |
| `site.context-connection.sync-failed` | Context sync failed |
| `site.context-connection.sync-skipped` | Skipped context sync |
| `site.context-connection.sync-started` | Started context sync |
| `site.context-connection.updated` | Updated site context connection |
| `site.finding.auto-resolved` | Auto-resolved site finding |
| `site.finding.updated` | Updated site finding |
| `site.mcp-server.created` | Created site MCP server |
| `site.mcp-server.deleted` | Deleted site MCP server |
| `site.mcp-server.updated` | Updated site MCP server |
| `site.topic-findings.deleted` | Deleted site topic findings |
| `site.topic.updated` | Updated site topic |

## Spaces

| Action ID | Label |
| --- | --- |
| `space.lifecycle.created` | Created space |
| `space.lifecycle.deleted` | Deleted space |
| `space.lifecycle.duplicated` | Created duplicate space |
| `space.lifecycle.restored` | Restored space |
| `space.settings.updated` | Updated space settings |

## Access and routing

| Action ID | Label |
| --- | --- |
| `organization.domain.added` | Added domain |
| `organization.domain.removed` | Removed domain |
| `organization.domain.updated` | Updated domain |
| `organization.domain.verification-failed` | Domain verification failed |
| `organization.domain.verification-started` | Started domain verification |
| `organization.domain.verified` | Verified domain |
| `site.domain.attached` | Attached custom domain |
| `site.domain.detached` | Detached custom domain |
| `site.domain.validation-failed` | Custom domain verification failed |
| `site.domain.validation-started` | Started custom domain validation |
| `site.domain.verified` | Verified custom domain |
| `site.publishing-auth.regenerated` | Regenerated publishing authentication key |
| `site.publishing-auth.updated` | Updated publishing authentication |
| `site.redirect.created` | Created site redirect |
| `site.redirect.deleted` | Deleted site redirect |
| `site.redirect.published` | Published site redirect |
| `site.redirect.updated` | Updated site redirect |
| `site.share-link.created` | Created share link |
| `site.share-link.deleted` | Deleted share link |
| `site.share-link.updated` | Updated share link |

## Integrations and workflows

| Action ID | Label |
| --- | --- |
| `gitsync.installation.created` | Connected Git Sync |
| `gitsync.installation.deleted` | Disconnected Git Sync |
| `gitsync.installation.updated` | Updated Git Sync configuration |
| `gitsync.sync.completed` | Completed Git Sync |
| `gitsync.sync.failed` | Git Sync failed |
| `gitsync.sync.skipped` | Skipped Git Sync |
| `gitsync.sync.started` | Started Git Sync |
| `integration.site.connected` | Connected integration to site |
| `integration.site.disconnected` | Disconnected integration from site |
| `integration.site.updated` | Updated site integration |
| `openapi.spec.created` | Created OpenAPI specification |
| `openapi.spec.deleted` | Deleted OpenAPI specification |
| `openapi.spec.processing-completed` | Completed OpenAPI processing |
| `openapi.spec.processing-failed` | OpenAPI processing failed |
| `openapi.spec.processing-started` | Started OpenAPI processing |
| `openapi.spec.update-requested` | Requested OpenAPI specification update |
| `openapi.spec.visibility-updated` | Changed OpenAPI specification visibility |

