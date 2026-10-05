# Error Code Catalog System

This document describes the canonical error code catalog system used in the Callora Backend.

## Overview

The error code catalog provides a single source of truth for all machine-readable error codes emitted by the backend. The system uses a YAML catalog as the authoritative source, with automatic code generation for TypeScript enums, documentation, and OpenAPI schemas.

<!-- BEGIN GENERATED ERROR CODES -->
## Canonical error code catalog

This section is generated from `docs/error-codes.yaml`. Run `npm run error-codes:generate` after changing the catalog.

| Code | Catalog section |
|---|---|
| `BAD_REQUEST` | HTTP status derived / base app codes |
| `UNAUTHORIZED` | HTTP status derived / base app codes |
| `FORBIDDEN` | HTTP status derived / base app codes |
| `NOT_FOUND` | HTTP status derived / base app codes |
| `PAYMENT_REQUIRED` | HTTP status derived / base app codes |
| `TOO_MANY_REQUESTS` | HTTP status derived / base app codes |
| `CONFLICT` | HTTP status derived / base app codes |
| `INTERNAL_SERVER_ERROR` | HTTP status derived / base app codes |
| `BAD_GATEWAY` | HTTP status derived / base app codes |
| `SERVICE_UNAVAILABLE` | HTTP status derived / base app codes |
| `GATEWAY_TIMEOUT` | HTTP status derived / base app codes |
| `VALIDATION_ERROR` | Validation |
| `INVALID_BODY` | Validation |
| `INVALID_QUERY` | Validation |
| `INVALID_PARAMS` | Validation |
| `INVALID_VALUE` | Validation |
| `GATEWAY_AUTH_CONTEXT_MISSING` | Gateway / proxy |
| `UPSTREAM_TARGET_BLOCKED` | Gateway / proxy |
| `INSUFFICIENT_BALANCE` | Billing / Soroban |
| `SOROBAN_RPC_TIMEOUT` | Billing / Soroban |
| `SOROBAN_RPC_ERROR` | Billing / Soroban |
| `BILLING_DEDUCTION_FAILED` | Billing / Soroban |
| `BILLING_REQUEST_NOT_FOUND` | Billing request |
| `DEVELOPER_NOT_FOUND` | Developer / API keys |
| `API_ACCESS_FORBIDDEN` | Developer / API keys |
| `API_KEY_NOT_FOUND` | Developer / API keys |
| `API_KEY_FORBIDDEN` | Developer / API keys |
| `MISSING_REFRESH_TOKEN` | Refresh-token auth |
| `INVALID_REFRESH_TOKEN` | Refresh-token auth |
| `REVOKED_TOKEN` | Refresh-token auth |
| `EXPIRED_TOKEN` | Refresh-token auth |
| `REFRESH_FAILED` | Refresh-token auth |
| `REVOKE_FAILED` | Refresh-token auth |
| `NOT_AUTHENTICATED` | Refresh-token auth |
| `TOKEN_INFO_FAILED` | Refresh-token auth |
| `VAULT_NOT_FOUND` | Vault / deposit |
| `VAULT_BALANCE_RETRIEVAL_FAILED` | Vault / deposit |
| `MISSING_AMOUNT` | Vault / deposit |
| `INVALID_AMOUNT_TYPE` | Vault / deposit |
| `INVALID_AMOUNT_FORMAT` | Vault / deposit |
| `INVALID_NETWORK` | Vault / deposit |
| `NETWORK_MISMATCH` | Vault / deposit |
| `INVALID_SOURCE_ACCOUNT` | Vault / deposit |
| `INVALID_TRANSACTION_INPUT` | Vault / deposit |
| `SOURCE_ACCOUNT_NOT_FOUND` | Vault / deposit |
| `INVALID_CONTRACT_ID` | Vault / deposit |
| `NETWORK_UNAVAILABLE` | Vault / deposit |
| `TRANSACTION_BUILD_FAILED` | Vault / deposit |
| `INTERNAL_ERROR` | Vault / deposit |
| `INVALID_WEBHOOK_REGISTRATION` | Webhooks |
| `INVALID_WEBHOOK_EVENT_TYPES` | Webhooks |
| `WEBHOOK_NOT_FOUND` | Webhooks |
| `INVALID_WEBHOOK_URL` | Webhooks |
| `WEBHOOK_URL_VALIDATION_FAILED` | Webhooks |
| `MISSING_WEBHOOK_SIGNATURE_HEADERS` | Webhooks |
| `INVALID_WEBHOOK_TIMESTAMP` | Webhooks |
| `WEBHOOK_TIMESTAMP_OUT_OF_WINDOW` | Webhooks |
| `MALFORMED_WEBHOOK_SIGNATURE` | Webhooks |
| `INVALID_WEBHOOK_SIGNATURE` | Webhooks |
| `MALFORMED_WEBHOOK_NONCE` | Webhooks |
| `WEBHOOK_NONCE_REPLAYED` | Webhooks |
| `INVALID_DELIVERY_ID` | Webhooks |
| `INVALID_RETRY_POLICY` | Webhooks |
| `DLQ_ENTRY_NOT_FOUND` | Webhooks |
| `INVALID_IP_FORMAT` | IP allowlist |
| `IP_NOT_ALLOWED` | IP allowlist |
| `DATABASE_NOT_AVAILABLE` | DB / infrastructure |
| `IDEMPOTENCY_CONFLICT` | Idempotency |
| `IDEMPOTENCY_IN_PROGRESS` | Idempotency |
| `SIMULATION_FAILED` | Misc / direct middleware responses |
| `INVALID_AUTH_HEADER` | Route-specific / auth overrides (documented in docs/error-codes.md) |
| `MISSING_TOKEN` | Route-specific / auth overrides (documented in docs/error-codes.md) |
| `INVALID_TOKEN` | Route-specific / auth overrides (documented in docs/error-codes.md) |
| `MISSING_CLAIMS` | Route-specific / auth overrides (documented in docs/error-codes.md) |
| `TOKEN_EXPIRED` | Route-specific / auth overrides (documented in docs/error-codes.md) |
| `TOKEN_NOT_ACTIVE` | Route-specific / auth overrides (documented in docs/error-codes.md) |
| `QUOTA_REQUEST_NOT_FOUND` | Quota self-service |
| `QUOTA_REQUEST_ALREADY_RESOLVED` | Quota self-service |
| `INVALID_QUOTA_REQUEST` | Quota self-service |
| `REQUEST_TIMEOUT` | HTTP fallback derived codes referenced by documentation |
| `REQUEST_BODY_TOO_LARGE` | HTTP fallback derived codes referenced by documentation |
| `UNSUPPORTED_MEDIA_TYPE` | HTTP fallback derived codes referenced by documentation |
| `UNPROCESSABLE_ENTITY` | HTTP fallback derived codes referenced by documentation |
| `USAGE_AGGREGATE_NOT_FOUND` | Admin usage management |
| `INVALID_EXPORT_SCHEDULE` | Export schedules |
| `EXPORT_SCHEDULE_NOT_FOUND` | Export schedules |
| `MISSING_AUTH_FIELDS` | Auth |
| `AUTH_NOT_IMPLEMENTED` | Auth |
| `COMPONENT_NOT_CONFIGURED` | Health / dependency probes |
<!-- END GENERATED ERROR CODES -->

