# Heroku Deployment

Magnum CI provides an ability to deploy your applications directly to Heroku cloud
after build execution. Deployments are only trigged if the build passes and skipped 
on failures. 

Code pushes to Heroku are done via git strategy. Its a default and the easiest way
to update code. Anvil strategy is not supported. 

## Setup

To configure deployment settings, go to project build settings and click "Deployments".
In the list you will see all available deployment service that Magnum CI
integrates with.

![Index](https://s3.amazonaws.com/magnum-ci/deployment-heroku.png)

Click on "Install" button within Heroku box. That'll bring you to configuration
screen.

![Form](https://s3.amazonaws.com/magnum-ci/deployment-heroku-form.png)

Available fields and options on the form:

- **Branch** - specify a branch name on which deployments are triggered
- **Application* - specify an application name used by Heroku
- **API token** - specify your account's API token
- **Enabled** - enable / disable deployments at any time without deleting configuration.
- **Forced Push** - make git push forced, overwriting everything in Heroku repository
- **Maintenance Mode** - use Heroku maintenance mode
- **Backup Database** - backup database associated with application before code push
- **Migrate Database** - run database migration

### API token

If you're already authenticated with Heroku and you have CLI installed, you can simply
run command to get your API token:

```
heroku auth:token
```

You will see output similar to this:

```
ffza32c5-9298-4461-902d-aecfa0a7fd85
```

It's your API token, you can drop it into field on the deployment configuration form.

If you're not authenticated yet, you can do that by running command:

```
heroku auth:login
```

### Maintenance mode

Heroku's maintenance mode feature serves a static page to all visitors 
allowing developers to perform maintenance tasks without exposing any parts
of the application to external users.

Visit [Heroku DevCenter article](https://devcenter.heroku.com/articles/maintenance-mode) for details

### Database backup

Build worker could perform a database backup before pushing any code to Heroku. If
you're using addon `pgbackups` you can enable this option to create new backups
automatically. Worker will execute the following command via heroku CLI:

```
heroku pgbackups:capture --app=my-app-name
```

### Database migration

Automatic database migration option is not available for all project type. Its 
only available for Ruby / Rails applications that provide `rake db:migrate` task
via Rakefile. This options will not appear in the form for non-ruby projects.

Once enabled, build worker will execute the following command via heroku CLI:

```
heroku run rake db:migrate --app=my-app-name
```

