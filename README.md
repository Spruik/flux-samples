# flux-samples

Here are some sample flux queries to perform common functions in machine downtime analysis

## Interpolating at time range boundaries

When quering a time range, it's good to get an interpolated record at the start and end of the time range that is being queried, and raw data for the rest of the query.

An example of when this is useful is machine state change events. Here I want to be able to see:
- what was the state of the machine at the start of the time range
- What changes in state occured during the range
- What was the state of the machine at the end of the time range

```
start = from(bucket:"smart_factory/autogen")  
|> range(start:-1y,stop:time(v: $__from*1000000))
|> filter(fn: (r) => r._measurement == "Availability")
|> filter(fn: (r) => r._field == "held")
|> last()
|> drop(columns:["_time"])
|> duplicate(column: "_stop", as: "_time")

end = from(bucket:"smart_factory/autogen")  
|> range(start:-1y,stop:time(v: $__to*1000000))
|> filter(fn: (r) => r._measurement == "Availability")
|> filter(fn: (r) => r._field == "held")
|> last()
|> drop(columns:["_time"])
|> duplicate(column: "_stop", as: "_time")

data = from(bucket:"smart_factory/autogen")  
|> range($range)
|> filter(fn: (r) => r._measurement == "Availability")
|> filter(fn: (r) => r._field == "held")

 union(tables: [start, data, end])
```


## Event Duration query

Often, we need to see and aggregate the duration in of a machine state event. This is slightly different to the built-in function elapsed, which shows how long since the previous record, machine state needs to show how long till the next record.


```

```
