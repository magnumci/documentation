# Integration

Magnum CI supports a few integration methods via web hooks from services:

- Github
- Bitbucket
- Beanstalkapp
- Gitlab

Custom post-receive hooks are also supported.

## Overview

To trigger a new build you should send a JSON payload with the following structure:

```json
{
  "commit": "bc11eb14d6e96c14afdec81799193d3a8e75ee4f",
  "committer": "John Doe",
  "author": "John Doe",
  "message": "Commit message goes here",
  "branch": "master",
  "commit_url": "Link to view commit",
  "compare_url": "Link to view commit compare (if diff includes many commits)"
}
```

## Github Hook

Add a new service hook to Github and new builds will be automatically scheduled once you push your code.

Service hook URL:

```
https://magnum-ci.com/api/v1/payload/github?token=PROJECT_API_TOKEN
```

## Custom Hook

If you're using a self-hosted repositories and wish to use Magnum, you can simply 
trigger the build using API: 

```
POST https://magnum-ci.com/api/v1/payload?token=PROJECT_API_TOKEN
```

Example in Ruby:

```ruby
require 'faraday'
require 'json'

payload = {
  "commit"      => "Commit SHA",
  "committer"   => "John Doe",
  "author"      => "John Doe",
  "message"     => "Commit Message",
  "branch"      => "master",
  "commit_url"  => "http://domain.com/commit/...",
  "compare_url" => "http://domain.com/compare/..."
}

project_token = "Your project API token"
url = "https://magnum-ci.com/api/v1/payload?token=#{project_token}"

Faraday.post(url, :payload => payload.to_json)
```