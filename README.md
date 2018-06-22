# The Library of Monitoring Objects - LMO

## Overview

A set of data source objects, mapping real-world entities, like weather stations, environmental sensors, ICT infrastructure: computer, network systems, operating systems, entreprise services including the metrics and summary statistics required for analysing their performance, availability and reliability. The objects are grouped by specific industries, like ICT, Environmental Monitoring, Meterology, Business Intelligence, IIoT.

In general, people collect thousands of metrics without any idea what to do with them or if they _really_ need them. Even more  people spend a tremendous amount of time developing solutions to collect and analyse such metrics which soon become deprecated and not useful anymore. The library of monitoring objects is essential and central for any data analytics process from data recording to analysis and visualization. 

The library is designed for software engineers, devops, scientists, analysts, meteorologists and companies involved in data analysis, performance monitoring and analytics.

## Concepts

### Data source

A data source, is described as a system connected to a public or private network with at least one valid IPv4 or IPv6 address, capable to send and receive data. Example: a server, a logger, a graphic workstation, or an IoT sensor. Examples:

 * Computer systems
 
 * HTTP servers
 
 * Operating systems
 
 * Enterprise services
 
 * Weather stations

### Data message
All collected metrics over time are combined as a data message. There can be many types of data messages: metrics regarding computer system utilization cpu or memory utilization, or weather data from a meteorological station, or water cubic meters per hour from an water pump. A data message is in direct relation to a data source. To describe one or many data messages, we have built a library of monitoring objects, (LMO) documented here: [library of monitoring objects](https://github.com/sparvu/lmo)

### Metrics

### Summary Statistics

A series of summary statistic functions, like MAX, MIN, SUM, COUNT, MEAN, PERCENTILE. These functions are direct 
involved in turning data into useful information. These summary statistics have been developed by experts from each 
industry, by carefully looking and analysing what information is required by the end-user or applications.

## Format
Currently the library is structured as a series of JSON, XML, YAML files.

## Industries
The LMO can map and describe data from different industries, currently handling ICT, Meteorology and 
Environmental Monitoring. We are starting to work and define different object types for IoT and IIoT.

![](https://raw.github.com/sparvu/lmo/master/img/lmo-light.png)

 * Industrial IoT (IIoT)
 * Environmental Monitoring
 * Finance
 * Business Intelligence
 * Information Communications & Technology (ICT)
 * Weather and Meteorology
 