## Architecture

### Components

1. **YAML Catalog** (`docs/error-codes.yaml`)
   - Human-readable source of truth
   - Contains code, section, and description for each error
   - Edited manually by developers

2. **TypeScript Enum** (`src/errors/codes.ts`)
   - Auto-generated from YAML
   - Provides type-safe error code constants
   - Includes JSDoc comments with descriptions

3. **Generation Script** (`scripts/generate-error-codes.mjs`)
   - Parses YAML catalog
   - Generates TypeScript enum
   - Updates markdown documentation
   - Updates OpenAPI schema

4. **CI Gate**
   - Validates catalog consistency
   - Ensures generated files are up-to-date
   - Runs in CI/CD pipeline

## YAML Catalog Format

The catalog is structured as a list of error code entries:

```yaml
error_codes:
  - code: ERROR_CODE_NAME
    section: Category Name
    description: Human-readable explanation

  - code: ANOTHER_ERROR
    section: Category Name
    description: When this error occurs
```

### Field Definitions

- **`code`** (required): Error code identifier in SCREAMING_SNAKE_CASE
- **`section`** (required): Category for documentation grouping
- **`description`** (required): Human-readable explanation of when this error occurs

### Validation Rules

1. **Code Format**: Must be SCREAMING_SNAKE_CASE (uppercase letters, numbers, underscores)
2. **Uniqueness**: No duplicate codes allowed
3. **Completeness**: All three fields (code, section, description) required
4. **Consistency**: Code value must match the enum key

