[![Build Status](https://travis-ci.org/sinsoku/rails-env-credentials.svg?branch=master)](https://travis-ci.org/sinsoku/rails-env-credentials)

# RailsEnvCredentials

It enhances the Credentials feature introduced by Rails v5.2.0.

## Why make it?

Credentials is a good feature, but we cannot use it on development and test environment.

DHH wrote as follow in the pull request for initial implementation:

> It's only in production (and derivative environments, like exposed betas) where the secret actually needs to be secret.
>
> refs: https://github.com/rails/rails/pull/30067

However, I have to manage secrets in the staging environment.

I do not have the confidence to explain explicit use cases to Rails team, so I implemented as a gem.

If many people use it, I would like to send a pull request to Rails.:octocat::heart:

## Installation

Add this line to your Rails application's Gemfile:

```ruby
group :development, :test do
  gem 'rails-env-credentials'
end
```

And then execute:

```
$ bundle
```

## Usage

RailsEnvCredentials will automatically generate encrypted file and the master key when you starts editing credentials at first:

```
$ rails env_credentials:edit -e development
```

If you want to see decrypted contents, use `env_credentials:show`

```
$ rails env_credentials:show -e development
```

## Additional information

### Other environments support

For example, if the `config/environments/staging.rb` exists, RailsEnvCredentials will automatically generate `config/credentials-staging.yml.enc`.

### Display a diff

You can’t directly compare encrypted files between two versions, but it turns out you can see a diff using Git attributes.

Put the following line in your `.gitattributes` file:

```
config/credentials*.yml.enc diff=env_credentials
```

Then configure Git to use `env_credentials:show`:

```
$ git config diff.env_credentials.textconv 'rails env_credentials:show --file'
```

This tells Git that encrypted files should decrypt by the `env_credentials:show` task when you try to display a diff.

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/sinsoku/rails-env-credentials. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Rails::Env::Credentials project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/sinsoku/rails-env-credentials/blob/master/CODE_OF_CONDUCT.md).
