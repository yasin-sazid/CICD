# Express Application with Continuous Integration

A compact Node.js project demonstrating the path from an HTTP endpoint to automated integration tests and a GitHub Actions deployment workflow. Its small application surface keeps the delivery pipeline easy to follow.

## Application behavior

| Request | Response |
| --- | --- |
| `GET /` | `Hello World!` |
| `GET /:stringToBePrinted` | The supplied path parameter |

[index.js](index.js) creates the Express application, starts the HTTP listener, and exports the app for request-level testing. The default port is **8000**, with `PORT` available as an override.

## Run and test

```bash
npm ci
npm start
```

In another terminal:

```bash
curl http://localhost:8000/
curl http://localhost:8000/yasin
npm test
```

[test/test.js](test/test.js) uses Mocha and Supertest to assert the root response and the `/yasin` route. These tests exercise the Express request/response behavior directly.

## Delivery workflow

[The Node.js CI workflow](.github/workflows/node.js.yml) runs for pushes and pull requests targeting `master`. Its build job installs dependencies with `npm ci`, executes a build script when present, and runs the tests across Node.js 12, 14, and 16.

A dependent deployment job uses the Heroku deployment action. The workflow references the repository secret `HEROKU_API_KEY` and the application settings recorded in the YAML file.

## Technical focus

Express routing, parameterized requests, exported application instances for integration tests, a Node.js version matrix, and build-to-deployment job dependencies form an approachable end-to-end example of automated delivery.
