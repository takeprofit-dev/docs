Install the [Mintlify CLI](https://www.npmjs.com/package/mintlify) to preview the documentation changes locally. To install, use the following command

```bash
npm i -g mintlify
```

Run the following command at the root of your documentation (where mint.json is)

```bash
mintlify dev
```

```bash
npx @mintlify/scraping@latest openapi-file ./docs/partner-api/openapi.json -o ./docs/partner-api

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
