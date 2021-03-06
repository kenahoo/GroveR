[![Build Status](https://travis-ci.org/focusenergy/GroveR.svg?branch=master)](https://travis-ci.org/focusenergy/GroveR)

GroveR brings [Declarative Programming](https://en.wikipedia.org/wiki/Declarative_programming)
to data-centered applications.  For example, suppose your code looks like this:

```
create_foo <- function(bar, BaZzO) {
  ## create foo stuff here...
}

create_bar <- function() {
  ## create bar stuff here...
}

create_baz <- function() {
  ## create baz stuff here...
}

create_quux <- function(bazz) {
  ## create quux stuff here...
}

x <- create_bar()
BAZ <- create_baz()
result <- create_foo(x, BAZ)
```

Using the tools of `GroveR`, that can be transformed to this:

```
App <- GroveR$new()
`%createdBy%` <- App$auto

foo %createdBy% function(bar, baz) {
  ## create foo stuff here...
}

bar %createdBy% function() {
  ## create bar stuff here...
}

baz %createdBy% function() {
  ## create baz stuff here...
}

quux %createdBy% function(baz) {
  ## create quux stuff here...
}

## This builds any dependencies necessary to create 'foo'
result <- App$getArtifact('foo')
```

As benefits, the application now has:

 * automatic caching of intermediate artifacts
 * intelligent rebuilding of artifacts when dependencies change
 * standardized naming of data artifacts throughout the application
 * configurable logging of artifact creation using [futile.logger](https://cran.r-project.org/web/packages/futile.logger/index.html)
 * graphical tools to show data dependencies (colors indicate what's up-to-date or not):

   ![data dependencies](docs/gv.png)

Copyright (c) 2016 Windlogics, Inc.
See the DESCRIPTION file for licensing information.
