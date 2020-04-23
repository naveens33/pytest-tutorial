# Command line Options

You can run your pytest test using below command,

```
pytest [options] [file_or_dir] [file_or_dir]
```

in \[options\] place holder you can provide the pytest options. You can get the available options using below command,

```
pytest --help|zless
```

### Test selection control options:
```
-k EXPRESSION           only run tests which match the given substring expression. 
                        An expression is a python evaluative expression where all names 
                        are substring-matched against test names and their parent classes. 
                        
                        Example: -k 'test_method or test_other' matches all test functions 
                        and classes whose name contains 'test_method' or 'test_other',
                        while -k 'not test_method' matches those that don't contain 'test_method' 
                        in their names. -k 'not test_method and not test_other' will 
                        eliminate the matches.
                        
                        Additionally keywords are matched to classes and functions containing 
                        extra names in their 'extra_keyword_matches' set, as well as 
                        functions which have names assigned directly to them. 
                        The matching is case-insensitive.

-m MARKEXPR             only run tests matching given mark expression. example: -m 'mark1 and not mark2'.
```

### Test execution control options:
```
-x, --exitfirst        exit instantly on first error or failed test.

--maxfail=num          exit after first num failures or errors.

--lf, 
--last-failed          rerun only the tests that failed at the last run (or all if none failed)

--ff, --failed-first   run all tests but run the last failures first. 
                       This may re-order tests and thus lead to repeated fixture setup/teardown

--nf, --new-first      run tests from new files first, then the rest of the tests sorted by file mtime  

--lfnf={all,none}, 
--last-failed-no-failures={all,none}
                       which tests to run with no previously (known) failures.

--sw, --stepwise       exit on test failure and continue from last failing test next time

--stepwise-skip        ignore the first failing test but stop on the next failing test

```

### Configuration File options:
```
-c file                load configuration from `file` instead of trying to locate one of the implicit configuration files.
```

### Reporting options:
```
--junit-xml=path       create junit-xml style report file at given path.

--junit-prefix=str     prepend prefix to classnames in junit-xml output

--html=report.html     create html report file at given path
```

### Logging options:
```
--no-print-logs        disable printing caught logs on failed tests.

--log-level=LEVEL      level of messages to catch/display. Not set by default, so it depends on the root/parent log handler's effective level, where it is "WARNING" by default.

--log-format=LOG_FORMAT
                       log format as used by the logging module.

--log-date-format=LOG_DATE_FORMAT
                       log date format as used by the logging module.

--log-cli-level=LOG_CLI_LEVEL
                       cli logging level.

--log-cli-format=LOG_CLI_FORMAT
                       log format as used by the logging module.

--log-cli-date-format=LOG_CLI_DATE_FORMAT
                       log date format as used by the logging module.

--log-file=LOG_FILE    path to a file when logging will be written to.

--log-file-level=LOG_FILE_LEVEL
                       log file logging level.

--log-file-format=LOG_FILE_FORMAT
                       log format as used by the logging module.

--log-file-date-format=LOG_FILE_DATE_FORMAT
                       log date format as used by the logging module.

--log-auto-indent=LOG_AUTO_INDENT
                       Auto-indent multiline messages passed to the logging module. Accepts true|on, false|off or an integer.
```

### Output capture option:
```
-s                     show Output, do not caputure

-rs                    show extra summary info for SKIPPED

-r chars               show extra test summary info as specified by chars:
                       (f)ailed, (E)error, (s)skipped, (x)failed, (X)passed
                       (w)pytest-warnings (p)passed, (P)passed with output,
                       (a)all except pP.

--durations=N          show N slowest setup/test durations (N=0 for all).

-v, --verbose          increase verbosity.

-q, --quiet            decrease verbosity.

--disable-warnings, 

--disable-pytest-warnings
                       disable warnings summary
```

### Tracebacks options:
```
 --showlocals          Show local variables in tracebacks

 -l                    Show local variables (shortcut)

 --tb=auto             (default) 'long' tracebacks for the first and last entry, but 'short' style for the other entries

 --tb=long             Exhaustive, informative traceback formatting

 --tb=short            Shorter traceback format

 --tb=line             Only one line per failure

 --tb=native           Python standard library formatting

 --tb=no               No traceback at all
```

### Other options:
```
--markers              show markers (builtin, plugin and per-project ones).

--strict-markers,      
--strict               markers not registered in the `markers` section of the configuration file raise errors.

--fixtures, 
--funcargs             show available fixtures, sorted by plugin appearance (fixtures with leading '_' are only shown with '-v') 

--fixtures-per-test    show fixtures per test
```