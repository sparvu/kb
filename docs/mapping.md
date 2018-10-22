## Data Mapping

This section describes how can you create a new data source object, along with all needed 
information: the data messages, the summary statistics, the alarms and devices. For this 
example we will use a simple indoor air quality device, from Tongdy corporation, called
G01-IAQ, documented [here][1]

### Pre-requisites

Before writing the new DS object, make sure you collect the following details:

 * if it is a a hardware device: the model and type
 
 * if it is a software, the name of the software and its model, version
 
 * the protocol used to communicate, for example MODBUS or SERIAL ASCII POLLED, or TCP
 
 * and the parameters required for analysis and visualisation

### Hardware characteristics

For our example, Tongdy G01-IAQ, we start by simple writing down the hardware details 
about the device:

 * manufacturer: Tongdy
 * device: G01-IAQ
 * model: in this case is the same as the device name: G01-IAQ
 * protocol: this device uses MODBUS-RTU

Summarising these we will define a new object, called tongdy_g01, to map the vendor and
the hardware device model to the new object.

### The message

#### Parameters

From this device we are interested in few parameters, like air temperature (Ta), relative 
humidity (Rh), the carbon dioxide (CO2) and the volatile organic compound (VOC). We will
define a single message for all these parameters, fetching data every 60 seconds, with
a STALL alarm of 120seconds. 

#### STALL alarm

The STALLL alarm defines the maximum number of seconds after which we set an alarm marking
no data was received. Since we receive data every minute from this device, the STALL alarm
of 2 minutes is more than enough. The SLI means the Service Level Indicator, and it is
used to mark that this message is directly linked in marking the data source as being 
STALLed. 

Note: there are data sources which can have one or many messages, and not all messages
will be direct responsbile for the data source state. Maybe only part of the messages
will direct affect the data source status: ONLINE, OFFLINE. The SLI marker is used exactly
to mark what messages are direct linked to the data source status.

This will be the JSON defintion of the message:

```
        "iaq_g01": {
          "id": "iaq_g01",
          "rawdata": "iaq_g01.krd",
          "stall": 120,
          "sli": "yes",
          "format": {
            "fields_separator": ":",
            "fields": [
              {
                "name": "subscription_id",
                "type": "metadata",
                "role": "subscription_id"
              },
              {
                "name": "ds_id",
                "type": "metadata",
                "role": "ds_id"
              },
              {
                "name": "timestamp",
                "type": "timestamp",
                "timestamp_format": "unix"
              },
              {
                "name": "device_id",
                "type": "metadata",
                "role": "device_id"
              },
              {
                "name": "ta",
                "type": "numeric"
              },
              {
                "name": "rh",
                "type": "numeric"
              },
              {
                "name": "td",
                "type": "numeric"
              },
              {
                "name": "co2",
                "type": "numeric"
              },
              {
                "name": "voc",
                "type": "numeric"
              },
              {
                "name": "hash",
                "type": "hash",
                "function": "sha256"
              }
            ]
          },
          "statistics": [...]
        }
```

#### Summary statistics functions

The last part will describe what summary statistics are associated to each recorded 
parameter. These are direct connected to how and what data we present on the UI: charts,
indicators, maximum or minimum per day of certain parameters. For all our recorded metrics
we have selected the following summary statistics functions: MIN, MAX, MEAN and LAST.

Another part of the summary statistics functions comes over what period of time are we
gonna record and keep these numbers. 

For example here is defined for a single parameter, like air temperature what summary 
statistics functions we gonna need and their time intervals.

```
{
  "name": "ta",
  "functions": {
    "MEAN": [ [900, 900], [3600, 3600], [21600, 21600], [86400, 86400], [21600, 60], [43200, 300], [86400, 600], [604800, 3600], [2592000, 10800], [ 7776000, 32400 ], [ 15552000, 64800 ], [ 31104000, 86400] ],
    "MAX": [ [900, 900], [3600, 3600], [21600, 21600], [86400, 86400], [21600, 60], [43200, 300], [86400, 600], [604800, 3600], [2592000, 10800], [ 7776000, 32400 ], [ 15552000, 64800 ], [ 31104000, 86400] ],
    "MIN": [ [900, 900], [3600, 3600], [21600, 21600], [86400, 86400], [21600, 60], [43200, 300], [86400, 600], [604800, 3600], [2592000, 10800], [ 7776000, 32400 ], [ 15552000, 64800 ], [ 31104000, 86400] ],
    "LAST": [ [60, 60], [900, 900], [3600, 3600], [21600, 21600], [86400, 86400], [21600, 60], [43200, 300], [86400, 600], [604800, 3600], [2592000, 10800], [ 7776000, 32400 ], [ 15552000, 64800 ], [ 31104000, 86400] ]
    }
},
```


### The object

Finally the new object, including its message and summary statistics functions, looks
like below [JSON version](tongdy.g01.json) and graphically:

![](https://github.com/sparvu/lmo/blob/master/docs/img/Tongdy.G01.DS.svg) 

[1]: http://en.tongdy.com/a/COjiancechanpin/44.html