# [atet](https://github.com/atet) / [learn](https://github.com/atet/learn) / [**_regex_**](https://github.com/atet/learn/tree/master/regex)

[![.img/logo_sharex.png](.img/logo_regex.png)](#nolink)

# Introduction to Regular Expressions

* Estimated time to completion: 15 minutes.
* This quick introduction to regular expressions (regex) is meant to cover only the absolute necessary material to get you up and running in a minimal amount of time.
* You are here because **you want to quickly process large amounts of text data**.
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
* [6. Tabular Data](#6-tabular-data)
* [7. Bigger Data](#7-bigger-data)
* [8. Next Steps](#8-next-steps)

### Supplemental

* [Troubleshooting](#troubleshooting)
* [Acknowledgments](#acknowledgments)

--------------------------------------------------------------------------------------------------

## 0. Requirements

* This tutorial was developed on Microsoft Windows 10 with Windows Subsystem for Linux (WSL) using Ubuntu 18.04 LTS
* [If you are using MacOS, your Terminal is Bash](https://en.wikipedia.org/wiki/Terminal_(macOS))
* Most Linux distributions use or can use Bash

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 1. Installation

### Windows 10

* Windows Subsystem for Linux (WSL) is a fully supported Microsoft product for Windows 10, learn how to install it here: [https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* Please choose Ubuntu 18.04 LTS as the distribution you use with WSL
* WSL is only available for Windows 10

### MacOS

* You do not need to install anything, your Terminal program is Bash

### Linux

* I recommend using Ubuntu

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 2. Preface

### What is Bash?

* Bash is a command line interface (CLI) that allows you to use your operating system purely by text commands (a huge benefit over clicking buttons in a graphical user interface if you have a ton of repetitive and routine tasks)
* If you're a Windows user like I am, unlike DOS Command Prompt that is tied to Microsoft, Windows Subsystem for Linux finally allows some cross-compatibility with Linux and MacOS

### WARNING: CLI is very powerful

* With great power comes great responsibility; be vigilant of code you run so accidents don't happen
* If this is your first experience with using a command line interface, don't be intimidated, this is worth learning

### Regular Expressions

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 3. Basic Use

### Navigation

* Before we dive into regular expressions, let's go over some basic commands

### File Management

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 4. Example Files

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 5. Your First `grep`

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 6. Tabular Data

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 7. Bigger Data

* We will use a larger dataset of news articles as an example<sup>[[1]](#acknowledgments)</sup>.
* Click here for the dataset (right-click and "Save as..." then save as _newsCorpora.zip_): <a href="https://raw.githubusercontent.com/atet/learn/master/regex/data/newsCorpora.zip" target="_blank">https://raw.githubusercontent.com/atet/learn/master/regex/data/newsCorpora.zip</a>
* This Tab Separated Values (TSV) file contains 423,812 records of news articles and 8 attributes describing them:



[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 8. Next Steps

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Troubleshooting

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Acknowledgments

1. newsCorpora.tsv is modified from NewsAggregatorDataset.zip: <a href="http://archive.ics.uci.edu/ml/datasets/News+Aggregator" target="_blank">Dua, D. and Graff, C. (2019). UCI Machine Learning Repository [http://archive.ics.uci.edu/ml]. Irvine, CA: University of California, School of Information and Computer Science.</a>

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

<p align="center">Copyright © 2019-∞ Athit Kao, <a href="http://www.athitkao.com/tos.html" target="_blank">Terms and Conditions</a></p>