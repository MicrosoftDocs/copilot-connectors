[[_TOC_]]

# Error Code 1010 - External Group Quota - Jira Cloud

Use this guide if you see error code `1010` and the message indicates that the Microsoft 365 tenant has reached the quota for external groups.

## Error meaning

The tenant has reached the current limit for external groups used by Microsoft Graph connectors.

Typical error text:

`External groups per Microsoft 365 tenant has reached the 100,000 quota.`

## What this usually means for Jira Cloud

Jira Cloud ACL ingestion may create or sync many external groups, for example Jira groups or project-role-based groups. If the tenant-wide external group count reaches the platform quota, new group sync operations can fail.

## What to collect

- Full error screenshot on connector page
- Connection ID
- Tenant ID
- Approximate time when the error first appeared, in UTC
- Confirmation whether the error is reproducible

## What to do

This is a tenant quota issue and the quota needs to be increased.

- Request a quota increase for external groups in the Microsoft 365 tenant.
