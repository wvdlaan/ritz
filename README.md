# swank-clj

Refactored swank-clojure, with jpda debugging support.

This is alpha quality.

- Breaks on uncaught exceptions and breakpoints.
- Allows stepping from breakpoints
- Allows evaluation of expressions in the context of a stack frame

## Install

Add `[swank-clj "0.1.0-SNAPSHOT"]` to your project.clj `:dev-dependencies`.

A compatible slime.el is in slime/slime.el. It is available as a `package.el`
package file you can
[download](https://github.com/downloads/hugoduncan/swank-clj/slime-20101113.tar)
and install with `M-x package-install-file`.  Note that you will need to remove
this package to use
[swank-clojure](https://github.com/technomancy/swank-clojure) again.

## Usage

To run with jpda:

    lein swank-clj

To run without jpda:

    lein swank-clj 4005 localhost :server-ns swank-clj.repl

### Breakpoints

To set a breakpoint, eval `swank-clj.el` from src/main/elisp, put the cursor
on the line where you want a breakpoint, and `M-x slime-line-breakpoint`.

Note that breakpoints disappear on recompilation at the moment.

To list breakpoints, use `M-x slime-list-breakpoints`.  In the listing you can
use the following keys

 - e enable
 - d disable
 - g refresh list
 - k remove breakpoint
 - v view source location

## Open Problems

Recompilation of clojure code creates new classes, with the same location as the
code they replace.  Recompilation therefore looses breakpoints, which are set on
the old code. Setting breakpoints by line number finds all the old code too.

## Roadmap

A pure JDI backend, that doesn't require swank in the target VM is certainly a
possibility.

A slime-eval-symbol-at-point would be useful (requires determining the frame
in the current sldb stacktrace using file and line number).

Add watchpoints with logging of locals to an emacs buffer or file.

## Use Cases

### Development

Run swank server and JDI debugger in the same process to have a single JVM and keep
memory usage down

### Debug

Run swank and debugger in a seperate JVM process. Attach to any -Xdebug enabled
JVM process.

### Production server

Run swank server in process and attach slime as required. This requires the
debugger to run in process.

## License

Copyright (C) 2010, 2011 Hugo Duncan

Distributed under the Eclipse Public License.
