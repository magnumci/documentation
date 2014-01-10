## Authentication

User API authentication token could be passed as a request parameter:

- `api_token` or `api_key`

Or as a header:

- `X-API-TOKEN` or `X-API-KEY`

```
GET /api/v1/profile?api_token=YOUR_API_TOKEN
```

## Authenticate User

```
POST /api/v1/authenticate
```

Parameters:

- `login` - Username (required if email is blank)
- `email` - Email address (required if login is blank)
- `password` - Current user password (required)

Successful response:

```json
{
  "id": 1,
  "email": "user@email.com",
  "login": "username",
  "projects": 14,
  "time_used": 12.34,
  "time_quota": 20,
  "api_token": "e53cda185186db53e2dfdf1fc21e0fa...",
  "created_at": "2012-11-07T11:06:57-06:00"
}
```