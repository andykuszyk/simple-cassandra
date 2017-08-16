# simpcass
A simple client class for access a Cassandra database, controlling
the disposal of connections and exposing useful methods for batch
and dataframe (pandas) querying.

## Usage

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
