* [Smally](#Smally)
    * [JPEG Compression](#JPEG-Compression)
    * [PNG Compression](#PNG-Compression)
    * [GIF Compression](#GIF-Compression)
    * [Install Tools](#Install-Tools)
        * [Fedora](#Fedora)
        * [Ubuntu](#Ubuntu)
        * [Compile Install](#Compile-Install)
    * [Run Test](#Run-Test)
    * [Usage](#Usage)
    * [Screenshot](#Screenshot)
    * [Old Version](#Old-Version)
    * [Contributors](#Contributors)

# Smally

A simple tool to compress all JPEG, PNG and GIF files losslessly in a folder,
by invoking the famous `jpegtran`, `optipng` and `gifsicle`.

Smally uses `file` command to determine file type, and it would keep
the file name and mtime unchnaged after compression!

## JPEG Compression

1. Using jpegtran to reduce all metadata.
2. To compare among the original file, baseline format and progressive format
files, choose the smallest one in size.
3. Whenever possible, choose progressive format version.

## PNG Compression

Simply calling optipng to compress PNG, in the most crazy `-o7 -zm1-9` level.

## GIF Compression

Simple calling gifsicle to compress GIF, by using `-O3 --color 256`.

## Install Tools

Smally needs jpegtran, optipng and gifsicle to do it's job.

### Fedora

``` shell
$ sudo dnf install libjpeg-turbo-utils optipng gifsicle
```

### Ubuntu

``` shell
sudo apt install libjpeg-turbo-progs optipng gifsicle
```

### Compile Install

``` shell
$ sudo bash _install_tools.sh JPEG
$ sudo bash _install_tools.sh PNG
$ sudo bash _install_tools.sh GIF
$ # or all in one command
$ sudo bash _install_tools.sh JPEG PNG GIF
```

This will compile and install the latest version of jpegtran,
optipng and gifsicle at /usr/bin automatically.
**Be careful, the originals will be removed.**

For the success of installation, you might also need:

``` shell
$ sudo dnf install gcc make autoconf automake
```

##  Run Test

``` shell
$ bash test.sh
```

##  Usage

Normally:

``` shell
$ # for all jpeg, png and gif
$ find <path/to/image_folder> -type f -exec bash smally.sh {} \;
$ # only jpeg
$ find <path/to/image_folder> -type f -exec bash smally.sh -t JPEG {} \;
$ # only png
$ find <path/to/image_folder> -type f -exec bash smally.sh -t PNG {} \;
$ # only gif
$ find <path/to/image_folder> -type f -exec bash smally.sh -t GIF {} \;
```

Or to use `xargs' -P parameter` to take advantage of multi-core CPU:

``` shell
$ # -P4 means 4 paralleled processes
$ find <pathname> -type f -print0 | xargs -0 -P4 -I{} bash smally.sh {}
```

For single file:

``` shell
$ python3 smally.py --jpegtran <jpeg_file>
$ python3 smally.py --optipng <png_file>
$ python3 smally.py --gifsicle <gif_file>
```

For single file which you don't know the format:

``` shell
$ bash smally.sh <filename>
```

## Screenshot

![smally](/screenshot.png)

## Old Version

This version (from V0.51) of smally is a total refactor one, old versions
are too complicated, which I do not recommend!

## Contributors
* [@xinlin-z](https://github.com/xinlin-z) - author and primary contributor
* [@serzhenko](https://github.com/serzhenko) - cross-platform fixes to Python script