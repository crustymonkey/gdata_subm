# About
A library for Grafana data submissions.  You can use this library to create data structures for submission that is compatible with the format of the `write_http` module for `collectd`.

# Usage
The interface here is quite simple.  To create a chunk of data for submission, you simply do the following:

```
from gdata_subm import Gdata

data = Gdata(
    plugin='plugin_name',
    dstypes=['gauge', 'derive', 'counter'],
    dsnames=['metric1', 'metric2', 'metric3'],
    values=[1.0, 2.0, 3.0],
    host='host.example.com',
    interval=5.0,
)
```

Then, you can use the http submitter to submit your data to the server.

```
from gdata_subm import GdataSubmit

subm = GdataSubmit(
    username='myuser',
    password='supersecret',
    url='https://receiver.example.com',
)

success = subm.send_data([data])

```

That's it.  `GdataSubmit.send_data()` takes a list of Gdata objects and sends them to your server.
