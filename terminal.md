# Terminals, terminal emulators, and everything

## OSC 4

The Ps = 4 refers to (OSC Ps ; Pt ST) where OSC (the "Operating System Control" prefix) is ESC ] and ST (the "String Terminator" suffix) is backslash. The "4" is one of the possible subcommands to OSC.

general form:

    OSC PS ; Pt ST
    
where

    OSC = ESC]     ;; "Operating System Command|Control"
    ESC = \x1b     ;; \x1b implements escape when using 'printf'
    PS = 4         ;; one of possible subcommands to OSC
    ST = backslash ;; "String Terminator" suffix
    
### CSI Control Sequence Indicator

    CSI = ESC[     ;; ?
    
example

    \x1b[30m;      ;; switch the foreground color to black
    \x1b[31m;      ;; switch the foreground color to red
    \x1b[41m;      ;; switch the background color to red    
    \x1b[30;1m;    ;; using 'bold' parameter, switch to gray
    \x1b[0m        ;; reset to defaults
    
### colors

Change Color Number c to the color specified by spec:

    Ps = 4  ; c ; spec 
    
This can be a name or RGB specification as
per XParseColor.  Any number of c name pairs may be given.
The color numbers correspond to the ANSI colors 0-7, their
bright versions 8-15, and if supported, the remainder of the
88-color or 256-color table.

### solarized termcolor

    ANSI=$1
    RGB=$2
    printf "\x1b]4;$ANSI;rgb:${RGB}\a"

example: cset 0 $base02

    printf "\x1b]4;0;rgb:07/36/42\a"

### Other subcommands

Change VT100 text foreground color to Pt.

    Ps = 1 0
    
Change VT100 text background color to Pt.    
    
    Ps = 1 1

### Misc

* Thomas Dickey, xterm maintainer

## Terminal colors

in shell:

    echo $TERM

gnome-terminal profiles

    ~/.gconf/apps/gnome-terminal/profiles/Solarized/
    
terminfo

    /usr/share/terminfo/
    /lib/terminfo/
    
terminfo? ncurses? tput
