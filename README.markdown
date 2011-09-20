** This is color enhanced readlog which is modifed from http://github.com/xwz/readlog **

Change form original `readlog`
* added color ouput by HTTP status codes with a `--color` or `-c` flag
* change the few columns name
* changed the defualt date output to a readable common date/time format (set `--date` or '-d` to `unix` to format in UNIX timestamp)

Pipe apache logs into `readlog` to selectively display interesting information.

Example: show the access time as Unix epoch and ip addresses

    cat /var/log/apache2/access.log | readlog --color --columns=date,status,method,url

    or

    cat /var/log/apache2/access.log | readlog -rc date,status,method,url

Install
-------

Python 2.5 or later is required. The `ApacheReader` extension is required(included in the directory) and
can be compiled and installed by running:

    sudo python setup.py install
    sudo cp readlog /usr/bin/.

Command line options
--------------------

**readlog** offers 4 command line options: 

* `--color` or `-r`  - enable color ouput by HTTP status codes, no extra input needed, just a flag
* `--columns` or `-c`  - comma delimited list of column names
* `--params` or `-p`    - comma delimited list of query parameter names
* `--date` or `-d`     - output date format pattern, default is Unix epoch
* `--format` or `-f`   - log format pattern, default is `common`

The available column names, see http://httpd.apache.org/docs/2.2/logs.html#accesslog 
for details

* `ip`         - IP address of the client (remote host) 
* `username`    - userid by HTTP authentication.
* `ident`       - identity 
* `date`        - date that the request was received
* `tz`          - timezone
* `method`      - method used by the client 
* `url`         - requested url
* `path`        - hierarchical path in the url
* `query`       - query component in the url
* `fragment`    - fragment identifier in the url
* `protocol`    - protocol used by the client
* `status`      - status code that the server sends back to the client
* `size`        - size of the object returned to the client
* `referer`     - the site that the client reports having been referred from
* `user-agent`  - User-Agent HTTP request header

The names in the `--params` option can be used to show the corresponding query 
parameter values.

Example: show the query parameter values with names equal to `page` and `type`

    cat /var/log/apache2/access.log | ./readlog --params=page,type

The options `--params` and `--columns` can be combined.

The `--date` option defines the date format for the `time` column. For format 
patterns see:

http://docs.python.org/library/datetime.html#strftime-and-strptime-behavior

The `--format` option defines the log input format, in particular, `common` and 
`combined` corresponds to the apache common and combined log formats. A custom
input log format is supported by specifying the pattern string as argument.

See http://httpd.apache.org/docs/2.2/logs.html#accesslog for details.

Credits
-------
This build is slightly modified version 'readlog' from https://github.com/xwz/readlog
This package uses the `ApacheReader` extension from http://github.com/idealisms/apache-log-reader
