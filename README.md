# cecho #

Colorful echo for unix-like shell ( ascii color only )

----------

## Overview ##

A **light**, **self-adapting** wrapper of `echo`, with several useful features, such as color switches for **foreground**, **background** and **action** ( highlight, underline, blink ... ) . Decroate your life between command line and shell script with more colors.

Tested in [**zsh**](http://www.zsh.org/) and [**bash**](http://www.gnu.org/software/bash/).

## Screenshot ##

##### Active #####

![screenshot](https://raw.github.com/springlie/cecho/master/screenshot.png)

##### Inactive #####

![screenshot](https://raw.github.com/springlie/cecho/master/screenshot2.png)

## Install ##

Before use `cecho`, simply source it in your `.zshrc`, or any shell script you want to colorize: 

	source /path/to/cecho.sh

## Usage ##

Support multi-string in one command:

	cecho -color1 message1 [ -color2 message2 ... ] [ -done ]

Support setting foreground, background and action

	cecho -fg_color -bg_color -action message [...] [ -done ]

**All switches have two forms, short for convenience, long for readability.**

The short forms are the abbreviation from the corresponding long forms,

#### Foreground color arguments ##

| short |  long        |
| ----- | -------      |
| -r    | -red         |
| -g    | -green       |
| -y    | -yellow      |
| -b    | -blue        |
| -p    | -purple      |
| -c    | -cyan        |
| -w    | -white       |
| -gr   | -gray        |
| -bk   | -black       |

#### Background color arguments ####

| short |  long        |
| ----- | ------------ |
| -br   |  -b_red      |
| -bg   |  -b_green    |
| -by   |  -b_yellow   |
| -bb   |  -b_blue     |
| -bp   |  -b_purple   |
| -bc   |  -b_cyan     |
| -bw   |  -b_white    |
| -bgr  |  -b_gray     |
| -bbk  |  -b_black    |

#### Action arguments ####

| short |  long        |
| ----- | ------------ |
| -d    |  -done       |
| -hl   |  -highlight  |
| -ul   |  -underline  |
| -re   |  -reverse    |
| -bl   |  -blink      |
| -iv   |  -invisible  |

#### Escaped character ####

| short |  long        |
| ----- | ------------ |
| -B    |  -blank      |
| -t    |  -tab		   |
| -n    |  -newline    |

#### Functional ####

| short |  long        |
| ----- | ------------ |
| -h    | -help,--help |

## Example ##

##### set fg to *red*: #####
	
	cecho -r "hello world ! "
or

	cecho -red "hello world ! "

or

	cecho -r hello -B world -B !

##### *blank* & *tab* & *newline* #####

	cecho -r -t hello -B world -n !

##### set fg to *red*, bg to *yellow*, action to *highlight* and *underline*: #####

	cecho -r -by -hl "hello world ! "

##### set [ *red*, *yellow*, *highlight* & *underline* ] for "hello", [ *cyan*, *red*, *reverse* ] for "world", [ *green*, *black*, *blink* ] for "!" : #####

	cecho -r -by -hl -ul hello -d -B -c -br -re world -d -B -g -bl !

**Please refer to the help file for more examples:**

`cecho -h`

[**That colorful help page**](https://github.com/springlie/cecho#screenshot) is generated by `cecho` .

## Useful Variables ##

#### CECHO_IS_IMPORTED ####

Once you have sourced `cecho`, `CECHO_IS_IMPORTED=1` will be defined. 

That meams you can check this var `CECHO_IS_IMPORTED` to confirm if you are in a no_cecho env or not:

Exp: [**Sence 2**](https://github.com/springlie/cecho#2-my-script-maybe-runs-in-both-no-cecho-env-and-cecho-env/)

#### CECHO_IS_INACTIVE ####

If you want to deactive `cecho` temporarily, set `CECHO_IS_INACTIVE=1` before calling `cecho`.

**Note**: color and action can be disabled by `CECHO_IS_INACTIVE`, but `return`, `blank` and `tab` are still active, as you wish.

## Sence ##

##### 1 - I want my script outputs to file/pipe without color_ctrl chars #####

Needn't do any change, `cecho` can self-adapting this: colorful for stdout, non-colorful for file/pipe.

##### 2 - My script maybe runs in both "no-cecho env" and "cecho env" #####

Don't be disappointed, you only need to modify your script like this:

	if [ -z "$CECHO_IS_IMPORTED" ]
	then
		echo hello world
	else
		cecho -r -bg -hl hello -B world
	fi

Or shortly:

	[ -z "$CECHO_IS_IMPORTED" ] && echo "hello world" || cecho -r -bg -hl hello -B world

##### 3 - My script uses `cecho` but I want to disable it temporarily #####

	CECHO_IS_INACTIVE=1
	cecho -r -bg -hl hello world	# <-- now cecho is inactive
	CECHO_IS_INACTIVE=
	cecho -r -bg -hl hello world	# <-- now cecho is active

## Advanced ##

- Action flag `-d` ( same as `-done` ) will **turn off all settings** ( fg, bg and action ), Thus, in **single** command, you have to set flags again to retrive it back once there are other strings after `-d`.
- Some special characters ( with centain format ) don't work properly, such as `cecho "!"`. It's due to `echo`... use `cecho '!'` or `cecho !` instead.
- It's **not** necessary to use `-d` at the begin/end of commands, `cecho` will take care of it.
- Actions can overlaied.

## What's more ##

Another **C version** project is [coprintf](https://github.com/springlie/coprintf).

## Thanks ##

Thanks to [https://github.com/jonhiggs/cecho](https://github.com/jonhiggs/cecho), when I completed `cecho` script and try uploading it to github I found this -- with same name and almost same functions ... and then, I got the way to build table in README.md from there.
