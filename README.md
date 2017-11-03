[![Build Status](https://travis-ci.org/andykuszyk/simpcass.svg?branch=master)](https://travis-ci.org/andykuszyk/simpcass)

# simpcass
A simple client class for accessing a Cassandra database, controlling
the disposal of connections and exposing useful methods for batch
and dataframe (pandas) querying.

## Installation
`pip install simpcass`

## Usage

```
from simpcass import CassandraClient
```

Simple queries:
```
with CassandraClient('127.0.0.1', 9042) as client:
    rows = client.execute('select * from spam.eggs where foo = %s', ('bar',))
```

Results in a pandas dataframe:
```
with CassandraClient('127.0.0.1', 9042) as client:
    df = client.execute_df('select * from spam.eggs where foo = %s', ('bar',))
```

Batch execution:
```
with CassandraClient('127.0.0.1', 9042) as client:
    client.execute_batch(
        ['select * from spam.eggs where foo = %s', 'select * from spam.eggs where foo = %s'],
        [('bar',), ('bar',)]
    )
```
