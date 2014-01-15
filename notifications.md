# Build Notifications

Notifications on build statuses could be delivered via the following channels:

- Email
- [Slack](http://slack.com)
- [Hipchat](http://hipchat.com)
- [Flowdock](http://flowdock.com)
- [Campfire](https://campfirenow.com)
- IRC
- Webhooks

## Email

By default, build notifications are sent to all project collaborators via
email. To reduce amount of messages, successful build notifications are sent only 
once after execution is complete until build is broken. Failed build notifications
are sent every time build breaks so everybody is aware of the status.
Its possible to disable email notification completely. You can do that by
logging into your account settings and checking off "Receive build notifications" 
check box.

## Webhooks

If you want to receive build notifications as HTTP requests, you can add a new
web hook url. Magnum CI will send a POST request with JSON payload. 

Check **webhooks** page for details. 

## Chat services

Magnum CI supports all major hosted chat systems and provides a way to test
message delivery before real build sends worker any messages. Head to addons 
section of your project settings page to configure services. 

Configuration is a pretty straight-forward, in most cases it only requires
and third-party service API token and a room id. 

Build notifications are delivered to chat rooms per each build event regardless
of previous build status, unlike email notifications.

## Opensource

All delivery mechanisms (except email and webhooks) are available as addons in project
settings page. Most of them are also open source, check Magnum CI [github](https://github.com/magnumci) account for details

