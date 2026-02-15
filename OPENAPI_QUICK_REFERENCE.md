# OpenAPI Quick Reference Guide

A quick reference for understanding and maintaining the Dialgen OpenAPI specification.

## 📋 Table of Contents

- [File Structure](#file-structure)
- [OpenAPI Specification Sections](#openapi-specification-sections)
- [Common Tasks](#common-tasks)
- [Schema Patterns](#schema-patterns)
- [Response Codes](#response-codes)
- [Validation](#validation)

## 📁 File Structure

```
dialgen-docs/
├── openapi.json              # Main OpenAPI 3.0 specification
├── docs.json                 # Mintlify configuration (references openapi.json)
└── api-reference/
    └── introduction.mdx      # API introduction page
```

## 🔧 OpenAPI Specification Sections

### 1. Info Section

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "Dialgen API",
    "description": "API description",
    "version": "1.0.0",
    "contact": {
      "name": "Dialgen Support",
      "url": "https://sa.dialgen.ai"
    }
  }
}
```

### 2. Servers Section

```json
{
  "servers": [
    {
      "url": "https://sa.dialgen.ai",
      "description": "Production server"
    }
  ]
}
```

### 3. Security Section

```json
{
  "security": [
    {
      "bearerAuth": []
    }
  ],
  "components": {
    "securitySchemes": {
      "bearerAuth": {
        "type": "http",
        "scheme": "bearer",
        "bearerFormat": "JWT",
        "description": "Bearer token authentication"
      }
    }
  }
}
```

### 4. Paths Section

Defines all API endpoints:

```json
{
  "paths": {
    "/api/v1/endpoint": {
      "get": {
        "summary": "Endpoint summary",
        "description": "Detailed description",
        "operationId": "uniqueOperationId",
        "tags": ["Category"],
        "parameters": [...],
        "responses": {...}
      }
    }
  }
}
```

### 5. Components Section

Reusable schemas, responses, and parameters:

```json
{
  "components": {
    "schemas": {
      "SchemaName": {...}
    },
    "responses": {
      "ResponseName": {...}
    },
    "parameters": {
      "ParameterName": {...}
    }
  }
}
```

## 🛠️ Common Tasks

### Adding a New Endpoint

1. **Add to paths section**:

```json
{
  "paths": {
    "/api/v1/new-endpoint": {
      "post": {
        "summary": "New Endpoint",
        "description": "Description here",
        "operationId": "newEndpoint",
        "tags": ["Category"],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/NewRequest"
              }
            }
          }
        },
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
  }
}
```

2. **Add schemas**:

```json
{
  "components": {
    "schemas": {
      "NewRequest": {
        "type": "object",
        "required": ["field1"],
        "properties": {
          "field1": {
            "type": "string",
            "description": "Field description"
          }
        }
      },
      "NewResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean"
          }
        }
      }
    }
  }
}
```

3. **Update docs.json navigation**:

```json
{
  "navigation": {
    "tabs": [
      {
        "tab": "API Reference",
        "groups": [
          {
            "group": "Category",
            "pages": [
              "POST /api/v1/new-endpoint"
            ]
          }
        ]
      }
    ]
  }
}
```

### Adding Query Parameters

```json
{
  "parameters": [
    {
      "name": "paramName",
      "in": "query",
      "description": "Parameter description",
      "required": true,
      "schema": {
        "type": "string",
        "example": "example-value"
      }
    }
  ]
}
```

### Adding Request Body

```json
{
  "requestBody": {
    "required": true,
    "content": {
      "application/json": {
        "schema": {
          "$ref": "#/components/schemas/RequestSchema"
        },
        "example": {
          "field": "value"
        }
      }
    }
  }
}
```

### Adding Response

```json
{
  "responses": {
    "200": {
      "description": "Success description",
      "content": {
        "application/json": {
          "schema": {
            "$ref": "#/components/schemas/ResponseSchema"
          },
          "example": {
            "success": true,
            "data": {}
          }
        }
      }
    }
  }
}
```

## 📊 Schema Patterns

### Basic Object Schema

```json
{
  "SchemaName": {
    "type": "object",
    "required": ["field1", "field2"],
    "properties": {
      "field1": {
        "type": "string",
        "description": "Field description"
      },
      "field2": {
        "type": "number",
        "minimum": 0,
        "maximum": 100
      }
    }
  }
}
```

### Array Schema

```json
{
  "ArraySchema": {
    "type": "array",
    "items": {
      "$ref": "#/components/schemas/ItemSchema"
    },
    "minItems": 1,
    "maxItems": 100
  }
}
```

### Enum Schema

```json
{
  "StatusSchema": {
    "type": "string",
    "enum": ["PENDING", "PROCESSING", "COMPLETED", "FAILED"],
    "description": "Status of the operation"
  }
}
```

### Nested Object Schema

```json
{
  "ParentSchema": {
    "type": "object",
    "properties": {
      "childObject": {
        "type": "object",
        "properties": {
          "nestedField": {
            "type": "string"
          }
        }
      }
    }
  }
}
```

### Schema with Reference

```json
{
  "ComplexSchema": {
    "type": "object",
    "properties": {
      "simpleField": {
        "type": "string"
      },
      "referencedField": {
        "$ref": "#/components/schemas/OtherSchema"
      }
    }
  }
}
```

### Nullable Fields

```json
{
  "NullableSchema": {
    "type": "object",
    "properties": {
      "optionalField": {
        "type": "string",
        "nullable": true,
        "description": "Can be null"
      }
    }
  }
}
```

### Additional Properties

```json
{
  "FlexibleSchema": {
    "type": "object",
    "properties": {
      "knownField": {
        "type": "string"
      }
    },
    "additionalProperties": true
  }
}
```

## 🎯 Response Codes

### Standard Response Codes Used in Dialgen API

| Code | Name | Usage |
|------|------|-------|
| 200 | OK | Successful GET request |
| 202 | Accepted | Async operation accepted (batches) |
| 400 | Bad Request | Invalid parameters or body |
| 401 | Unauthorized | Missing/invalid API key |
| 402 | Payment Required | Insufficient credits |
| 403 | Forbidden | Access denied |
| 404 | Not Found | Resource not found |
| 409 | Conflict | Resource conflict (duplicate call) |
| 500 | Internal Server Error | Server error |

### Response Template

```json
{
  "responses": {
    "200": {
      "description": "Success",
      "content": {
        "application/json": {
          "schema": {...}
        }
      }
    },
    "400": {
      "$ref": "#/components/responses/BadRequest"
    },
    "401": {
      "$ref": "#/components/responses/Unauthorized"
    },
    "404": {
      "$ref": "#/components/responses/NotFound"
    },
    "500": {
      "$ref": "#/components/responses/InternalServerError"
    }
  }
}
```

## ✅ Validation

### Using Swagger Editor

1. Visit https://editor.swagger.io/
2. Copy `openapi.json` contents
3. Paste into editor
4. Check for errors in right panel

### Using Mint CLI

```bash
# Install Mintlify CLI
npm i -g mintlify

