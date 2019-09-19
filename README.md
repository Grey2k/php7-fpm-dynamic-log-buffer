php7-fpm-dynamic-log-buffer
===========================


DEPRECATION NOTICE
------------------

This repository is deprecated due to end of support for PHP 7.1 on December 1, 2019. You should migrate to PHP 7.3 which introduces  `log_limit` setting.


Description
-----------

When using PHP applications in containerized environment you should write logs to STDERR. If
you want to collect logs via Logstash and store them in Elasticsearch you may encounter a problem
when messages are truncated or split because they exceed the default buffer limit of 1024 characters.
This is a big problem, when you format logs in JSON.

Read [more](https://github.com/php/php-src/pull/1076#issuecomment-222096696).

This patch solves it by adding a new global option named `log_buffer_length` to the PHP-FPM configuration (`php-fpm.conf`):

```
; Log buffer length
; The value can vary from 1024 (default minimum) to 16384 (max).
; Default Value: 1024
;log_buffer_length = 1024
```

The patch was written and tested on PHP 7.1.12, but should applied correctly on higher versions. If not
don't hesitate to report an issue.
