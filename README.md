![CONSUL DEMOCRACY logo](img/consul_logo.png)

# CONSUL DEMOCRACY

Citizen Participation and Open Government Application

![Build status](https://github.com/consuldemocracy/consuldemocracy/workflows/tests/badge.svg)
[![Code Climate](https://codeclimate.com/github/consuldemocracy/consuldemocracy/badges/gpa.svg)](https://codeclimate.com/github/consuldemocracy/consuldemocracy)
[![Coverage Status](https://coveralls.io/repos/github/consuldemocracy/consuldemocracy/badge.svg)](https://coveralls.io/github/consuldemocracy/consuldemocracy?branch=master)
[![Crowdin](https://d322cqt584bo4o.cloudfront.net/consul/localized.svg)](https://translate.consuldemocracy.org/)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](http://www.gnu.org/licenses/agpl-3.0)

[![Accessibility conformance](https://img.shields.io/badge/accessibility-WAI:AA-green.svg)](https://www.w3.org/WAI/eval/Overview)
[![A11y issues checked with Rocket Validator](https://rocketvalidator.com/badges/checked_with_rocket_validator.svg?url=https://rocketvalidator.com)](https://rocketvalidator.com/opensource)

[![Join the chat at https://gitter.im/consul/consul](https://badges.gitter.im/consul/consul.svg)](https://gitter.im/consul/consul?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Help wanted](https://img.shields.io/badge/help-wanted-brightgreen.svg?style=flat-square)](https://github.com/consuldemocracy/consuldemocracy/issues?q=is%3Aopen+label%3A"help+wanted")

[![Knapsack Pro Parallel CI builds for RSpec tests](https://img.shields.io/badge/Knapsack%20Pro-Parallel%20/%20RSpec%20tests-%230074ff)](https://knapsackpro.com/dashboard/organizations/176/projects/202/test_suites/318/builds?utm_campaign=organization-id-176&utm_content=test-suite-id-318&utm_medium=readme&utm_source=knapsack-pro-badge&utm_term=project-id-202)

This is the opensource code repository of the eParticipation website CONSUL DEMOCRACY, originally developed for the Madrid City government eParticipation website

## Documentation

Check the ongoing documentation at [https://docs.consuldemocracy.org](https://docs.consuldemocracy.org) to learn more about how to start your own CONSUL DEMOCRACY fork, install it, customize it and learn to use it from an administrator/maintainer perspective.

## CONSUL DEMOCRACY Project main website

You can access the main website of the project at [http://consuldemocracy.org](http://consuldemocracy.org) where you can find documentation about the use of the platform, videos, and links to the community space.

## Configuration for development and test environments

**NOTE**: For more detailed instructions check the [docs](https://docs.consuldemocracy.org)

Prerequisites: install git, Ruby 3.0.6, CMake, pkg-config, shared-mime-info, Node.js and PostgreSQL (>=9.5).

```bash
git clone https://github.com/consuldemocracy/consuldemocracy.git
cd consuldemocracy
bundle install
cp config/database.yml.example config/database.yml
cp config/secrets.yml.example config/secrets.yml
bin/rake db:create
bin/rake db:migrate
bin/rake db:dev_seed
RAILS_ENV=test rake db:setup
```

Run the app locally:

```bash
bin/rails s
```

Run the tests with:

```bash
bin/rspec
```

You can use the default admin user from the seeds file:

 **user:** admin@consul.dev
 **pass:** 12345678

But for some actions like voting, you will need a verified user, the seeds file also includes one:

 **user:** verified@consul.dev
 **pass:** 12345678

## Configuration for production environments

See [installer](https://github.com/consuldemocracy/installer)

## Current state

Development started on [2015 July 15th](https://github.com/consuldemocracy/consuldemocracy/commit/8db36308379accd44b5de4f680a54c41a0cc6fc6). Code was deployed to production on 2015 september 7th to [decide.madrid.es](https://decide.madrid.es). Since then new features are added often. You can take a look at the current features at the [project's website](http://consuldemocracy.org/) and future features at the [Roadmap](https://github.com/orgs/consuldemocracy/projects/1) and [open issues list](https://github.com/consuldemocracy/consuldemocracy/issues).

## License

Code published under AFFERO GPL v3 (see [LICENSE-AGPLv3.txt](https://github.com/consuldemocracy/consuldemocracy/blob/master/LICENSE-AGPLv3.txt))

## Contributions

See [CONTRIBUTING.md](https://github.com/consul/consul/blob/master/CONTRIBUTING.md).
