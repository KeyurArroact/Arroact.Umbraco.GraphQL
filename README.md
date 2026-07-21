# Arroact Umbraco GraphQL

A powerful GraphQL API package for Umbraco with built-in authentication, interactive IDE dashboard, and comprehensive content/media querying capabilities. Version 5 supports Umbraco 18 and includes lazy loading, BlockGrid, MultiNodeTreePicker, and ElementPicker support, plus configurable API key authentication.

## Version Compatibility

| Package version | Compatible Umbraco version |
| --- | --- |
| Version 4.x | Umbraco 17 |
| Version 5.x | Umbraco 18 |

## Requirements

Install the package version that matches your Umbraco major version:

- **Version 4.x** requires **Umbraco 17**
- **Version 5.x** requires **Umbraco 18**

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
      "EnabledConsole": false
    }
  }
}
```

Restart the application after changing configuration.

## Use

- **GraphQL endpoint**: `/graphql`
- **Umbraco backoffice IDE**: Go to the **Arroact GraphQL** section and open the **GraphQL IDE** dashboard.

## GraphQL IDE

The built-in GraphQL IDE is accessible directly inside the Umbraco backoffice. It provides a full-featured environment for writing, testing, and exploring your GraphQL API without any external tools.

### Layout

The IDE is divided into three panels:

- **Left — Builder**: Visual schema explorer and query builder
- **Middle — Editor**: Query/Variables/cURL/Settings tabs
- **Right — Response**: Collapsible JSON tree result viewer

---

### Builder Panel

The Builder panel reads the live schema via introspection and lets you construct queries visually.

**How to use:**
1. Expand a root query (e.g. `getContent`, `getContentById`, `getBlockGridById`)
2. Check the checkbox next to it to select the operation
3. Expand **[Arguments]** to see all available arguments for that operation
4. Check scalar arguments (`id`, `culture`, `first`, `skip`) to include them in the query
5. For complex input type arguments (`where`, `orderBy`, `orderByProperty`), expand the argument row with the `▶` arrow to see its sub-fields, then check individual sub-fields (e.g. `propertyKey`, `propertyValue`, `direction`)
6. Expand the return type fields and check which fields to include in the response

The query is auto-generated in the **Query** tab as you make selections.

**Argument types supported:**
- **Scalar** (`String`, `Int`, `Boolean`, `UUID`) — generates a type-correct placeholder value
- **INPUT_OBJECT** (e.g. `where: ContentNodeFilterInput`) — expands to show all sub-fields; generates `where: { propertyKey: "", propertyValue: "" }`
- **LIST of INPUT_OBJECT** (e.g. `orderBy: [ContentNodeSortInput]`) — shown with `(list)` hint; generates `orderBy: [{ name: "" }]`

**Children arguments** (`first`, `skip`, `where`, `orderBy`, `orderByProperty`, `culture`) are fully supported and are included inline when `children` is selected as a field.

---

### Query Editor Tab

- Write or paste any GraphQL query directly
- Queries auto-populate from the Builder
- Keyboard shortcuts:
  - `Ctrl+Enter` / `Cmd+Enter` — Execute query
  - `Ctrl+Shift+F` / `Cmd+Shift+F` — Format/indent query

---

### Variables Tab

- Enter query variables as a JSON object (e.g. `{ "id": "abc-123" }`)
- Variables are automatically passed with the query on execution

---

### cURL & Postman Tab

- **cURL Command** — generates a ready-to-run `curl` command including all headers and the current query/variables; click **Copy** to copy to clipboard
- **Postman JSON** — generates the raw JSON body for use in Postman's Body → Raw tab; click **Copy** to copy to clipboard

---

### Settings Tab

- **GraphQL Endpoint** — override the default endpoint URL (default: `{origin}/graphql`)
- **HTTP Headers** — add, enable/disable, or remove custom headers sent with every request (e.g. `Authorization: Bearer <api-key>`). Headers are persisted in `localStorage`.

---

### Response Panel

- Displays the result as a **collapsible JSON tree**
- Click `▶` / `▼` to expand or collapse any object or array
- Collapsed nodes show item/key count at a glance
- **GraphQL errors** are displayed in a structured error list with location (line/column) and path
- Execution time is shown in milliseconds next to the Response panel header

---

### Query History

Query history is accessible from the Builder panel. Every executed query is saved automatically (up to 50 entries) with timestamp and success/error status. Click any history item to restore the query and variables. Use **Clear All** to reset history. History is persisted in `localStorage`.

---

### API Key Status

On load, the IDE checks whether an API key is configured. If no key is set in `appsettings.json`, a warning banner is shown with instructions. When a key is detected, the `Authorization: Bearer <key>` header is auto-populated so queries work immediately.

## What's New in Version 5.0.0

### Umbraco 18 Compatibility

Version 5 is compatible with Umbraco 18. For Umbraco 17 projects, use Version 4.

### ElementPicker Support

Properties using `Umbraco.ElementPicker` are returned as structured element data. Both single and multiple selections are supported. Each selected element includes its `id`, `contentType`, optional `name`, and recursively resolved `properties`.

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
