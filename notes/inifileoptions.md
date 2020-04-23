### Configuration file options

pytest look for pytest.ini, tox.ini and setup.cfg configuration file to execute the test. You can use below options to define your test in these files.

```
markers (linelist):             markers for test functions

testpaths (args):               directories to search for tests when no files or directories are given in the command line.

usefixtures (args):             list of default fixtures to be used with this project

console_output_style (string):  console output: "classic", or with additional progress information ("progress" (percentage) | "count").

xfail_strict (bool):            default for the strict parameter of xfail markers when not given explicitly (default: False)

junit_suite_name (string):      Test suite name for JUnit report

junit_logging (string):         Write captured log messages to JUnit report: one of no|log|system-out|system-err|out-err|all

junit_log_passing_tests (bool): Capture log information for passing tests to JUnit report:

junit_duration_report (string): Duration time to report: one of total|call

junit_family (string):          Emit XML for schema: one of legacy|xunit1|xunit2

filterwarnings (linelist):      Each line specifies a pattern for warnings.filterwarnings. Processed after -W/--pythonwarnings.

log_print (bool):               default value for --no-print-logs

log_level (string):             default value for --log-level

log_format (string):            default value for --log-format

log_date_format (string):       default value for --log-date-format

log_cli (bool):                 enable log display during test run (also known as "live logging").

log_cli_level (string):         default value for --log-cli-level

log_cli_format (string):        default value for --log-cli-format

log_cli_date_format (string):   default value for --log-cli-date-format

log_file (string):              default value for --log-file

log_file_level (string):        default value for --log-file-level

log_file_format (string):       default value for --log-file-format

log_file_date_format (string):  default value for --log-file-date-format

log_auto_indent (string):       default value for --log-auto-indent

faulthandler_timeout (string):  Dump the traceback of all threads if a test takes more than TIMEOUT seconds to finish. Not available on Windows.

addopts (args):                 extra command line options

minversion (string):            minimally required pytest version
```
