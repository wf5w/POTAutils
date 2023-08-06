# POTAutils
Various POTA Utilities

## pcc

**Find POTA Country Codes**

This simple command uses the JSON country codes API to find and list out a country code in question
It will also, find it by country name, if so desired.


### pcc - POTA country code finder

**usage: pcc [ country-code | -n country-name ]**

pcc without the -n switch will search for a country code

pcc with the -n switch will search by country name

all inputs are case insensitive for either search type

the output will consist of 3 lines: 
* country prefix, 
* country name, 
* and the number of parks in the pota database for that country

**NOTE: this uses the jq utility** - (see https://github.com/jqlang/jq), or just do $ sudo apt install jq

### Examples
```
$ pcc K
K
United States of America
9787
```

```
$ pcc -n japa
JA
Japan
1256
```

```
$ pcc -n japa | awk 'NR == 1'
JA
```

# yspots

## POTA spots

This short program uses jq and yad. So make sure you have these installed.

This program gets the current activator spots in POTA.

# spots

This is a version of POTA spots that does NOT use yad. it uses jq. 

It outputs to:
* stdout
* notify-send