# Validate OpenAPI spec
mintlify openapi-check openapi.json
```

### Common Validation Errors

**Missing operationId**
```json
// ❌ Wrong
{
  "get": {
    "summary": "Get Data"
  }
}

// ✅ Correct
{
  "get": {
    "summary": "Get Data",
    "operationId": "getData"
  }
}
```

**Invalid $ref**
```json
// ❌ Wrong
{
  "$ref": "#/components/schemas/NonExistentSchema"
}

// ✅ Correct
{
  "$ref": "#/components/schemas/ExistingSchema"
}
```

**Missing required fields**
```json
// ❌ Wrong
{
  "type": "object",
  "required": ["field1"],
  "properties": {
    "field2": {
      "type": "string"
    }
  }
}

// ✅ Correct
{
  "type": "object",
  "required": ["field1"],
  "properties": {
    "field1": {
      "type": "string"
    }
  }
}
```

## 🔍 Finding Information

### Find all endpoints with a specific tag

Search for `"tags": ["TagName"]` in the paths section.

### Find all schemas

Look in `components.schemas` section.

### Find all error responses

Look in `components.responses` section.

### Find authentication details

Look in `components.securitySchemes` section.

## 📝 Best Practices

### 1. Naming Conventions

- **operationId**: camelCase (e.g., `getAgent`, `createBatch`)
- **Schema names**: PascalCase (e.g., `Agent`, `CallStatus`)
- **Properties**: camelCase (e.g., `agentId`, `phoneNumber`)

### 2. Descriptions

- Always include descriptions for schemas and properties
- Use clear, concise language
- Include examples where helpful

### 3. Examples

- Provide realistic examples
- Include all required fields
- Show common use cases

### 4. Reusability

- Use `$ref` for repeated schemas
- Create reusable response templates
- Define common parameters once

### 5. Versioning

- Include version in info section
- Document breaking changes
- Maintain backward compatibility when possible

## 🚀 Quick Commands

### Start development server
```bash
cd dialgen-docs
mintlify dev
```

### Validate OpenAPI spec
```bash
mintlify openapi-check openapi.json
```

### Format JSON
```bash
# Using jq (if installed)
jq . openapi.json > openapi.formatted.json
```

### Search for specific endpoint
```bash
# Using grep (Git Bash or WSL)
grep -A 5 "/api/v1/agent" openapi.json
```

## 📚 Resources

- [OpenAPI 3.0 Specification](https://swagger.io/specification/)
- [Swagger Editor](https://editor.swagger.io/)
- [Mintlify OpenAPI Docs](https://mintlify.com/docs/api-playground/openapi-setup)
- [JSON Schema Reference](https://json-schema.org/understanding-json-schema/)

## 🎓 Learning Path

1. **Understand OpenAPI basics**
   - Read OpenAPI specification
   - Explore example APIs

2. **Study the Dialgen spec**
   - Review `openapi.json`
   - Understand schema structure

3. **Make small changes**
   - Update descriptions
   - Add examples

4. **Add new endpoints**
   - Follow existing patterns
   - Validate changes

5. **Advanced features**
   - Complex schemas
   - Custom responses
   - Webhooks

## 💡 Tips

- Always validate after making changes
- Use consistent formatting (2-space indentation)
- Keep examples up to date
- Document all required fields
- Use meaningful operationIds
- Group related endpoints with tags
- Reuse schemas when possible
- Include error responses for all endpoints

## 🆘 Troubleshooting

### Endpoint not appearing in docs

1. Check OpenAPI spec is referenced in `docs.json`
2. Verify endpoint path in navigation matches OpenAPI
3. Validate OpenAPI spec for errors
4. Clear browser cache and restart dev server

### Schema not rendering correctly

1. Check for syntax errors in schema definition
2. Verify all `$ref` paths are correct
3. Ensure required fields exist in properties
4. Validate with Swagger Editor

### Examples not showing

1. Add example to schema or response
2. Check JSON syntax is valid
3. Ensure example matches schema structure

## 📊 Dialgen API Statistics

- **Total Endpoints**: 11
- **GET Endpoints**: 6
- **POST Endpoints**: 5
- **Schemas**: 20+
- **Tags**: 3 (Agents, Calls, Batches)
- **Response Codes**: 8 (200, 202, 400, 401, 402, 403, 404, 409, 500)

## 🎯 Summary

This quick reference provides:
- ✅ Common OpenAPI patterns
- ✅ Schema examples
- ✅ Validation methods
- ✅ Best practices
- ✅ Troubleshooting tips
- ✅ Quick commands

Use this guide as a reference when working with the Dialgen OpenAPI specification.
