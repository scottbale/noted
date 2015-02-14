# EMACS

install packages

    M-x package-install
    clojure-mode

other (list packages, add/upgrade/delete them)

    M-x package-list-packages
    
rgrep (plus forward, backward navigation of results)

    M-x rgrep
    P
    N
    
emacs C-O all grep occurences

    M-: eval
    M-! shell command
    M-! shell command "tree"*
    
    
## kill ring

browse (need to install module)

    M-x

cycle through

    M-y

empty

    M-: (setq kill-ring nil)
    
## vc-mode
http://emacswiki.org/emacs/VersionControl

status

    C-x v d

diff

    C-x v D
    
annotate (blame)

    C-x v g

## clojure-mode

    M-x slime-connect
    C-c C-k load/compile
    C-c M-p repl at namespace
    C-x C-e eval expr
    C-c v eval buffer
    M-. func src
    M-* or C-x b ???

in repl use 

    (in-ns 'somenamespace)
    
hippie complete

    M-/
    
paredit cheat sheet
tw There should be a Clojure Lint called Clint
emacs color-theme debugging (thanks Ryan)
http://blog.dskang.com/2011/05/14/fixing-the-color-theme-problem-with-the-emacs-starter-kit/


## Emacs 24, building from source

### with graphics
(clone from github, cd into directory, then)

    sudo apt-get install autoconf automake
    ./autogen.sh
    sudo apt-get install texinfo libgtk3-dev libgif-dev libjpeg-dev
    libtiff-dev libxpm-dev libtinfo-dev
    ./configure --with-x-toolkit=gtk
    make
    src/emacs -Q    <-- test
    sudo make install

test
    
    src/emacs -Q

and finally...
    
    sudo make install

### terminal only (amazon aws microinstance)

    sudo apt-get install texinfo libtinfo-dev ncurses-dev
    ./configure --without-x

## query-replace

    M-%
    
then search string, replace string, then

    Spacebar - replace and find next occurrence
    Del      - skip and find next occurrence
    .        - replace then stop 
    !        - replace all
    ^        - return cursor to previously replaced

## global search and replace
http://emacswiki.org/emacs/DiredSearchAndReplace

    C-u M-x
    Dired listing switches: -lR
    
in dired mode, mark directories:

    * /
    
then toggle marks to mark only files

    t
    
(or, mark files according to regexp % m)
then do search replace regexp

    Q
    
accept all

    Y
    
In IBuffer (C-x C-b), mark all unsaved

    * u
    
then save all marked

    S
    
## regexp search and replace 
"Query" with "Transform"
(also works in above dired steps)

    M-x replace-regexp
    \([^a-zA-Z0-9]+\)Query+
    Ret
    \1Transform
    Ret

## Terminal colors

emacs color theme solarized - github.com/sellout/emacs-color-theme-solarized

    C-h v
    solarized-termcolors
    solarized-degrade
    window-system
    
see solarized-definitions.el

    defun solarized-color-definitions

in shell:

    echo $TERM

gnome-terminal profiles

    ~/.gconf/apps/gnome-terminal/profiles/Solarized/
    
terminfo

    /usr/share/terminfo/
    /lib/terminfo/
    
emacs terminal source code

    ~/sandbox/emacs/lisp/term/
    
emacs color cells

    (display-color-cells (selected-frame))
    
or

    (tty-display-color-cells (selected-frame))
    C-x C-e eval in scratch buffer
    
colors

    M-x list-colors-display
    
terminfo? ncurses? tput

## Misc

    eshell
    ansi-term

## Replace tabs w/ spaces

    M-x query-replace
    C-q, tab, then spaces
    ! to accept all

## keyboard macro

start

    M-x kmacro-start-macro
    C-x (

end

    M-x kmacro-end-macro

call

    M-x kmacro-call-macro

## variables

see variable value

    C-h v

set variable value

    M-x set-variable

## Clojure

1st change `inferior-lisp-program` variable (`M-x set-variable`) to

    "java -cp /home/scott/clojure/test:/home/scott/clojure/target/clojure-1.7.0-master-SNAPSHOT.jar:/home/scott/clojure/target/test-classes/:/home/scott/clojure/target/classes/:/home/scott/.m2/repository/org/clojure/test.generative/0.4.0/test.generative-0.4.0.jar:/home/scott/.m2/repository/org/clojure/tools.namespace/0.1.1/tools.namespace-0.1.1.jar:/home/scott/.m2/repository/org/clojure/java.classpath/0.1.1/java.classpath-0.1.1.jar:/home/scott/.m2/repository/org/clojure/data.generators/0.1.2/data.generators-0.1.2.jar clojure.main"

then

    M-x run-lisp

load file (`C-c C-l`) `test_helper.clj`, `compilation.clj`

then at prompt

    (require 'clojure.test.generative)
    (ns clojure.test-clojure.compilation)
    (run-tests)
    (CLJ-1400)

remember

    mvn exec:java -Dexec.classpathScope="test" -Dexec.mainClass="clojure.main"
    mvn dependency:build-classpath
    (println (seq (.getURLs (.getParent (.getContextClassLoader (Thread/currentThread))))))
    (use ['clojure.repl :only ['doc]])
