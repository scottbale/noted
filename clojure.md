## clojure

Jira https://clojure.atlassian.net/

Spelunking through source code

### compiler

https://clojure.org/reference/compilation

* `Opcodes.java`
* `Compiler.java`
  * `public static Object compile` a good starting point, see how it concludes with getting byte
    array from class writer/visitor and writing it to a class file
  * `public static Object eval(Object form)`
    * see inner `interface Expr#eval`, `class ObjExpr` etc.
* see `(defn load` in `core.java`

        (clojure.lang.RT/load (.substring path 1))

* `Compile.java` just a `main` method that invokes core `compile`
* core `defn compile`
* `Symbol.java`, `intern()`
* `Var.java`, `setDynamic()`
* `Intrinsics.java`

### reader

https://clojure.org/reference/reader
see also https://clojure.org/reference/evaluation

* `LispReader.java`
* see `defn read` in `core.clj`

        ([opts stream]
         (. clojure.lang.LispReader (read stream opts)))

  * `*read-eval*`
  > Note that read can execute code (controlled by *read-eval*)...
  * see also `read-string` core function
* `EdnReader.java`
* See also `tools.reader`: a reader implemented in Clojure, replaces `LispReader`

Alex
> You can invoke the Clojure.read() function to read a literal map or Clojure.var() to look up
> Clojure vars and invoke them
* This ^ refers to `clojure.java.api.Clojure`
  * `public static Object read(String s)`
  * `public static IFn var(...)` overloaded

## compojure

Starting REST API
* ring - https://github.com/ring-clojure/ring
  * https://www.baeldung.com/clojure-ring
  * ring-mock https://github.com/ring-clojure/ring-mock
* compojure - https://github.com/weavejester/compojure

        $ lein new compojure hello-world
        $ lein ring server

* https://github.com/ring-clojure/ring-defaults
* see also
  * https://github.com/metosin/compojure-api
  * https://github.com/metosin/reitit

## Sean Corfield talk 12/15/20

* CLI tools (1.10.1.763) plus dot-clojure repo/aliases
* VS Code + Clover + Socket REPL
* possible with lein, nREPL, emacs/vi/cursive
* tools.deps.alpha's add-lib3 branch to add dependencies to running app (can use Pomegrante with
  lein for same thing)
* Reveal (optional, supliment editor) see also: REBL (Cognitect)
* clj-kondo (borkdude)
* strict paredit
* parinfer
* tap
* selmer templating (similar to django, see also hiccup)
* spec
* Cryogen clojure markdown

## require/load/use

require -
* must require ns before using

load -

use -

Require isn't thread-safe https://ask.clojure.org/index.php/9893/require-is-not-thread-safe
* core `defn- serialized-require`, `defn requiring-resolve`
* `clojure.lang.RT/REQUIRE_LOCK`

## clojure|clj

Install from the official tap (not the homebrew built-in formula)

    brew install clojure/tools/clojure

https://clojure.org/releases/tools

installed `clj`, `rlwrap` https://clojure.org/guides/getting_started

> Use the `linux-install` script to download and run the install, which will create the executables
> `/usr/local/bin/clj`, `/usr/local/bin/clojure`, and the directory `/usr/local/lib/clojure`:

According to Alex
> tools.build is coming...

The `brew-install` repo contains the installed scripts including (confusingly) the
`linux-install.sh` script

commands

    man clojure
    clojure -X:deps tree

## repl

lein leiningen repl nrepl tools.nrepl cider repl-y reply

* `tools.nrepl` successor is `nrepl` (`0.3.1` should be drop-in replacement for `0.2.13`)
  * https://github.com/nrepl/nrepl
* `reply` aka `REPL-y` - a replacement for stock Clojure repl, unrelated to nrepl (but with
  integration)
  * https://github.com/trptcolin/reply


Upgrade a bunch of other packages including `cider`. As a reminder to self, then had to go update
version of `cider-nrepl` to match, in both `~/.lein/profiles.clj` and `~/.gradle/gradle.properties`.

### Investigating Gradle clojure cider-nrepl support

* `tools.nrepl` - https://github.com/clojure/tools.nrepl
  * `server.clj` defines `defn start-server`, `defn default-handler`
* leiningen - https://github.com/technomancy/leiningen
  * `repl.clj`
    * `defn- server-forms` builds handler, overrideable by plugins (e.g. for additional middleware)
    * `defn- handler-for` uses `nrepl-middleware` from `project.clj`
* `cider-nrepl` - https://github.com/clojure-emacs/cider-nrepl
  * additional middleware for `tools.nrepl`
  * `plugin.clj` (lein plugin) adds its own middleware to `:repl-options :nrepl-middleware` of
    `project.clj`
  * See `~/.lein/profiles.clj` - this sets the lein repl plugin
* `gradle-clojure` - https://github.com/clojurephant/clojurephant
  * gradle plugin providing simple clojure support
  * `clojure_nrepl.clj` - simply calls `nrepl/start-server` only specifying port - no hook to
    override middleware

### clojure main

https://clojure.org/reference/repl_and_main

* `main.java` `public static void main` (refered to by jar `manifest.mf`, see `build.xml`)
* `main.clj` `defn main` no args case
* `main.clj` `defn repl` actually implements a repl

"read-eval" refers to reading forms (the Clojure "reader") followed by eval (can include
compilation)
