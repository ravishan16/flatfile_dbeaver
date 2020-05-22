# Using flatfiles as database in dbeaver

## Usecases:
- query filter/group by or run any simple sql operation on a csv or any delimited file
- Dont want to create a new dbeaver connection for every file

## Solution:
- create a root folder that can be used for flatfiles
- create child folders csv, pipe, tsv .... so independent connections can be created for different file types in dbeaver. Here is my folder structure
```
├── data
│   ├── csv
│   │   └── dataset_csv_dat.csv
│   └── pipe
│       └── test_pipe_delimited_dat.csv
```
- create dbeaver connection for csv and set the path to data/csv
![](assets/create_csv_connection.mov)
- create create dbeaver connection for pipe or any delimited file typ, set the path to data/pipe(or the format). Update the seperator in "Driver Properties"