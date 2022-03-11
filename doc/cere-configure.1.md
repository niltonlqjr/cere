cere configure(1) -- Configures CERE to build and run an application
====================================================================

## SYNOPSIS

```
cere configure [-h] --run-cmd=RUN_CMD --build-cmd=BUILD_CMD --clean-cmd=CLEAN_CMD
               [--multiple-trace]
```

## DESCRIPTION

The first step before using **CERE** on an application is running **cere
configure**. This command tells **CERE** which commands must be used to build and
run the application.

## OPTIONS

  * `-h`:
    Prints a synopsis and a list of the most commonly used options.

  * `--run-cmd=RUN_CMD`:
    Sets the command used to run the application.

  * `--build-cmd=BUILD_CMD`:
    Sets the command used to build the application.

  * `--clean-cmd=CLEAN_CMD`:
    Sets the command used to clean the application.

  * `--multiple-trace`:
    Enables tracing multiple regions in a single run.  By default, multiple
    tracing is disabled and cere-trace(1) will only trace the requested region.
    If **--multiple-trace** is activated, cere-trace(1) traces all possible regions
    in a single run (regions must be non-nested). This can considerably decrease
    the tracing cost.

## EXAMPLES

Given a simple application `app` that is built using the following `Makefile`:

```make
all: app
app: app.o
     $(LD) -o $@ $<
app.o: app.c
     $(CC) -c $<
clean:
     rm app *.o *.ll
```

The user should call **cere configure** with the following arguments:

```
cere configure --build-cmd="make CC=ccc LD=ccc"
               --clean-cmd="make clean"
               --run-cmd="./app"
```

## OUTPUT FILES

  * `cere.json`:
    the configuration file. This file is read by most of **CERE**
    passes. You can manually edit this file.

## COPYRIGHT

cere is Copyright (C) 2014-2015 Universite de Versailles St-Quentin-en-Yvelines

## SEE ALSO

cere-trace(1) cere-capture(1) cere-replay(1)