## Generated Outputs

### 1. TypeScript Enum (`src/errors/codes.ts`)

```typescript
export const ErrorCode = {
  /** Human-readable description from YAML */
  ERROR_CODE_NAME: "ERROR_CODE_NAME",

  /** Another description */
  ANOTHER_ERROR: "ANOTHER_ERROR",
} as const;

export type ErrorCode = (typeof ErrorCode)[keyof typeof ErrorCode];

export function isErrorCode(value: unknown): value is ErrorCode {
  // Type guard implementation
}
```

Features:
- Const assertion for strict typing
- JSDoc comments with descriptions
- Type guard function
- Warning header about auto-generation

### 2. Markdown Catalog (`docs/error-code-catalog.md`)

The script injects a generated table between markers:

```markdown
<!-- BEGIN GENERATED ERROR CODES -->
## Canonical error code catalog

| Code | Catalog section |
|---|---|
| `ERROR_CODE_NAME` | Category Name |
| `ANOTHER_ERROR` | Category Name |
<!-- END GENERATED ERROR CODES -->
```

### 3. OpenAPI Schema (`docs/openapi.json`)

Adds ErrorCode enum to OpenAPI components:

```json
{
  "components": {
    "schemas": {
      "ErrorCode": {
        "type": "string",
        "enum": ["ERROR_CODE_NAME", "ANOTHER_ERROR"],
        "description": "Canonical Callora backend error code."
      },
      "ErrorResponse": {
        "properties": {
          "code": {
            "$ref": "#/components/schemas/ErrorCode"
          }
        }
      }
    }
  }
}
```

## Workflows

### Adding a New Error Code

1. **Edit YAML catalog**:
   ```bash
   vim docs/error-codes.yaml
   ```

2. **Add entry**:
   ```yaml
   - code: MY_NEW_ERROR
     section: My Feature
     description: Occurs when my feature fails validation
   ```

3. **Generate code**:
   ```bash
   npm run error-codes:generate
   ```

4. **Verify changes**:
   ```bash
   git diff src/errors/codes.ts docs/error-codes.md docs/openapi.json
   ```

5. **Commit all files**:
   ```bash
   git add docs/error-codes.yaml src/errors/codes.ts docs/error-codes.md docs/openapi.json
   git commit -m "feat: add MY_NEW_ERROR code"
   ```

### Modifying an Existing Code

1. **Edit the YAML entry** (description or section only - never change the code value)
2. **Regenerate**: `npm run error-codes:generate`
3. **Commit**: Include all updated files

**WARNING**: Changing a code value is a breaking change for API clients. Deprecate the old code and add a new one instead.

### Removing a Code

1. **Deprecation first**: Mark as deprecated in description
2. **Wait for migration**: Allow time for clients to update
3. **Remove from YAML**: After deprecation period
4. **Regenerate**: `npm run error-codes:generate`

## Using Error Codes in Code

### Importing

```typescript
import { ErrorCode } from './errors/codes.js';
```

### In Error Classes

```typescript
throw new BadRequestError('Invalid input', ErrorCode.VALIDATION_ERROR);
```

### Type-Safe Checks

```typescript
if (error.code === ErrorCode.INSUFFICIENT_BALANCE) {
  // Handle insufficient balance
}
```

### Runtime Validation

```typescript
import { isErrorCode } from './errors/codes.js';

if (isErrorCode(unknownValue)) {
  // unknownValue is now typed as ErrorCode
}
```

## CI/CD Integration

### Pre-commit Hook

Add to `.git/hooks/pre-commit`:

```bash
#!/bin/bash
npm run error-codes:check || {
  echo "Error codes are out of sync. Run: npm run error-codes:generate"
  exit 1
}
```

### GitHub Actions

Add to `.github/workflows/ci.yml`:

```yaml
- name: Check error code generation
  run: npm run error-codes:check
```

