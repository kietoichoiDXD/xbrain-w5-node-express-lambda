# AWS Lambda Deployment Notes

## Strategy
**serverless-http wrapper**

## Rationale
- **Minimal Code Changes**: Only added 2 lines to `app.js` and installed 1 dependency (`serverless-http`). The core logic remains identical to the local Express app.
- **Framework Pure**: The application still runs perfectly locally using `node server.js` without any modification to the entry point.
- **Production Ready**: `serverless-http` is a widely adopted, battle-tested library for running Express on AWS Lambda.

## Performance
- **Cold Start**: ~530ms (Total request time: ~1.26s)
- **Warm Start**: ~730ms (Total request time: ~0.73s)
- **Configuration**: Node.js 20.x, 512MB RAM, arm64 architecture.

## Deployment Details
- **Region**: us-west-2 (Oregon)
- **API Type**: HTTP API (v2)
- **Lambda Handler**: `app.handler`
