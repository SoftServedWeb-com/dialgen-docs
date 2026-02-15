# HTTP Method Badges in Mintlify

This document shows how HTTP method badges appear in the Dialgen API documentation.

## What are HTTP Method Badges?

HTTP method badges are visual indicators that show the HTTP method (GET, POST, PUT, DELETE, etc.) for each API endpoint. Mintlify automatically generates these badges when using OpenAPI specifications.

## Badge Appearance

In the Dialgen documentation, badges appear in several places:

### 1. Navigation Sidebar

When browsing the API Reference section, each endpoint shows its HTTP method badge:

```
API Reference
├── Introduction
├── Agents
│   └── GET /api/v1/agent
├── Calls
│   ├── POST /api/v1/call/dial
│   ├── GET /api/v1/status/call
│   ├── GET /api/v1/call/check-status
│   ├── GET /api/v1/call/get-metric
│   └── POST /api/v1/call/create-summary
└── Batches
    ├── POST /api/v1/batch
    ├── GET /api/v1/status/batch
    ├── GET /api/v1/batch/check-status
    ├── GET /api/v1/batch/list
    └── POST /api/v1/batch/cancel
```

### 2. Endpoint Pages

At the top of each endpoint page, a prominent badge displays the HTTP method:

**Example: Get Agent**
```
[GET] Get Agent
Retrieves the configuration and details for a specific AI agent.
```

**Example: Start a Single Call**
```
[POST] Start a Single Call
Initiates a single outbound call immediately.
```

### 3. Search Results

When users search for endpoints, the badges help identify the method at a glance.

## Badge Colors

Mintlify uses color-coding to make HTTP methods instantly recognizable:

| Method | Color | Use Case |
|--------|-------|----------|
| GET | Green | Retrieving data (read operations) |
| POST | Blue | Creating or submitting data (write operations) |
| PUT | Orange | Updating existing data |
| PATCH | Purple | Partially updating data |
| DELETE | Red | Removing data |

### Dialgen API Methods

In the Dialgen API, we use:

- **GET** (Green) - 6 endpoints
  - Get Agent
  - Get Live Call Status
  - Persistent Call Status
  - Get Call Metrics
  - Get Live Batch Status
  - Get Batch Statistics
  - List All Batches

- **POST** (Blue) - 5 endpoints
  - Start a Single Call
  - Create Call Summary
  - Create a New Call Batch
  - Cancel Batch

## Using Badges in MDX Content

You can also manually add badges in MDX content using the Badge component:

### Syntax

```mdx
<Badge icon="circle" color="green">GET</Badge>
<Badge icon="circle" color="blue">POST</Badge>
<Badge icon="circle" color="orange">PUT</Badge>
<Badge icon="circle" color="red">DELETE</Badge>
```

### Example Usage

```mdx
## Endpoint Overview

The Dialgen API provides several endpoints:

- <Badge icon="circle" color="green">GET</Badge> `/api/v1/agent` - Retrieve agent details
- <Badge icon="circle" color="blue">POST</Badge> `/api/v1/call/dial` - Start a call
- <Badge icon="circle" color="green">GET</Badge> `/api/v1/status/call` - Check call status
```

### With Icons

Badges can include various icons from Font Awesome:

```mdx
<Badge icon="check" color="green">Success</Badge>
<Badge icon="clock" color="orange">Pending</Badge>
<Badge icon="ban" color="red">Failed</Badge>
<Badge icon="circle-check" color="green">Completed</Badge>
```

## Benefits of HTTP Method Badges

### 1. Visual Clarity
Users can quickly identify the type of operation without reading the full description.

### 2. Consistent Design
All endpoints follow the same visual pattern, making the documentation easier to navigate.

### 3. Accessibility
Color-coding helps users with different learning styles quickly understand the API structure.

### 4. Professional Appearance
Badges give the documentation a polished, modern look that matches industry standards.

### 5. Quick Scanning
Developers can scan the sidebar and immediately know which endpoints read data vs. modify data.

## Automatic Generation

With OpenAPI specification, badges are automatically generated based on the HTTP method defined in the spec:

