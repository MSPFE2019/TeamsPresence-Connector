# Teams Presence custom connector

This repository contains an OpenAPI 2.0 definition for a Power Platform custom
connector that reads a user's current Microsoft Teams presence through
Microsoft Graph.

## API

The connector exposes:

```text
GET https://graph.microsoft.com/v1.0/communications/presences/{user-id}
```

`user-id` is the user's Microsoft Entra object ID (GUID), not an email address
or display name. A successful response includes `availability` and `activity`,
for example `Available` and `Available`.

## Requirements

- A Microsoft Entra tenant with Microsoft Teams
- Permission to create or update a Power Platform custom connector
- Admin consent for the Microsoft Graph delegated permission
  `Presence.Read.All`

## Import the connector

1. In Power Automate or Power Apps, open **Data > Custom connectors**.
2. Select **New custom connector > Import an OpenAPI file**.
3. Select `Teams-Presence-API.swagger.json`.
4. On the **Security** tab, select **OAuth 2.0** and **Azure Active Directory**.
5. Enter the application registration's client ID and client secret.
6. Use the generated redirect URL in the app registration's Web redirect URI.
7. Save the connector, create a connection, and test it with a user object ID.

The OpenAPI definition uses the Microsoft identity platform v2 endpoints and
requests the `Presence.Read.All` delegated scope. The connector's OAuth
configuration may still require the client ID and secret to be entered in the
Power Platform designer because those values are tenant-specific.

## Register the application

Create an app registration in the Microsoft Entra admin center, add Microsoft
Graph delegated permission `Presence.Read.All`, and grant admin consent.
Create a client secret only if the connector designer requires one; store it in
the Power Platform connection configuration and never commit it to this
repository.

Microsoft Graph documentation:

- [Get user presence](https://learn.microsoft.com/graph/api/presence-get?view=graph-rest-1.0)
- [Presence resource type](https://learn.microsoft.com/graph/api/resources/presence?view=graph-rest-1.0)
- [Microsoft Graph permissions reference](https://learn.microsoft.com/graph/permissions-reference)

## Troubleshooting

- **403 Forbidden:** confirm `Presence.Read.All` is granted and admin consent
  has been applied.
- **404 Not Found:** verify that the supplied value is a valid Entra object ID
  for a user in the tenant.
- **429 Too Many Requests:** honor the Graph `Retry-After` response and avoid
  polling presence more frequently than necessary.
