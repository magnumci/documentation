## User Account

```
GET /api/v1/profile
```

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

## Project API

Project API does not use a regular user authentication, instead, it uses an `token` parameter that corresponds to `api_token` of Project model. 

### Project Details

```
GET /api/v1/project?token=TOKEN
```

If project token is missing the output will be like this:

```json
{"error": "Project API token required.", "status": 403}
```

On invalid project token you'll get:

```json
{"error": "Project does not exist.", "status": 404}
```

Successful output:

```json
{
  "id": 29,
  "name": "foobar",
  "source_type": "git",
  "source_url": "git@github.com:foo/bar.git",
  "enabled": true,
  "builds_count": 9,
  "subscribers_count": 0,
  "created_at": "2012-11-01T20:30:19-05:00",
  "updated_at": "2012-11-07T23:22:08-06:00"
}
```

### Project Builds

```
GET /api/v1/project/builds?token=TOKEN
```

Output:

```json
{
  "current_page": 1,
  "total_pages": 1,
  "per_page": 25,
  "count": 19,
  "builds": [
    {
      "id": 100,
      "project_id": 29,
      "number": 9,
      "commit": "6257066c3fb124c92ab4f25c8d19dcdd327f9525",
      "author": "Author Name",
      "committer": "Committer Name",
      "message": "Commit message",
      "branch": "master",
      "state": "pending",
      "started_at": "2012-11-09T19:41:25-06:00",
      "finished_at": "2012-11-09T19:41:38-06:00",
      "result": null,
      "created_at": "2012-11-09T19:44:28-06:00",
      "updated_at": "2012-11-09T19:44:50-06:00"
    }
  ]
}
```

### Build Details

```
GET /api/v1/project/build
```

Request parameters:

- `token` - Project API token (required)
- `id` - Build ID (not number) (required)
- `log` - Flat to include build log (optional)

If build ID is missing, you get error:

```json
{"error": "Build ID required", "status": 400}
```

If build was not found, you get error:

```json
{"error": "Build does not exist", "status": 404}
```

Build details:

```json
{
  "id": 100,
  "project_id": 29,
  "number": 9,
  "commit": "6257066c3fb124c92ab4f25c8d19dcdd327f9525",
  "author": "Author Name",
  "committer": "Committer Name",
  "message": "Commit message",
  "branch": "master",
  "state": "pending",
  "started_at": "2012-11-09T19:41:25-06:00",
  "finished_at": "2012-11-09T19:41:38-06:00",
  "result": null,
  "created_at": "2012-11-09T19:44:28-06:00",
  "updated_at": "2012-11-09T19:44:50-06:00"
}
```

### Build Log

```
GET /api/v1/project/build/log
```

Request parameters:

- `token` - Project API token (required)
- `id` - Build ID (required)

Response is encoded as `text/html`. Example:

```
$ git --version
git version 1.7.9.5
$ gem --version
1.8.24
$ ruby --version
ruby 1.9.3p327 (2012-11-10 revision 37606) [x86_64-linux]
$ rvm --version

.... other data ....
```

## Stats

Get build stats for the last 30 days.

```
GET /api/v1/stats
```

Success output:

```json
[
  {
    "date": "2013-02-23",
    "total": 6,
    "failed": 0
  }, 
  {
    "date": "2013-02-24",
    "total": 7,
    "failed": 1
  }
]
```

Get build stats filtered by project:

```
GET /api/v1/stats?project_id=12345
```

Parameters:

- `project_id` - Filter stats by project. (*Integer*)

If project does not exist, API will return error:

```json
{"error": "Project does not exist", "status": 404}
```