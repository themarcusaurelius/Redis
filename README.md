## Collects and parses the slow logs created by Redis

When you run this module, it performs a few tasks under the hood:

- Sets the default paths to the log files (but don’t worry, you can override the defaults)
- Makes sure each multiline log event gets sent as a single event
- Uses ingest node to parse and process the log lines, shaping the data into a structure suitable for visualizing in Kibana
- Deploys dashboards for visualizing the log data

The ```redis``` module has two filesets:

The ```log``` fileset collects and parses the logs that Redis writes to disk.
The ```slowlog``` fileset connects to Redis via the network and retrieves the slow logs by using the ```SLOWLOG``` command.

For the ```log``` fileset, make sure the ```logfile``` option, from the Redis configuration file, is set to ```redis-server.log```.

For the ```slowlog``` fileset, make sure the ```slowlog-log-slower-than``` option, from the Redis configuration file, is set to a lower value than the default one.

### Compatibility

The Redis ```log``` fileset was tested with logs from Redis versions 1.2.6, 2.4.6, and 3.0.2, so we expect compatibility with any version 1.x, 2.x, or 3.x.

On Windows, the default paths assume that Redis was installed from the Chocolatey repository.

The Redis ```slowlog``` fileset was tested with Redis 3.0.2 and 2.4.6. We expect compatibility with any Redis version newer than 2.2.12, when the SLOWLOG command was added.


### Installation

### Linux:

<i>If you haven't already installed filebeat...</i>

1. Enter the following script into the console using elevated privileges

```
curl https://github.com/themarcusaurelius/vizion.ai/blob/master/beat-install-scripts/install-config-redis.sh > install-config-redis.sh; chmod a+x  install-config-redis.sh; ./install-config-redis.sh _PLACEHOLDER_API_ENDPOINT_
```

2. When prompted, select the proper environment to complete the installation.

**Data should now be shipping to your Vizion Elastic app. Check the ```Discover``` tab in Kibana for the incoming logs**

<i>If you have already installed filebeat...</i>

1. Enable the module.

```
filebeat modules enable redis
```

2. Restart Filebeat.

```
service filebeat restart
```

**Data should now be shipping to your Vizion Elastic app. Check the ```Discover``` tab in Kibana for the incoming logs**

<hr>

## Example Dashboard

This module comes with a sample dashboard. For example:

![Imgur](https://imgur.com/iOIHQbu.png)
