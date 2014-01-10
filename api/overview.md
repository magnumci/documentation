# API Reference

Magnum CI exposes an API with the following specs:

- Endpoint: `https://magnum-ci.com/api/v1`
- Response format: JSON

API token for the user account is available in the [account settings](/account)

## Reponse codes

Request that failed always have a status code different from 200. List of used error codes:

- `400` - Bad request
- `401` - Authentication Failed or Resource Not Authorized
- `422` - Unprocessable entity 
- `500` - Internal server error

Typical error response looks like this:

```json
{
  "error": "Error message goes here",
  "status": 404
}
```