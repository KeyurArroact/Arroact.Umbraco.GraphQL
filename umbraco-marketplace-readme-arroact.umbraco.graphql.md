# Arroact Umbraco GraphQL

A powerful GraphQL API package for Umbraco with built-in authentication, interactive IDE dashboard, and comprehensive content/media querying capabilities. Features include lazy loading, BlockGrid support, MultiNodeTreePicker handling, and configurable API key authentication.

## Requirements

- Umbraco 17+

## Installation

Install from NuGet:

```bash
dotnet add package Arroact.Umbraco.GraphQL
```

Build and run your Umbraco site.

## Configuration

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

## Usage

- GraphQL endpoint: `/graphql`
- Backoffice IDE: Go to the **Arroact GraphQL** section and open the **GraphQL IDE** dashboard.

## License

This package is free to use but not open source. See `LICENSE`.
