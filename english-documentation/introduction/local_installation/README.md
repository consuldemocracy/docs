# Local installation

1. Before installing Consul and having it up and running make sure all [prerequisites](prerequisites.md) are installed.

2. After you have fully loaded and checked the installation of [prerequisites](prerequisites.md)
clone the [Consul Github repository](https://github.com/consul/consul/) and enter the project folder:

```bash
git clone https://github.com/consul/consul.git
cd consul
```

3. Install the Ruby version we need with your Ruby version manager. Here are some examples:

```bash
rvm install `cat .ruby-version` # If you're using RVM
rbenv install `cat .ruby-version` # If you're using rbenv
asdf install ruby `cat .ruby-version` # If you're using asdf
```

4. Check we're using the Ruby version we've just installed:

```bash
ruby -v
=> # (it should be the same as the version in the .ruby-version file)
```

5. Install [Bundler](http://bundler.io/):

```bash
gem install bundler --version 1.17.1
```

6. Install the required gems using Bundler:

```bash
bundle
```

7. Copy the environment example configuration files inside new readable ones:

```bash
cp config/database.yml.example config/database.yml
cp config/secrets.yml.example config/secrets.yml
```

And setup database credentials with your `consul` user in your new `database.yml` file.
# Had issues with progress past this point. I think you need implicit instruction on the edit of database.yml! Otherwise rake tasks abort!

# On recent install rake loaded v 13.0.3 which caused the process to stall
8. Run the following [Rake tasks](https://github.com/ruby/rake -v 13.0.1) to create and fill your local database with the minimum data needed to run the application:

```bash
rake db:create
rake db:setup
rake db:dev_seed
rake db:test:prepare
```

9. Check everything is fine by running the test suite \(beware it might take more than an hour\):

```bash
bin/rspec
```

10. Now you have all set, run the application:

```bash
bin/rails s
```

Congratulations! Your local Consul application will be running now at `http://localhost:3000`.

In case you want to access the local application as admin, a default user verified and with admin permissions was created by the seed files with **username** `admin@consul.dev` and **password** `12345678`.

If you need an specific user to perform actions such as voting without admin permissions, a default verified user is also available with **username** `verified@consul.dev` and **password** `12345678`.

