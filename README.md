# Node.js Fundamentals

A set of guided learning exercises covering core Node.js concepts. The repository includes a small HTTP API built with Node's native `http` module, a JSON-file-backed data store, and standalone stream examples. It is an educational codebase rather than a production service.

## Exercises

- `scr/`: route matching, query-string parsing, JSON request-body handling, and CRUD operations for users.
- `db.json`: local JSON data written by the database helper.
- `streams/`: examples of readable, transform, and writable streams, plus a streamed HTTP request body.

The sample API uses port `3333` and supports:

- `GET /users` with an optional `search` query parameter.
- `POST /users` to create a user with a name and email.
- `PUT /users/:id` to update a user.
- `DELETE /users/:id` to remove a user.

## Technology

Node.js ES modules and the native HTTP and Stream APIs. The `fastify` dependency is present in `package.json`, while the current sample server is implemented with `node:http`.

## Run locally

Install the dependency and start the watched HTTP server:

```bash
npm install
npm run dev
```

The server prints that it is listening on port `3333`. To try the stream examples, run the relevant files directly, for example:

```bash
node streams/fundamentals.js
```

`streams/fake-upload-to-http-stream.js` sends a request to port `3334`, so it requires a compatible receiving server to be running separately.

## Learning-project notes

This repository contains guided exercises and deliberately small examples. The JSON database is a local file and is not a concurrent or transactional database. There is no test suite or production deployment configuration in the repository. The stream examples illustrate API mechanics rather than a complete upload service.

## Source guide

| Source | What to inspect |
| --- | --- |
| [HTTP entry point](scr/server.js) | Native server setup and request dispatch. |
| [Routes](scr/routes.js) | CRUD handlers and route patterns. |
| [JSON middleware](scr/middlewares/json.js) | Request body parsing and response content type. |
| [File persistence](scr/database.js) | Local JSON-file reads and writes. |
| [Route matching](scr/utils/build-route-path.js) | Conversion of parameterized paths into matching rules. |

## Suggested reading order

Start with `scr/server.js`, follow a matching route in `scr/routes.js`, then inspect the JSON middleware and file-backed database helper. The directory is named `scr` in this repository; use that spelling when opening the files.

The independent examples under `streams/` explore stream behavior separately from the CRUD API. The streamed upload example needs its own receiver on port `3334`; starting the user API on `3333` does not provide that receiver.
