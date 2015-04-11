# bedrock-capistrano

These are the Capistrano configs for deploying [Bedrock](https://github.com/roots/bedrock) projects.

[Capistrano](http://www.capistranorb.com/) is a remote server automation and deployment tool. It will let you deploy or rollback your application in one command:

Screencast (:moneybag:): [Deploying WordPress with Capistrano](https://roots.io/screencasts/deploying-wordpress-with-capistrano/)

## Requirements

* Ruby >= 1.9

Required Gems:

* `capistrano` (> 3.1.0)
* `capistrano-composer`

These can be installed manually with `gem install <gem name>` but it's highly suggested you use [Bundler](http://bundler.io/) to manage them. Bundler is basically the Ruby equivalent to PHP's Composer. Just as Composer manages your PHP packages/dependencies, Bundler manages your Ruby gems/dependencies. Bundler itself is a Gem and can be installed via `gem install bundler` (sudo may be required).

The `Gemfile` in the root of this repo specifies the required Gems (just like `composer.json`). Once you have Bundler installed, run `bundle install` to install the Gems in the `Gemfile`. When using Bundler, you'll need to prefix the `cap` command with `bundle exec` as seen below (this ensures you're not using system Gems which can cause conflicts).

See http://capistranorb.com/documentation/getting-started/authentication-and-authorisation/ for the best way to set up SSH key authentication to your servers for password-less (and secure) deploys.

## Installation/configuration

1. Copy the following files into the root of your Bedrock project:
  * `Capfile`
  * `Gemfile`
  * `Gemfile.lock`
2. Copy the following files/folders into your `config` directory:
  * `deploy/`
  * `deploy.rb`
3. Edit your `config/deploy/` stage/environment configs to set the roles/servers and connection options.
4. Before your first deploy, run `bundle exec cap <stage> deploy:check` to create the necessary folders/symlinks.
5. Add your `.env` file to `shared/` in your `deploy_to` path on the remote server for all the stages you use (ex: `/srv/www/example.com/shared/.env`)
6. Run the normal deploy command: `bundle exec cap <stage> deploy`
7. Enjoy one-command deploys!

## Usage

* Deploy: `cap production deploy`
* Rollback: `cap production deploy:rollback`

Composer support is built-in so when you run a deploy, `composer install` is automatically run. Capistrano has a great [deploy flow](http://www.capistranorb.com/documentation/getting-started/flow/) that you can hook into and extend it.

## Contributing

Contributions are welcome from everyone. We have [contributing guidelines](CONTRIBUTING.md) to help you get started.

## Support

Use the [Roots Discourse](https://discourse.roots.io/) forum to ask questions and get support.