```json
{
  "paths": {
    "/api/v1/agent": {
      "get": {
        "summary": "Get Agent",
        ...
      }
    },
    "/api/v1/call/dial": {
      "post": {
        "summary": "Start a Single Call",
        ...
      }
    }
  }
}
```

Mintlify reads the `"get"` or `"post"` key and automatically:
1. Generates the appropriate badge
2. Applies the correct color
3. Displays it in the navigation and page header

## Customization

While Mintlify automatically generates badges from the OpenAPI spec, you can customize:

### Badge Appearance in docs.json

```json
{
  "api": {
    "playground": {
      "display": "interactive"
    }
  }
}
```

### Custom Badge Styles

For custom badges in content, you can use various combinations:

```mdx
<!-- Status badges -->
<Badge color="green">Active</Badge>
<Badge color="red">Deprecated</Badge>
<Badge color="orange">Beta</Badge>

<!-- With icons -->
<Badge icon="star" color="yellow">Premium</Badge>
<Badge icon="lock" color="gray">Requires Auth</Badge>

<!-- HTTP methods -->
<Badge icon="circle" color="green">GET</Badge>
<Badge icon="circle" color="blue">POST</Badge>
```

## Best Practices

### 1. Consistency
Always use the same color for the same HTTP method across all documentation.

### 2. Clarity
Ensure badges are visible against the background color.

### 3. Accessibility
Don't rely solely on color - the method name should always be visible.

### 4. Placement
Place badges at the beginning of endpoint names for easy scanning.

### 5. Documentation
Explain what each badge color means in your introduction or getting started guide.

## Examples from Dialgen API

### Agent Endpoints

```
GET /api/v1/agent
```
- **Badge**: Green GET badge
- **Purpose**: Retrieve agent configuration
- **Operation**: Read-only

### Call Endpoints

```
POST /api/v1/call/dial
GET /api/v1/status/call
GET /api/v1/call/check-status
GET /api/v1/call/get-metric
POST /api/v1/call/create-summary
```

- **POST badges**: Blue - Creating new calls or summaries
- **GET badges**: Green - Retrieving call information

### Batch Endpoints

```
POST /api/v1/batch
GET /api/v1/status/batch
GET /api/v1/batch/check-status
GET /api/v1/batch/list
POST /api/v1/batch/cancel
```

- **POST badges**: Blue - Creating batches or canceling them
- **GET badges**: Green - Retrieving batch information

## Testing Badge Display

To test how badges appear:

1. Start local development server:
   ```bash
   mintlify dev
   ```

2. Navigate to API Reference section

3. Check that badges appear:
   - In the sidebar navigation
   - On endpoint pages
   - In search results

4. Verify colors match HTTP methods:
   - GET = Green
   - POST = Blue

## Troubleshooting

### Badges Not Appearing

If badges don't appear:

1. **Check OpenAPI reference in docs.json**
   ```json
   {
     "openapi": "openapi.json"
   }
   ```

2. **Verify navigation uses OpenAPI paths**
   ```json
   {
     "pages": [
       "GET /api/v1/agent",
       "POST /api/v1/call/dial"
     ]
   }
   ```

3. **Validate OpenAPI spec**
   ```bash
   mintlify openapi-check openapi.json
   ```

### Wrong Colors

If colors are incorrect:
- Verify the HTTP method in the OpenAPI spec matches the intended operation
- Check that the method key (`get`, `post`, etc.) is lowercase
- Ensure no typos in the method name

## Resources

- [Mintlify Badge Component](https://mintlify.com/docs/components/badge)
- [Mintlify OpenAPI Setup](https://mintlify.com/docs/api-playground/openapi-setup)
- [OpenAPI Specification](https://swagger.io/specification/)
- [HTTP Methods Reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

## Summary

HTTP method badges in Mintlify provide:
- ✅ Visual clarity for API endpoints
- ✅ Consistent design across documentation
- ✅ Quick identification of operation types
- ✅ Professional, modern appearance
- ✅ Automatic generation from OpenAPI spec

The Dialgen API documentation now includes automatic HTTP method badges for all 11 endpoints, making it easier for developers to understand and navigate the API.
