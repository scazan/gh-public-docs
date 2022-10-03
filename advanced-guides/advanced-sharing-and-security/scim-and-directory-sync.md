---
description: >-
  Auto-provision users and teams from your company directory with our Directory
  Sync (backed by SCIM)
---

# SCIM & Directory Sync

**Directory Sync** in GitBook allows you to automatically provision/deprovision users and teams from your company directory into your GitBook organization.

As users join your directory, they will be created and added to your GitBook organization.

You can also have teams in GitBook synchronize to your directory groups, and have all user memberships synchronize automatically.

### Getting Started

{% hint style="info" %}
Directory Sync is currently an enterprise-only feature that must be manually enabled. If you're interested in using Directory Sync, please contact us.
{% endhint %}

Start by clicking "Setup Directory Sync" from your organization settings SSO page.

![](<../../.gitbook/assets/Screenshot 2022-07-26 at 21.18.04.png>)

You'll be taken through a setup process specific to your Identity Provider. Once the steps are complete, you'll be brought back to GitBook with directory sync enabled.

### Synchronization

Once Directory Sync is setup, all synchronization is done automatically. As you make changes in your Identity Provider, those changes are reflected in GitBook.

## GitBook Teams

You can synchronize your directory groups to GitBook teams. Once you've set up directory sync, click the link to "configure your teams" from the organizationsettings SSO page.

Each group you select will be synchronized to one team in GitBook. The name will be taken, and any members of the group will be synchronized as members of the team.

## Permissions

When a user is provisioned in GitBook, we use the following logic to determine their permission level in the organization:

* If the user has the `gitbookRole` attribute (case sensitive) in the Identity Provider set to a valid GitBook role (`admin` `create` `edit` `review` `comment` `read`), we use that. If the `gitbookRole` attribute is set to `null` or `none`, the user will not be provisioned into GitBook. Refer to your Identity Provider documentation for how to set custom attributes.
* If your organization has SAML enabled, we will default to the SAML default role.
* If we do not find a user-specific role, and if SAML is not enabled, the user will be added with the `read` role.

## Interaction with SAML single sign-on

Directory Sync is designed to work with SAML single sign-on. When an organization has both SAML single sign-on and directory sync set up in the same organization:

* Any users who login with SAML will be linked to their appropriate user in the directory.
* Any users who are provisioned by the directory are required to log in with SAML.

## Security

### A Single Source of Truth

When users and teams are provisioned through Directory Sync, the directory becomes the source of truth. You cannot change a user's name, e-mail address, or organization-level permission through the GitBook interface - it must all be done in the directory.

### User Trust

Users who are created via directory sync can only be members of that organization. If you have multiple GitBook organizations using the same directory sync, users will only be synced to one of the organizations.&#x20;

If you require the same directory for multiple organizations, please get in touch with us.