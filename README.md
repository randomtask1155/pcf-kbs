Loggregator Handbook
===========

-   Version-controlled
-   Forkable
-   Continuously updated
-   [Written in markdown](https://sculpin.io/)

Loggregator is composed of:
* **Sources**: Logging agents that run on the Cloud Foundry components.
* **Metron**: Metron agents are co-located with sources. They collect logs and forward them to:
* **Doppler**: Responsible for gathering logs from the **Metron agents**, storing them in temporary buffers, and forwarding logs to 3rd party syslog drains.
* **Traffic Controller**: Handles client requests for logs. Gathers and collates messages from all Doppler servers, and provides external API and message translation (as needed for legacy APIs).

Source agents emit the logging data as [protocol-buffers](https://github.com/google/protobuf), and the data stays in that format throughout the system.

#### Runner VMs

1. App Container
  2. App Instance (N)
  3. Logs 
2. Diego Executioner
  3. Metreon Agent
  4. Logs
4. Diego
  5. StatsD Metrics
    6. StatsD Injector
    7. Metron Agent
  8. Logs

![Loggregator Diagram](https://github.com/cloudfoundry/loggregator/blob/develop/docs/loggregator.png )

In a redundant CloudFoundry setup, Loggregator can be configured to survive zone failures. Log messages from non-affected zones will still make it to the end user. On AWS, availability zones could be used as redundancy zones. The following is an example of a multi zone setup with two zones.

### Runner VMS

<img src="https://github.com/timani/pcf-loggregator/blob/structure/img/Screen%20Shot%202016-09-12%20at%209.55.08%20PM.png" width="200" />

#### App Container

#### Diego Executor


#### StatsD Metrics
- StatsD Injector
- Metron Agent

### Cloud Controller VMs

<img src="https://github.com/timani/pcf-loggregator/blob/structure/img/Screen%20Shot%202016-09-12%20at%209.55.20%20PM.png" width="200" />

- Cloud Controller
- UAA
- Go Router

#### StatsD Metrics
- StatsD Injector
- Metron Agent

#### Ryslog

#### Component
- Syslog Drain
- Splunk
- Papertrail

### Contributing

Read [CONTRIBUTING.md](<CONTRIBUTING.md>) for more details on contributing
documentation improvements.

