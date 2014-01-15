# Webhooks

One way to notify a third-party service or application is to use project hooks. 
These are simple HTTP endpoints that will receive a POST payload with build result
details. Hooks are triggered when build execution is complete.

Hook delivery is a one-time process and in case if the service or application is
unable to accept or process build payload no notifications or warning will be raised.
You can always test hook before running any live builds. 

Individual hook could be triggered on build fail, build pass, build error
or on any result. You can also simply enable or disable project hooks at any time. 

## Hook Payload

Hook payload is a simple JSON-encoded object with the following structure:

```json
{
  "id": 1603,
  "project_id": 43,
  "title": "[PASS] project-name #130 (master - e91e132) by Dan Sosedoff",
  "number": 130,
  "commit": "e91e132612d263d95211aae6de2df9e503f22704",
  "author": "Dan Sosedoff",
  "committer": "Dan Sosedoff",
  "message": "Commit Message",
  "branch": "master",
  "state": "finished",
  "status": "pass",
  "result": 0,
  "duration": 158,
  "duration_string": "2m 38s",
  "commit_url": "http://domain.com/commit/e91e132612d263...",
  "compare_url": null,
  "build_url": "http://magnum-ci.com/projects/43/builds/1603",
  "started_at": "2013-02-14T00:09:01-06:00",
  "finished_at": "2013-02-14T00:11:39-06:00"
}
```

Where:

- `result`      - Build script exit status (Integer)
- `duration`    - Overall build duration in seconds (Integer)
- `commit_url`  - Link to a page with commit diff (github, etc) (String)
- `compare_url` - Link to a page with commits diff (if push includes many) (String)
- `build_url`   - Direct link to view build result (String)

## Code examples

Example ruby and sinatra application to parse incoming payload:

```ruby
require 'sinatra'
require 'json'

post '/' do
  push = JSON.parse(params[:payload])
  "I got some JSON: #{push.inspect}"
end

```

## Troubleshooting

Use service like [RequestBin](http://requestb.in/) to troubleshoot hooks.