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
      "EnabledConsole": false
    }
  }
}
```

Restart the application after changing configuration.

## Usage

- GraphQL endpoint: `/graphql`
- Backoffice IDE: Go to the **Arroact GraphQL** section and open the **GraphQL IDE** dashboard.

## What's New in Version 2.0.0

### Child Content Filtering and Ordering
You can now filter and order child content using powerful query arguments:

- **`where`**: Filter child content by contentType, name, published status, or custom property values
- **`orderBy`**: Sort children by multiple fields (name, createDate, updateDate, sortOrder, etc.)
- **`orderByProperty`**: Sort by custom property values with ascending/descending direction
- **`first`**: Limit the number of results
- **`skip`**: Skip a number of results for pagination

**Example Query:**
```graphql
query {
  contentById(id: "your-content-id") {
    name
    children(
      first: 10,
      where: { contentType: "blogPost", published: true },
      orderByProperty: { propertyKey: "publishDate", direction: DESC }
    ) {
      items {
        name
        contentType
        properties {
          key
          value
        }
      }
      totalCount
      pageInfo {
        hasNextPage
      }
    }
  }
}
```

### Enhanced Dashboard
- Interactive query builder with support for nested arguments
- Expandable argument sections for complex input types
- Visual tree structure for exploring schema and building queries

## Support

For support, feature requests, or bug reports:

- **Website**: https://www.arroact.com
- **Company**: Arroact Technologies Pvt. Ltd.

## 📄 License

Copyright © Arroact Technologies Pvt. Ltd.

This is a commercial product. Please contact Arroact Technologies for licensing information.

## 🏢 About Arroact

Arroact Technologies Pvt. Ltd. specializes in developing powerful tools and extensions for Umbraco CMS, helping businesses build better web experiences.

Made with ❤️ by Arroact Technologies
