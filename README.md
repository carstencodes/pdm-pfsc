# Plug-In Foundation Services Collection

The [Python Development Master](https://pdm-project.org) offers various extension points.

You can either add plug-ins or signals. Some parts are not very intuitive for the
experienced python developer who are used to work with python standard libraries like logging or
is hard to test as there are some points that are not that easy to test.

This collection offers a set of services helping to write better plug-ins.

## `abstractions`

This module provides three protocols, that will abstract PDM core and PDM project classes, so
that they can easily mocked in unit tests.

## `actions`

Actions are a collection of actions to run. This can be useful, if you
want to add different verbal commands.

Each of this action can add options to the parser. They all can be
registered in an `ActionRegistry`. This provides an instance method called `register`
which can be used to decorate implementations of `ActionBase`.

## `config`

The configuration section is unstable.

## `hook`

Hooks surround `actions` by hooks - an action can provide an implementation of
the `HookGenerator` protocol, that must emit instances of `HookInfo`, a dataclass
that gives information about the `HookBase` class to instantiate and run
before and after the action is executed itself.

## `logging`

The `logging` module provides a logger based on the python standard logging facilities.

The `TermUIHandler` uses `pdm.core.ui.echo` to write data to a log. The `TracingLogger` is
created to add a log-level called `TRACE` to the logging, which is later used by `traced_function`.

The default instance for the logging is added in the `logger` variable. It's default value
can be set using `setup_logger`. The value passed is identical to the `verbose` level
of the `pdm` invocation arguments.

The decorator `traced_function` can be used to decorate a function for tracing the sequence of
events - just like `set -x` does in POSIX scripts.

## `proc`

The `CliRunnerMixin` allows you to run child-processes from your plug-in or signal.
It offers a class-var called `run_process`, that has the same signature like
`subprocess.run` from the python standard library, but can be overwritten for your tests.
