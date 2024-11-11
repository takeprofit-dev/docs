Install the [Mintlify CLI](https://www.npmjs.com/package/mintlify) to preview the documentation changes locally. To install, use the following command

```bash
npm i -g mintlify
```

Run the following command at the root of your documentation (where mint.json is)

```bash
mintlify dev
```

Postman to OpenAPI

```bash
npm i -g postman-to-openapi@3.0.1
```

```bash
p2o ./docs/partner-api/postman.json -f ./docs/partner-api/openapi.json -o ./docs/partner-api/p2o.options.json
```

Generate clients

```bash
npm install -g @openapitools/openapi-generator-cli
```

Python

```bash
openapi-generator-cli generate -i openapi.json -g python -o ./sdk/python-client
```

JS

```bash
openapi-generator-cli generate -i openapi.json -g javascript -o ./sdk/javascript-client
```

Go

```bash
openapi-generator-cli generate -i openapi.json -g go -o ./sdk/go-client
```

C#

```bash
openapi-generator-cli generate -i openapi.json -g csharp -o ./sdk/csharp-client
```

# Link API Documentation

The Link API allows partners to manage the linkage between their own securities and the securities provided by TakeProfit. This includes creating, retrieving, and deleting links between securities.

## Overview

The Link API provides methods to:

- List all linked securities.
- Get a linked security by its GUID.
- Link a security to a partner's own identifier.
- Unlink a security.

## Base URL

```plaintext
https://api.dev.tpinf.in
```

## Authorization

**Type**: Bearer Token

To access the API, you must use an access token obtained through the [Auth API](#). The token should be passed in the `accesstoken` header.

**Example Authorization Header:**

```
accesstoken: YOUR_ACCESS_TOKEN_HERE
```

---

## Endpoints

- [ListLinkedSecurities](#listlinkedsecurities)
- [GetLinkedSecurity](#getlinkedsecurity)
- [LinkSecurity](#linksecurity)
- [UnlinkSecurity](#unlinksecurity)

---

## ListLinkedSecurities

Retrieve a list of all securities linked by the partner.

### HTTP Request

`POST /takeprofit.partner.external.security.v1.LinkApi.ListLinkedSecurities`

### Headers

- `accesstoken`: Access token (required)
- `Content-Type`: `application/json`

### Request Body

```json
{}
```

### Response

**Success (HTTP 200):**

```json
{
	"status": {
		"code": 0,
		"message": "",
		"details": []
	},
	"linked_securities": [
		{
			"security_guid": "6ef11658-5a1c-4baf-9387-d977dcca6129",
			"partner_security_id": "124"
		}
		// Other linked securities...
	]
}
```

**Response Fields:**

- `status`: Operation status.
  - `code` (integer): Status code (`0` indicates success).
  - `message` (string): Status message.
  - `details` (array): Additional details.
- `linked_securities` (array): List of linked securities.
  - Each item contains:
    - `security_guid` (string): GUID of the security in TakeProfit system.
    - `partner_security_id` (string): Partner's own identifier for the security.

### Example Request

```bash
curl --location 'https://api.dev.tpinf.in/takeprofit.partner.external.security.v1.LinkApi.ListLinkedSecurities' \
--header 'accesstoken: YOUR_ACCESS_TOKEN_HERE' \
--header 'Content-Type: application/json' \
--data '{}'
```

### Example Response

<details>
<summary>Successful Response</summary>

```json
{
	"status": {
		"code": 0,
		"message": "",
		"details": []
	},
	"linked_securities": [
		{
			"security_guid": "6ef11658-5a1c-4baf-9387-d977dcca6129",
			"partner_security_id": "124"
		}
	]
}
```

</details>

---

## GetLinkedSecurity

Retrieve the linkage information for a specific security.

### HTTP Request

`POST /takeprofit.partner.external.security.v1.LinkApi.GetLinkedSecurity`

### Headers

- `accesstoken`: Access token (required)
- `Content-Type`: `application/json`

### Request Body

```json
{
	"security_guid": "SECURITY_GUID"
}
```

**Fields:**

- `security_guid` (string, required): GUID of the security in TakeProfit system.

### Response

**Success (HTTP 200):**

```json
{
	"status": {
		"code": 0,
		"message": "",
		"details": []
	},
	"linked_security": {
		"security_guid": "6ef11658-5a1c-4baf-9387-d977dcca6129",
		"partner_security_id": "124"
	}
}
```

**Response Fields:**

- `status`: Operation status.
- `linked_security`: The linked security information.
  - `security_guid` (string): GUID of the security.
  - `partner_security_id` (string): Partner's identifier.

### Example Request

```bash
curl --location 'https://api.dev.tpinf.in/takeprofit.partner.external.security.v1.LinkApi.GetLinkedSecurity' \
--header 'accesstoken: YOUR_ACCESS_TOKEN_HERE' \
--header 'Content-Type: application/json' \
--data '{
    "security_guid": "6ef11658-5a1c-4baf-9387-d977dcca6129"
}'
```

### Example Response

<details>
<summary>Successful Response</summary>

```json
{
	"status": {
		"code": 0,
		"message": "",
		"details": []
	},
	"linked_security": {
		"security_guid": "6ef11658-5a1c-4baf-9387-d977dcca6129",
		"partner_security_id": "124"
	}
}
```

</details>

---

## LinkSecurity

Link a security to the partner's own security identifier. This will overwrite any existing link.

### HTTP Request

`POST /takeprofit.partner.external.security.v1.LinkApi.LinkSecurity`

### Headers

- `accesstoken`: Access token (required)
- `Content-Type`: `application/json`

### Request Body

```json
{
	"security_guid": "SECURITY_GUID",
	"partner_security_id": "PARTNER_SECURITY_ID"
}
```

**Fields:**

- `security_guid` (string, required): GUID of the security in TakeProfit system.
- `partner_security_id` (string, required): Partner's own identifier for the security.

### Response

**Success (HTTP 200):**

```json
{
	"status": {
		"code": 0,
		"message": "Security linked successfully.",
		"details": []
	}
}
```

**Response Fields:**

- `status`: Operation status.

### Example Request

```bash
curl --location 'https://api.dev.tpinf.in/takeprofit.partner.external.security.v1.LinkApi.LinkSecurity' \
--header 'accesstoken: YOUR_ACCESS_TOKEN_HERE' \
--header 'Content-Type: application/json' \
--data '{
    "security_guid": "6ef11658-5a1c-4baf-9387-d977dcca6129",
    "partner_security_id": "124"
}'
```

### Example Response

<details>
<summary>Successful Response</summary>

```json
{
	"status": {
		"code": 0,
		"message": "Security linked successfully.",
		"details": []
	}
}
```

</details>

---

## UnlinkSecurity

Remove the linkage between a security and the partner's identifier.

### HTTP Request

`POST /takeprofit.partner.external.security.v1.LinkApi.UnlinkSecurity`

### Headers

- `accesstoken`: Access token (required)
- `Content-Type`: `application/json`

### Request Body

```json
{
	"security_guid": "SECURITY_GUID"
}
```

**Fields:**

- `security_guid` (string, required): GUID of the security to unlink.

### Response

**Success (HTTP 200):**

```json
{
	"status": {
		"code": 0,
		"message": "Security unlinked successfully.",
		"details": []
	}
}
```

**Response Fields:**

- `status`: Operation status.

### Example Request

```bash
curl --location 'https://api.dev.tpinf.in/takeprofit.partner.external.security.v1.LinkApi.UnlinkSecurity' \
--header 'accesstoken: YOUR_ACCESS_TOKEN_HERE' \
--header 'Content-Type: application/json' \
--data '{
    "security_guid": "6ef11658-5a1c-4baf-9387-d977dcca6129"
}'
```

### Example Response

<details>
<summary>Successful Response</summary>

```json
{
	"status": {
		"code": 0,
		"message": "Security unlinked successfully.",
		"details": []
	}
}
```

</details>

---

## JSON Schemas

### Common Objects

#### Status

```json
{
	"type": "object",
	"properties": {
		"code": { "type": "integer" },
		"message": { "type": "string" },
		"details": { "type": "array", "items": {} }
	},
	"required": ["code", "message"]
}
```

#### LinkedSecurity

```json
{
	"type": "object",
	"properties": {
		"security_guid": { "type": "string" },
		"partner_security_id": { "type": "string" }
	},
	"required": ["security_guid", "partner_security_id"]
}
```

### Request Schemas

#### LinkSecurityRequest

```json
{
	"type": "object",
	"properties": {
		"security_guid": { "type": "string" },
		"partner_security_id": { "type": "string" }
	},
	"required": ["security_guid", "partner_security_id"]
}
```

#### UnlinkSecurityRequest

```json
{
	"type": "object",
	"properties": {
		"security_guid": { "type": "string" }
	},
	"required": ["security_guid"]
}
```

### Response Schemas

#### LinkSecurityResponse

```json
{
	"type": "object",
	"properties": {
		"status": { "$ref": "#/definitions/Status" }
	},
	"required": ["status"]
}
```

#### ListLinkedSecuritiesResponse

```json
{
	"type": "object",
	"properties": {
		"status": { "$ref": "#/definitions/Status" },
		"linked_securities": {
			"type": "array",
			"items": { "$ref": "#/definitions/LinkedSecurity" }
		}
	},
	"required": ["status", "linked_securities"]
}
```

---

## Usage Recommendations

- **Authorization**: Always use a valid `accesstoken` in the `accesstoken` header.
- **Error Handling**: Check the `status` field in the response to determine the success of the operation.
- **Data Consistency**: Ensure that the `partner_security_id` used to link securities is unique within your system to prevent conflicts.

---

## Frequently Asked Questions

### What should I do if I receive an "Invalid access token" error?

Ensure you are using a valid `accesstoken` obtained through the [Auth API](#). Tokens may expire, in which case you need to obtain a new one using the `refresh_token`.

### Can I overwrite an existing link?

Yes, calling `LinkSecurity` with the same `security_guid` will overwrite the existing `partner_security_id`.

### How do I list all the securities I have linked?

Use the `ListLinkedSecurities` endpoint to retrieve all linked securities.

---

## Support

If you have questions or encounter issues, please contact our support team at [support@takeprofit.com](mailto:support@takeprofit.com).

---

## Additional Resources

- [Auth API Documentation](#)
- [SecurityInfo API Documentation](#)

---

## Changelog

- **v1.0.0** - Initial version of the Link API documentation.

---

_This documentation is created to assist developers in integrating with the Link API and follows best practices for API documentation._

---

**Note:** Remember to replace placeholders like `YOUR_ACCESS_TOKEN_HERE`, `SECURITY_GUID`, and `PARTNER_SECURITY_ID` with your actual data when making requests.
