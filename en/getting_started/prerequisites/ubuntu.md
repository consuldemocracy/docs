# Configuration for development and test environments (Ubuntu 18.04)

## Git

Git is officially maintained in Ubuntu:

```bash
sudo apt install git
```

## Ruby

Ruby versions packaged in official repositories are not suitable to work with CONSUL, so we'll have to install it manually.

First, we need to install Ruby's development dependencies:

```bash
sudo apt install libssl1.0-dev autoconf bison build-essential libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm5 libgdbm-dev
```

Note we're installing `libssl1.0-dev` instead of `libssl-dev`. That's because Ruby 2.3.2 (which CONSUL uses in version 0.19) is not compatible with OpenSSL 1.1.

The next step is installing a Ruby version manager, like rbenv:

```bash
wget -q https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer -O- | bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
```

Finally, install Ruby 2.3.2, which will take a few minutes:

```bash
rbenv install 2.3.2
```

## Bundler

Check we're using the Ruby version we've just installed:

```bash
rbenv global 2.3.2
ruby -v
=> ruby 2.3.2p217
```

And install Bundler with:

```bash
gem install bundler
```

## Node.js

To compile the assets, you'll need a JavaScript runtime. Node.js is the preferred option. As with Ruby, we don't recommend installing Node from your distro's repositories.

To install it, you can use [n](https://github.com/tj/n)

Run the following command on your terminal:

```bash
wget -L https://git.io/n-install | bash -s -- -y lts
```

It will install the latest LTS (Long Term Support) Node version on your `$HOME` folder automatically (using [n-install](https://github.com/mklement0/n-install))

## PostgreSQL

Install postgresql and its development dependencies with:

```bash
sudo apt install postgresql libpq-dev
```

You also need to configure a user for your database. As an example, we'll choose the username "consul":

```bash
sudo -u postgres createuser consul --createdb --superuser --pwprompt
```

## ChromeDriver

To run E2E integration tests, we use Selenium along with Headless Chrome.

To get it working, install the chromium-chromedriver package and make sure it's available on your shell's PATH:

```bash
sudo apt install chromium-chromedriver
sudo ln -s /usr/lib/chromium-browser/chromedriver /usr/local/bin/
```

Now you're ready to go [get CONSUL installed](../local_installation.html)!