## New Relic Disk Plugin

If you can't see the disk I/O utilization in New Relic you may run your server in a OpenVZ container. New Relic does not
support this because that an OpenVZ container doesn't behave exactly like a real VM--it's a piece of a machine, not running 
its own full OS, and they just don't have capability to monitor it because we rely on OS-level stats which you won't have 
access to from your container.

This plugin allows you to monitor your server's disks usage in a OpenVZ container. 

### Requirements

In order to use this plugin, you must have an active New Relic account.

Plugin should work on any generic Unix environment with the following
software components installed:

  - Ruby (>= 1.8.7)
  - bundler for Ruby: https://github.com/carlhuda/bundler

### Instructions for running the agent

1. run `bundle install` to install required gems
2. Edit `config/newrelic_plugin.yml` and replace "YOUR_LICENSE_KEY_HERE" with your New Relic license key
3. Running the plugin

Plugin can be started as a daemon using the following command (as root):

```./newrelic_disk_agent.daemon start```

In this case you can check its status by running

```./newrelic_disk_agent.daemon status```

and stop it with

```./newrelic_disk_agent.daemon stop```
