## New Relic FreeRADIUS Plugin

Monitors FreeRADIUS, The world's most popular RADIUS Server.

### Requirements

In order to use this plugin, you must have an active New Relic account.

Plugin should work on any generic Unix environment with the following
software components installed:

  - Ruby (>= 1.8.7)
  - bundler for Ruby: https://github.com/carlhuda/bundler
  - FreeRADIUS server with status enabled or a [status virtual server](http://wiki.freeradius.org/config/Status)
  - radclient (Installed as part of FreeRADIUS)

### Instructions for running the FreeRADIUS plugin agent

1. run `bundle install` to install required gems
2. Copy `config/newrelic_plugin.yml.example` to `config/newrelic_plugin.yml`
3. Edit `config/newrelic_plugin.yml` and replace "YOUR_LICENSE_KEY_HERE" with your New Relic license key
4. Edit the `config/newrelic_plugin.yml` file and add Redis connection string
5. Running the plugin

In order to check your configuration, you can launch the plugin
in foreground mode, with all output going to stdout:

  ./newrelic_freeradius_agent

Carefully check plugin's output for any possible error messages.
In case of success, collected data should appear in the New Relic
user interface shortly after starting.

Plugin can also be started as a daemon using the following command:

  ./newrelic_freeradius_agent.daemon start

In this case you can check its status by running

  ./newrelic_freeradius_agent.daemon status

and stop it with

  ./newrelic_freeradius_agent.daemon stop

### Monit example

```
check process newrelic_freeradius_agent
  with pidfile /home/ubuntu/newrelic_freeradius_agent/newrelic_freeradius_agent.pid
  start program = "/bin/su - ubuntu -c '/home/ubuntu/newrelic_freeradius_agent/newrelic_freeradius_agent.daemon start'" with timeout 90 seconds
  stop program = "/bin/su - ubuntu -c '/home/ubuntu/newrelic_freeradius_agent/newrelic_freeradius_agent.daemon stop'" with timeout 90 seconds
  if totalmem is greater than 250 MB for 2 cycles then restart
  group newrelic_agent
```
