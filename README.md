# checkalive
### Quick &amp; dirty HTTP/HTTPS monitoring script

This quick bash script allows for a very basic http/https monitoring service, using HTTP response status codes returned by the requested webserver (**HTTP200 = OK**).

It is meant to be scheduled at recurring times (eg: every X minutes) using cron or similar services.

Alerts will be sent on a Telegram chat every time the status changes (OK -> Error -> OK ..) or, when in error, repeatedly, according to ``ERR_REPEAT_SECS`` variable, which can be customized into the script (default = every 2 hours).

Alerts are delivered using *Telegram.sh* (https://github.com/fabianonline/telegram.sh), which is automatically installed upon first run (installation directory can also be customized).

Please refer to the relevant documentation on how to set up your bot, token and chat ID.

#### Syntax
```$ ./checkalive [URL to be checked] [Telegram token] [Telegram chat ID]```

The command requires 3 parameters:
- Domain/URL to be checked
- Telegram token
- Telegram chat ID
which can be provided as commandline params, or as variables in the script itself (in that case, command will run without any params).

Example of crontab scheduling:
```
# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed

* * * * * user /home/user/checkalive/checkalive http://mydomain.com 0000000000:xxxxxxxx-xxxxxx-xxxxxxxxxxxxxxxxxx 123456789
```
