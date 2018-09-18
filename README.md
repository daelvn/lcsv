# lcsv
Lua CSV parsing library.
## Installing
```
$ sudo luarocks install lcsv
```
## Documentation
### Filenames
#### `getmetatable (lcsv.open (string:file, [string:mode])).name -> string:file`
Used to get the filename from handles.
### Source handling
#### `lcsv.open (string:file, [string:mode]) -> File:csvh`
Opens a .csv file. It defaults to "r+" mode.
### Parsing
#### `lcsv.mapLineToHeader (table:csvl, table:header) -> table:csvl`
It will map a CSV line that is numerically indexed to its correspondant header indexes. The header table must be a map of each index to a string (the header).
#### `lcsv.mapHeaderToLine (table:csvl, table:header) -> table:csvl`
Using the same tables as `.mapLineToHeader`, it will turn `csvl` into a numerically indexed table.
#### `lcsv.toLines (string:str) -> table:lines`
Splits a string into lines.
#### `lcsv.parseLine (string:str, [table:header]) -> table:csvl`
It will parse a single line of CSV into a table, optionally with a header.
#### `lcsv.parseAll (table:lines, [boolean:hasHeader]) -> table:csvt, [table:header]`
It parses a table of CSV lines into a table, and if specified, will use the first line as header.
### Reading
#### `lcsv.readHeader (File:csvh, [boolean:move]) -> table:header`
Reads the first line as header. If `move` is set to true, it will go back to the original position, otherwise sets the cursor at the next line of the header. 
#### `lcsv.readLine (File:csvh, [table:header]) -> table:csvl`
It will read the next line in the file handle and parse it into a CSV line.
#### `lcsv.readAll (File:csvh, [boolean:hasHeader]) -> table:csvt, [table:header]`
It reads all the file and parses it into a CSV table.
### Escaping
#### `lcsv.escape (string:str) -> string:escaped`
It escapes a string for use in CSV files.
### To CSV
#### `lcsv.newCsvLine (...) -> string:line`
It escapes all the arguments and puts them in a CSV string.
#### `lcsv.newCsv (table:t) -> string:csvs`
It gets a table of CSV line tables ordered like this:
```lua
{
  { "a", "b", "c"},
  { "d", "e", "f"}
}
```
and turns it into a CSV string like this:
```
a,b,c
d,e,f
```
#### `lcsv.toCsvLine (table:csvl, [table:header]) -> string:line`
Turns a CSV line table into a CSV string.
#### `lcsv.toCsv (table:csvt, [table:header]) -> string:csvs`
Turns a whole CSV table into a CSV string. Will remove the header keys.
### Writing
#### `lcsv.writeRawLine (File:csvh, ...)`
Wrapper around `.newCsvLine` that will write into the document.
#### `lscv.writeLine (File:csvh, ...)`
Wrapper around `.toCsvLine` that writes to the document.
#### `lcsv.writeRawAll (File:csvh, table:t)`
Wrapper around `.newCsv` that writes to the document.
#### `lscv.writeAll (File:csvh, table:csvt, [table:header])`
Wrapper around `.toCsv` that will write into the document.
## License
This project is licensed under MIT.
Cristian Muñiz (c) 2018
