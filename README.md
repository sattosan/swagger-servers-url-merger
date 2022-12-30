# Merge Swagger Difinisions

Merge each servers.url and path for multiple Swagger definitions.

# Requirement

- "js-yaml": "^4.1.0"
- "yargs": "^17.6.2"

# Installation

```bash
$ npm install -g swagger-servers-url-merger
```

https://www.npmjs.com/package/swagger-servers-url-merger

# Usage

In this example, openapi-v1.yaml and openapi-v2.yaml are merged to produce openapi.yaml.

Concretely, `servers.url` in `openapi-v1.yaml` is concatenated with `path` written in `paths`. Do the same for `openapi-v2.yaml`. Merge the respective `paths` and further replace them with the new `servers.url` to generate `openapi.yaml`.

The contents of `openapi-v1.yaml` are as follows.

<details><summary>openapi-v1.yaml</summary>

```yaml
openapi: 3.0.0
info:
  title: example-api
  version: v.1.0
  description: Example RESTful API
servers:
  - url: /v1
paths:
  /example:
    get:
      operationId: example
      summary: example
      description: example
      parameters:
        - $ref: "#/components/parameters/example"
      responses:
        "200":
          description: 200 (OK)
          content:
            application/json:
              schema:
                title: response
                type: object
                properties:
                  result:
                    $ref: "#/components/schemas/success"
        "400":
          description: >-
            error occurred - see status code and problem object for more
            information.
          content:
            application/problem+json:
              schema:
                $ref: "#/components/schemas/bad_request_response"
        "500":
          description: >-
            error occurred - see status code and problem object for more
            information.
          content:
            application/problem+json:
              schema:
                $ref: "#/components/schemas/internal_error_response"
```

</details>

The contents of `openapi-v2.yaml` are as follows.

<details><summary>openapi-v2.yaml</summary>

```yaml
openapi: 3.0.0
info:
  title: example-api
  version: v.1.0
  description: Example RESTful API
servers:
  - url: /v2
paths:
  /example:
    get:
      operationId: example
      summary: example
      description: example
      parameters:
        - $ref: "#/components/parameters/example"
      responses:
        "200":
          description: 200 (OK)
          content:
            application/json:
              schema:
                title: response
                type: object
                properties:
                  result:
                    $ref: "#/components/schemas/success"
        "400":
          description: >-
            error occurred - see status code and problem object for more
            information.
          content:
            application/problem+json:
              schema:
                $ref: "#/components/schemas/bad_request_response"
        "500":
          description: >-
            error occurred - see status code and problem object for more
            information.
          content:
            application/problem+json:
              schema:
                $ref: "#/components/schemas/internal_error_response"
```

</details>

```bash
$ swagger-servers-url-merger -i ./openapi-v1.yaml -i ./openapi-v2.yaml -o ./openapi.yaml -u http://localhost:8080
```

- `-i` or `--input`: Specify the file path of openapi.yaml to be merged.
- `-o` or `--output`: Output file path of openapi.yaml after merging.
- `-u` or `--url`: Specify the new `servers.url` to be replaced.

The contents of `openapi.yaml` are as follows.

<details><summary>openapi.yaml</summary>

```yaml
openapi: 3.0.0
info:
  title: example-api
  version: v.1.0
  description: Example RESTful API
servers:
  - url: /v1
paths:
  /example:
    get:
      operationId: example
      summary: example
      description: example
      parameters:
        - $ref: "#/components/parameters/example"
      responses:
        "200":
          description: 200 (OK)
          content:
            application/json:
              schema:
                title: response
                type: object
                properties:
                  result:
                    $ref: "#/components/schemas/success"
        "400":
          description: >-
            error occurred - see status code and problem object for more
            information.
          content:
            application/problem+json:
              schema:
                $ref: "#/components/schemas/bad_request_response"
        "500":
          description: >-
            error occurred - see status code and problem object for more
            information.
          content:
            application/problem+json:
              schema:
                $ref: "#/components/schemas/internal_error_response"
```

</details>

# Author

- Yuya Sato
- sato.yuya1211@gmail.com

# License

"swagger-servers-url-merger" is under [MIT license](https://en.wikipedia.org/wiki/MIT_License).
