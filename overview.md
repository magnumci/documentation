# Overview

Magnum CI is a hosted continuous integration service for private projects. It 
supports multiple languages and tools to run test suite. 

Service suppors all major version control software and integrates with most 
popular code hosting platforms. There are no restrictions or limitations on where
you store your source code, so even your own self-hosted repository will work 
right away.

## Source Code Providers

Magnum CI build environment supports a variety of external source code hosting platforms 
and can be hooked up with the following providers:

- **Github** - git
- **Bitbucket** - git, mercurial
- **Beanstalkapp** - git, mercurial, subversion - *partial support*
- **Gitlab** - git
- **Self Hosted** - git, mercurial, subversion

Integration is performed via simple API that will be automatically called when
the new push is received. For a custom repository (ex git) you can trigger CI
build by creating a new `post-receive` hook. For samples please check the
[documentation](/docs/hooks).

## Build Flow

Based on the project type, build process might have a set of steps to execute your
test suite. The starting point is when a new code push hook with the commit payload
is received. Then worker performs the following steps:

- Creates a new virtual machine (VM) for the build. Environment varies based on project type (ruby, node, etc)
- Opens a new SSH connection with the target VM
- Clones repository with git, mercurial or subversion
- Checks out the build code revision specified in the payload
- Detects configuration file and runs hook commands if any
- Executes a test suite (test/unit, rspec, etc)
- Collects the build log and updates build status
- Closes connection and destroys build VM

## Security

For security reasons, Magnum CI generates new private and public keys for each project 
that need to be added to code provider settings. That means that the code 
is only accessible from build environment assigned to your project. 
Host system (and other components) that handles builds does not have any access to 
your code and all troubleshooting will only happen with written permission. 

Virtual machines are also configured in a way that only host system that runs the build 
could access it via SSH. In situations where host system runs multiple build 
virtual machines at the same time, communications between VM's are restricted. 
All resources (mysql, postgres, redis, etc) are configured to run only on 
local (127.0.0.1) interface and also not accessible outside of the VM. 