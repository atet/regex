# [atet](https://github.com/atet) / [learn](https://github.com/atet/learn) / [**_regex_**](https://github.com/atet/learn/tree/master/regex)

[![.img/logo_sharex.png](.img/logo_regex.png)](#nolink)

# Introduction to Regular Expressions

* Estimated time to completion: 15 minutes.
* This quick introduction to regular expressions (regex) is meant to cover only the absolute necessary material to get you up and running in a minimal amount of time.
* You are here because **you want to learn a few simple tricks to quickly process large amounts of text data**.
* We will be using <a href="https://en.wikipedia.org/wiki/Bash_(Unix_shell)" target="_blank">Bash Command Line Interface (CLI)</a> to perform basic operations; advanced material is not covered here.

--------------------------------------------------------------------------------------------------

## Table of Contents

### Introduction

* [0. Requirements](#0-requirements)
* [1. Installation](#1-installation)
* [2. Preface](#2-preface)
* [3. Basic Use](#3-basic-use)
* [4. Example Files](#4-example-files)
* [5. Your First `grep`](#5-your-first-grep)
* [6. Extended `grep`](#6-extended-grep)
* [7. Tabular Data](#7-tabular-data)
* [8. Bigger Data](#8-bigger-data)
* [9. Next Steps](#9-next-steps)

### Supplemental

* [Other Resources](#other-resources)
* [Troubleshooting](#troubleshooting)
* [Acknowledgments](#acknowledgments)

--------------------------------------------------------------------------------------------------

## 0. Requirements

* This tutorial was developed on Microsoft Windows 10 with Windows Subsystem for Linux (WSL) using Ubuntu 18.04 LTS
* If you are using MacOS, [your Terminal program is Bash](https://en.wikipedia.org/wiki/Terminal_(macOS))
* Most Linux distributions use or can use Bash

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 1. Installation

### Windows 10

* Windows Subsystem for Linux (WSL) is a fully supported Microsoft product for Windows 10, learn how to install it here: [https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* Please choose Ubuntu 18.04 LTS as the distribution you use with WSL
* WSL is only available for Windows 10

### MacOS

* You do not need to install anything, [your Terminal program is Bash](https://en.wikipedia.org/wiki/Terminal_(macOS))

### Linux

* I recommend using Ubuntu 18.04 LTS

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 2. Preface

### What is Bash?

* Bash is a command line interface (CLI) that allows you to use your operating system purely by text commands 
   * This is a huge benefit over clicking buttons in a graphical user interface **especially if you have a ton of repetitive and routine tasks**
* If you're a Windows user like I am, _unlike DOS Command Prompt that is tied to Microsoft_, Windows Subsystem for Linux finally allows some cross-compatibility with Linux and MacOS

### WARNING: CLI is very powerful

* With great power comes great responsibility; be vigilant of code you run so accidents don't happen
* If this is your first experience with using a command line interface, don't be intimidated, this is worth learning

### Regular Expressions

* Basically, regular expressions are special notation that describes a pattern
* This notation can be:
   * As simple as "." (regex wildcard), in which you can use ".\\.pdf" to search for all PDF filenames on your computer
   * Or a bit more complex like "[A-z0-9]+@[A-z0-9]+\\.[A-z]+" to search for all valid email addresss in a huge mailing list

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 3. Basic Use

### Welcome to CLI

* Before we dive into regular expressions, let's go over some basic commands to get around in Bash
* When you first start your command line interface (CLI), you'll typically be greeted with something similar to this:

```
atet:LAPTOP:~$ _
```
* For the sake of this tutorial, type out any commands you see after the `$` in the examples below

### Navigation

* If you're accustomed to using a graphical user interface (GUI) file explorer, just continue to think of your files and folders (a.k.a. "directories") in a tree-like structure

[![.img/step03a.png](.img/step03a.png)](#nolink)

* If you execute the command `pwd` ("print working directory"), you'll see where you are currently in your file system

```
atet@LAPTOP:~$ pwd
/home/atet
```

* We can see what files are in your current working directory by executing `ls` ("list")

```
atet@LAPTOP:~$ ls
book.txt  new  song.mp3
```

* If you need more information about your files, you can add the flag `-l` to see more detail

```
atet@LAPTOP:~$ ls -l
total 0
-rw-rw-rw- 1 mba mba    0 Dec 21 18:39 book.txt
drwxrwxrwx 1 mba mba 4096 Dec 21 18:42 new
-rw-rw-rw- 1 mba mba    0 Dec 21 18:39 song.mp3
```

* A lot of information, but in this example we see that the file `new` is actually a directory (look all the way to the left and you see the `d`)
* If you have directories you want to navigate in and out of, you can use `cd <DIRECTORY NAME>` ("change directory") to go in and `cd ..` to go out

```
atet@LAPTOP:~$ cd new
atet@LAPTOP:~/new$ cd ..
atet@LAPTOP:~$
```

### File Management

* We only need to know four commands for file management this tutorial
* To make a new directory, use `mkdir <NEW NAME>` ("make directory")

```
atet@LAPTOP:~$ mkdir folder
atet@LAPTOP:~$ cd folder
atet@LAPTOP:~/folder$
```

* We will download an example files from my GitHub to work on, let's download one now with the program `wget`

```
atet@LAPTOP:~/folder$ wget https://raw.githubusercontent.com/atet/learn/master/regex/data/jane.txt

<A BUNCH OF WGET STATUS TEXT>

atet@LAPTOP:~/folder$ ls
jane.txt
```

* This is a short file, so we can take a peek at **all** the text contents using the program `cat` (don't use `cat` on big files, use `head` or `tail`)

```
atet@LAPTOP:~/folder$ cat jane.txt
Andrew_WK_-_Party_Hard.mp4
Beethoven_-_Fur_Elise.m4a
Beethoven_-_Symphony_No_6.mp3
Eddie_Murphy_-_Party_All_the_Time.mp3
LMFAO_-_Party_Rock_Anthem.mp4
Miley_Cyrus_-_Party_In_The_USA.mp4
Rick_Astley_-_Never_Gonna_Give_You_Up.m4a
```

* Let's **permanently delete** this file for now with `rm` ("remove")
   * WARNING: There will be no confirmation to delete files nor is there a concept of "recycling bin" here, be very careful with `rm`

```
atet@LAPTOP:~/folder$ ls
jane.txt
atet@LAPTOP:~/folder$ rm jane.txt
atet@LAPTOP:~/folder$ ls
atet@LAPTOP:~/folder$ _
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 4. Example Files

* **I will now start each line with only `$`, type everything _after_ this**
* Let's start at your home directory (a.k.a. `~`) and make a new empty directory to work from

```
$ cd ~
$ mkdir regex
$ cd regex 
```

* Download these two example files from my GitHub using `wget` and chaining the two commands into one line using `&&`

```
$ wget https://raw.githubusercontent.com/atet/learn/master/regex/data/jane.txt && wget https://raw.githubusercontent.com/atet/learn/master/regex/data/john.txt

<A BUNCH OF WGET STATUS TEXT>

$ ls
jane.txt  john.txt
```

* We can take a look at the text content of all the files in the current directory using `cat` and the wildcard `*` (this means **ALL** files)

```
$ cat *
Andrew_WK_-_Party_Hard.mp4
Beethoven_-_Fur_Elise.m4a
Beethoven_-_Symphony_No_6.mp3
Eddie_Murphy_-_Party_All_the_Time.mp3
LMFAO_-_Party_Rock_Anthem.mp4
Miley_Cyrus_-_Party_In_The_USA.mp4
Rick_Astley_-_Never_Gonna_Give_You_Up.m4a
Party All the Time - Eddie Murphy.m4a
MOZART PIANO SONATA 11.M4A
eddie - party all the time (remix).mp4
mozart_requiem.mp3
Rick Astley - Never Gonna Give You Up.m4a
ANDREW WK - PARTY HARD.MP4
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 5. Your First `grep`

* We need to find songs in John's music library which are of the `*.mp3` file type:

```
$ grep -n "mp3" john.txt
4:mozart_requiem.mp3
```

* It looks like line number 4 has the one file were were looking for (`-n` flag will output line number, try without it)

* We need to find songs in John's library that are NOT `*.m4a` audio (`-v` flag, you can stack different flags together):

```
$ grep -vn "m4a" john.txt
2:MOZART PIANO SONATA 11.M4A
3:eddie - party all the time (remix).mp4
4:mozart_requiem.mp3
6:ANDREW WK - PARTY HARD.MP4
```

* Almost, line 2 is an *.m4a file and was included, let's ignore case (`-i`):

```
$ grep -vni "m4a" john.txt
3:eddie - party all the time (remix).mp4
4:mozart_requiem.mp3
6:ANDREW WK - PARTY HARD.MP4
```

* Let's see all the songs that have "party" in the title in John's library AND (remember `&&`) also count them (`-c`):

```
$ grep -ni "party" john.txt && grep -ci "party" john.txt
1:Party All the Time - Eddie Murphy.m4a
3:eddie - party all the time (remix).mp4
6:ANDREW WK - PARTY HARD.MP4
3
```

* Three party songs! Now let's include Jane's library in this search
* Currently, your working directory only has the `john.txt` and `jane.txt` file, so if we use the wildcard `*` instead of a file name, all files in the current directory will be searched together
* Additionally we just want to output which file (not all the file contents) contains songs by Beethoven (`-l"`)

```
$ grep -li "beethoven" *
jane.txt
```

* Looks like only Jane has songs from Beethoven, how about Mozart

```
$ grep -li "mozart" *
john.txt
```

* Looks like only John has songs from Mozart, how about "party" songs

```
$ grep -li "party" *
jane.txt
john.txt
```

* Looks like they both like to party, let's see all the party songs between the two of them:

```
* grep -ni "party" *
jane.txt:1:Andrew_WK_-_Party_Hard.mp4
jane.txt:4:Eddie_Murphy_-_Party_All_the_Time.mp3
jane.txt:5:LMFAO_-_Party_Rock_Anthem.mp4
jane.txt:6:Miley_Cyrus_-_Party_In_The_USA.mp4
john.txt:1:Party All the Time - Eddie Murphy.m4a
john.txt:3:eddie - party all the time (remix).mp4
john.txt:6:ANDREW WK - PARTY HARD.MP4
```

* That's a lot of party songs, but what if we only want remixes of party songs? This will require us to perform two `grep` operations:
   1. The first operation will look for all songs with "party" and pass these results to...
   2. The second operation which will further look for songs with "remix"
* We can combine the two operations using the pipe operator "`|`" to pass information (this is different than `&&` earlier which just performed two separate commands)
   * Note that the second operation doesn't need the `-n` flag or `*` wildcard since it is getting "filtered" input directly from the first operation

```
$ grep -ni "party" * | grep "remix"
john.txt:3:eddie - party all the time (remix).mp4
```

* Like the great Eddie Murphy always says:

> _"Party all the time"_ -Eddie Murphy

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 6. Extended `grep`

### **TLDR**: Just use `grep -E` or `egrep`

* In order to use more advanced `grep` functionality, **you must use the `-E` flag**
   * I recommend always using this flag with any `grep` command or use `egrep` ("extended `grep`")
   * Using extended `grep` will not require you to use [escape characters](https://en.wikipedia.org/wiki/Escape_character#Bourne_shell) for some symbols
   * `egrep` has all the same functionality as `grep`

### Back to the show

* Let's search for songs by both mozart OR beethoven using an extended `grep` command "`|`"
   * "`|`" used in `grep` context between the quotations means "or", not pipe as above in Bash context
   * You must use the `-E` flag for use of pattern matching commands like "`|`", try without `-E` and it won't work

```
$ grep -En "mozart|beethoven" *
john.txt:4:mozart_requiem.mp3
```

* I know there were more songs.. oops, don't forget to ignore case

```
$ grep -Eni "mozart|beethoven" *
jane.txt:2:Beethoven_-_Fur_Elise.m4a
jane.txt:3:Beethoven_-_Symphony_No_6.mp3
john.txt:2:MOZART PIANO SONATA 11.M4A
john.txt:4:mozart_requiem.mp3
```

* Let's see which of these classical songs have numbers in the title
* `[0-9]` means to look for numerals 0 through 9 and the `+` after means one or more of the thing before
* Let's also combine this with the Bash pipe operator `|` (remember, different "meaning" than regex "or")

```
$ grep -Eni "mozart|beethoven" * | grep -E "[0-9]+"
jane.txt:2:Beethoven_-_Fur_Elise.m4a
jane.txt:3:Beethoven_-_Symphony_No_6.mp3
john.txt:2:MOZART PIANO SONATA 11.M4A
john.txt:4:mozart_requiem.mp3
```

* Oh no, looks like some file extensions with numbers were picked up here too
* Let's make this more specific by adding the regex wildcard `.` and one or more `+`
* This means that the numbers we are looking for can't be at the end of the filename (i.e. file extension) since there has to be some characters after

```
$ grep -Ei "mozart|beethoven" * | grep -E "[0-9]+.+"
jane.txt:Beethoven_-_Fur_Elise.m4a
jane.txt:Beethoven_-_Symphony_No_6.mp3
john.txt:MOZART PIANO SONATA 11.M4A
```

* Almost, looks like "mp3" was removed, but not "m4a", let's be more specific to say that you need a space before the number

```
$ grep -Ei "mozart|beethoven" * | grep -E " [0-9]+.+"
john.txt:MOZART PIANO SONATA 11.M4A
```

* Could've sworn there were two files, Oh! the other file had an underscore, not a space before the number 6, let's try a regex or "`|`"

```
$ grep -Ei "mozart|beethoven" * | grep -E " [0-9]+.+|_[0-9]+.+"
jane.txt:Beethoven_-_Symphony_No_6.mp3
john.txt:MOZART PIANO SONATA 11.M4A
```

* We've seen so far that the results were just printed out to the screen, let's write that output into a new file called `results.txt` using redirection "`>`"

```
$ grep -Ei "mozart|beethoven" * | grep -E " [0-9]+.+|_[0-9]+.+" > results.txt
$ cat results.txt
jane.txt:Beethoven_-_Symphony_No_6.mp3
john.txt:MOZART PIANO SONATA 11.M4A
```

* Cool, now let's clear out all the files to work on different data in the next section:

```
$ rm john.txt && rm jane.txt && rm results.txt
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 7. Tabular Data

* Looks like John and Jane updated their library data with additional information, let's download it:

```
$ wget https://raw.githubusercontent.com/atet/learn/master/regex/data/jane.csv && wget https://raw.githubusercontent.com/atet/learn/master/regex/data/john.csv
```

* Let's take a look at the new data using `head -3` (show only the first three lines of each file):

```
$ head -3 *
==> jane.csv <==
owner,filename,genre,length,date modified
Jane,Andrew_WK_-_Party_Hard.mp4,Hard Rock,3:26,2016-10-24
Jane,Beethoven_-_Fur_Elise.m4a,Classical,2:56,2007-01-04

==> john.csv <==
owner,filename,genre,length,date modified
John,Party All the Time - Eddie Murphy.m4a,Funk,4:08,2008-11-20
John,MOZART PIANO SONATA 11.M4A,Classical,14:31,2007-03-07
```

* Looks like it's comma separated values (CSV), like something you'd see in a spreadsheet program like Excel
* Unfortunately it's not very readable above, let's use the `column` command to make it a bit prettier (with some flags):

```
$ head -3 * | column -t -s,
==> jane.csv <==
owner             filename                               genre      length  date modified
Jane              Andrew_WK_-_Party_Hard.mp4             Hard Rock  3:26    2016-10-24
Jane              Beethoven_-_Fur_Elise.m4a              Classical  2:56    2007-01-04
==> john.csv <==
owner             filename                               genre      length  date modified
John              Party All the Time - Eddie Murphy.m4a  Funk       4:08    2008-11-20
John              MOZART PIANO SONATA 11.M4A             Classical  14:31   2007-03-07
```

**Under Construction: Please check back later!**

* Cool, now let's clear out all the files to work on different data in the next section:

```
$ rm john.csv && rm jane.csv && rm results.csv
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 8. Bigger Data

* We will download a larger dataset of news articles as another example<sup>[[1]](#acknowledgments)</sup>.

```
$ wget https://raw.githubusercontent.com/atet/learn/master/regex/data/newsCorpora.zip
```

* This file is pretty big and has been compressed, let's extract the file:

```
$ unzip newsCorpora.zip
```

* This Tab Separated Values (TSV) file contains 423,812 records (plus top row header) of news articles and 8 attributes describing them
* We can double check how many lines of data a file has with `wc -l`

```
$ wc -l newsCorpora.tsv
423813 newsCorpora.tsv
```

* Since this is a really big file, we wouldn't want to use commands like `cat` to output everything to the console
   * **If you accidentally `cat`, type `CTRL+C` to cancel the current execution**
* We should only use `head` or `tail` to only see a subset whenever we need to check results
   * Remember that with all the fine tuning we had to do earlier to get the right results, not being able to see everything might cause us to miss a few things
 
```
$ head -2 newsCorpora.tsv | column -t -s $'\t'
ID  TITLE                                                                 URL                                                                                                                          PUBLISHER          CATEGORY  STORY                          HOSTNAME         TIMESTAMP
1   Fed official says weak data caused by weather, should not slow taper  http://www.latimes.com/business/money/la-fi-mo-federal-reserve-plosser-stimulus-economy-20140310,0,1312750.story\?track=rss  Los Angeles Times  b         ddUyU0VZz0BRneMioxUPQVP6sIxvM  www.latimes.com  1394470370698
```

* Looks pretty dense, and there's 423,811 more records!

**Under Construction: Please check back later!**

* Done for now, let's clear out all the files:

```
$ rm newsCorpora.csv && rm newsCorpora.zip
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 9. Next Steps

**Regex can get very complex to match specific patterns, but it is a powerful tool worth learning**

* We've seen that John was a bit lax with his naming conventions while Jane was a bit more tidy and consistent. In the real world you may have to deal with data that is not so tidy
* When you have the opportunity to start recording your own data, it might be best practice to start off with an organized and consistent format

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Other Resources

Description | Link
--- | ---
`grep` manual | https://www.gnu.org/software/grep/manual/grep.html
Basic vs. Extended `grep` | https://www.gnu.org/software/grep/manual/html_node/Basic-vs-Extended.html
Bash Reference Manual | https://www.gnu.org/software/bash/manual/bash.pdf

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Troubleshooting

Issue | Solution
--- | ---
`$: command not found` | Don't type the `$` at the beginning of the example commands, that's there for line reference
There's no match result to my `grep` | Use `egrep` to see if you forgot to use an [escape character](https://en.wikipedia.org/wiki/Escape_character#Bourne_shell) somewhere
Don't have `unzip` | Install with `$ sudo apt-get install unzip` which requires `sudo` (administrator) permission

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Acknowledgments

1. newsCorpora.tsv is modified from NewsAggregatorDataset.zip: <a href="http://archive.ics.uci.edu/ml/datasets/News+Aggregator" target="_blank">Dua, D. and Graff, C. (2019). UCI Machine Learning Repository [http://archive.ics.uci.edu/ml]. Irvine, CA: University of California, School of Information and Computer Science.</a>

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

<p align="center">Copyright © 2019-∞ Athit Kao, <a href="http://www.athitkao.com/tos.html" target="_blank">Terms and Conditions</a></p>