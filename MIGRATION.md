# API Documentation Migration to OpenAPI

This document describes the migration from individual MDX endpoint files to OpenAPI specification.

## What Changed

### Before
- Individual MDX files for each endpoint in `api-reference/endpoint/`
- Manual maintenance of endpoint documentation
- Inconsistent formatting across endpoints

### After
- Single `openapi.json` file containing all API specifications
- Automatic generation of endpoint pages from OpenAPI spec
- Consistent formatting and structure
- HTTP method badges automatically displayed by Mintlify

## Benefits

1. **Single Source of Truth**: All API specifications in one file
2. **Automatic Validation**: OpenAPI spec can be validated using tools like Swagger Editor
3. **Better Consistency**: All endpoints follow the same structure
4. **HTTP Method Badges**: Mintlify automatically displays HTTP method badges (GET, POST, etc.)
5. **Interactive Playground**: Built-in API playground for testing endpoints
6. **Easier Maintenance**: Update one file instead of multiple MDX files

## File Structure

```
dialgen-docs/
├── openapi.json              # OpenAPI 3.0 specification
├── docs.json                 # Updated to reference OpenAPI spec
├── api-reference/
│   ├── introduction.mdx      # API introduction (kept)
│   └── endpoint/             # Old MDX files (can be archived/removed)
└── MIGRATION.md              # This file
```

## OpenAPI Specification Details

### Base URL
```
https://sa.dialgen.ai
```

### Authentication
Bearer token authentication via `Authorization` header:
```
Authorization: Bearer <YOUR_API_KEY>
```

### Endpoints

#### Agents
- `GET /api/v1/agent` - Get Agent details

#### Calls
- `POST /api/v1/call/dial` - Start a Single Call
- `GET /api/v1/status/call` - Get Live Call Status
- `GET /api/v1/call/check-status` - Persistent Call Status
- `GET /api/v1/call/get-metric` - Get Call Metrics
- `POST /api/v1/call/create-summary` - Create Call Summary

#### Batches
- `POST /api/v1/batch` - Create a New Call Batch (Campaign)
- `GET /api/v1/status/batch` - Get Live Batch Status (Detailed)
- `GET /api/v1/batch/check-status` - Get Batch Statistics (Overall Progress)
- `GET /api/v1/batch/list` - List All Batches
- `POST /api/v1/batch/cancel` - Cancel Batch

## Mintlify Features

### HTTP Method Badges
Mintlify automatically displays HTTP method badges for each endpoint:
- <Badge icon="circle" color="green">GET</Badge> for GET requests
- <Badge icon="circle" color="blue">POST</Badge> for POST requests

### API Playground
Each endpoint now has an interactive API playground where users can:
- Test endpoints directly from the documentation
- See request/response examples
- Authenticate using their API key

### Schema Documentation
All request/response schemas are defined in the OpenAPI spec under `components/schemas`:
- Agent
- DialSingleRequest/Response
- CallStatus
- BatchStatusResponse
- And more...

## Validation

To validate the OpenAPI specification:

1. **Using Swagger Editor**:
   - Visit https://editor.swagger.io/
   - Copy the contents of `openapi.json`
   - Paste into the editor

2. **Using Mint CLI** (if installed):
   ```bash
   mint openapi-check openapi.json
   ```

## Next Steps

1. ✅ Created `openapi.json` with all endpoint specifications
2. ✅ Updated `docs.json` to reference the OpenAPI spec
3. ⏳ Test the documentation locally or in staging
4. ⏳ Archive or remove old MDX endpoint files (optional)
5. ⏳ Update any external references to the old endpoint URLs

## Rollback Plan

If needed, you can rollback by:
1. Reverting the `docs.json` changes
2. Restoring the old navigation structure with MDX file references
3. Keeping the `openapi.json` for future use

## Resources

- [Mintlify OpenAPI Setup](https://mintlify.com/docs/api-playground/openapi-setup)
- [OpenAPI Specification 3.0](https://swagger.io/specification/)
- [Mintlify Badge Component](https://mintlify.com/docs/components/badge)
