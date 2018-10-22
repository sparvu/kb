## Data Mapping

This section describes how can you create a new data source object, along with all needed 
information: the data messages, the summary statistics, the alarms and devices. For this 
example we will use a simple indoor air quality device, from Tongdy corporation, called
G01-IAQ, documented ![here](http://en.tongdy.com/a/COjiancechanpin/44.html)


Before doing that, you need to create a new data source object, by
defining what data messages, summary statistics you are interested in and ultimately
what information you will visualize and report. 

![](https://github.com/sparvu/lmo/blob/master/docs/img/Tongdy.G01.DS.svg)

### Format
Currently the library is structured as a series of JSON, XML, YAML files.
