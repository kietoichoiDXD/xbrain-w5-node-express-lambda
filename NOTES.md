# BYOL Challenge: Node.js Express on Lambda

## Strategy: Strategy A — `serverless-http` adapter

### Why this strategy?
- **Minimal Code Change:** Only 3 lines of code in a new `lambda.js` file.
- **Framework Pure:** The existing `app.js` and `server.js` remain completely untouched, keeping the Express logic decoupled from AWS Lambda specifics.
- **Robustness:** `serverless-http` handles binary types, cookies, and multi-value headers correctly, which are common pain points when manually translating API Gateway events.

### Cold Start Measurement
- **Measured Init Duration:** 336.78 ms
- **Method:** Checked `REPORT` line in CloudWatch logs after first invocation.

### Links
- **API Gateway URL:** https://fpylwbd5wk.execute-api.us-west-2.amazonaws.com
- **GitHub Source:** https://github.com/kietoichoiDXD/xbrain-w5-node-express-lambda
