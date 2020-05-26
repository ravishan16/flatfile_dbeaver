![](https://github.com/ravishan16/flatfile_dbeaver/blob/master/assets/flatfile_dbeaver.png?raw=true)

Flat files come in different shapes and sizes. Excel is powerful to analyze and manipulate data. It can get overwhelming for complex analysis. If you want to run SQL queries on large flat files, typically, you import the data into a PostgreSQL/SQLite/MySQL or database of your preference. Another useful tool for quick analysis is using [DBeaver](https://DBeaver.io/), a popular database developer tool's CSV connection. I use the DBeaver CSV connection and scripts to make life easier. 

### [Github Repository Link](https://github.com/ravishan16/flatfile_dbeaver)


## Usecases:
- query filter/group by or run simple SQL operation on a CSV or any delimited file
- Don't want to create a new DBeaver connection for every file/folder

## Solution:
- create a root folder that can be used for flat files
- create child folders CSV, pipe, TSV .... so independent connections can be created for different file types in DBeaver. Here is my folder structure
``` shell
├── data
│   ├── csv
│   │   └── dataset_csv_dat.csv
│   └── pipe
│       └── test_pipe_delimited_dat.csv
```

### One Time Setup
- create DBeaver connection for csv and set the path to data/csv
![](https://github.com/ravishan16/flatfile_dbeaver/blob/master/assets/create_csv_connection.gif?raw=true)


- create DBeaver connection for pipe or any delimited file type, set the path to data/pipe(or the format). Update the separator in "Driver Properties."
![](https://github.com/ravishan16/flatfile_dbeaver/blob/master/assets/create_pipe_connection.gif?raw=true)

- Add this shell function to ~/.zshrc or ~/.bash_profile
``` shell
#usage setdb pipe foo.dat or setdb bar.csv
#open CSV/TSV/PIPE delimited file in DBeaver
#set your DIRECTORY to folder where you wan to root directory where you want to store csv/tsv
# ARgument 1 is csv/tsv/pipe you also should create a folder under the db_root for csv/pipe or what ever delimiter
function setdb(){
	db_root=flatfile_dbeaver/data
	#Take file basename
	orig_filename="$(basename $2)"
	#replace . with _
	filename=${orig_filename//"."/"_"}
	#copy file to csv/tsv/pipe folder under dbroot based on $1 paramter
	eval "cp $2 $db_root/$1/$filename.csv"
}

```

## Usage for a csv file

- Let's say we get a CSV file foo.csv. Run the below command and what this does is copies the foo.csv as foo_csv.csv to flatfile_dbeaver/data/csv
``` shell
setdb csv foo.csv
```
- Refresh the CSV file connection in DBeaver the new file will show as a table under the CSV connection


## Usage for a pipe-delimited file

- Let's say we get a pipe-delimited file bar.txt Run the below command, and what this does is copies the bar.txt as bar_txt.csv to flatfile_dbeaver/data/pipe. Just to keep it simple for the DBeaver connection we use .csv you can change the extension the connection looks for in the Driver Properties
```
setup pipe bar.txt
``` shell
- Refresh the CSV file connection in DBeaver the new file will show as a new table under the CSV connection
![](https://github.com/ravishan16/flatfile_dbeaver/blob/master/assets/move_refresh.gif?raw=true)
```

## Thank You!!