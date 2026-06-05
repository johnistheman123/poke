<!-- API Documentation for the poke project -->
# API Documentation

This document describes the minimal API for the `poke` project and links to an OpenAPI (Swagger) stub.

## Overview

The API exposes simple CRUD operations for a `pokemon` resource.

Base path: `/api`

## Endpoints

- `GET /api/pokemon` — List all pokemon
  - Query params: `limit` (integer), `offset` (integer)
- `GET /api/pokemon/{id}` — Get a single pokemon by id
- `POST /api/pokemon` — Create a new pokemon
  - Body: JSON with `name`, `type`, and optional `notes`
- `PUT /api/pokemon/{id}` — Update an existing pokemon
- `DELETE /api/pokemon/{id}` — Remove a pokemon

## Example request

GET /api/pokemon

Response (200):

```json
[
  {"id": 1, "name": "Pikachu", "type": "electric"},
  {"id": 2, "name": "Bulbasaur", "type": "grass"}
]
```

## Authentication

This repo does not include a production auth scheme. If you add auth, document the header/bearer token details here.

## OpenAPI

A starter OpenAPI stub is included in `docs/openapi.yaml`.
