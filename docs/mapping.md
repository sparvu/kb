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

#### Hardware characteristics

For our example, Tongdy G01-IAQ, we start by simple writing down the hardware details 
about the device:

 * manufacturer: Tongdy
 * device: G01-IAQ
 * model: in this case is the same as the device name: G01-IAQ
 * protocol: this device uses MODBUS-RTU

Summarising these we will define a new object, called tongdy_g01, to map the vendor and
the hardware device model to the new object.

#### The messages

From this device we are interested in few parameters, like air temperature (Ta), relative 
humidity (Rh), the carbon dioxide (CO2) and the volatile organic compound (VOC). We will
define a single message for all these parameters, fetching data every 60 seconds, with
a STALL alarm of 120seconds. 

The STALLL alarm defines the maximum number of seconds after which we set an alarm marking
no data was received. Since we receive data every minute from this device, the STALL alarm
of 2 minutes is more than enough.

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

#### Summary statistics

#### The object

![](https://github.com/sparvu/lmo/blob/master/docs/img/Tongdy.G01.DS.svg)

[1]: http://en.tongdy.com/a/COjiancechanpin/44.html