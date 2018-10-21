## Design

### Data source
A data source, is described as a system connected to a public or private network with at 
least one valid IPv4 or IPv6 address, capable to send and receive data. Example: a server,
 a logger, a graphic workstation, or an IoT sensor. Examples:

 * Computer systems
 
 * HTTP servers
 
 * Operating systems
 
 * Enterprise services
 
 * Weather stations

Below you can see the structure of a data source object, including its messages, summary
statistics, the devices.

![](https://github.com/sparvu/lmo/blob/master/docs/img/DS.Object.svg)

<img src="https://github.com/sparvu/lmo/blob/master/docs/img/DS.Object.svg" align="center" />
<br/>

### Data message
All collected metrics over time are combined as a data message. There can be many types of
 data messages: metrics regarding computer system utilization cpu or memory utilization, 
 or weather data from a meteorological station, or water cubic meters per hour from an 
 water pump. A data message is in direct relation to a data source.

### Metrics
Any system parameter required for data analysis process. All metrics are grouped in 
data messages.

### Summary Statistics
A series of summary statistic functions, like MAX, MIN, SUM, COUNT, MEAN, PERCENTILE or 
FREQUENCY COUNT applicable to one or more metrics and a time interval. 

The function is defined as a time interval defined: __function__[seconds, precision]. 

 * MAX[10800,60] - stores a series of MAX values, over 3 hours, aggregating data every 
 minute for certain metric
 
 * MAX[300,300] - stores a single value over 5 minutes for a certain metric


Example: _the CPU utilization metric, with MAX, COUNT, SUM, LAST summary statistics 
functions_

```
"statistics": [
  {
    "name": "cpupct",
    "functions": {
      "MAX": [ [ 300, 300 ], [ 10800, 60 ], [ 21600, 300 ], [ 43200, 900 ], [ 86400, 1800 ] ],
      "COUNT": [ [ 300, 300 ], [ 1800, 1800 ], [ 10800, 60 ], [ 21600, 300 ], [ 43200, 900 ], [ 86400, 1800 ] ],
      "SUM": [ [ 300, 300 ], [ 1800, 1800 ], [ 10800, 60 ], [ 21600, 300 ], [ 43200, 900 ], [ 86400, 1800 ] ], 
      "LAST": [ [ 300, 300 ], [ 10800, 60 ], [ 21600, 300 ], [ 43200, 900 ], [ 86400, 1800 ] ]
    }
  }
]
```

### Format
Currently the library is structured as a series of JSON, XML, YAML files.
