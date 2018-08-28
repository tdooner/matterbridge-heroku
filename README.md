# Matterbridge-heroku

This is a fork of [the original
`matterbridge-heroku`](https://github.com/cadecairos/matterbridge-heroku).

It includes [a custom config file][config] specific to one implementation, but this can easily be modified in a new fork.

## About this Fork

[**Heroku**](https://www.heroku.com/what) is a platform for easily deploying
applications.

A [**buildpack**](https://docs.cloudfoundry.org/buildpacks/) provides
framework and runtime support for apps running on platforms like Heroku.

An [**_inline_ buildpack**](https://github.com/kr/heroku-buildpack-inline#readme) is a special buildpack that includes code for both the app and the
buildpack that _runs_ the app.

[**Matterbridge**](https://github.com/42wim/matterbridge#readme) is a
simple _bridge_ that can relay messages between a number of different
chat services, essentially connecting separate chat tools.

This fork is intended to help bridge channels between both the EDGI and
Archivers Slack teams.

* Required envvars:
  * `MATTERBRIDGE_VERSION`. Use a [matterbridge git tag][git-tags].
  * `MATTERBRIDGE_SLACK_<team name>_TOKEN`. See [_Slack bot setup_ documentation][bot-setup].

## Setup
```bash
cp .env.example .env
# [fill in .env file with credentials]
heroku create
heroku config:set $(cat .env)
heroku buildpacks:add http://github.com/tdooner/matterbridge-heroku
heroku ps:scale worker=1
heroku dyno:type worker=hobby
```
