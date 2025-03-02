# Introduction

`page` is a minimalist terminal pager written in C with no dependencies.

* Supports UTF-8 (and only UTF-8).
* Handles all ANSI escape codes (e.g. colors) except codes that move the cursor.
* Shows percentage progress when displaying a file.
* Should be portable to most POSIX systems, though it is not strictly POSIX compliant since there wasn't a POSIX compliant way to get the terminal dimensions in C until 2024 which isn't supported everywhere yet.
* `page` is about 260 lines of code.

# Usage

    <command> | page
    page <file>

Backwards movement only works when paging a file, but you can convert a stream
to a file with the `fpipe` utility which writes the whole stream to a temporary
file. This should only be used when the stream is not too large.

    <command> | fpipe page

# Commands

* `ENTER`/`DOWN`/`j` - scroll down one line
* `SPACE` - scroll down one screen
* `d` - scroll down half a screen
* `UP`/`k` - sroll up one line (when paging a file)
* `b` - scroll up one screen (when paging a file)
* `u` - scroll up half a screen (when paging a file)
* `g` - go to top of file (when paging a file)
* `Ng` - go to line number N (going backwards only supported when paging a file)
* `G` - go to the end
* `Np` - go to next line after N% of file size (when paging a file)
* `q`/`ESC` - quit

Scrolling commands can be prefixed by a number N to make them repeat N times.

Scrolling backwards won't work after a byte-based jump like the `p` command
until a line-based jump command like `g` is executed.

# Building

Run `./make` or `env CC=musl-gcc ./make`.
