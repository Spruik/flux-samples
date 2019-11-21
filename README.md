# flux-samples

Here are some sample flux queries to perform common functions in machine downtime analysis

## Interpolating at time range boundaries

When quering a time range, it's good to get an interpolated record at the start and end of the time range that is being queried, and raw data for the rest of the query.

An example of when this is useful is machine state change events. Here I want to be able to see:
- what was the state of the machine at the start of the time range
- What changes in state occured during the range
- What was the state of the machine at the end of the time range

```

```


## Event Duration query

Often, we need to see and aggregate the duration in of a machine state event. This is slightly different to the built-in function elapsed, which shows how long since the previous record, machine state needs to show how long till the next record.


```

```
