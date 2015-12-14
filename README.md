# storm-jmx-metrics

An project is to get all storm built-in metrics and send to Jmx, Ganglia and Graphite. 
The idea came up with an open source project named storm-graphite (https://github.com/verisign/storm-graphite)

This project used Coda Hale metrics (http://metrics.dropwizard.io) and deployed IMetricsConsumer of Storm.

To use this:
- Setup on local mode (I just test on this)
- Add lines in $STORM_HOME/conf/storm.yaml file:

  topology.metrics.consumer.register:
    - class: "storm.jmx.metrics.consumer.CustomMetricsConsumer"
- To report to Jmx, just put parameters in $STORM_HOME/conf/storm.yaml or Config in topology:
  argument:
    - storm.reporter: "storm.jmx.reporter.JmxMetricRepoter"
    - domainname: "storm.metrics"
- To report to Ganglia, just put parameters in $STORM_HOME/conf/storm.yaml or Config in topology
 argument:
    - storm.reporter: "storm.jmx.reporter.GangliaMetricRepoter"
    - storm.ganglia.host: "localhost"
    - storm.ganglia.port: 8649
- To report to Graphite (not tested yet), put parameters in $STORM_HOME/conf/storm.yaml or Config in topology:
 argument:
	- storm.reporter: "storm.jmx.reporter.GraphiteRepoter"
	- storm.graphite.host: "localhost"
	- storm.graphite.port: 2003
	- storm.graphite.protocol: "UDP"
	
- To send metrics to Logstash by Jmx.
	
   - First, install Jmx Plugin in Logstash
   - Create pipeline: see in resource folder
   - Create json file to query remote object: see in resource folder
   *NOTE: in object_name, storm.metrics is your domain name when configuring in storm.yaml

- To send metrics to Logstash with Ganglia and Graphite input, just create pipeline in Logstash.
