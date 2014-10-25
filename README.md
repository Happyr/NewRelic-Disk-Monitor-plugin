## New Relic Disk Monitor Plugin

If you can't see the disk I/O utilization in New Relic it's may be because you run your server in a OpenVZ container. New Relic does not
support this because that an OpenVZ container doesn't behave exactly like a real VM--it's a piece of a machine, not running 
its own full OS, and they just don't have capability to monitor it because we rely on OS-level stats which you won't have 
access to from your container.

This plugin allows you to monitor your server's disks usage in a OpenVZ container. It does not provide you with information
about reads and writes. The purpose of this plugin is that it will warn you when your disks are almost full.

### Requirements

In order to use this plugin, you must have an active New Relic account.

Plugin should work on any generic Unix environment with the following
software components installed:

  - Ruby (>= 1.8.7)
  - bundler for Ruby: https://github.com/carlhuda/bundler

### Instructions for running the agent

1. Clone the repository into `/opt/newrelic-disk-monitor`
2. Run `cd /opt/newrelic-disk-monitor`
3. Run `bundle install` to install required gems
4. Edit `config/newrelic_plugin.yml` and replace "YOUR_LICENSE_KEY_HERE" with your New Relic license key
5. Copy the init file for your distribution e.g. `sudo cp /opt/newrelic-disk-monitor/init.d/debian /etc/init.d/newrelic-disk-monitor`
6. Give the init file the correct permissions with `sudo chmod +x /etc/init.d/newrelic-disk-monitor`
7. Start the plugin by running `sudo /etc/init.d/newrelic-disk-monitor start`

### Troubleshoot

1. Make sure you get a representable response from `hostname -f`.
2. Make sure to update the init file or `/etc/default/newrelic-disk-monitor` with a proper path to the repository clone.
3. For some init.d scripts make sure that the `newrelic` user has a shell - `usermod -s /bin/sh newrelic`.
4. Check if the plugin has started with `ps aux | grep newrelic-disk-monitor`. If you don't find any running process (except from the ´ps` command) you may remove the pid file. `sudo rm /var/run/newrelic-disk-monitor.pid`.
