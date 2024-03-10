# POTAutils
Various POTA Utilities

## pcc

**Find POTA Country Code Prefixes by either name or prefix**

This simple command uses the JSON country codes API to find and list out a country code in question
It will also, find it by country name, if so desired.


### POTA country code prefix finder Usage

**usage: pcc [ country-code | -n country-name ]**

pcc without the -n switch will search for a country code

pcc with the -n switch will search by country name

all inputs are case insensitive for either search type

the output will consist of 3 lines: 
* country prefix, 
* country name, 
* and the number of parks in the pota database for that country

**NOTE: this uses the jq utility** - (see https://github.com/jqlang/jq), or just do $ sudo apt install jq

#### Examples
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
## pcc1

**Find POTA Country Code Prefixes by either name or prefix**

This simple command uses the JSON country codes API to find and list out anything that matches either a country prefix or a name or both.

### POTA country code prefix finder Usage

**usage: pcc1 [ country-code | country-name ]**

**NOTE: this uses the jq utility** - (see https://github.com/jqlang/jq), or just do $ sudo apt install jq

#### Examples

```
$ pcc1 united
K - United States of America
...
```

```
$ pcc1 japa
JA - Japan
...
```

**Note: There might be many entries, so you need to choose**

# POTA Spotting

## setfreq

There is a new setfreq python script, which uses xmlrpc to communicate with FLRig over the localhost. It is used now in yspots to set the frequency.
It has been tested on my FT-710 and works great. As long as cat control works with FLRig to your rig, this should work flawlessly.

usage: setfreq frequency-in-KHz (e.g. 14292)

Be sure to put setfreq in your path, or yspots won't find it.

## yspots

This short program uses jq and yad. So make sure you have these installed.

This program gets the current activator spots in POTA.

$ yspots - will be short width on the right of the screen

$ yspots -f will be a centered almost full width of the screen

yspots now has a checkbox for each entry. If you check the boxes it will be saved to $HOME/potaspots.selections 

when you invoke yspots again, those spots if they still exist will be selected again. This is so you can know which ones you have contacted. When you are completely done, you can use the clear button at the bottom to clear those selections.

**UPDATE: 2024-03-10**

There is a new companion script, **setfreq**, which will set the frequency of your rig (in KHz), if you use FLRig.

When you now double-click on a row in yspots it will call setfreq and attempt to communicate with FLRig to change the frequency.

Note: This only works with SSB.

yspots now has a new command line option `-c` which will copy the spot callsign to the clipboard. This required that *xclip* is installed.


**UPDATE: 2023-09-13**

yspots now has 2 new command line options

-b band

This will limit your spots to the band in question.

-m mode

This will limit your spots to the mode in question.

```
$ yspots -h

$ yspots -b 20m

$ yspots -b 20m -m ssb

$ yspots -b 20

$ yspots -m ft8

$ yspots -m ft8 -b 20
```

## spots

This is a version of POTA spots that does NOT use yad. it uses jq. 
spots and yspots are separate files. spots has options -b and -m, like its counterpart yspots.

It outputs to:
* stdout
* notify-send
  
## getcsvfilefrompota

This script gets a download of entities from a specific country code to a csvfile you choose.

usage: **getcsvfilefrompota** [prefix | name] > csvfilename.csv

to get ALL of USA into one file do the following:

$ **getcsvfilefrompota** K > USA.csv

**NOTE: you need jq, fzf and pcc1 to run this utility**

pcc1 is found in this repository, (jq and fzf can be installed on your system, either by building from source, or by using the apt install utility)