### package.json Scripts

```json
{
  "scripts": {
    "error-codes:generate": "node scripts/generate-error-codes.mjs",
    "error-codes:check": "node scripts/generate-error-codes.mjs --check",
    "prebuild": "npm run error-codes:check"
  }
}
```

## Testing

### Unit Tests

Run script tests:

```bash
node scripts/generate-error-codes.test.mjs
```

### Coverage

Test scenarios:
- ✅ Valid YAML parsing
- ✅ Duplicate detection
- ✅ Format validation
- ✅ TypeScript generation
- ✅ Markdown update
- ✅ OpenAPI schema update
- ✅ Check mode validation
- ✅ Missing catalog handling
- ✅ Idempotency

### Integration Tests

```bash
# Generate and verify
npm run error-codes:generate
npm run error-codes:check # Should pass

# Modify generated file
echo "// test" >> src/errors/codes.ts
npm run error-codes:check # Should fail
```

## Migration from Legacy System

### Before (Manual TypeScript)

```typescript
// src/errors/errorCatalog.ts
export const ErrorCode = {
  // HTTP status derived
  BAD_REQUEST: "BAD_REQUEST",
  UNAUTHORIZED: "UNAUTHORIZED",
  // ... manually maintained
} as const;
```

### After (YAML + Codegen)

```yaml
# docs/error-codes.yaml
error_codes:
  - code: BAD_REQUEST
    section: HTTP status derived
    description: The request is invalid
```

Generated TypeScript is identical, but source of truth is YAML.

## Benefits

1. **Single Source of Truth**: YAML catalog is the definitive reference
2. **Type Safety**: Generated TypeScript enum provides compile-time checks
3. **Documentation**: Automatically updates docs and OpenAPI
4. **Consistency**: CI gate prevents drift between catalog and code
5. **Review**: YAML diffs are easier to review than TypeScript
6. **Validation**: Format and uniqueness checks prevent errors
7. **Maintainability**: Clear separation of data and code

## Troubleshooting

### "Duplicate error codes" Error

**Cause**: Same code appears multiple times in YAML

**Solution**: Search for duplicates and remove/rename

```bash
grep -n "code: YOUR_CODE" docs/error-codes.yaml
```

### "Invalid error code format" Error

**Cause**: Code doesn't match SCREAMING_SNAKE_CASE

**Solution**: Use only uppercase letters, numbers, and underscores

```yaml
# Bad
- code: myError
- code: My-Error
- code: my_error

# Good
- code: MY_ERROR
```

### "No error codes found" Error

**Cause**: YAML syntax error or empty catalog

**Solution**: Validate YAML syntax

```bash
# Install yamllint
pip install yamllint

# Validate
yamllint docs/error-codes.yaml
```

### Generated Files Out of Sync

**Cause**: Manual edits to generated files

**Solution**: Regenerate from YAML

```bash
npm run error-codes:generate
```

### CI Check Fails

**Cause**: Generated files not committed

**Solution**: Run generation and commit all changes

```bash
npm run error-codes:generate
git add src/errors/codes.ts docs/error-codes.md docs/openapi.json
git commit --amend --no-edit
```

## Security Considerations

1. **No Secrets in Errors**: Never include sensitive data in error descriptions
2. **Client-Safe Messages**: Descriptions may appear in client-facing documentation
3. **Stable Codes**: Error codes are part of the public API contract
4. **Audit Trail**: All changes tracked in git history

## Performance

- **Build Time**: ~50ms to parse YAML and generate files
- **Runtime**: Zero overhead - generated code is identical to hand-written
- **CI Time**: Check mode adds ~30ms to builds

## Future Enhancements

Potential improvements:
- [ ] Add i18n support for error messages
- [ ] Generate error code documentation site
- [ ] Add severity levels to catalog
- [ ] Generate Prometheus metrics labels
- [ ] Add suggested HTTP status codes to catalog
- [ ] Validate error usage in codebase

## References

- [Error Response Format](./error-codes.md) - Full error documentation
- [YAML Specification](https://yaml.org/spec/1.2.2/)
- [TypeScript Enums](https://www.typescriptlang.org/docs/handbook/enums.html)
- [OpenAPI Schema Objects](https://swagger.io/specification/#schema-object)
