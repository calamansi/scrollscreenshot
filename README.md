scrollscreenshot
================

Make Android screenshots of scrollable screen content - brought to you by [PGS Software SA](http://www.pgs-soft.com)


This tool makes a number of screenshots, scrolling screen content automatically between each shot. By default status bar and navigation bar are included only once.



**This software has been modified** by [Calamansi](https://github.com/calamansi/) in the following way:
 * take several multi-page (composite) screen shots (use option -f)
 * scroll to the very top of a long screen to stitch top-down without taking screenshots (see Todo)
   (use option -t to determine the number of pages to scroll up)

 https://github.com/calamansi/scrollscreenshot



![Illustration how images are merged](https://github.com/PGSSoft/scrollscreenshot/blob/master/illustration.png "Illustration how images are merged")


Documentation:
--------------

```
Usage: com.pgssoft.scrollscreenshot.ScrollScreenShot [options]
  Options:
    -c, --count
       Number of pages in one composite screenshot
       Default: 5
    -v, --device
       Device ID, first device is used if not specified (i.e. "4df1902336814fa6"
       or "192.168.56.102:5555")
    -d, --direction
       Swipe direction: topdown (default), bottomup, leftright (implies "--stitch none")
       Default: topdown
    -e, --inertia
       Inertia of content, how many pixels are required to start dragging. Use
       non-zero value if there are duplicated stripes.
       Default: 0
    -f, --files
       Number of composite screenshots (files) to be created (use "-c" to determine number of pages in a composite)
       Default: 0
    -h, --help
       Display this help
       Default: false
  * -i, --inputdevice
       Digitizer input device number, N in /dev/input/eventN
       Default: 1
    -n, --nameprefix
       Output filename prefix
       Default: out
    -p, --pathsdk
       Path to Android SDK
    -s, --stitch
       Stitch mode: full (smooth stitch), none (merged full screenshots),
       separate (separate files)
       Default: full
    -t, --top
        Scroll up only, do not take screenshots
        t > 0 giving the number of pages (screen heights) to scroll up.
        Overrides any other setting
        Default: 0 (not scrolling)
    -x, --steps
        Number of steps to scroll the screen. If there is a problem (doesn't scroll correctly), try 10.
        Default: 1

```



How to use
----------

You need to know digitizer device input number, which is specific to every device and ROM.

Use command 
```sh
adb shell getevent -l
```
and move finger on screen. You will see something like
```
/dev/input/event2: EV_SYN       SYN_REPORT           00000000
/dev/input/event2: EV_ABS       ABS_MT_WIDTH_MAJOR   00000014
/dev/input/event2: EV_ABS       ABS_MT_POSITION_X    00000247
/dev/input/event2: EV_ABS       ABS_MT_POSITION_Y    0000030c
/dev/input/event2: EV_ABS       ABS_MT_TOUCH_MAJOR   0000001a
/dev/input/event2: EV_ABS       ABS_MT_TOUCH_MINOR   0000000e
/dev/input/event2: EV_ABS       003c                 ffffffb3
```
In your case device you are looking for has number **2** (/dev/input/event **2** ).


You can now start screen capturing. Download [latest multi-page scrollscreenshot binary](https://github.com/calamansi/scrollscreenshot/blob/master/scrollscreenshotmultipage.jar?raw=true), unlock screen, start app you want to scroll-capture and type (replace *2* by your device input number):

```
java -jar scrollscreenshotmultipage.jar -i 2
```

Scroll up by 1000 screen heights
```
java -jar scrollscreenshotmultipage.jar -i 2 -t 1000
```

Take 10 multi-page (composite) screenshots consisting of 25 pages each seamlessly stitched.
```
java -jar scrollscreenshotmultipage.jar -i 2  -s full -c 25 -f 10
```



If everything goes well, you will get file `out_01.png` with something like:

<img src="https://github.com/PGSSoft/scrollscreenshot/blob/master/sample.png" alt="SAMPLE" width="200">

Left-to-right mode will give you something like this:

<img src="https://github.com/PGSSoft/scrollscreenshot/blob/master/samplehorizontal.png" alt="SAMPLE" width="800">


Todo (original source):
-----

* scrolling in all 4 directions (*update* v 0.2 of this fork: bottom-up screenshots are possible)
* automatic detection of scroll area edge


Changelog
---------

* 0.1 - forked and modified to take several composite screenshots rather than just one as in the [original source](https://github.com/PGSSoft/scrollscreenshot/)
* 0.2 - bottom up screenshots ("`-d bottomup`") - consider that the `-e, --inertia` might be a negative value now! ;-)


Acknowledgments
---------------

* software development by [PGS Software SA](https://github.com/PGSSoft/scrollscreenshot/)

* description of input events was taken from
[this blog post](http://ktnr74.blogspot.com/2013/06/emulating-touchscreen-interaction-with.html)

* command line parsing uses http://jcommander.org/ licensed under [Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0)

* device communication handled by [AOSP](http://source.android.com/) tools licensed under [Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0)


[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-scrollscreenshot-brightgreen.svg?style=flat)](https://android-arsenal.com/details/1/1047)

License
----

scrollscreenshot for Android

Copyright (c) 2014 PGS Software SA

https://github.com/PGSSoft/scrollscreenshot

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated
documentation files (the "Software"), to deal in the Software without restriction, including without limitation
the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and
to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions
of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO
THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF
CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS
IN THE SOFTWARE.
