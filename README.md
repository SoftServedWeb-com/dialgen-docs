# Dialgen API Documentation

This directory contains the Mintlify-based documentation for the Dialgen API.

## 📁 Structure

```
dialgen-docs/
├── openapi.json                    # OpenAPI 3.0 specification (main API spec)
├── docs.json                       # Mintlify configuration
├── MIGRATION.md                    # Migration guide from MDX to OpenAPI
├── README.md                       # This file
├── index.mdx                       # Documentation homepage
├── quickstart.mdx                  # Quick start guide
├── changelog.mdx                   # Version history
├── api-reference/
│   ├── introduction.mdx            # API introduction and authentication
│   └── endpoint/                   # Legacy MDX endpoint files (archived)
└── essentials/                     # Core documentation pages
```

## 🚀 Quick Start

### Local Development

1. Install Mintlify CLI:
   ```bash
   npm i -g mintlify
   ```

2. Start the development server:
   ```bash
   cd dialgen-docs
   mintlify dev
   ```

3. Open your browser to `http://localhost:3000`

### Validate OpenAPI Spec

```bash
mintlify openapi-check openapi.json
```

Or use the [Swagger Editor](https://editor.swagger.io/).

## 📚 Documentation

### API Reference

The API documentation is now powered by OpenAPI 3.0 specification. All endpoints are defined in `openapi.json` and automatically generate:

- Interactive API playground
- Request/response schemas
- HTTP method badges
- Authentication details
- Example requests and responses

### Endpoints Overview

#### <Badge icon="circle" color="green">GET</Badge> Agents
- Get Agent details

#### <Badge icon="circle" color="blue">POST</Badge> / <Badge icon="circle" color="green">GET</Badge> Calls
- Start a single call
- Get live call status
- Get persistent call status
- Get call metrics
- Create call summary

#### <Badge icon="circle" color="blue">POST</Badge> / <Badge icon="circle" color="green">GET</Badge> Batches
- Create new batch campaign
- Get live batch status
- Get batch statistics
- List all batches
- Cancel batch

## 🎨 Mintlify Features

### HTTP Method Badges

Mintlify automatically displays HTTP method badges for each endpoint. The badges are color-coded:
- **GET** - Green (retrieval operations)
- **POST** - Blue (creation/modification operations)

### Interactive API Playground

Each endpoint includes an interactive playground where users can:
- Test API calls directly from the docs
- See real-time responses
- Authenticate using their API key
- View request/response examples

### Schema Documentation

All data models are documented in the OpenAPI spec under `components/schemas`:
- Agent
- Contact
- CallStatus
- BatchOptions
- Error responses
- And more...

## 🔧 Configuration

### docs.json

The main configuration file that defines:
- Navigation structure
- Theme colors
- OpenAPI specification reference
- Footer links
- Logo paths

Key configuration:
```json
{
  "openapi": "openapi.json",
  "navigation": {
    "tabs": [
      {
        "tab": "API Reference",
        "openapi": "openapi.json",
        "groups": [...]
      }
    ]
  }
}
```

### openapi.json

The OpenAPI 3.0 specification that defines:
- All API endpoints
- Request/response schemas
- Authentication methods
- Error responses
- Examples

## 📝 Making Changes

### Adding a New Endpoint

1. Edit `openapi.json`
2. Add the new endpoint under `paths`
3. Define request/response schemas under `components/schemas`
4. Update the navigation in `docs.json` if needed

Example:
```json
"/api/v1/new-endpoint": {
  "get": {
    "summary": "New Endpoint",
    "description": "Description here",
    "operationId": "newEndpoint",
    "tags": ["Category"],
    "responses": {
      "200": {
        "description": "Success",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/NewResponse"
            }
          }
        }
      }
    }
  }
}
```

### Updating Documentation Content

1. For API endpoints: Edit `openapi.json`
2. For guides: Edit the respective `.mdx` files
3. For navigation: Edit `docs.json`

## 🔍 Best Practices

1. **Always validate** the OpenAPI spec after changes
2. **Use consistent naming** for operationIds and schemas
3. **Include examples** for all request/response bodies
4. **Document all parameters** with descriptions
5. **Keep error responses** consistent across endpoints

## 📦 Deployment

The documentation is automatically deployed when changes are pushed to the main branch. Mintlify handles:
- Building the documentation site
- Generating API pages from OpenAPI spec
- Deploying to production

## 🆘 Support

- [Mintlify Documentation](https://mintlify.com/docs)
- [OpenAPI Specification](https://swagger.io/specification/)
- [Dialgen Dashboard](https://sa.dialgen.ai)

## 📄 License

This documentation is part of the Dialgen project.
