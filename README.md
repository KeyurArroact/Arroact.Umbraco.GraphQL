# Arroact Umbraco GraphQL

GraphQL support for Umbraco.

## Requirements

- Umbraco 17+

## Install

Install from NuGet:

```bash
dotnet add package Arroact.Umbraco.GraphQL
```

Build and run your Umbraco site.

## Configure

Add settings in `appsettings.json`:

```json
{
  "Arroact": {
    "GraphQL": {
      "Enabled": true,
      "ApiKey": "CHANGE-ME",
      "EnabuledConsole": false
    }
  }
}
```

Restart the application after changing configuration.

## Use

- **GraphQL endpoint**: `/graphql`
- **Umbraco backoffice IDE**: Go to the **Arroact GraphQL** section and open the **GraphQL IDE** dashboard.

## License

Freeware proprietary license. See `LICENSE`.
