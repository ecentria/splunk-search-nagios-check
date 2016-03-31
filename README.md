# Splunk search result nagios check
Nagios plugin that executes Splunk search, and alerts when there are too many events found

Requirements:
 * Python 2.6+
 * Splunk Python SDK (pip install splunk-sdk)
 * argparse package (pip install argparse)

# Installation

 * Copy check_splunk_query to your nagios plugins folder
 * define command for splunk query check (use splunk_query.cfg as a template)
 
# Usage

Add service check for splunk query with corresponding arguments (as defined in the cfg file):

```
...
    check_command       check_splunk_query!5!20!index=default status>=500 earliest_time=-2h
...
```

Pay special attention to 2 things:

 * If your search string has ! you need to escape it with a single backslash
 * Your search query **must** contatin time frame definition. By default it's "all time." If that works for you, great, 
but most likely you want to limit it to the most recent hours or days. Otherwise your search might take a long time to execute.

# Other things to note

Internally, plugin adds `| stats count(_raw)` at the end of the query to get just one number, instead of the whole feed. 
Currently there is no support for alternative aggregation methods.

With SDK's "one shot" method, it's unclear if results reader would always wait for search to fully complete, or will 
it start showing stuff as it is populated. If you notice any issues - please submit a PR or issue report to fix.

# Development

Vagrantfile is included for development convenience. Just `vagrant up` in the cloned folder, and you should be able to run plugin from command line.
